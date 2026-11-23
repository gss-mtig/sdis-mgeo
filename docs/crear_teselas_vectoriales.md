# Crear teselas vectoriales con `ogr2ogr`

En esta práctica convertirás un GeoJSON con **10.000 puntos** en un archivo MBTiles con teselas vectoriales. `ogr2ogr` forma parte de GDAL, que se instala junto con QGIS. El archivo está incluido en los materiales para que no dependas de una descarga externa.

## Objetivo y materiales

Al terminar podrás generar un archivo de teselas a partir de una capa vectorial y reconocer el efecto de los niveles de zoom.

Necesitas:

- QGIS instalado y su terminal de OSGeo4W disponible.
- El archivo [puntos_10000.geojson](ejemplos/vector_tiles/puntos_10000.geojson), con 10.000 puntos sintéticos.
- Una carpeta de trabajo local, por ejemplo `teselas-clase`.

Los puntos se distribuyen aproximadamente por España, pero son **datos inventados**: no representan observaciones ni entidades reales. El archivo ocupa alrededor de 1,7 MB.

## 1. Abre la terminal de QGIS

En Windows, abre **OSGeo4W Shell** desde el menú de inicio de QGIS. Comprueba que `ogr2ogr` está disponible:

```bat
ogr2ogr --version
```

Si Windows indica que no reconoce el comando, comprueba que abriste la terminal de OSGeo4W instalada con QGIS. En otros sistemas, usa una terminal donde `ogr2ogr` esté en la ruta.

Descarga el GeoJSON enlazado arriba y guárdalo en tu carpeta de trabajo con el nombre `puntos_10000.geojson`. En la terminal, sitúate en esa carpeta. La ruta exacta depende de dónde hayas guardado el archivo.

## 2. Genera el archivo MBTiles

Ejecuta el comando en una sola línea:

```bat
ogr2ogr -f MBTILES puntos.mbtiles puntos_10000.geojson -nln puntos -dsco MINZOOM=0 -dsco MAXZOOM=12
```

El comando crea `puntos.mbtiles` a partir de `puntos_10000.geojson`. `-nln puntos` fija el nombre de la capa que se publicará, y `MINZOOM` y `MAXZOOM` determinan el intervalo de niveles para los que se generan teselas. El nivel máximo 12 permite explorar el conjunto sin crear niveles de detalle muy altos.

El controlador MBTiles de GDAL almacena las teselas en un archivo SQLite y admite teselas vectoriales MVT. La escritura vectorial requiere que la compilación de GDAL incluya GEOS, dependencia que incluye la distribución habitual de QGIS. La salida usa el sistema Web Mercator (EPSG:3857), aunque el GeoJSON de origen esté en longitud y latitud.

## 3. Comprueba la salida

Comprueba que el archivo `puntos.mbtiles` existe. Si tienes `ogrinfo` disponible, puedes inspeccionar su estructura y el recuento de entidades:

```bat
ogrinfo -ro -so puntos.mbtiles
```

Observa el nombre de la capa, el recuento de entidades y los campos disponibles. Debe aparecer la capa `puntos`, con 10.000 puntos y los atributos `nombre`, `tema` y `valor`. El nombre de la capa de teselas se utiliza después en la configuración del estilo.

Si repites la generación, elige otro nombre para el archivo de salida o elimina primero el archivo anterior: GDAL no puede crear de nuevo un archivo que ya existe en esa ruta.

!!! question "Comprobación de comprensión"

    ¿Qué parámetro cambiarías para generar teselas hasta un nivel de zoom más detallado? ¿Qué efecto esperas en el número de teselas generadas?

## Actividad de clase

**En parejas, 5–10 minutos:** generad el archivo, anotad el nombre de la capa y los campos que aparecen en `ogrinfo`, y comparad el tamaño del GeoJSON y del MBTiles.

**Resultado esperado:** un archivo `puntos.mbtiles` y una nota con el recuento de puntos, los campos y el tamaño de ambos archivos. MBTiles puede ocupar más espacio porque incluye varios niveles de zoom; la ventaja que se observará al consumirlo es que el cliente solicita las teselas de la vista actual en vez de descargar de una vez todo el GeoJSON.

## Ampliación: transformar un CSV de accidentes de Barcelona

Este segundo ejemplo muestra que `ogr2ogr` también puede convertir una tabla CSV con coordenadas en geometrías y generar teselas en un solo proceso. El conjunto de [vehículos implicados en accidentes de la Guardia Urbana](https://opendata-ajuntament.barcelona.cat/data/ca/dataset/accidents-vehicles-gu-bcn) incluye las columnas `Longitud_WGS84` y `Latitud_WGS84`. Descarga, por ejemplo, el [CSV de 2025](https://opendata-ajuntament.barcelona.cat/data/dataset/317e3743-fb79-4d2f-a128-5f12d2c9a55a/resource/7921ef46-5a4e-4f77-8c91-9d315664a6e4/download) y guárdalo en tu carpeta de trabajo. Si el portal publica otra versión, comprueba los encabezados y ajusta los nombres de las columnas del comando.

```bash
ogr2ogr -f MBTILES accidentes_barcelona.mbtiles 2025_accidents_vehicles_gu_bcn.csv \
  -oo X_POSSIBLE_NAMES=Longitud_WGS84 \
  -oo Y_POSSIBLE_NAMES=Latitud_WGS84 \
  -oo KEEP_GEOM_COLUMNS=NO \
  -oo EMPTY_STRING_AS_NULL=YES \
  -s_srs EPSG:4326 \
  -t_srs EPSG:3857 \
  -skipinvalid \
  -nln accidentes \
  -dsco MINZOOM=10 \
  -dsco MAXZOOM=17
```

GDAL interpreta longitud como X y latitud como Y. `-s_srs EPSG:4326` indica que las coordenadas del CSV están en WGS 84, y `-t_srs EPSG:3857` las reproyecta a Web Mercator. `-skipinvalid` omite las geometrías no válidas que no se puedan escribir en las teselas. `KEEP_GEOM_COLUMNS=NO` evita añadir las columnas originales de longitud y latitud como atributos duplicados. No combines `-a_srs` con `-t_srs`: para reproyectar se usan `-s_srs` y `-t_srs`.

Comprueba el resultado con:

```bat
ogrinfo -ro -so accidentes_barcelona.mbtiles
```

**Ten en cuenta:** cada fila describe un vehículo implicado y un accidente puede tener varios vehículos. Los puntos pueden coincidir; no interpretes el número de puntos como el número de accidentes únicos. El archivo contiene más atributos que quizá quieras publicar en un mapa: revisa la tabla y selecciona solo los campos necesarios antes de compartir el resultado. El conjunto está publicado bajo licencia CC BY 4.0; conserva su atribución.

Si quieres abrir este MBTiles con TileServer GL, cambia en `config.json` el nombre del archivo y configura el estilo para la capa interna `accidentes`.

## Fuentes y siguiente paso

- [Documentación de GDAL: controlador MBTiles y opciones de creación vectorial](https://gdal.org/en/stable/drivers/raster/mbtiles.html), consultada el 22 de noviembre de 2026.
- [Documentación de GDAL: controlador MVT](https://gdal.org/en/stable/drivers/vector/mvt.html).
- [Documentación de GDAL: opciones del controlador CSV, incluidas las columnas X/Y](https://gdal.org/en/stable/drivers/vector/csv.html).
- [Documentación de GDAL: opciones `-s_srs`, `-t_srs` y `-a_srs` de `ogr2ogr`](https://gdal.org/en/stable/programs/ogr2ogr.html).
- [Datos.gob.es: catálogo del conjunto de vehículos implicados en accidentes de Barcelona](https://datos.gob.es/es/catalogo/l01080193-vehiculos-implicados-en-accidentes-gestionados-por-la-guardia-urbana-en-la-ciudad-de-barcelona), distribución CSV de 2025 y licencia CC BY 4.0.

Continúa con [servir el archivo con TileServer GL Light](servir_teselas_vectoriales.md).

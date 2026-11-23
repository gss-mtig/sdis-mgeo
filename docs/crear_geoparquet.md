# Crear un archivo GeoParquet con GDAL

Convertirás el GeoJSON sintético de la práctica de publicación estática en un archivo Parquet con geometría y metadatos espaciales.

## Comprueba el controlador

Abre la terminal de QGIS (en Windows, **OSGeo4W Shell**) y ejecuta:

```bash
ogrinfo --formats
```

Busca el controlador `Parquet`. GDAL necesita haberse compilado con Apache Arrow/Parquet para leer y escribir estos archivos. La presencia de `ogr2ogr` no garantiza por sí sola que ese controlador esté instalado en todas las distribuciones de QGIS.

Si no aparece, anota la versión de QGIS/GDAL y utiliza una instalación preparada que incluya el controlador Parquet. No intentes resolverlo instalando paquetes en los equipos del aula durante la sesión.

## Convierte la capa

Descarga [puntos.geojson](ejemplos/publicacion_estatica/puntos.geojson) y, desde la carpeta donde lo guardaste, ejecuta:

```bash
ogr2ogr -f Parquet puntos.parquet puntos.geojson -nln puntos -lco COMPRESSION=SNAPPY -lco GEOMETRY_ENCODING=WKB
```

`-f Parquet` elige el contenedor. `-nln puntos` asigna un nombre claro a la capa. `COMPRESSION=SNAPPY` solicita compresión sin pérdida, y `GEOMETRY_ENCODING=WKB` usa una codificación de geometría ampliamente interoperable. El controlador incluye los metadatos necesarios de GeoParquet.

## Inspecciona el resultado

```bash
ogrinfo -ro -so puntos.parquet
```

Comprueba que aparecen los tres registros, la columna de geometría y los campos descriptivos. Guarda una copia como `puntos-generados.parquet` si quieres conservar el archivo de salida y comparar.

!!! question "Comprueba tu comprensión"

    ¿Qué aporta la geometría al archivo Parquet y qué ventaja puede tener el almacenamiento columnar cuando una tabla contiene muchos atributos?

**Resultado esperado:** un archivo `puntos.parquet` que contiene la geometría y los atributos del GeoJSON.

## Fuentes

- [Controlador Parquet de GDAL: codificación geométrica y compresión](https://gdal.org/en/stable/drivers/vector/parquet.html), consultado el 14 de noviembre de 2026.
- [GeoParquet: especificación y versiones](https://geoparquet.org/releases/).

**Siguiente:** [publicar el archivo GeoParquet](servir_geoparquet.md).

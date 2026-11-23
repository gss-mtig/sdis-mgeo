# Qué son las teselas vectoriales

Cuando navegamos por un mapa web, el navegador no suele descargar de una vez todos los datos del territorio. Solicita pequeñas piezas correspondientes a la zona visible y al nivel de zoom. Esas piezas son **teselas** (*tiles*). Una tesela vectorial contiene geometrías y atributos; el cliente web las dibuja con un estilo.

## De una capa a un conjunto de teselas

Imagina una capa de puntos de interés. En vez de enviar toda la capa cada vez que alguien abre el mapa, se prepara por adelantado un conjunto organizado por nivel de zoom y posición. El navegador pide solo las teselas necesarias mientras la persona desplaza o amplía el mapa.

En el esquema `z/x/y`, `z` indica el nivel de zoom y `x`, `y` identifican la tesela dentro de ese nivel. Al aumentar el zoom, hay más teselas y se muestra una zona menor con más detalle.

```text
Datos vectoriales originales
          │
          ├── preparación: recorte, simplificación y división por zoom
          ▼
Teselas vectoriales (geometrías + atributos)
          │
          ├── servidor de teselas
          ▼
Cliente web aplica el estilo y las dibuja
```

## Datos y estilo son cosas distintas

Una tesela vectorial suele guardar geometrías y algunos atributos, pero no decide por sí sola el color o el grosor con que se dibujan. El estilo se aplica en el cliente de mapas. Así, una misma fuente de teselas puede representarse de maneras diferentes sin volver a generar los datos.

El formato **Mapbox Vector Tile (MVT)** es una codificación común para las teselas vectoriales. Los datos MVT suelen transmitirse como archivos binarios `.pbf`. La especificación describe cómo codificar las capas, entidades, geometrías y atributos de cada tesela.

## MVT y MBTiles no son lo mismo

Conviene distinguir estos dos términos:

- **MVT** describe cómo se codifica el contenido vectorial de una tesela.
- **MBTiles** es un contenedor SQLite que organiza teselas y metadatos en un solo archivo. Puede almacenar teselas ráster o vectoriales; cuando almacena vectoriales, estas pueden estar codificadas como MVT.

Por eso en esta práctica generaremos un archivo `.mbtiles` que contiene teselas vectoriales. No significa que MBTiles sea el formato de codificación de las geometrías.

## ¿Cuándo convienen?

Las teselas vectoriales son útiles para mapas web interactivos que deben cargar con rapidez, ofrecer varios niveles de detalle y permitir cambiar el estilo en el navegador. También reducen la cantidad de información enviada para cada vista respecto a descargar una capa completa.

Tienen límites: durante la preparación se pueden simplificar o recortar geometrías y excluir atributos. Por ello, no deben considerarse automáticamente una copia íntegra de los datos originales ni un sustituto de un archivo de descarga, una API de entidades o una base de datos para análisis. Conserva y publica el dato original por separado cuando sea necesario.

## Relación con otros servicios

Un servidor como TileServer GL puede ofrecer las teselas a clientes de mapas web. El protocolo de teselas vectoriales MVT también se utiliza en implementaciones relacionadas con **OGC API – Tiles**; en esta lección nos centraremos en preparar un archivo y servirlo, sin estudiar el estándar de servicio en detalle. Una tesela vectorial tampoco es un WMS: WMS devuelve una imagen de mapa, mientras que estas teselas contienen datos vectoriales codificados que un cliente puede dibujar.

## Ejemplo en España: unidades administrativas del IGN

El IGN publica las unidades administrativas de España como teselas vectoriales MVT. La plantilla de acceso a los datos es [`https://vt-unidades-administrativas.ign.es/1.0.0/uadministrativa/{z}/{x}/{y}.pbf`](https://vt-unidades-administrativas.ign.es/1.0.0/uadministrativa/%7Bz%7D/%7Bx%7D/%7By%7D.pbf); para visualizarla, el IGN ofrece un [estilo gris](https://vt-unidades-administrativas.ign.es/demo/style_s3_cloud.json) y un [estilo verde](https://vt-unidades-administrativas.ign.es/demo/style_s3_green.json). El estilo define la representación; no forma parte de los datos de cada tesela.

La [ficha del servicio en el catálogo de la IDEE](https://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/metadata/spaignmvt_unidades_administrativas) describe el recurso. En la [página del IGN con estilos para teselas vectoriales](https://www.ign.es/web/estilos-de-los-servicios-de-teselas-vectoriales) puedes consultar los enlaces actualizados. En [consumir teselas vectoriales](consumir_teselas_vectoriales.md) usamos este servicio desde QGIS y MapLibre.

## Actividad breve: ¿qué publicarías?

Piensa en una capa de equipamientos municipales que se quiere mostrar en una web:

1. ¿Qué atributos necesitaría el mapa para dibujar y etiquetar los equipamientos?
2. ¿Qué información convendría conservar en el conjunto de descarga original, aunque no se incluya en las teselas?
3. ¿Publicarías solo teselas o también el dato original? Explica para qué serviría cada acceso.

**Resultado esperado:** distinguir la capa de origen, el subconjunto preparado para visualización y el estilo del cliente.

## Fuentes

- [Documentación de GDAL: Mapbox Vector Tiles (MVT)](https://gdal.org/en/stable/drivers/vector/mvt.html), consultada el 14 de noviembre de 2026.
- [Documentación de GDAL: MBTiles](https://gdal.org/en/stable/drivers/raster/mbtiles.html), consultada el 14 de noviembre de 2026.
- [Conceptos de teselas vectoriales en los materiales de Geoservicios para Smart Cities](https://github.com/gss-mtig/gss-mtig/blob/v25.26/docs/3_conceptos_vector_tiles.md).
- [IGN: estilos para servicios de teselas vectoriales](https://www.ign.es/web/estilos-de-los-servicios-de-teselas-vectoriales).
- [IDEE: ficha del servicio MVT de unidades administrativas](https://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/metadata/spaignmvt_unidades_administrativas).

**Siguiente:** [crear las teselas con `ogr2ogr`](crear_teselas_vectoriales.md).

# Qué es un Cloud Optimized GeoTIFF

Un **Cloud Optimized GeoTIFF (COG)** es un GeoTIFF dispuesto para poder leer partes de una imagen remota sin descargarla entera. Sigue siendo un archivo ráster TIFF/GeoTIFF; su organización interna añade teselas y niveles de resolución reducida (*overviews*) colocados para que los programas encuentren los bloques que necesitan con pocas peticiones HTTP.

La optimización depende de dos piezas que trabajan juntas:

1. El archivo está estructurado con teselas internas y overviews.
2. El servidor permite pedir rangos de bytes del archivo mediante HTTP (`Range`).

Al abrir un COG remoto, un cliente compatible puede descargar metadatos y solo los bloques necesarios para la zona y escala visibles. Si el servidor no permite esas peticiones, el COG no ofrece la misma ventaja de acceso parcial.

## Qué resuelve y qué no

Un COG facilita distribuir y leer rásteres grandes desde almacenamiento HTTP u objetos en la nube. Se usa con imágenes de satélite, ortofotos, modelos de elevación y otros datos ráster.

El COG **no es un servicio de mapas**: es un archivo. Tampoco decide por sí mismo una simbología ni reemplaza al dato original para todos los flujos de análisis. El cliente aplica una representación y solicita los bloques. Para publicar un mapa ya renderizado se pueden usar servicios de mapas o teselas ráster.

El formato se basa en GeoTIFF y el [estándar COG del OGC](https://docs.ogc.org/is/21-026/21-026.html) fija requisitos tanto de organización del archivo como del acceso remoto por rangos. Es un estándar OGC aprobado.

## Flujo de la práctica

En las páginas siguientes usarás un recorte real de la ortofoto territorial en color del ICGC, localizado a través de su ficha en el catálogo de la IDEC. Descargarás una zona pequeña en GeoTIFF, la convertirás a COG con GDAL, la servirás en tu ordenador mediante HTTP con soporte de rangos y la abrirás en QGIS. La ficha consultada corresponde a la cobertura de 2024 e indica una resolución de 25 cm y licencia CC BY 4.0.

La práctica descarga solo un área reducida para que el archivo sea manejable. Conserva la atribución al ICGC al reutilizar la imagen.

**Siguiente:** [crear un COG con GDAL](crear_cog.md).

## Fuentes

- [Estándar OGC Cloud Optimized GeoTIFF, versión 1.0](https://docs.ogc.org/is/21-026/21-026.html), aprobado en 2023.
- [IDEC: ficha de la Ortofoto en color de Catalunya 25 cm, cobertura 2024](https://catalegs.ide.cat/geonetwork/srv/api/records/ortofoto-25cm-v4r0-color-2024?language=cat).
- [ICGC: visor de descargas](https://visors.icgc.cat/appdownloads/).
- [Controlador COG de GDAL](https://gdal.org/en/stable/drivers/raster/cog.html), consultado el 14 de noviembre de 2026.
- [Sistemas virtuales de archivo de GDAL y acceso remoto con `/vsicurl/`](https://gdal.org/en/stable/user/virtual_file_systems.html).

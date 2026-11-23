# Publicar un archivo GeoParquet

GeoParquet es un archivo, no un servicio. Para compartir una capa pequeña, puedes alojar el `.parquet` en un sitio estático o almacenamiento de archivos accesible por HTTPS y enlazarlo desde una ficha de datos. El cliente lo descarga o lo abre si reconoce el formato.

## Publicación sencilla en GitHub Pages

Como práctica, coloca `puntos.parquet` en la carpeta de un repositorio configurado para publicar archivos estáticos mediante GitHub Pages. Sigue el mismo flujo que en [la lección de publicación de GeoJSON estático](publicar_geojson_estatico.md): los datos se alojan como archivo y la página web puede enlazar su descarga.

Una vez publicado, la URL sigue la forma:

```text
https://<usuario>.github.io/<repositorio>/datos/puntos.parquet
```

Usa una URL HTTPS directa al archivo, no una página HTML de vista previa de GitHub. Para conjuntos grandes o actualizados con frecuencia, selecciona un almacenamiento y un proceso de distribución adecuados al tamaño, las licencias y las necesidades de acceso.

## Comprueba la publicación

1. Abre la URL en el navegador y confirma que responde con el archivo.
2. Descarga el archivo y compara su tamaño con el generado localmente.
3. Comprueba que la dirección no requiere iniciar sesión.
4. Enlaza el archivo desde una ficha descriptiva e incluye productor, fecha, licencia, CRS y campos relevantes.

El hecho de que la descarga funcione no implica que todos los clientes puedan analizarlo directamente desde la URL. Las capacidades de lectura remota dependen de GDAL, Arrow y el cliente; para la siguiente práctica puedes descargar el archivo antes de abrirlo en QGIS.

## Actividad breve

**En parejas, 5 minutos:** redactad la URL que compartiríais con otra persona y enumerad tres datos de la ficha descriptiva que debe acompañar al archivo.

**Resultado esperado:** enlace directo al `.parquet` y una nota con CRS, licencia y fecha o productor.

**Siguiente:** [consumir el archivo GeoParquet en QGIS](consumir_geoparquet.md).

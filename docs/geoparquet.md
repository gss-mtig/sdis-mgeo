# Qué es GeoParquet

**Apache Parquet** es un formato columnar: organiza los datos por columnas en lugar de guardar cada fila completa una detrás de otra. Esto permite leer solo las columnas necesarias y aplicar compresión de forma eficiente, algo útil para conjuntos tabulares grandes.

**GeoParquet** añade a Parquet metadatos y convenciones para que las geometrías y los sistemas de referencia se interpreten de forma interoperable. Una geometría puede almacenarse como WKB (Well-Known Binary), y el archivo incluye metadatos que identifican la columna geométrica y el CRS.

## ¿Para qué sirve?

GeoParquet es adecuado para intercambiar o analizar conjuntos vectoriales grandes en flujos de trabajo de datos y computación en la nube. Puede contener atributos tabulares y geometrías en un archivo compacto. No es un servicio web: el archivo se descarga o se consulta mediante herramientas que entienden Parquet y GeoParquet.

No sustituye siempre a GeoPackage, GeoJSON o una base de datos. Para edición de escritorio o pequeños conjuntos de datos, GeoPackage puede ser más cómodo; para intercambio sencillo con aplicaciones web, GeoJSON puede resultar más accesible. La compatibilidad depende de las versiones de los programas y de la especificación escrita.

La especificación comunitaria publica versiones con niveles de soporte diferentes: a fecha de consulta, el sitio del proyecto lista GeoParquet 2.0.0 como la versión más reciente, mientras que el controlador GDAL estable documenta soporte de lectura y escritura hasta 1.1.0. Para priorizar la compatibilidad del ejercicio usaremos la versión que escriba el GDAL instalado y comprobaremos si incluye el controlador.

## Flujo de la práctica

Convertiremos el GeoJSON sintético de tres puntos que ya usamos en el curso a Parquet, lo publicaremos como un archivo estático descargable y lo abriremos desde QGIS.

**Siguiente:** [crear un archivo GeoParquet con GDAL](crear_geoparquet.md).

## Fuentes

- [Especificación y versiones de GeoParquet](https://geoparquet.org/releases/), consultada el 14 de noviembre de 2026.
- [Documentación GDAL del controlador (Geo)Parquet](https://gdal.org/en/stable/drivers/vector/parquet.html), consultada el 14 de noviembre de 2026.
- [Apache Parquet](https://parquet.apache.org/).

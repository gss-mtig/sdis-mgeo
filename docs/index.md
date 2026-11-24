# Infraestructuras de datos espaciales y estándares de geoservicios

Materiales para la asignatura de Infraestructuras de Datos Espaciales (IDEs) del Máster de Geoinformación de la UAB.

## Recorrido: descubrir y evaluar recursos en una IDE

1. [Qué es una IDE](introduccion_a_las_ides.md): sus componentes y el papel de la interoperabilidad.
2. Metadatos, en este orden:
   - [Qué son los metadatos](metadatos.md).
   - [Cómo funciona un catálogo de metadatos](catalogo_metadatos.md).
   - [Qué estándares los describen](estandares_ISO.md).
   - [Cómo crear metadatos](creacion_metadatos.md).
3. [Iniciativas de IDE y marco legal](iniciativas_ides.md): ejemplos de Cataluña, España y Europa.
4. [Caso práctico](caso_idec_inundaciones.md): búsqueda y comparación de dos recursos del catálogo IDEC.
5. [Ejercicio de aplicación](ejercicio_aplicado_ide.md): plantea un problema propio y resuélvelo usando otra IDE.

## Recorrido: servicios interoperables y estándares geoespaciales

1. [Interoperabilidad y estándares OGC](estandares_OCG.md): por qué se necesitan estándares compartidos.
2. [WMS](wms.md): solicitar y consultar mapas como imágenes.
3. [Descarga ATOM](descarga_atom.md): localizar y descargar conjuntos municipales INSPIRE.
4. [Pirámides de teselas ráster](piramides_teselas.md): comprender XYZ y compararlo con WMTS y OGC API – Tiles.
5. [De los servicios clásicos a las OGC API](api.md): entender las correspondencias y sus límites.
6. [OGC API – Features](ogc_api_features.md): descubrir colecciones y consultar entidades con GeoJSON.
7. [Panorama de otros estándares](otros.md): reconocer otras familias y formatos.

## Otros materiales

- [GeoJSON](geojson.md)
- [Clientes de mapas](clientes_de_mapa.md)
- [Servidores de mapas: panorama y alternativas](servidores_de_mapa.md)
- Materiales en revisión: [publicar con QGIS Server](qgis_server.md) y [georreferenciación](georeferenciacion.md).
- Publicar datos:
  - [Archivo estático en GitHub Pages](publicar_geojson_estatico.md)
  - [Base de datos online con Supabase](bd_online.md)
- Teselas vectoriales:
  - [Qué son las teselas vectoriales](teselas_vectoriales.md)
  - [Crearlas con `ogr2ogr`](crear_teselas_vectoriales.md)
  - [Servirlas con TileServer GL Light](servir_teselas_vectoriales.md)
  - [Consumirlas en QGIS y MapLibre GL JS](consumir_teselas_vectoriales.md)
- Catálogos STAC:
  - [Descubrir datos con un catálogo STAC](catalogo_stac.md)
  - [Explorar y consumir un catálogo Portolan](portolan.md)
- Cloud Optimized GeoTIFF (COG):
  - [Qué es un COG](cog.md)
  - [Crear un COG con GDAL](crear_cog.md)
  - [Servir un COG por HTTP](servir_cog.md)
  - [Consumir un COG en QGIS](consumir_cog.md)
- GeoParquet:
  - [Qué es GeoParquet](geoparquet.md)
  - [Crear GeoParquet con GDAL](crear_geoparquet.md)
  - [Publicar un archivo GeoParquet](servir_geoparquet.md)
  - [Consumir GeoParquet en QGIS](consumir_geoparquet.md)
- [Instalación de programas](instalacion_de_programas.md)

## Ejercicio final

[Descubre y publica datos geográficos](ejercicio_final_ide.md): integra lo aprendido para buscar datos en una IDE, evaluar su ficha, descargarlos, publicarlos y crear una visualización.

## Autores

* Wladimir Szczerban (alias Bolo), [X (@bolosig)](https://x.com/bolosig), [LinkedIn](https://www.linkedin.com/in/bolosig/), [MapTiler](http://maptiler.com) (Departamento de Geografía UAB)

!!! note "Condiciones de reutilización de estos apuntes"

    Estos materiales están publicados bajo licencia
    [CreativeCommons (by-sa) 4.0 internacional](https://creativecommons.org/licenses/by-sa/4.0/deed.es_ES)

    Usted es libre de:
    * Compartir — copiar y redistribuir el material en cualquier medio o formato
    * Adaptar — remezclar, transformar y crear a partir del material para cualquier finalidad, incluso comercial.

    Bajo las condiciones siguientes:

    * Reconocimiento — Debe reconocer adecuadamente la autoría, proporcionar un enlace a la licencia e indicar si se han realizado cambios. Puede hacerlo de cualquier manera razonable, pero no de una manera que sugiera que tiene el apoyo del licenciador o lo recibe por el uso que hace.
    
    * Compartir igual — Si remezcla, transforma o crea a partir del material, deberá difundir sus contribuciones bajo la misma licencia que el original.
    
    * No hay restricciones adicionales — No puede aplicar términos legales o medidas tecnológicas que legalmente restrinjan realizar aquello que la licencia permite.

**Empieza el recorrido:** [Qué es una IDE](introduccion_a_las_ides.md).

# Servidores de mapas
    
## Qué es un geoservicio?

Un geoservicio es un servidor que ofrece algún servicio relacionado con el ámbito SIG, su principal función es acceder a información geoespacial existente en diferentes formatos y servir dicha información a clientes a través de protocolos estándares.

El servidor es el elemento encargado de ofrecer el servicio como tal, respondiendo a las peticiones del cliente. A medida que los clientes se hacen más complejos y presentan mayor número de funcionalidades, también los servidores deben ser capaces de proporcionar servicios más elaborados.

## Qué es un servidor de mapas?

Es un servidor que provee cartografía a través de la red tanto en modo vectorial como en ráster.
    
## Servidores de mapas estándar

Son servidores de mapas que cumplen los estándares OGC de WMS y/o WFS. 

Algunos software de servidores de mapas son:

### UMN Mapserver 

Es un servidor de código abierto programado en C/C++, permite compartir y editar datos geoespaciales. Originalmente fue desarrollado por la Universidad de Minnesota (UMN) y por eso también se le conoce como Minnesota MapServer para diferenciarlo del producto comercial “map server” de Autodesk. Implementa las especificaciones Web Map Service (WMS) (cliente/servidor), Web Feature Service no-transaccional (WFS) (cliente/servidor), Web Map Context (WMC), Web Coverage Service(WCS), Filter Encoding, Styled Layer Descriptor (SLD), Geography Markup Language (GML), Sensor Observation Service (SOS), Observations and Measurements (OM).

http://www.mapserver.org/

**Principales características**

* Proporciona una API (MapScript) que permite acceder a las funcionalidades de MapServer desde diferentes lenguajes de programación como PHP, Java, Python, Perl, Ruby y .NET (C#).
* Soporta múltiples formatos de entrada (vectorial/ráster) y salida ya que usa GDAL/OGR.
* Soporta fuentes TrueType (útil para el etiquetado de elementos).
* Configuración “al vuelo” vía parámetros GET pasados por URL.
* Configuración basada en el fichero mapfile .map.
* Incluye la posibilidad de usar una plantilla HTML MapServer para generar una página web.
* Es multiplataforma
* Incluye un componente de cacheado MapCache para generar pirámides de teselas (tiles) con la finalidad de acelerar y optimizar la respuesta a la hora de servir mapas. Soporta el estándar WMTS, también soporta otras salidas como TMS, VirtualEarth/Bing y peticiones Google Maps.
* Incluye un componente TinyOWS que da soporte para edición de datos a través del protocolo WFS transactional (WFS-T).
* Mapbox Vector Tile (MVT)

### GeoServer

Es un servidor de código abierto programado en Java, permite compartir y editar datos geoespaciales. GeoServer sirve de implementación de referencia del estándar Web Feature Service (WFS) de la OGC, también implementa las especificaciones Web Map Service (WMS) y Web Coverage Service(WCS).

http://geoserver.org/

**Principales características**

* Fácil utilización y administración a través de una herramienta de administración web. No es necesario tocar archivos de configuración.
* Soporte para edición de datos a través del protocolo WFS transactional (WFS-T).
* Al ser programado en Java está basado en servlets (JEE), puede funcionar en cualquier contenedor de servlets. Es multiplataforma.
* Es compatible para ser usado con extensiones.
* Incluye integrado un cliente OpenLayers que permite visualizar las capas de datos.
* Incluye un componente de cacheado GeoWebCache para generar pirámides de teselas (tiles) con la finalidad de acelerar y optimizar la respuesta a la hora de servir mapas. Soporta los estándares WMS-C y WMTS, también soporta otras salidas como TMS, Google Maps KML, Virtual Earth.
* Hay formatos y opciones de publicación adicionales disponibles como extensiones, incluido el Servicio de procesamiento web (WPS) y el Servicio de mosaicos de mapas web (WMTS).
* Produce mosaicos vectoriales en tres formatos: GeoJSON, TopoJSON y MapBox Vector (MVT)

### Maproxy 

Es un proxy de código abierto para datos geoespaciales. Almacena en caché, acelera y transforma los datos de los servicios de mapas existentes y sirve a cualquier cliente GIS de escritorio o web.

https://mapproxy.org

MapProxy no es sólo una solución de caché de mosaico, también ofrece muchas características nuevas e innovadoras como soporte completo para clientes WMS.

**Principales características**

* Sirve como cache de teselas
* Reprojecta WMS y teselas a otros SRS
* Guardar teselas identicas sólo una vez (Ej. teselas del mar)
* Permite manipular las bandas de las imagenes para crear imagenes de otros colores (Ej. escala de grises)
* Permite pregenerar caches (Seeding) de areas determinadas
* Combina múltiples capas y servicios

### QGIS Server 

Es una implementación de código abierto WMS 1.3, WFS 1.0.0, WFS 1.1.0 y WCS 1.1.1 que, además, implementa características cartográficas avanzadas para mapeo temático. QGIS Server es una aplicación FastCGI / CGI (Common Gateway Interface) escrita en C ++ que funciona junto con un servidor web (por ejemplo, Apache, Nginx). Tiene compatibilidad con el complemento Python, lo que permite un desarrollo e implementación rápidos y eficientes de nuevas funciones.

https://docs.qgis.org/testing/en/docs/user_manual/working_with_ogc/server/index.html

**Principales características**

* QGIS Server utiliza QGIS como back-end para la lógica GIS y para la representación de mapas. Además, la biblioteca Qt se utiliza para gráficos y para programación C ++ independiente de la plataforma. A diferencia de otro software WMS, el QGIS Server utiliza reglas cartográficas como lenguaje de configuración, tanto para la configuración del servidor como para las reglas cartográficas definidas por el usuario.
* Como QGIS Desktop y QGIS Server utilizan las mismas bibliotecas de visualización, los mapas que se publican en la web tienen el mismo aspecto que en el GIS de escritorio.


### Cómo preparar la geoinformación
    * BBDD
    * RAW data
    * Pirámides cache

## Práctica implementar un servidor de mapas
## Otros estándares OGC

### Web Map Context (WMC)

Especifica formato estandarizado para almacenar un contexto. Un contexto recoge la información necesaria para reproducir las condiciones de una determinada sesión de uso de un cliente, de tal forma que ese cliente pueda restablecerlas posteriormente. El contexto se almacena en un archivo XML. [^2]

En el contexto se almacena información sobre las capas que forman el mapa representado por el cliente y los servidores de los que estas se obtienen, la región cubierta por el mapa, así como información adicional para anotar este mapa.

Permite:
* Crear vistas predefinidas, mapas temáticos
* Guardar Y/o cargar on-line estas vistas

Se puede ver la especificación en [https://www.ogc.org/standards/wmc](https://www.ogc.org/standards/wmc)

### Keyhole Markup Language (KML)

Es un lenguaje XML centrado en la descripción y visualización de la geoinformación en actuales y futuras aplicaciones webs de gestión de mapas (2d y 3d). 

Este lenguaje fue presentado por Google al OGC con el objetivo de incorporarlo como un estándar. Actualmente OGC y Google trabajan en colaboración para asegurar este proceso.

Se puede ver la especificación en [https://www.ogc.org/standards/kml](https://www.ogc.org/standards/kml)

### Web Coverage Service(WCS)

Amplía la interfaz Web Map Server para permitir el acceso a "coberturas" geoespaciales que representen valores o propiedades de localizaciones geográficas; más que los mapas generados por WMS (imágenes). 

La diferencia principal con el WMS es que el servicio WCS proporciona los datos junto con su descripción detallada, define peticiones con una sintaxis rica para obtener esos datos y devuelve la información con su semántica original, lo cual permite que puedan ser interpretados, extrapolados, etc., y no sólo representados de forma estática.

Básicamente sirve para descargar archivos raster a escala 1 a 1 y preparados para poder trabajarlos en un sig raster.

Principales interfaces:
* GetCapabilities
* DescribeCoverage
* GetCoverage

### Web Processing Service (WPS)

Servicio de publicación de procesos geoespaciales en la Web. Se entiende por procesos cualquier algoritmo, cálculo o modelo, que opere sobre datos espacialmente referenciados tanto en formato raster como vectorial, de este modo un WPS puede ofrecer cualquier tipo de funcionalidad GIS a través de una red.

Se puede ver la especificación en [https://www.ogc.org/standards/wps](https://www.ogc.org/standards/wps)

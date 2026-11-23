# Panorama de otros estándares OGC

Además de WMS y OGC API – Features, encontrarás estándares OGC para otras tareas. No hace falta estudiarlos todos con el mismo detalle: identifica qué problema resuelven y comprueba qué estándar y versión declara cada servicio.

| Estándar o familia | Para qué sirve | Evolución o relación |
|---|---|---|
| **WMTS** | Entrega mapas en teselas precalculadas, normalmente para mostrarlos con rapidez. | OGC API – Tiles ofrece una evolución basada en recursos web y permite teselar diferentes tipos de información. |
| **WCS** | Da acceso a coberturas, como datos ráster que se quieren consultar o procesar como valores. | OGC API – EDR cubre patrones de consulta útiles para datos medioambientales; no es un reemplazo universal de WCS. |
| **WPS** | Publica procesos geoespaciales que un cliente puede solicitar al servidor. | OGC API – Processes define una interfaz web moderna para describir y ejecutar procesos. |
| **SOS** | Facilita el acceso a observaciones de sensores mediante operaciones de servicio. | SensorThings API ofrece un modelo y una API modernos para datos de sensores; no es simplemente una nueva versión de SOS. |
| **GML** | Codifica entidades geográficas en XML. Es un formato, no un servicio. | Puede utilizarse con WFS y otras aplicaciones que necesiten esa codificación. GeoJSON es otra opción común en servicios web actuales. |
| **SLD / Symbology Encoding** | Describe estilos cartográficos que algunos servicios de mapas pueden aplicar. | Es una especificación de estilo; no es una API de acceso a datos ni todas las implementaciones WMS la admiten. |
| **KML** | Codifica elementos y estilos para visualización geográfica, especialmente en globos y visores. | Es un formato de intercambio y visualización, no un servicio de mapas. |
| **WMC** | Guardaba el contexto de un cliente de mapas: capas, vistas y servicios de una sesión. | Es una especificación heredada; no forma parte del recorrido práctico de esta asignatura. |

Estas relaciones no siempre son equivalencias uno a uno. Las OGC API se organizan en estándares modulares, algunas partes ya están aprobadas y otras continúan en desarrollo. Para nuevas implementaciones, OGC recomienda considerar las API modernas; los servicios clásicos siguen utilizándose y conviene poder reconocerlos.

Para profundizar, consulta el [catálogo oficial de estándares OGC](https://www.ogc.org/standards/) y la [familia OGC API](https://ogcapi.ogc.org/).

**Siguiente:** [GeoJSON: leer y usar datos geográficos en la Web](geojson.md).

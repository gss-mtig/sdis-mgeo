# De los servicios OGC a las OGC API

Las OGC API forman una familia de estándares web modulares. Cada estándar describe recursos y operaciones para una tarea geoespacial. Las respuestas pueden incluir HTML para navegar desde un navegador y formatos legibles por aplicaciones, como JSON. OpenAPI documenta las operaciones y parámetros disponibles.

Una API suele ofrecer una página de entrada desde la que se siguen enlaces a recursos relacionados: colecciones, elementos, mapas, teselas, registros o procesos. No todas las API ofrecen las mismas operaciones ni todos los servicios implementan las mismas partes del estándar.

## Cómo se relacionan con los estándares clásicos

Las asociaciones siguientes sirven para orientarse. Son continuidades funcionales, no siempre equivalencias exactas:

| Necesidad                        | Estándar clásico | OGC API relacionada                                      | Relación general                                                                                                 |
| -------------------------------- | ---------------- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Ver un mapa como imagen          | WMS              | [OGC API – Maps](https://ogcapi.ogc.org/maps/)           | Permite descubrir y solicitar mapas mediante una API web.                                                        |
| Consultar entidades geográficas  | WFS              | [OGC API – Features](https://ogcapi.ogc.org/features/)   | Expone colecciones y elementos para descubrirlos y consultarlos.                                                 |
| Obtener mapas o datos en teselas | WMTS             | [OGC API – Tiles](https://ogcapi.ogc.org/tiles/)         | Evoluciona el acceso a teselas y puede servir distintos tipos de datos teselados, incluidas teselas vectoriales. |
| Buscar fichas descriptivas       | CSW              | [OGC API – Records](https://ogcapi.ogc.org/records/)     | Ofrece patrones web modernos para descubrir y consultar registros de metadatos.                                  |
| Ejecutar un proceso geoespacial  | WPS              | [OGC API – Processes](https://ogcapi.ogc.org/processes/) | Permite describir y ejecutar procesos mediante una API.                                                          |

El servicio **SOS** se relaciona con datos de sensores y observaciones; en iniciativas actuales también puede encontrarse **SensorThings API**, que tiene su propio modelo y no debe presentarse como un simple cambio de versión de SOS. **GML**, por su parte, es un formato de datos, no un servicio; puede aparecer como codificación en algunos flujos clásicos y modernos.

## Qué cambia en la experiencia web

En muchos servicios clásicos, el cliente envía operaciones con parámetros como `REQUEST=GetMap` o `REQUEST=GetFeature`. En una OGC API, el navegador puede recorrer URL que identifican recursos y seguir sus enlaces. Por ejemplo, una API de entidades suele exponer una página inicial, sus colecciones y los elementos de cada colección.

Esto facilita explorar el servicio desde un navegador y conectar aplicaciones web. Pero la interfaz web no elimina la necesidad de comprender el recurso: hay que revisar qué colección se consulta, qué propiedades contiene, qué formato devuelve, qué sistema de referencia utiliza y qué licencia se aplica.

## Aprobado y en desarrollo

OGC API no es un estándar único. Cada familia se divide en partes que tienen su propio estado. Por ejemplo, OGC API – Features Part 1: Core y Part 2: CRS by Reference son estándares aprobados; otras partes de Features siguen en desarrollo. OGC API – Records Part 1: Core está aprobado, mientras que sus partes 2 y 3 figuran como borradores en la documentación de OGC consultada el **5 de noviembre de 2026**. Antes de implementar una capacidad, comprueba el estado de la parte concreta en la página oficial correspondiente.

Continúa con [OGC API – Features](ogc_api_features.md) o consulta el [panorama de otros estándares](otros.md).

## Fuentes

- [OGC API: visión general](https://ogcapi.ogc.org/).
- [OGC API – Features](https://ogcapi.ogc.org/features/).
- [OGC API – Maps](https://ogcapi.ogc.org/maps/).
- [OGC API – Tiles](https://ogcapi.ogc.org/tiles/).
- [OGC API – Records](https://ogcapi.ogc.org/records/).
- [OGC API – Processes](https://ogcapi.ogc.org/processes/).

**Siguiente:** [OGC API – Features](ogc_api_features.md).

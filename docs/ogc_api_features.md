# OGC API – Features: acceder a entidades geográficas

Un WMS entrega una imagen de mapa. **OGC API – Features** permite descubrir colecciones de datos vectoriales y consultar sus entidades —puntos, líneas o polígonos— junto con sus propiedades.

La API organiza la información como recursos relacionados. Puedes navegar desde la página de entrada a las colecciones, y desde cada colección a sus entidades. Muchos servicios muestran páginas HTML para las personas y ofrecen las mismas entidades en GeoJSON para aplicaciones.

## Actividad práctica en clase: rastrear una entidad — 25 minutos

**Objetivo:** recorrer una OGC API desde su página de entrada hasta una entidad y reconocer qué aporta su representación GeoJSON.

**Materiales:** navegador web y la API de entidades del [Instituto Geográfico Nacional de España (IGN)](https://api-features.ign.es/). La página de entrada y sus colecciones respondieron en la consulta realizada el **5 de noviembre de 2026**. Al ser un servicio externo, su disponibilidad puede cambiar.

**Pasos:**

1. Abre la [página de entrada de la API](https://api-features.ign.es/). Identifica el proveedor y la descripción del servicio.
2. Entra en [Collections](https://api-features.ign.es/collections). Esta página enumera los conjuntos de información disponibles.
3. Abre la colección [AU Administrative unit](https://api-features.ign.es/collections/administrativeunit). Revisa su descripción, licencia, referencia espacial y enlaces.
4. Sigue el enlace para explorar los elementos de la colección. Abre uno, por ejemplo el registro [Abla](https://api-features.ign.es/collections/administrativeunit/items/1166238), y revisa sus propiedades.
5. En la página del elemento, abre el enlace de formato JSON. La representación GeoJSON permite ver la geometría y las propiedades estructuradas.
6. En pareja, comparad la representación HTML con GeoJSON. Después decidid cuál usaríais para mostrar un mapa y cuál os permitiría inspeccionar y reutilizar las entidades y sus atributos.

**Resultado:** una captura anotada con el nombre de la colección, el ID de una entidad, dos propiedades, su tipo de geometría y el orden de coordenadas.

**Reflexiona:** ¿por qué consultar una entidad en GeoJSON ofrece posibilidades distintas a pedir una imagen con WMS?

Si el servidor no responde, usa el [ejemplo GeoJSON local](ejemplos/ogcapi_features/feature-ejemplo.geojson) para identificar `FeatureCollection`, `Feature`, `geometry` y `properties`. El ejemplo es didáctico y no reproduce los datos del IGN; la navegación por colecciones quedará pendiente hasta recuperar la conexión.

## Reconocer los recursos

| Recurso | Qué puedes averiguar |
|---|---|
| Página de entrada | Quién ofrece la API, qué contiene y dónde seguir navegando. |
| `/conformance` | Qué clases de conformidad declara la implementación. |
| `/collections` | Qué colecciones ofrece el servicio. |
| `/collections/{id}` | Qué describe una colección y qué enlaces ofrece. |
| `/collections/{id}/items` | Qué entidades contiene, con opciones de paginación o consulta que dependen del servicio. |
| `/collections/{id}/items/{itemId}` | Una entidad concreta, con su geometría y propiedades. |

Los nombres y capacidades disponibles se deben leer en la documentación del servicio. No todas las API implementan todas las partes ni todos los parámetros opcionales.

## GeoJSON y sistemas de referencia

Las entidades suelen servirse como **GeoJSON**, un formato que representa objetos con geometría y propiedades. Su estructura más común incluye:

- una `FeatureCollection`, que agrupa entidades;
- cada `Feature`, con un identificador, `geometry` y `properties`;
- una geometría (`Point`, `LineString`, `Polygon`, etc.) con sus coordenadas.

La parte *Core* de OGC API – Features usa por defecto coordenadas en WGS 84 con orden de ejes longitud-latitud, compatible con GeoJSON de RFC 7946. Otras referencias espaciales dependen de las partes implementadas por el servicio; comprueba la colección y los enlaces que declara antes de interpretar coordenadas.

## Cómo se relaciona con WFS

**Web Feature Service (WFS)** también permite acceder a entidades geográficas. OGC API – Features ofrece una interfaz web más reciente basada en recursos y prácticas como REST, con navegación por URL y respuestas web. WFS sigue presente en muchos servicios; OGC recomienda Features para implementaciones nuevas que necesiten las funciones de acceso a entidades de WFS.

OGC API – Features se compone de partes. Part 1: Core y Part 2: CRS by Reference son estándares aprobados; Part 3: Filtering también está aprobada. Otras capacidades, como las transacciones para crear o modificar entidades, están en partes que siguen en desarrollo. Estado consultado el **5 de noviembre de 2026** en la [página oficial de OGC API – Features](https://ogcapi.ogc.org/features/).

## Ejercicio evaluable: explora una OGC API – Features

!!! question "Ejercicio 1 punto"

    Elige una **OGC API – Features publicada por cualquier IDE**. Puede ser de tu comunidad autónoma, de España, de otro país o una IDE temática. No es obligatorio usar el servicio del IGN de la práctica guiada.

    En un documento breve, incluye enlaces a la página de entrada de la API, a una colección y a una entidad. Añade capturas legibles de la colección y de la entidad, y responde:

    - ¿Qué IDE y organismo ofrecen la API? ¿Qué información publica?
    - ¿Qué colección elegiste y qué representa?
    - ¿Qué identificador tiene la entidad y qué dos propiedades puedes interpretar?
    - ¿Qué tipo de geometría devuelve y en qué orden aparecen las coordenadas?
    - ¿Qué diferencia principal hay entre consultar esta entidad y solicitar un mapa con WMS?

    Comprueba que el recurso elegido es una OGC API – Features: debe ofrecer una colección de entidades y permitir acceder a sus elementos. Si no encuentras una en la IDE elegida o el servicio no responde, prueba otra IDE. Si ninguna API elegida está disponible, usa el [ejemplo local](ejemplos/ogcapi_features/feature-ejemplo.geojson) para la parte de GeoJSON y documenta qué IDE y términos consultaste.

    **Criterios:** 0,2 puntos por identificar la IDE, el organismo y la API; 0,2 por describir la colección; 0,2 por identificar la entidad y sus propiedades; 0,2 por interpretar la geometría y las coordenadas; 0,2 por comparar el acceso con WMS y aportar evidencias claras.

## Fuentes

- [OGC API – Features: estándar y estado de sus partes](https://ogcapi.ogc.org/features/).
- [API de entidades del IGN](https://api-features.ign.es/).
- [RFC 7946: GeoJSON](https://www.rfc-editor.org/rfc/rfc7946).

**Siguiente:** [Panorama de otros estándares](otros.md).

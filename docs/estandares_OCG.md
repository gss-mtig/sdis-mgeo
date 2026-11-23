# Estándares OGC: interoperabilidad en la Web

El **Open Geospatial Consortium (OGC)** es una organización internacional que desarrolla estándares abiertos para que distintas aplicaciones y organizaciones puedan publicar, encontrar y usar información geográfica de manera interoperable.

Un estándar define reglas compartidas para que un cliente y un servidor puedan entenderse. Por ejemplo, un cliente SIG puede conectarse a un servicio de mapas de otra organización sin que el alumnado tenga que convertir manualmente cada capa.

## Dos generaciones de estándares web

Durante años, muchos servicios geográficos se han publicado con interfaces OGC como **WMS**, **WFS** y **WMTS**. Siguen presentes en geoportales, administraciones y aplicaciones, por lo que es útil aprender a reconocerlos y utilizarlos.

OGC está desarrollando una familia más reciente: las **OGC API**. Estas API organizan el acceso en recursos y usan prácticas habituales de la Web, como HTTP, respuestas HTML o JSON y descripciones OpenAPI. No son simplemente una nueva versión con otro nombre: modernizan patrones de acceso y, según el caso, sustituyen, amplían o complementan funciones de los servicios anteriores.

En esta asignatura estudiaremos **WMS en detalle**, porque permite entender la publicación de mapas como imágenes y continúa siendo muy común. Después veremos **OGC API – Features** como forma moderna de descubrir colecciones y consultar entidades geográficas. Los demás estándares se presentan como un panorama para reconocerlos y saber dónde profundizar.

## Qué debes recordar

- Los estándares OGC permiten que programas distintos intercambien información geográfica mediante reglas comunes.
- Los servicios clásicos y las OGC API coexisten; los estándares anteriores no han desaparecido de los geoportales.
- Cada estándar sirve para una tarea concreta: mostrar mapas, consultar entidades, distribuir teselas, buscar metadatos o ejecutar procesos.
- Antes de conectar un cliente, conviene consultar la ficha del catálogo y comprobar qué ofrece realmente el servicio.

Continúa con [WMS: mapas como imágenes](wms.md), sigue con las [pirámides de teselas ráster](piramides_teselas.md) y después revisa [la transición hacia las OGC API](api.md).

## Fuentes

- [Estándares OGC](https://www.ogc.org/standards/).
- [OGC API: visión general oficial](https://ogcapi.ogc.org/).

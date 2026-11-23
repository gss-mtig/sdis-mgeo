# WFS: acceso clásico a entidades geográficas

**Web Feature Service (WFS)** es un estándar OGC clásico para descubrir y consultar entidades geográficas en un servidor. Según la versión y la implementación, sus operaciones incluyen `GetCapabilities`, para describir el servicio, y `GetFeature`, para recuperar entidades; algunas implementaciones también permiten transacciones.

WFS todavía aparece en servicios y programas SIG. Sus respuestas suelen estar codificadas en GML, aunque los formatos disponibles dependen del servidor.

OGC API – Features ofrece una interfaz web más reciente para acceder a colecciones y entidades. OGC recomienda considerarla para nuevas implementaciones que necesiten las funciones de acceso a entidades de WFS. Consulta la lección de [OGC API – Features](ogc_api_features.md) para explorar una implementación actual.

Fuentes: [estándar WFS de OGC](https://www.ogc.org/standards/wfs/) y [OGC API – Features](https://ogcapi.ogc.org/features/).

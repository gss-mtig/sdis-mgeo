# Estándares para describir recursos geográficos

Los metadatos permiten entender y encontrar un recurso geográfico. Para que distintas organizaciones los puedan intercambiar y comprender, conviene describirlos con una estructura compartida. Los estándares de metadatos proporcionan esa estructura común.

No hace falta memorizar sus códigos. Lo importante es reconocer que hay normas para describir recursos, extensiones para necesidades específicas y reglas para codificar e intercambiar los registros.

## Una analogía

Imagina que cada biblioteca inventara sus propios campos para describir libros: unas usarían «autor», otras «persona autora» y otras guardarían ese dato dentro de «notas». Sería difícil buscar y comparar sus catálogos.

Un estándar de metadatos funciona como un modelo compartido: establece qué tipos de información se pueden describir y cómo se relacionan. Luego, un perfil concreta qué elementos se piden en un contexto determinado. Por eso dos fichas pueden tener aspectos distintos y aun así basarse en estándares relacionados.

## Algunas normas y para qué sirven

La familia ISO 19100 incluye normas para información geográfica. En metadatos, estas son algunas referencias útiles para orientarse:

| Norma | Idea principal | Cuándo importa |
|---|---|---|
| **ISO 19115-1** | Modelo general para describir recursos geográficos: identificación, extensión, calidad, referencia espacial y distribución, entre otros aspectos. | Como referencia general para describir datos geográficos. |
| **ISO 19115-2** | Amplía el modelo para describir la adquisición y el procesamiento de información geográfica, incluidas imágenes. | Cuando se necesita documentar con más detalle imágenes, observaciones o procesos de obtención. |
| **ISO 19119** | Trata los servicios geográficos y su arquitectura y categorización. | Cuando el recurso que se describe es un servicio y no solo un conjunto de datos. |
| **ISO 19115-3** | Define esquemas XML para codificar e intercambiar metadatos basados en ISO 19115-1 y 19115-2. | Cuando un sistema necesita exportar, importar o validar registros en XML. |

Las normas fijan modelos y reglas generales; no todas las fichas tienen que mostrar exactamente los mismos campos. Un **perfil de metadatos** selecciona y concreta elementos para un contexto, una comunidad o una iniciativa. Las reglas de metadatos de INSPIRE son un ejemplo de requisitos aplicados a un marco europeo.

## Modelo, perfil y formato

Este esquema resume cómo se relacionan las piezas:

```text
Norma: modelo común de descripción
          ↓
Perfil: selección y requisitos para un contexto
          ↓
Registro: ficha completada para un recurso
          ↓
Codificación: formato para guardar o intercambiar el registro
```

El formato de codificación no es lo mismo que el contenido de la ficha. Una persona puede leer los mismos metadatos en una página web, mientras que el catálogo los guarda o intercambia en un formato estructurado, por ejemplo XML.

## ¿Qué debes recordar?

- Los estándares ayudan a describir metadatos con una estructura común y favorecen su intercambio.
- Algunas normas son generales y otras se centran en necesidades concretas, como servicios o imágenes.
- Los perfiles adaptan las reglas generales a un contexto.
- No es necesario memorizar los números: al crear una ficha, la herramienta o el catálogo suele ofrecer una plantilla basada en un perfil.

Los estándares también evolucionan y las implementaciones pueden adoptar sus versiones en momentos distintos. Por eso todavía se pueden encontrar registros o herramientas que usan esquemas anteriores.

## Estado de las referencias citadas

La información se ha revisado en las páginas oficiales de ISO el **5 de noviembre de 2026**:

- [ISO 19115-1:2014 — Fundamentos](https://www.iso.org/standard/53798.html): publicada y vigente; ISO indica que está en revisión.
- [ISO 19115-2:2019 — Adquisición y procesamiento](https://www.iso.org/standard/67039.html): edición vigente; sustituye a la edición de 2009.
- [ISO 19119:2016 — Servicios](https://www.iso.org/standard/59221.html): publicada y confirmada en 2021.
- [ISO 19115-3:2023 — Esquemas XML](https://www.iso.org/obp/ui?_escaped_fragment_=iso%3Astd%3Aiso%3A19115%3A-3%3Aed-1%3Av1%3Aen): proporciona esquemas integrados para ISO 19115-1 y 19115-2; reemplaza ISO/TS 19139:2007 y 19139-2:2012.
- [Guías de metadatos de INSPIRE](https://knowledge-base.inspire.ec.europa.eu/metadata-technical-guidelines_en): explican cómo aplicar los requisitos de metadatos de esa iniciativa.

El siguiente paso es ver cómo se aplican estas ideas en una herramienta: continúa con [la creación de metadatos](creacion_metadatos.md).

# Caso práctico: información sobre inundaciones en IDEC

## La pregunta

Un ayuntamiento prepara una primera nota sobre inundaciones en Cataluña. El equipo necesita aclarar dos cosas:

1. ¿Qué municipios tienen la obligación o recomendación de elaborar un Plan de Actuación Municipal por riesgo de inundación y cuál es su estado?
2. ¿Qué información relacionada con el agua se puede consultar para entender mejor el territorio?

En el catálogo IDEC aparecen estas dos fichas:

1. [Pla d'Actuació Municipal per risc d'Inundacions](https://catalegs.ide.cat/geonetwork/proteccio-civil/api/records/mapa-proteccio-civil-pam-inuncat?language=cat)
2. [Servei de visualització WMS d'aigua](https://catalegs.ide.cat/geonetwork/srv/cat/catalog.search#/metadata/aigua-wms) ([vista directa de la ficha](https://catalegs.ide.cat/geonetwork/srv/api/records/aigua-wms?language=cat))

Aunque las dos fichas tratan sobre inundaciones, describen recursos distintos. Para elegir cuál consultar, primero hay que leer qué representa cada recurso y qué pregunta puede responder.

## Leer las fichas

### Ficha 1: planificación municipal por riesgo de inundaciones

La ficha describe un conjunto de datos que representa qué municipios tienen la obligación o recomendación de elaborar un Plan de Actuación Municipal (PAM) por riesgo de inundaciones y el estado del plan. Identifica como propietario a la Direcció General de Protecció Civil de la Generalitat de Catalunya y enlaza a un visor, una descarga y un servicio de visualización. También indica que para elaborar la cobertura se tuvieron en cuenta, entre otros elementos, las zonas inundables del INUNCAT de la Agència Catalana de l'Aigua (ACA).

La ficha indica una revisión del **28 de mayo de 2026**, cobertura de Cataluña, formatos SHP y KML, sistema de referencia EPSG:25831 y una licencia abierta de uso de información de Cataluña. Estas características pertenecen a la ficha consultada; comprueba los metadatos vigentes si vuelves a utilizar el recurso.

**Puede ayudar a responder:** ¿qué municipios deben elaborar un PAM por riesgo de inundaciones y cuál es el estado del plan?

**No responde por sí sola:** no es una delimitación detallada de todas las zonas inundables. Describe planificación municipal, aunque su elaboración utiliza información relacionada con inundaciones.

### Ficha 2: servicio de visualización de agua

La ficha describe un servicio de visualización de la Generalitat de Catalunya. Enumera contenidos relacionados con el agua, como masas de agua, red hidrográfica, acuíferos, depuradoras, pozos, fuentes, calados, líneas de inundación y zonas vulnerables a nitratos. La ficha declara el estándar OGC WMS versión 1.3.0 y enlaza al servicio de mapas.

La ficha indica cobertura de Cataluña y una revisión de metadatos del **6 de mayo de 2022**. Esa fecha no confirma cuándo se actualizaron las capas del servicio. Para saber qué capas concretas están disponibles y qué representa cada una habría que consultar el servicio y su leyenda.

El título de esta ficha incluye las siglas **WMS**. En esta actividad no hace falta conocer el estándar ni cómo funciona: basta con identificar que la ficha describe un servicio que permite visualizar información en un mapa. Lo estudiaremos más adelante.

**Puede ayudar a responder:** ¿qué información relacionada con el agua se puede visualizar para el territorio?

**No debes asumir:** que todas las capas sean zonas inundables, que compartan la misma escala o fecha, ni que el servicio proporcione los datos vectoriales originales.

## Aplicar el recorrido de búsqueda

1. **Define la pregunta.** Decide qué necesitas saber, de qué territorio y para qué decisión.
2. **Busca en el catálogo.** Prueba palabras relacionadas con el tema y el territorio. En este caso puedes usar `INUNCAT`, `inundabilitat` o los títulos de las fichas.
3. **Lee cada ficha completa.** Localiza productor, propósito, cobertura, fecha, tipo de recurso, condiciones de uso y enlaces.
4. **Sigue el enlace de acceso adecuado.** Puede llevar a un visor, una descarga o un servicio. No hace falta abrir el servicio para completar esta comparación.
5. **Anota qué falta.** Si la ficha no informa de la escala, la actualidad o las capas concretas, no lo adivines: anota qué tendrías que comprobar.

## Actividad guiada

Completa la tabla consultando las dos fichas:

| Dato que tienes que localizar | PAM por inundaciones | Servicio de agua |
|---|---|---|
| ¿Qué tipo de recurso describe? |  |  |
| ¿Quién lo produce o mantiene? |  |  |
| ¿Qué territorio cubre? |  |  |
| ¿Qué fecha de revisión informa? |  |  |
| ¿Cómo se puede acceder? |  |  |
| ¿Qué pregunta ayuda a responder? |  |  |
| ¿Qué limitación debes tener en cuenta? |  |  |

Después, completa:

> Para saber __________________, empezaría por consultar __________________ porque __________________.
>
> Para responder con más detalle también necesitaría __________________. Antes de usarlo, comprobaría __________________.

### Comprobación

Una respuesta razonable es empezar por la ficha PAM si la pregunta se refiere a las obligaciones municipales y al estado de los planes. Para visualizar información hidrológica, la ficha del servicio de agua ofrece un punto de entrada; después habría que comprobar qué capas contiene y qué representa cada una.

Si el objetivo fuera delimitar una zona inundable para analizarla, ninguna de estas dos fichas basta por sí sola. Habría que localizar la capa adecuada y comprobar su cobertura, fecha, escala, leyenda, método y condiciones de uso. El estado de un plan municipal no representa la extensión física de una inundación.

## Fuentes

- [Ficha IDEC del PAM por riesgo de inundaciones](https://catalegs.ide.cat/geonetwork/proteccio-civil/api/records/mapa-proteccio-civil-pam-inuncat?language=cat).
- [Ficha IDEC del servicio de visualización de agua](https://catalegs.ide.cat/geonetwork/srv/api/records/aigua-wms?language=cat).

Después de esta práctica, realiza el [ejercicio de aplicación en otra IDE](ejercicio_aplicado_ide.md).

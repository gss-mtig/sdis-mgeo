# WMS: publicar y consultar mapas como imágenes

El **Web Map Service (WMS)** es un estándar del Open Geospatial Consortium (OGC) para solicitar mapas georreferenciados a través de la Web. El servidor prepara una imagen del área, las capas, el tamaño y el estilo pedidos por el cliente.

Un WMS permite visualizar y superponer mapas de distintas fuentes. La respuesta de `GetMap` es una imagen —por ejemplo, PNG o JPEG—, no la capa vectorial original. Si necesitas descargar o analizar las entidades y sus atributos, tendrás que buscar otra forma de acceso. Algunos servicios permiten consultar información puntual mediante `GetFeatureInfo`, pero esa respuesta no equivale a descargar el conjunto de datos.

## Descubrir qué ofrece un servicio: `GetCapabilities`

La operación `GetCapabilities` devuelve una descripción del servicio. Ahí puedes revisar:

- las versiones y operaciones que admite;
- los nombres y títulos de las capas;
- qué capas se pueden consultar con `GetFeatureInfo`;
- los sistemas de referencia y extensiones geográficas disponibles;
- los formatos de imagen y de respuesta admitidos.

La dirección que aparece en una ficha de catálogo suele ser la URL base del servicio. Para pedir sus capacidades, se añaden los parámetros:

```text
?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0
```

El orden de los parámetros puede variar. La respuesta habitual es un documento XML; muchos programas SIG lo leen y presentan sus capas en una lista.

**Ejemplo:** [abrir `GetCapabilities` del WMS de divisiones administrativas del ICGC](https://geoserveis.icgc.cat/servei/catalunya/divisions-administratives/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0). En el XML, busca el nombre y el título de una capa.

## Solicitar un mapa: `GetMap`

`GetMap` pide una imagen para una selección concreta de capas y una zona del territorio. La solicitud incluye, entre otros:

| Parámetro         | Para qué sirve                                                                                   |
| ----------------- | ------------------------------------------------------------------------------------------------ |
| `LAYERS`          | Identifica las capas que se dibujarán; usa el valor `Name` del documento de capacidades.         |
| `STYLES`          | Indica el estilo de cada capa; puede dejarse vacío si se usa el estilo predeterminado.           |
| `CRS` o `SRS`     | Sistema de referencia de la imagen. WMS 1.3.0 usa `CRS`; versiones anteriores suelen usar `SRS`. |
| `BBOX`            | Extensión espacial de la imagen: coordenadas mínima y máxima.                                    |
| `WIDTH`, `HEIGHT` | Tamaño de la imagen en píxeles.                                                                  |
| `FORMAT`          | Formato de la imagen, como `image/png` o `image/jpeg`.                                           |
| `TRANSPARENT`     | Solicita fondo transparente cuando el formato y el servidor lo permiten; suele usarse con PNG.   |

La URL debe solicitar una combinación que el servicio realmente ofrezca. Los nombres de capa, formatos y sistemas de referencia se consultan en `GetCapabilities`.

Una solicitud simplificada para WMS 1.3.0 tiene esta forma. Sustituye los valores entre llaves por los que declara el servicio:

```text
URL_BASE?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&LAYERS={nombre_de_capa}&STYLES=&CRS=EPSG:25831&BBOX={minx},{miny},{maxx},{maxy}&WIDTH=800&HEIGHT=600&FORMAT=image/png&TRANSPARENT=TRUE
```

**Ejemplo:** [ver una petición `GetMap` de municipios a escala 1:100.000](https://geoserveis.icgc.cat/servei/catalunya/divisions-administratives/wms?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&LAYERS=divisions_administratives_municipis_100000&STYLES=&CRS=EPSG:25831&BBOX=411321.5,4565198,434331.5,4590698&WIDTH=768&HEIGHT=850&FORMAT=image/png). El resultado es una imagen PNG. La página del [ICGC sobre divisiones administrativas](https://www.icgc.cat/ca/Geoinformacio-i-mapes/Geoinformacio-en-linia-Geoserveis/WMS-i-WFS-Limits-administratius/WMS-i-WFS-Divisions-administratives) enumera las capas y sus rangos de visualización.

### CRS y orden de coordenadas

La caja `BBOX` debe expresarse en el sistema de referencia pedido. En WMS 1.3.0, el orden de los ejes depende del CRS definido por la norma. Por ejemplo, para EPSG:4326 el orden puede ser latitud-longitud; en servicios antiguos o con otros CRS puede encontrarse otro orden. Si la imagen sale vacía o en un lugar inesperado, revisa juntos la versión WMS, el CRS y el orden de las cuatro coordenadas.

## Consultar una posición: `GetFeatureInfo`

`GetFeatureInfo` permite preguntar al servidor qué información tiene sobre una posición de la imagen. La petición reutiliza los parámetros de mapa —capas, CRS, BBOX, ancho y alto— e indica:

- `QUERY_LAYERS`: capa o capas consultables;
- `I` y `J` en WMS 1.3.0, o `X` e `Y` en versiones anteriores: posición del píxel;
- `INFO_FORMAT`: formato de respuesta que el servicio admite, por ejemplo HTML o texto.

La operación solo funciona si la capa está marcada como consultable y el servidor la ofrece. Puede devolver atributos de las entidades cercanas al píxel, pero no necesariamente todos los datos ni todos sus campos.

De forma simplificada, la petición vuelve a incluir los parámetros de `GetMap` y añade:

```text
&REQUEST=GetFeatureInfo&QUERY_LAYERS={nombre_de_capa}&I={columna_del_pixel}&J={fila_del_pixel}&INFO_FORMAT=text/html
```

Los nombres `I` y `J` corresponden a WMS 1.3.0; en versiones anteriores suelen usarse `X` e `Y`. En un cliente SIG el programa calcula la posición del píxel al hacer clic sobre el mapa.

**Ejemplo:** [consultar información en el centro del mapa con `GetFeatureInfo`](https://geoserveis.icgc.cat/servei/catalunya/divisions-administratives/wms?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetFeatureInfo&LAYERS=divisions_administratives_municipis_100000&QUERY_LAYERS=divisions_administratives_municipis_100000&STYLES=&CRS=EPSG:25831&BBOX=411321.5,4565198,434331.5,4590698&WIDTH=768&HEIGHT=850&FORMAT=image/png&INFO_FORMAT=text/html&I=384&J=425). La respuesta depende de que la capa sea consultable y de que haya una entidad bajo ese píxel.

## Diagnosticar problemas frecuentes

- **La URL devuelve una imagen de error o XML:** comprueba el nombre de la operación, la versión y los nombres de las capas.
- **El mapa aparece vacío:** revisa el `BBOX`, el CRS, el orden de coordenadas y los límites de escala de la capa.
- **La petición se rechaza:** confirma que el formato, el CRS y el tamaño de imagen estén admitidos.
- **`GetFeatureInfo` no devuelve resultados:** verifica que la capa sea consultable y que la posición del píxel caiga dentro de la imagen y de una entidad.
- **El mapa no es transparente:** usa un formato que admita transparencia y comprueba que el servicio acepte `TRANSPARENT=TRUE`.

## Actividades prácticas en clase

Estas actividades se realizan en parejas y no sustituyen el ejercicio evaluable de esta lección.

### 1. Descubrir una capa en `GetCapabilities` — 15 minutos

**Objetivo:** aprender a leer qué ofrece un servicio antes de conectarlo.

**Materiales:** navegador o QGIS; ficha del [servicio WMS de agua de IDEC](https://catalegs.ide.cat/geonetwork/srv/api/records/aigua-wms?language=cat), que enlaza al WMS de la Generalitat y describe información hidrológica. La ficha indica WMS 1.3.0 y una revisión de metadatos del 6 de mayo de 2022; esa fecha no confirma la actualización de las capas.

**Pasos:**

1. Desde la ficha, abre el punto de conexión del servicio o añádelo en QGIS como WMS/WMTS.
2. Carga la lista de capas y escoge una relacionada con una pregunta concreta.
3. Localiza en `GetCapabilities` o en la ventana del cliente el nombre técnico, el título, los CRS disponibles y si la capa es consultable.

**Resultado:** anotad esos cuatro datos para una capa y una pregunta que podría ayudar a responder.

**Reflexiona:** ¿qué información no puedes deducir solo del nombre de la capa?

### 2. Construir un mapa y corregir una petición — 25 minutos

**Objetivo:** relacionar capas, extensión, CRS y transparencia con la imagen que devuelve `GetMap`.

**Materiales:** el mismo servicio WMS y QGIS. Si no responde durante la clase, usa otro WMS de una IDE que se haya comprobado antes de la sesión.

**Pasos:**

1. Añade una capa y visualízala sobre el territorio que te interesa.
2. Añade una segunda capa y activa la transparencia cuando el formato lo permita.
3. Cambia la extensión o el CRS del proyecto y observa qué ocurre.
4. El docente entregará una petición `GetMap` con un error sencillo: por ejemplo, un nombre de capa incorrecto, un CRS no admitido o una extensión (`BBOX`) fuera de cobertura. En pareja, localizad el error consultando `GetCapabilities` y corregidlo.

**Resultado:** una captura del mapa final y una frase que explique el error y cómo lo detectasteis.

**Reflexiona:** ¿qué combinación de capas y extensión comunica mejor la información necesaria?

### 3. ¿Qué puede decirnos un píxel? — 15 minutos

**Objetivo:** distinguir la imagen de `GetMap` de la respuesta puntual de `GetFeatureInfo`.

**Materiales:** una capa consultable del servicio WMS y QGIS con la herramienta de información. Si ninguna capa lo permite, comparad la declaración `queryable` de dos capas en `GetCapabilities`.

**Pasos:**

1. Haced clic en una entidad visible con la herramienta de información.
2. Leed la respuesta y anotad qué atributos devuelve.
3. Si la capa no es consultable, buscad la indicación correspondiente en las capacidades del servicio.

**Resultado:** una nota con un atributo obtenido y una limitación de la consulta.

**Reflexiona:** ¿por qué `GetFeatureInfo` no equivale a descargar las entidades completas?

## WMS y las OGC API

WMS continúa siendo común en IDE y geoportales. [OGC API – Maps](https://ogcapi.ogc.org/maps/) ofrece otra manera estándar de descubrir y solicitar mapas mediante recursos web. Los dos pueden devolver una imagen cartográfica, pero organizan el acceso de forma distinta:

| | WMS | OGC API – Maps |
|---|---|---|
| **Cómo se descubre** | Se solicita `GetCapabilities`, que describe operaciones, capas, CRS y formatos. | Se abre la página inicial de la API y se siguen sus enlaces a las colecciones y a la definición OpenAPI. |
| **Cómo se pide un mapa** | Se envía `GetMap` con parámetros como `LAYERS`, `BBOX`, `CRS`, `WIDTH` y `HEIGHT`. | Se solicita un recurso de mapa, normalmente `/collections/{id}/map`, con parámetros como `bbox`, `width` y `height`. |
| **Qué se recibe** | Una imagen georreferenciada, por ejemplo PNG. | También una imagen de mapa; la API puede ofrecer formatos alternativos según la implementación. |
| **Consultar entidades** | Algunas capas permiten `GetFeatureInfo`, que devuelve información asociada a un píxel. | OGC API – Maps Core no define una operación equivalente a `GetFeatureInfo`. Para consultar entidades y sus propiedades, se necesita una API de datos, como OGC API – Features, si el proveedor publica allí el conjunto. |

Por tanto, al pulsar sobre el mapa de la API de la IDEE no se obtiene automáticamente la información de la entidad situada bajo el cursor. Si los datos vectoriales están publicados también como entidades, OGC API – Features permite consultarlas por colección y zona; para ciertos datos ambientales, OGC API – EDR ofrece consultas por posición. Son otros recursos y pueden requerir que el cliente transforme la posición del clic al sistema de coordenadas que espera esa API. La especificación de [OGC API – Maps, apartado C.2.3](https://docs.ogc.org/is/20-058/20-058.html#_no_equivalent_to_getfeatureinfo_as_part_of_the_ogc_api_maps_part_1) explica esta diferencia y propone consultar otras OGC API.

### Ejemplo con la API de mapas de la IDEE

La [API de mapas de la Infraestructura de Datos Espaciales de España (IDEE)](https://api-maps.idee.es/) ofrece mapas base, ortoimágenes y representaciones del relieve. En la página inicial, abre **View the collections in this service** y selecciona **Street map**. Su identificador es `IGNBaseTodo`.

En WMS descubrimos el servicio con `GetCapabilities` y pedimos la imagen con `GetMap`. Aquí podemos recorrer los recursos desde el navegador:

1. [Abrir las colecciones de la API](https://api-maps.idee.es/collections?f=html) y localizar el mapa callejero.
2. [Consultar la descripción de la colección `IGNBaseTodo`](https://api-maps.idee.es/collections/IGNBaseTodo?f=html).
3. [Solicitar una imagen del mapa callejero para la España peninsular](https://api-maps.idee.es/collections/IGNBaseTodo/map?bbox=-9.3,35.8,4.5,43.9&width=1000&height=600&f=png).

La última dirección sigue el patrón `/collections/IGNBaseTodo/map` y añade la extensión `bbox`, el tamaño en píxeles y el formato PNG. En este ejemplo, `bbox` utiliza el orden longitud mínima, latitud mínima, longitud máxima y latitud máxima, en el CRS84 predeterminado. Puedes cambiar el `bbox` o las dimensiones y volver a abrir el enlace para ver cómo cambia el mapa.

El resultado sigue siendo una **imagen**, igual que con `GetMap`; no contiene las entidades vectoriales originales. La colección describe las fuentes y el contenido representado, y la API ofrece enlaces a formatos HTML y JSON. Para consultar objetos y atributos, continúa con [OGC API – Features](ogc_api_features.md). La [especificación de OGC API – Maps](https://ogcapi.ogc.org/maps/overview.html) describe estos recursos y parámetros.

## Ejercicio: descubrir, solicitar y consultar un WMS

!!! question "Ejercicio 2 puntos"

    En un documento breve, selecciona un servicio WMS publicado por una IDE. Puedes partir del [catálogo de IDEC](https://catalegs.ide.cat/geonetwork/srv/search?orgName=Infraestructura+de+Dades+Espacials+de+Catalunya) o de otra IDE. Elige un servicio que responda a una pregunta geográfica que te interese.

    1. Incluye el enlace a la ficha del catálogo y la URL de `GetCapabilities`. Indica quién publica el servicio y qué capas ofrece.
    2. Prepara una solicitud `GetMap` para una de sus capas. Incluye la URL, identifica el CRS y explica qué zona define el `BBOX`. Añade una captura de la imagen recibida.
    3. Comprueba si la capa permite `GetFeatureInfo`. Si es posible, consulta una posición y resume qué información devuelve. Si no está habilitado, indícalo y explica cómo lo comprobaste.
    4. Explica una limitación del WMS para tu pregunta: recuerda que `GetMap` entrega una imagen y no el conjunto de entidades original.

    **Entrega:** documento de texto con enlaces, respuesta breve y capturas legibles. Si un servicio no responde, vuelve a la ficha y prueba otro servicio de la misma IDE; anota el fallo si afecta a tu elección.

    **Criterios:** 0,5 puntos por identificar el servicio y leer sus capacidades; 0,75 por construir y explicar `GetMap`; 0,5 por probar o comprobar `GetFeatureInfo`; 0,25 por explicar una limitación relevante.

## Fuentes

- [Estándar WMS de OGC](https://www.ogc.org/standards/wms/).
- [OGC API – Maps](https://ogcapi.ogc.org/maps/).

**Siguiente:** [Pirámides de teselas ráster: XYZ, WMTS y OGC API – Tiles](piramides_teselas.md).

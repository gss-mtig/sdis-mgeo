# Clientes de mapas

Un **cliente de mapas** es una aplicación que permite a una persona consultar o utilizar datos geográficos. Puede mostrar un servicio remoto, abrir archivos locales o combinar ambas fuentes. El cliente transforma los datos o las respuestas de un servicio en una representación con la que podemos interactuar.

Por ejemplo, un WMS entrega imágenes de mapa. Un cliente como QGIS o un visor web solicita esas imágenes y las muestra. El mismo servicio puede verse en clientes distintos, aunque cada uno ofrezca herramientas diferentes.

## ¿Qué cliente conviene usar?

La elección depende de la tarea:

- **Visor web:** consultar un mapa sin instalar software y compartirlo mediante un enlace.
- **SIG de escritorio, como QGIS:** combinar servicios y archivos, inspeccionar capas y atributos, cambiar simbología y realizar análisis.
- **Visor web propio:** integrar uno o varios recursos en una página adaptada a una necesidad concreta. En esta lectura construiremos uno pequeño con Leaflet.

Un cliente no cambia el contenido ni la calidad de los datos del servicio. Para valorar si una capa sirve para nuestro problema, hay que revisar también su ficha, cobertura, fecha, escala y condiciones de uso.

## Práctica: el mismo WMS en QGIS y en Leaflet

**Objetivo:** comprobar cómo dos clientes distintos muestran un mismo servicio y localizar en sus capacidades el nombre de la capa que se va a pedir.

**Materiales:** navegador con conexión a internet, QGIS y el servicio WMS de mapa base del Institut Cartogràfic i Geològic de Catalunya (ICGC).

### 1. Explorar las capacidades del WMS

Abre la [respuesta `GetCapabilities` del servicio](https://geoserveis.icgc.cat/servei/catalunya/mapa-base/wms?SERVICE=WMS&VERSION=1.1.1&REQUEST=GetCapabilities). Es un documento XML que describe, entre otras cosas, las capas disponibles, sus nombres, sistemas de coordenadas y formatos.

Busca la capa llamada `topografic`. Ese nombre es el identificador que el cliente debe enviar al servicio; no tiene por qué coincidir exactamente con el título legible de una capa.

### 2. Abrir la capa en QGIS

Si ya has añadido WMS en la [lección sobre WMS](wms.md), reutiliza ese procedimiento. La URL de conexión es:

```text
https://geoserveis.icgc.cat/servei/catalunya/mapa-base/wms?
```

Conecta al servicio, busca la capa `topografic` y añádela al mapa. Observa cómo QGIS presenta el servicio y permite gestionar la capa desde su panel.

### 3. Abrir la capa en Leaflet

Leaflet es una biblioteca JavaScript para crear mapas interactivos en páginas web. En este ejemplo no instalaremos un servidor ni configuraremos XAMPP: guardaremos un archivo HTML y lo abriremos directamente con el navegador. El archivo carga Leaflet desde una red de distribución de contenidos (CDN), por lo que se necesita conexión a internet.

Descarga esta [plantilla HTML de Leaflet con el WMS](ejemplos/clientes_mapa/wms_leaflet.html), ábrela con un editor de texto y revisa las líneas indicadas. Después, abre el archivo en el navegador.

```html
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">
<div id="mapa"></div>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
  const mapa = L.map('mapa').setView([41.68, 1.85], 8);

  L.tileLayer.wms('https://geoserveis.icgc.cat/servei/catalunya/mapa-base/wms?', {
    layers: 'topografic',
    format: 'image/png',
    transparent: true
  }).addTo(mapa);
</script>
```

La plantilla completa incluye la estructura HTML y el tamaño del mapa. En el fragmento, `setView` define el centro y el zoom iniciales. `tileLayer.wms` indica la URL del servicio y las opciones de la petición. El valor de `layers` procede del nombre encontrado en `GetCapabilities`.

El servicio WMS actúa como capa de mapa. No estamos descargando las entidades geográficas ni sus atributos: recibimos imágenes para la extensión y escala que solicita el cliente.

### 4. Comparar los dos clientes

Con la misma capa abierta en QGIS y en Leaflet, comentad en parejas:

1. ¿Qué pasos son iguales en ambos casos?
2. ¿Dónde se indica el nombre de la capa? ¿Qué ocurre si se escribe un nombre que no aparece en `GetCapabilities`?
3. ¿Qué controles ofrece QGIS que no aparecen en el visor mínimo de Leaflet?
4. ¿En qué situación elegiríais QGIS y en cuál un visor web propio?

**Resultado esperado:** la capa `topografic` se visualiza en los dos clientes, y puedes explicar que ambos solicitan un mapa al mismo WMS aunque la interfaz y las posibilidades sean diferentes.

!!! warning "Si el mapa no aparece"
    Comprueba que tienes conexión a internet, que la URL acaba en `?` y que `layers` contiene exactamente `topografic`. Vuelve a abrir `GetCapabilities` para comprobar que el servicio y la capa están disponibles. Los servicios externos pueden cambiar o dejar de responder; si ocurre, utiliza el WMS alternativo indicado por el docente.

## Ejercicio

!!! question "Ejercicio 1 punto"

    Modifica la plantilla de Leaflet para mostrar otra capa de un servicio WMS de una IDE.

    1. Localiza una ficha o página oficial del servicio y copia su URL de conexión.
    2. Abre `GetCapabilities` e identifica el nombre exacto de una capa adecuada para una pregunta geográfica que te interese.
    3. Cambia en la plantilla la URL del servicio y el nombre de la capa. Ajusta el centro y el zoom iniciales para que el mapa muestre el territorio de interés.
    4. Comprueba que el mapa se ve en el navegador y entrega el archivo HTML junto con un breve texto que indique la IDE, la capa elegida y cómo encontraste su nombre en las capacidades.

    **Criterios:** visualización funcional (0,5 puntos), identificación correcta de la capa a partir de `GetCapabilities` (0,25 puntos) y referencia a la IDE y descripción breve del proceso (0,25 puntos).

    Si el servicio elegido no funciona durante la evaluación, incluye en el texto la URL de la ficha y una captura o fragmento de `GetCapabilities` donde se vea la capa seleccionada. Así se puede revisar el procedimiento aunque el servicio tenga una interrupción temporal.

## Referencias

- [Guía de inicio rápido de Leaflet](https://leafletjs.com/examples/quick-start/).
- [Servicio de Mapa Base del ICGC: información técnica y capacidades](https://www.icgc.cat/es/Geoinformacion-y-mapas/Servicio-de-Mapa-Base).

**Siguiente:** [Servidores de mapas: panorama y alternativas](servidores_de_mapa.md).

# Consumir teselas vectoriales en QGIS y MapLibre GL JS

El servidor expone el archivo MBTiles como una fuente de teselas. Ahora la añadiremos a dos clientes distintos: QGIS, para explorarla en un SIG de escritorio, y MapLibre GL JS, para integrarla en un mapa web.

## Antes de empezar

1. Completa las páginas de [creación](crear_teselas_vectoriales.md) y [publicación local](servir_teselas_vectoriales.md).
2. Para el visor MapLibre completo, genera también `accidentes_barcelona.mbtiles` y arranca TileServer GL Light con `config.json`, de modo que publique las capas `puntos` y `accidentes` en `http://localhost:8081`.
3. Comprueba que abre [la descripción TileJSON de la fuente](http://localhost:8081/data/puntos.json). Si esa dirección no responde, el servidor no está en marcha o está usando otro puerto.

El ejemplo de MapLibre compara los puntos sintéticos en dos formas: teselas vectoriales y el GeoJSON completo original. La capa de accidentes es una segunda fuente de teselas. El servicio local solo estará disponible mientras el servidor esté en ejecución.

## Opción 1: añadir el servicio en QGIS

QGIS puede conectarse a teselas vectoriales genéricas que se sirven como archivos `.pbf`.

1. Abre QGIS y el **Administrador de fuentes de datos**.
2. Selecciona **Teselas vectoriales** y crea una conexión genérica nueva. También puedes usar el panel **Navegador**: clic derecho en **Teselas vectoriales** y elige **Nueva conexión genérica**.
3. Completa la conexión:

   - **Nombre:** `Puntos de ejemplo (local)`.
   - **URL de origen:** `http://localhost:8081/data/puntos/{z}/{x}/{y}.pbf`.
   - **Zoom mínimo:** `0`.
   - **Zoom máximo:** `12`.

4. Guarda la conexión y añádela al proyecto.
5. Acércate a Catalunya si no se muestra automáticamente. Abre las propiedades de la capa para revisar los campos y ajustar la simbología.

El patrón `{z}/{x}/{y}` indica a QGIS qué tesela pedir para el nivel de zoom y la posición que necesita. Si elegiste otro puerto al iniciar TileServer GL, reemplaza `8081` en esta URL y en las demás direcciones del visor.

!!! question "Comprueba la capa"

    ¿Puedes ver la nube de puntos? ¿Qué campos aparecen en las propiedades? ¿Qué ocurre al ampliar el mapa hasta el nivel de zoom máximo publicado?

## Ejemplo de un servicio publicado por el IGN

La [ficha de metadatos de la IDEE](https://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/metadata/spaignmvt_unidades_administrativas) describe el servicio de teselas vectoriales de **Unidades administrativas de España**, publicado por el Instituto Geográfico Nacional (IGN). La [página de estilos del IGN](https://www.ign.es/web/estilos-de-los-servicios-de-teselas-vectoriales) ofrece la plantilla de datos MVT y dos estilos MapLibre.

- **Teselas MVT:** `https://vt-unidades-administrativas.ign.es/1.0.0/uadministrativa/{z}/{x}/{y}.pbf`
- **Estilo gris listo para usar:** [style_s3_cloud.json](https://vt-unidades-administrativas.ign.es/demo/style_s3_cloud.json)
- **Estilo verde:** [style_s3_green.json](https://vt-unidades-administrativas.ign.es/demo/style_s3_green.json)

El archivo `.pbf` contiene las geometrías y atributos; el estilo JSON indica cómo dibujarlos. En QGIS, crea una conexión genérica de teselas vectoriales con la plantilla anterior. En MapLibre, puedes cargar el estilo directamente como `style`:

```javascript
const mapa = new maplibregl.Map({
  container: "mapa",
  style: "https://vt-unidades-administrativas.ign.es/demo/style_s3_cloud.json",
  center: [-3.7, 40.2],
  zoom: 5
});
```

También puedes abrir [el ejemplo HTML local](ejemplos/vector_tiles/visor_unidades_administrativas_ign.html). Requiere conexión a Internet para cargar MapLibre y el servicio del IGN. El registro indica licencia CC BY 4.0: conserva la atribución indicada por el proveedor si reutilizas los datos.

## Opción 2: mostrar la fuente en MapLibre GL JS

MapLibre GL JS es una biblioteca JavaScript para crear mapas interactivos en el navegador. En el ejemplo siguiente, MapLibre consulta el documento TileJSON del servidor local y aplica un estilo propio. No se usa un mapa base externo, así que solo se representa la capa del ejercicio.

Abre [el ejemplo MapLibre](ejemplos/vector_tiles/visor_maplibre.html) con el GeoJSON [puntos_10000.geojson](ejemplos/vector_tiles/puntos_10000.geojson) en la misma carpeta o en el mismo directorio publicado. El ejemplo carga MapLibre GL JS 6.18.0 desde el CDN de UNPKG, las teselas desde TileServer GL y los puntos GeoJSON desde el archivo estático. Requiere conexión a Internet para descargar la biblioteca. Si trabajas con una copia descargada, sirve ambos archivos desde un servidor web local: el navegador normalmente bloquea la lectura del GeoJSON cuando el HTML se abre directamente como `file://`.

El visor completo incluye controles para activar y desactivar las dos capas vectoriales y la capa GeoJSON. Además, puedes filtrar los puntos por tema (`agua`, `energía`, `movilidad` o `vegetación`) y alternar entre una simbología uniforme y colores por tema. El mismo filtro y los mismos colores se aplican a la versión MVT y a la versión GeoJSON para facilitar la comparación. Pulsa un punto para consultar sus atributos.

La configuración espera estas fuentes locales:

```javascript
sources: {
  puntosMVT: { type: "vector", url: "http://localhost:8081/data/puntos.json" },
  accidentes: { type: "vector", url: "http://localhost:8081/data/accidentes.json" },
  puntosGeoJSON: { type: "geojson", data: "puntos_10000.geojson" }
}
```

En las fuentes MVT, `url` apunta al TileJSON publicado por TileServer GL, y `source-layer` debe coincidir con el nombre de la capa interna de cada MBTiles (`puntos` o `accidentes`). La fuente GeoJSON carga el archivo completo. El estilo y los filtros cambian la representación en el navegador; no modifican los datos de origen ni las teselas.

### Actividad: cambia una representación

En parejas, 5–10 minutos:

1. Abre `visor_maplibre.html` con un editor de texto.
2. Activa y desactiva las capas para compararlas por separado.
3. Filtra los puntos por uno de los temas y cambia entre símbolo uniforme y color por tema.
4. Pulsa un punto para consultar sus propiedades y abre los metadatos de `data/puntos.json` y `data/accidentes.json`.

**Resultado esperado:** las capas se pueden comparar desde el panel, los puntos se filtran y simbolizan sin regenerar los datos y se identifica qué describe el TileJSON.

### Actividad: comparar GeoJSON y teselas vectoriales — 5–10 minutos

1. Abre las herramientas de desarrollo del navegador, entra en **Red / Network** y activa **Disable cache / Desactivar caché**.
2. Recarga el visor y filtra las solicitudes por `puntos_10000.geojson` y `.pbf`.
3. Anota el tamaño transferido y el tiempo de carga del GeoJSON completo. Después, anota el tamaño y el número de teselas MVT solicitadas para la vista inicial.
4. Desplaza y amplía el mapa, y repite la observación: las solicitudes `.pbf` cambian con el área y el nivel de zoom; el GeoJSON completo ya se descargó como un solo recurso.
5. Desactiva una capa y luego la otra para distinguirlas visualmente. Ten en cuenta que este visor carga las dos fuentes para permitir la comparación; ocultar una capa no equivale a evitar su descarga.

**Resultado esperado:** una comparación de bytes transferidos, número de solicitudes y tiempos observados en ese equipo. Explica que las teselas entregan solo partes adecuadas a la vista actual, mientras que GeoJSON descarga el conjunto completo. MapLibre también prepara internamente las fuentes GeoJSON para dibujarlas; por eso esta actividad compara el flujo de carga de estos datos en este visor, no una regla universal sobre la velocidad de representación. El resultado depende del zoom, el tamaño de las teselas, la compresión, la caché, el navegador y la red. El archivo GeoJSON ocupa alrededor de 1,7 MB sin comprimir; MBTiles puede ocupar más en disco porque almacena varios niveles de zoom.

## Qué tienen en común y qué cambia

Ambos clientes consultan la misma fuente de teselas publicada por TileServer GL Light. QGIS la integra como una capa para explorar en un proyecto SIG; MapLibre la representa en una aplicación web mediante un estilo definido en código o en un documento de estilo. El cliente decide la representación visual, pero no recupera necesariamente todas las entidades ni todos los atributos del conjunto original.

Si el visor web no carga, confirma que TileServer sigue activo, que la dirección del TileJSON es correcta y que hay conexión para descargar MapLibre desde el CDN. Si el archivo se abre desde `file://` y el navegador bloquea las peticiones locales, sirve el HTML desde un servidor web local sencillo o abre la actividad en el entorno preparado por el docente.

## Fuentes

- [Manual de QGIS 3.44: uso de servicios de teselas vectoriales](https://docs.qgis.org/3.44/en/docs/user_manual/managing_data_source/opening_data.html#using-vector-tiles-services), consultado el 14 de noviembre de 2026.
- [Documentación oficial de MapLibre GL JS](https://maplibre.org/maplibre-gl-js/docs/), consultada el 14 de noviembre de 2026.
- [Documentación de MapLibre: fuentes GeoJSON](https://maplibre.org/maplibre-gl-js/docs/API/classes/GeoJSONSource/).
- [Especificación de estilos de MapLibre: fuentes GeoJSON](https://maplibre.org/maplibre-style-spec/sources/).
- [Ejemplo oficial de MapLibre: añadir una fuente de teselas vectoriales](https://maplibre.org/maplibre-gl-js/docs/examples/add-a-vector-tile-source/).
- [Especificación de estilos de MapLibre: fuentes](https://maplibre.org/maplibre-style-spec/sources/).
- [IDEE: ficha de metadatos del servicio de unidades administrativas](https://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/metadata/spaignmvt_unidades_administrativas).
- [IGN: estilos de los servicios de teselas vectoriales](https://www.ign.es/web/estilos-de-los-servicios-de-teselas-vectoriales).

**Siguiente:** [Descubrir datos con un catálogo STAC](catalogo_stac.md).

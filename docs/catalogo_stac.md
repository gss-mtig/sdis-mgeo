# Descubrir datos con un catálogo STAC

Cuando hay miles de imágenes satelitales, no resulta práctico descargarlas una por una para averiguar cuál cubre una zona, cuándo se capturó o si está nublada. **STAC** (*SpatioTemporal Asset Catalog*) ofrece una forma común de describir y descubrir datos geoespaciales mediante documentos JSON y, cuando se implementa como API, mediante búsquedas por lugar, fecha y otras propiedades.

STAC no es un formato de imagen ni una base de datos concreta. Describe recursos y enlaza sus archivos: por ejemplo, una escena Sentinel‑2 puede estar representada por un *Item* STAC y ofrecer varios activos como bandas, máscaras, metadatos o una vista previa. El archivo de imagen puede ser un GeoTIFF optimizado para la nube (COG), pero STAC y COG cumplen funciones distintas.

## Las piezas principales

- **Collection:** describe un conjunto de datos relacionado, como imágenes Sentinel‑2 de nivel 2A. Puede incluir extensión espacial y temporal, licencia, proveedores y enlaces.
- **Item:** describe un elemento individual del conjunto, por ejemplo una escena adquirida en una fecha y sobre una zona. Usa una geometría GeoJSON y añade propiedades y enlaces a sus activos.
- **Asset:** enlace a un archivo asociado al Item, como una banda, una máscara de nubes o una miniatura.
- **Catálogo:** agrupa o enlaza Collections e Items para que puedan explorarse. Un catálogo estático se compone de archivos enlazados; una **STAC API** permite además realizar búsquedas dinámicas.

Una búsqueda STAC ayuda a encontrar registros. No garantiza que todos los archivos enlazados sean públicos, gratuitos o accesibles sin autenticación: hay que revisar la licencia y las condiciones del proveedor.

## Ejemplo: catálogo de Copernicus

El Copernicus Data Space Ecosystem (CDSE) ofrece una STAC API pública con colecciones de observación de la Tierra. La usaremos para descubrir escenas **Sentinel‑2 Level‑2A** sobre Catalunya. Consultaremos el catálogo, sin crear ni publicar registros.

### Explora el catálogo en el navegador

1. Abre el [navegador STAC de Copernicus](https://browser.stac.dataspace.copernicus.eu/).
2. En el catálogo, localiza la colección **Sentinel‑2 Level‑2A** (`sentinel-2-l2a`). Si el navegador presenta filtros o un mapa de búsqueda, limita la búsqueda a Catalunya.
3. Prueba un intervalo temporal de un mes y un filtro de nubosidad, por ejemplo menos del 20 %. Si no aparecen resultados, amplía el periodo o el área de búsqueda.
4. Abre un Item y examina su fecha, geometría, propiedades, enlaces y lista de Assets.
5. Elige un Asset y lee su nombre, tipo de medio, función (`roles`) y enlace (`href`). Antes de descargarlo o abrirlo, comprueba si el proveedor indica autenticación, firma temporal o condiciones de uso.

El navegador web puede cambiar su interfaz. También es posible navegar directamente desde la [API STAC de Copernicus](https://stac.dataspace.copernicus.eu/v1/), consultar sus [colecciones](https://stac.dataspace.copernicus.eu/v1/collections) o abrir la [descripción de Sentinel‑2 Level‑2A](https://stac.dataspace.copernicus.eu/v1/collections/sentinel-2-l2a).

### Conecta QGIS al catálogo

Las versiones actuales de QGIS permiten explorar catálogos estáticos y conectarse a STAC API. En QGIS 3.44:

1. Abre el panel **Navegador**, localiza **STAC** y elige **Nueva conexión**.
2. Ponle un nombre, por ejemplo `Copernicus Data Space`, e introduce como URL:

   ```text
   https://stac.dataspace.copernicus.eu/v1/
   ```

3. Expande la conexión para explorar colecciones. Para filtrar resultados, abre el **Administrador de fuentes de datos**, pestaña **STAC**, selecciona la conexión y usa **Filtros**.
4. Busca la colección `sentinel-2-l2a`, delimita la zona de interés y el intervalo de fechas. Examina los Items y sus metadatos.
5. Si un Asset es accesible sin credenciales y QGIS reconoce su formato, prueba a añadirlo al mapa. Si el enlace requiere autenticación o no está disponible, utiliza el Item para completar la tarea de descubrimiento y evaluación.

La disponibilidad y el comportamiento de acceso a los activos dependen del proveedor y pueden cambiar. Para la actividad, el resultado principal es identificar una escena adecuada y justificar la elección a partir de su ficha.

## Actividad de clase: elige una escena útil

**Objetivo:** seleccionar una imagen satelital que pueda servir para observar un cambio ambiental en Catalunya.

**Pasos:**

1. Busca una escena Sentinel‑2 Level‑2A sobre un área de Catalunya que te interese.
2. Reduce los resultados usando un periodo de fechas y la nubosidad. Anota los filtros empleados.
3. Abre el Item y registra su identificador, fecha de adquisición, porcentaje de nubosidad, área cubierta y dos Assets disponibles.
4. Explica cuál Asset consultarías primero y qué comprobarías en su licencia y acceso antes de usarlo.

**Resultado esperado:** una ficha breve de una escena elegida y una justificación de su utilidad y limitaciones. No es necesario descargar una imagen.

**Pregunta de reflexión:** ¿qué información te aporta el Item antes de abrir el archivo, y qué preguntas importantes todavía debes responder sobre el propio dato?

## Qué debes recordar

- STAC estandariza metadatos y enlaces para descubrir recursos geoespaciales.
- Un Item suele describir un recurso individual; sus Assets enlazan los archivos asociados.
- Un catálogo estático permite navegar por documentos enlazados; una STAC API añade búsquedas dinámicas.
- Encontrar un Asset no implica que sea accesible sin credenciales ni que su licencia permita cualquier uso.
- COG es un formato de ráster optimizado para acceso remoto; STAC puede describir y enlazar ese COG.

Como ejemplo de un catálogo STAC con reglas adicionales para organizar y documentar formatos cloud-native, consulta [Portolan y su catálogo de ejemplo](portolan.md).

## Fuentes

- [Documentación del catálogo STAC de Copernicus Data Space Ecosystem](https://documentation.dataspace.copernicus.eu/APIs/STAC.html), consultada el 14 de noviembre de 2026. El endpoint vigente es `https://stac.dataspace.copernicus.eu/v1/`; la documentación indica que el catálogo implementa STAC 1.1.0 y que su inventario disponible es limitado y puede evolucionar.
- [Especificación STAC: Items, Catalogs, Collections y catálogos estáticos y dinámicos](https://stacspec.org/en/about/stac-spec/).
- [Manual de QGIS 3.44: conexión y búsqueda en catálogos STAC](https://docs.qgis.org/3.44/en/docs/user_manual/working_with_ogc/ogc_client_support.html#stac-spatio-temporal-asset-catalogs), consultado el 14 de noviembre de 2026.

**Siguiente:** [Explorar y consumir un catálogo Portolan](portolan.md).

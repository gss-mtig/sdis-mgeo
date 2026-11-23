# Explorar y consumir un catálogo Portolan

Portolan es una especificación abierta y un conjunto de herramientas para organizar y publicar datos geoespaciales como archivos cloud-native acompañados de metadatos y documentación. No es un portal central que almacene todos los datos ni una API de geoservicios: el catálogo y los datos pueden permanecer en el almacenamiento de cada proveedor.

Portolan se apoya en estándares y formatos existentes. Su catálogo usa **STAC** para enlazar colecciones y elementos; los datos pueden ofrecerse como **GeoParquet** para análisis vectorial, **PMTiles** para visualización vectorial y **COG** para ráster, entre otros formatos. La especificación añade convenciones sobre estructura, metadatos y documentación para que personas y herramientas puedan encontrar y usar los recursos.

## Catálogo, registro y navegador

Conviene distinguir tres elementos:

- **Catálogo Portolan:** los archivos de metadatos STAC y los datos publicados por un proveedor.
- **Registro Portolan:** un directorio que permite buscar catálogos publicados de forma independiente. No centraliza ni copia sus datos.
- **Portolan Browser:** una interfaz web para navegar por un catálogo y consultar sus colecciones y recursos.

El Registro ayuda a encontrar una dirección de catálogo. El navegador o QGIS lee sus metadatos y, cuando se solicita, el cliente accede al archivo enlazado. Por tanto, los metadatos, el registro, la interfaz y el archivo de datos son piezas relacionadas, pero distintas.

Portolan aún está en desarrollo y su especificación es anterior a la versión 1.0; sus convenciones pueden cambiar con más rapidez que los estándares de base, como STAC o GeoParquet. En la sesión consultada, el Registro mostraba catálogos con versiones Portolan 0.2.0. Al trabajar con una implementación concreta, comprueba siempre la versión y la fecha que aparecen en el catálogo.

## Ejemplo: datos neerlandeses de gestión del agua

Exploraremos **Portolan NL**, un catálogo demostrativo con datos de distintas instituciones neerlandesas. Incluye una colección de **áreas de retención de agua** de Rijkswaterstaat, la autoridad neerlandesa de obras públicas y gestión del agua. La colección describe 1.545 polígonos y ofrece GeoParquet y PMTiles.

Este catálogo es una demostración/mirror elaborado a partir de servicios públicos originales. No es el catálogo oficial de Rijkswaterstaat y puede no estar tan actualizado como la fuente original. Para un análisis o una decisión real, localiza y contrasta la fuente oficial, la fecha, la licencia y la procedencia indicadas en los metadatos.

### 1. Encuentra el catálogo

Abre el [Registro Portolan](https://www.portolan-sdi.org/registry) y busca `Portolan NL`. Puedes abrir también directamente su [página de publicación](https://source.coop/cholmes/portolan-nl), el [catálogo STAC en formato JSON](https://data.source.coop/cholmes/portolan-nl/catalog.json) o [el catálogo en Portolan Browser](https://browser.portolan-sdi.org/#/external/data.source.coop/cholmes/portolan-nl/catalog.json).

El registro y la publicación pueden cambiar. Si el nombre ya no aparece, prueba el [Portolan Browser](https://browser.portolan-sdi.org/) o abre la dirección del catálogo directamente.

### 2. Explora sus metadatos

En el Portolan Browser, abre el catálogo y navega hasta la colección de Rijkswaterstaat **Flood Retention Areas** (*áreas de retención de agua*). Revisa:

1. **Productor y procedencia:** quién produce los datos y de qué tipo de fuente se obtuvieron.
2. **Descripción y geometría:** qué representan los polígonos y cuántas entidades contiene la colección.
3. **Fecha y licencia:** cuándo se actualizó el mirror y qué condiciones de reutilización indica la ficha. Verifica la licencia en esa colección concreta; no la deduzcas de otra colección del catálogo.
4. **Formatos y enlaces:** distingue el enlace a metadatos de los enlaces a GeoParquet y PMTiles.
5. **Vista previa:** abre el mapa de la colección si está disponible y observa la extensión geográfica de los datos.

### 3. Consume el recurso

Usa la vista del Portolan Browser para localizar una entidad y comprobar cómo se representa la capa PMTiles. Esa es una forma de consumir el recurso para exploración y visualización.

Si QGIS en tu ordenador incluye el controlador GeoParquet, prueba a descargar [el archivo GeoParquet de esta colección](https://data.source.coop/cholmes/portolan-nl/rijkswaterstaat/bergingsgebieden/bergingsgebieden.parquet) y abrirlo como capa vectorial. Revisa sus atributos y sistema de referencia. Si tu versión no reconoce GeoParquet, completa la actividad con la vista del navegador y anota qué formato descargable elegirías para seguir trabajando. No necesitas instalar extensiones durante la clase.

La colección de este ejemplo se distribuye en el sistema neerlandés EPSG:28992; por eso, sus coordenadas pueden aparecer en metros y no en longitud/latitud. La vista PMTiles puede reproyectarse para el mapa web. Comprueba el CRS antes de combinar o comparar las entidades con datos de otra región.

## Actividad de clase: evalúa una colección

**En parejas, 10 minutos.** Explorad la colección *Flood Retention Areas* y completad estas notas:

- ¿Qué organismo produce originalmente los datos y quién publica este catálogo demostrativo?
- ¿Qué representa cada entidad y cuántas hay?
- ¿Qué licencia y fecha de actualización declara la ficha?
- ¿Qué diferencias de uso hay entre el enlace de metadatos, GeoParquet y PMTiles?
- ¿Usaríais esta copia en un análisis oficial? ¿Qué fuente o dato contrastaríais antes?

**Resultado esperado:** una recomendación razonada sobre si la colección sirve para una exploración inicial y qué comprobar antes de reutilizarla en un trabajo real.

## Relación con las IDE

El catálogo facilita el descubrimiento, aporta contexto y enlaza con los datos. El Registro crea una puerta de entrada común a catálogos que siguen distribuidos. Esta arquitectura comparte con una IDE la idea de conectar productores, descripciones, recursos y clientes, aunque Portolan propone una forma específica de publicar archivos cloud-native.

Compáralo con el catálogo de metadatos visto anteriormente: ambos ayudan a encontrar y evaluar recursos; Portolan enfatiza la publicación directa de archivos con formatos preparados para consulta en la nube, mientras que el catálogo de metadatos puede describir recursos servidos por servicios o distribuidos de otras maneras.

## Fuentes

- [Portolan: visión general y funcionamiento](https://www.portolan-sdi.org/), consultado el 16 de noviembre de 2026.
- [Especificación Portolan en GitHub](https://github.com/portolan-sdi/portolan-spec), consultada el 16 de noviembre de 2026. El proyecto indica que se apoya en STAC 1.1.0 y que la especificación Portolan sigue en desarrollo antes de 1.0.
- [Registro Portolan](https://www.portolan-sdi.org/registry), consultado el 16 de noviembre de 2026.
- [Portolan NL: catálogo, fuentes, formatos y colecciones](https://source.coop/cholmes/portolan-nl), consultado el 16 de noviembre de 2026. La página identifica el catálogo como una prueba de concepto basada en datos publicados originalmente por servicios públicos neerlandeses.
- [Catálogo STAC de Portolan NL](https://data.source.coop/cholmes/portolan-nl/catalog.json).

**Siguiente:** [Qué es un Cloud Optimized GeoTIFF (COG)](cog.md).

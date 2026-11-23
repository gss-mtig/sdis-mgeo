# Instrucciones para trabajar en este repositorio

## Contexto y alcance

- Este repositorio contiene materiales en español para la asignatura de Infraestructuras de Datos Espaciales (IDEs) del Máster de Geoinformación de la UAB. El material actual trata conceptos, estándares, metadatos, catálogos, clientes y servidores; la actualización debe mantener las IDEs como eje central.
- El objetivo de la revisión pedagógica es convertir la materia en una experiencia más actual, dinámica y práctica, con menos exposición teórica continua y más actividades aplicadas.
- La asignatura tiene 16 horas lectivas. Prioriza la práctica guiada y un reto acumulativo; ajusta la amplitud de los temas modernos a este límite y distingue con claridad qué se aprende en profundidad y qué se presenta como panorama.
- El usuario quiere conservar WMS como contenido central, enseñarlo con detalle y dedicarle varios ejercicios/preguntas de clase. GeoJSON también es un contenido prioritario por su uso en la Web y en portales de datos abiertos.
- La formación sobre metadatos debe simplificar la explicación teórica de ISO, pero incluir la creación de registros y su publicación en GeoNetwork para apoyar el proyecto final del primer cuatrimestre.
- Enseña por separado la publicación de los datos (archivo, descarga, API o servicio) y la publicación de su ficha descriptiva en un catálogo como GeoNetwork; el flujo completo debe mostrar cómo se enlazan.
- Para asegurar que los ejercicios se puedan completar, organiza un menú acotado de casos o conjuntos de datos revisados antes de clase. Cada caso debe tener datos locales descargables y una ruta de acceso preparada; los servicios externos deben tener comprobación de disponibilidad y una alternativa local. No prometas disponibilidad continua de un servicio de terceros.
- El curso complementario de geoservicios está en el repositorio hermano `gss-mtig`. Evita duplicar o trasladar unidades enteras entre asignaturas. Coordina los conceptos compartidos y adapta su profundidad al objetivo de cada curso.
- La fuente del sitio está en `docs/`: páginas Markdown, imágenes en `docs/img/` y ejemplos en `docs/ejemplos/`. La configuración del sitio está en `mkdocs.yml`; Zensical la utiliza para generar y previsualizar la documentación. GitHub Actions publica el sitio en GitHub Pages.
- El usuario revisa la reformulación por bloques comprensibles. Para cambios amplios, trabaja en unidades coherentes, resume qué cambió y deja visible qué parte queda por revisar; no hagas una sustitución masiva difícil de revisar.
- No publiques, hagas `push` ni despliegues sin una solicitud explícita.

## Criterios pedagógicos y editoriales

- Diseña cada tema alrededor de una pregunta o tarea real que pueda resolverse usando una IDE: descubrir datos, evaluar su procedencia y condiciones de uso, consultar metadatos, visualizar o descargar información, combinar fuentes, o explicar cómo se coordinan los actores y servicios.
- Prioriza actividades observables y resultados concretos sobre listas de definiciones. Mantén la teoría necesaria para entender la actividad y vincúlala a una decisión o resultado práctico.
- Distribuye la participación durante la clase: ejercicios breves en parejas o grupos, búsquedas guiadas, comparación de resultados, discusión de casos y pausas de comprobación. Si una explicación conceptual se prolonga unos 30 minutos, intercala una actividad de 5–10 minutos que no tenga que entregarse.
- Cuando sea posible, usa ejemplos y datos abiertos de Catalunya, España y Europa, junto con casos comparables de otras regiones. Explica quién produce los datos, qué territorio y fecha cubren, cómo se actualizan y bajo qué condiciones se pueden reutilizar.
- No des por supuestos conocimientos de programación. Empieza con interfaces web, catálogos y clientes SIG; ofrece código como extensión cuando ayude a entender o automatizar un flujo.
- En la práctica WMS, trabaja las capacidades del servicio, selección de capas, `GetMap`, `GetFeatureInfo`, CRS/BBOX, formatos y transparencia, y diagnóstico de errores comunes. Explica que WMS entrega imágenes de mapa y cómo se diferencia de descargar o consultar las entidades.
- En GeoJSON, enseña a reconocer `Feature` y `FeatureCollection`, geometría y propiedades, orden de coordenadas y CRS de RFC 7946, cargar/exportar datos y decidir cuándo conviene usar el formato.
- GeoNetwork debe usarse de forma práctica en una instancia de aula o entorno preparado: crear un registro desde una plantilla, completarlo, validar lo esencial y ajustar permisos/publicarlo. Evita consumir horas lectivas instalando y configurando servidores desde cero.
- Las OGC APIs, vector tiles, COG, STAC y GeoParquet deben relacionarse con tareas de descubrimiento, acceso, análisis o publicación. Evita tratarlos como un listado exhaustivo; diferencia estándares aprobados, especificaciones comunitarias y borradores.
- Para cada actividad, deja claros su objetivo, materiales o datos, pasos, resultado esperado y una breve pregunta de reflexión. Para los ejercicios evaluables, conserva puntuación y criterios existentes salvo que el usuario solicite reformarlos.
- Mantén las actividades factibles en el tiempo y el equipo disponibles. Evita instalaciones complejas, registros obligatorios y servicios frágiles cuando exista una alternativa gratuita y sencilla.
- Corrige ortografía y consistencia terminológica. Usa “OGC” (no “OCG”), “IDE” o “IDEs” de forma consistente, y explica las siglas cuando aparecen por primera vez.
- Escribe en español claro, con secciones cortas, instrucciones directas, capturas o diagramas cuando ayuden y enlaces a documentación oficial. Evita convertir las páginas en apuntes enciclopédicos.

## Actualización de contenido y fuentes

- Comprueba la vigencia de leyes, normas, estándares, software, servicios, endpoints y conjuntos de datos antes de basar una práctica en ellos. Para estándares y software, prioriza documentación oficial; para datos, cita el catálogo o proveedor original.
- Indica si un estándar, API o procedimiento está aprobado, en borrador, en retirada o sustituido. Distingue entre cambios de la norma y cambios de una implementación concreta.
- Comprueba los enlaces externos y la disponibilidad de los servicios que se usarán en clase. Incluye una alternativa de reserva para las actividades que dependan de un servicio remoto.
- Cita las fuentes de afirmaciones factuales y ofrece enlaces estables a las especificaciones, guías o catálogos usados. Registra fechas cuando la vigencia importe.
- Reutiliza las imágenes y ejemplos existentes cuando sigan siendo correctos y comprensibles; actualízalos si muestran interfaces antiguas, pasos obsoletos o flujos que ya no se pueden reproducir.
- No incluyas claves API, tokens, contraseñas ni datos personales en páginas, ejemplos, capturas o historial de Git. Diseña las prácticas para que no requieran credenciales; si son imprescindibles, usa variables o entradas locales y nunca expongas su valor.

## Organización de la materia

- Conserva el hilo conductor de las IDEs: actores y marco institucional, datos y metadatos, catálogos, servicios e interoperabilidad, aplicaciones cliente, acceso y reutilización.
- Presenta los estándares como herramientas para resolver problemas y facilitar la interoperabilidad; evita tratarlos como un inventario desconectado de los flujos de trabajo.
- Relaciona las IDE locales, regionales, estatales y europeas para mostrar cómo se descubren y conectan los recursos entre escalas.
- Al proponer una nueva secuencia, explicita el tiempo estimado, el objetivo de aprendizaje y el producto o evidencia de cada bloque. No presupongas que todas las páginas actuales deban conservarse como unidades separadas.
- Mantén una distinción clara entre material explicativo, instrucciones para el alumnado, tareas evaluables y notas docentes.

## Sitio, ejemplos y publicación

- Actualiza la navegación en `mkdocs.yml` cuando cambien páginas o títulos. Mantén `site_url`, enlaces relativos, rutas de imágenes y nombres de archivos coherentes para GitHub Pages.
- Usa `zensical serve` para previsualizar localmente y `zensical build` para generar el sitio en `site/`. El sitio se publica con `.github/workflows/docs.yml`; no subas artefactos de build.
- Después de editar páginas o navegación, comprueba que la compilación de Zensical funciona y que las páginas, imágenes, enlaces internos y ejercicios aparecen correctamente.
- Si un visor web forma parte de una práctica, conserva una copia ejecutable en `docs/ejemplos/<nombre>/` y enlázala desde la lección. En GitHub Pages, proporciona una vista previa estática si la aplicación requiere un backend.
- Antes de fijar una práctica, verifica su paquete de datos, licencia, instrucciones y enlaces de servicio. Mantén una copia local pequeña del conjunto de datos y del material necesario para completar la actividad si falla la conexión o el proveedor externo.
- Mantén sincronizados los ejemplos funcionales y el código que se muestre en la lección. Fija versiones de dependencias externas y prefiere paquetes mantenidos.
- No añadas pruebas automatizadas o servicios de CI para las prácticas sin que aporten valor claro al alumnado o el usuario las solicite. Las comprobaciones manuales de servicios externos deben poder ejecutarse antes de la clase y no formar parte de `zensical build`.
- Antes de preparar una publicación solicitada, busca credenciales en los archivos que se vayan a publicar. No reescribas el historial ni purgues ramas remotas sin autorización explícita.

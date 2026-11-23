# Servidores de mapas

Una **IDE** permite encontrar y utilizar información geográfica publicada por distintas organizaciones. Para compartirla, una organización puede ofrecer archivos descargables, una API o un servicio de mapas. En esta lectura nos centramos en los servidores que responden a solicitudes de clientes y en las alternativas disponibles para publicarlos.

## Servidor, servicio y cliente

- El **servidor** es el software o la plataforma que recibe solicitudes y prepara una respuesta.
- El **servicio** es la forma de acceso que ofrece, definida por una interfaz o protocolo, por ejemplo WMS u OGC API – Features.
- El **cliente** es la aplicación que realiza la solicitud y presenta o utiliza la respuesta, como QGIS o un visor web.

El flujo general es:

```text
datos de origen → servidor → servicio → cliente
                         ↘ catálogo de metadatos
```

La ficha del catálogo describe el recurso y enlaza a su servicio o a los datos descargables. El catálogo no sustituye al servidor de mapas: ayuda a descubrir y comprender el recurso.

## ¿Qué se puede publicar?

La elección depende de lo que necesite hacer quien consulta los datos:

- **Una imagen de mapa:** el cliente recibe una representación cartográfica. WMS es el ejemplo que ya hemos estudiado.
- **Entidades geográficas:** el cliente puede consultar geometrías y atributos. WFS y OGC API – Features son dos interfaces con las que podemos acceder a entidades.
- **Teselas de mapa:** el territorio se entrega en piezas pequeñas para facilitar la visualización a distintas escalas. WMTS publica teselas de mapa; las teselas vectoriales contienen datos vectoriales preparados para su representación. Las veremos en una lección posterior.
- **Procesos geoespaciales:** un servicio puede ejecutar operaciones y devolver resultados. En esta asignatura basta con reconocer esta posibilidad.

Los catálogos de metadatos cumplen otra función: describen y ayudan a descubrir recursos. Por eso CSW y OGC API – Records se estudian en el contexto de catálogos, no como alternativas a un servidor de mapas.

## Alternativas de software

No existe un único servidor adecuado para todas las situaciones. Estas herramientas permiten publicar datos, pero se diferencian en el tipo de configuración y en las tareas para las que suelen elegirse.

### GeoServer

Servidor de propósito general con interfaz de administración web. Puede publicar mapas y datos mediante WMS, WFS, WCS, WMTS y OGC API – Features. Puede ser una opción cuando se necesita gestionar varias capas y servicios desde una misma aplicación. La disponibilidad de cada servicio depende de la versión y de las extensiones instaladas.

[Documentación de GeoServer](https://docs.geoserver.org/main/en/user/introduction/overview/)

### QGIS Server

Publica servicios a partir de proyectos de QGIS. Puede ser una opción cuando la simbología y la composición del proyecto ya se han preparado en QGIS y se quiere reutilizar esa configuración en un servicio. Su despliegue requiere configurar un entorno de servidor.

[Documentación de QGIS Server](https://docs.qgis.org/3.44/en/docs/server_manual/)

### MapServer

Servidor de mapas de código abierto que se configura principalmente mediante archivos de configuración llamados *mapfiles*. Es una alternativa cuando se busca controlar de forma explícita la definición de capas y servicios. Su configuración suele requerir conocimientos más técnicos.

[Documentación de MapServer](https://mapserver.github.io/documentation.html)

### pygeoapi

Implementación de las OGC API. Puede ser una opción cuando el objetivo principal es ofrecer acceso web a colecciones de datos y procesos con interfaces REST. Requiere configurar las fuentes de datos y el servidor.

[Documentación de pygeoapi](https://docs.pygeoapi.io/en/stable/)

### MapProxy

Actúa como intermediario entre servicios y clientes. Puede combinar servicios existentes, almacenar respuestas en caché o adaptar la forma en que se ofrecen. No sustituye necesariamente al servidor que mantiene y publica los datos originales.

[Sitio oficial de MapProxy](https://mapproxy.org/)

## El software no es lo mismo que el alojamiento

Además de elegir qué software utilizar, hay que decidir **dónde se ejecutará**:

- En un servidor de la propia organización, que esta administra.
- En una máquina virtual o servicio de alojamiento gestionado.
- En una plataforma de datos que ofrece una base de datos y una API.
- En un alojamiento estático, si basta con publicar archivos que no requieren consultas dinámicas.

Un software de servidor no garantiza por sí mismo que el servicio vaya a estar disponible en Internet. También hacen falta una máquina accesible, configuración de red, mantenimiento, medidas de seguridad y una estrategia para actualizar los datos. Más adelante compararemos la publicación de un archivo estático y una base de datos online.

## Antes de publicar

Antes de poner un recurso a disposición de otras personas, conviene comprobar:

1. **Qué se ofrece:** archivo, imagen de mapa, entidades, teselas o proceso.
2. **Quién puede acceder:** público, usuarios identificados o personal de una organización.
3. **Qué necesita el cliente:** protocolo, formato, sistema de coordenadas y extensión geográfica.
4. **Cómo se mantiene:** fecha de actualización, persona u organización responsable y disponibilidad esperada.
5. **Qué condiciones se aplican:** licencia, atribución, privacidad y restricciones de uso.
6. **Cómo se descubre:** ficha de metadatos con un enlace al servicio o a la descarga.

## Actividad: elegir una alternativa

**Objetivo:** relacionar una necesidad de publicación con el tipo de recurso y el servidor que podría ofrecerlo.

**Materiales:** esta lectura y las páginas enlazadas de los proyectos.

En parejas, leed estos escenarios y para cada uno proponed:

1. qué necesita recibir el usuario (imagen, entidades, teselas o archivo);
2. una herramienta de las presentadas que investigaríais;
3. una razón para elegirla y una cuestión que habría que resolver antes de publicarla.

**Escenarios:**

- Una administración quiere mostrar una cartografía temática con la simbología definida por su equipo SIG.
- Un portal necesita que otros programas consulten las entidades y sus atributos.
- Una IDE ya dispone de varios servicios lentos y quiere reutilizarlos mediante una caché.
- Un equipo tiene datos en GeoJSON y quiere ofrecer colecciones mediante OGC API.

**Resultado esperado:** una propuesta razonada para cada escenario; no hay una única respuesta correcta. La herramienta debe corresponder al tipo de recurso y a la necesidad indicada.

**Reflexión:** ¿qué responsabilidades tendría que asumir la organización además de instalar o contratar el software?

!!! note "Materiales trasladados para revisar"
    Se han separado de esta lectura el [tutorial de QGIS Server](qgis_server.md) y la [práctica de georreferenciación](georeferenciacion.md). Sus procedimientos se revisarán más adelante.

## Referencias

- [GeoServer: introducción y estándares disponibles](https://docs.geoserver.org/main/en/user/introduction/overview/).
- [QGIS Server: servicios disponibles](https://docs.qgis.org/3.44/en/docs/server_manual/services.html).
- [MapServer: documentación oficial](https://mapserver.github.io/documentation.html).
- [pygeoapi: servidor de las OGC API](https://pygeoapi.io/).
- [MapProxy: proxy y caché de servicios geoespaciales](https://mapproxy.org/).

**Siguiente:** [Publicar con QGIS Server](qgis_server.md).

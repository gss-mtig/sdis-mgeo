# Metadatos

## Qué es un metadato

El término «metadatos» no tiene una definición única. Según la definición más difundida de metadatos es que son «datos sobre datos». También hay muchas declaraciones como «informaciones sobre datos», «datos sobre informaciones» e «informaciones sobre informaciones».

![Metagato](img/metagato.jpg "Metagato")
Metagato

Los metadatos (del griego μετα, meta, 'después de, más allá de' y latín datum, 'lo que se da', «dato»​), literalmente «sobre datos», son datos que describen otros datos. En general, un grupo de metadatos se refiere a un grupo de datos que describen el contenido informativo de un objeto al que se denomina recurso.​ El concepto de metadatos es análogo al uso de índices para localizar objetos en vez de datos. [^1]

Por ejemplo, en una biblioteca se usan fichas que especifican autores, títulos, casas editoriales y lugares para buscar libros. Así, los metadatos ayudan a ubicar datos.

Surge así el concepto de metadatos. Literalmente, los metadatos son «datos acerca de los datos», y su misión es explicar el significado de los datos. Es decir, ayudan a los usuarios de los datos a entender mejor el significado que estos tienen y la información que guardan. Los metadatos son un documento adicional que acompaña a los datos, y que permite una mejor gestión y una utilización más precisa de ellos. [^2]

Los metadatos son utilizados muy a menudo. Cuando alguien entra en una biblioteca, puede ir a buscar el cajón dónde hay las fichas de los libros (si no está informatizada), o bien puede ir a buscar al catálogo electrónico de la biblioteca. Ambas soluciones utilizan metadatos. Imaginad que entráis en un Supermercado y veis que no hay ningún producto que tenga etiquetas. ¿Cómo sabríamos qué estamos comprando? Las etiquetas nos informan del contenido del envase, por lo tanto son metadatos.

Hay que pensar en los metadatos espaciales como una leyenda, mucho más detallada que la del mapa en papel, que describe la gente que ha producido los datos, las fuentes documentales utilizadas en la producción, los atributos que hay asociados a los datos, la fecha de publicación, el sistema de referencia, la frecuencia de mantenimiento...

Es importante utilizar estándares para la creación de metadatos, porque aportan un lenguaje común a la hora de describir los datos. El estándar internacional ISO 19115 es el que actualmente se está imponiendo frente a todos los otros en el proceso de describir la información geográfica existente y el ISO 19119 para describir servicios. Este estándar está atado a la ISO 19139, que da las pautas para la implementación del ISO 19115.

Un ejemplo de metadato global de una capa puede ser el nombre de su autor o la fecha en la que ese dato ha sido creado. El sistema de referencia en el que se expresan las coordenadas de cada entidad recogida es un tipo de metadato relativo a la componente espacial. Y en lo referente a la componente temática, los metadatos pueden recoger las unidades en las que se recoge una variable asociada a cada entidad, o bien almacenar cualquier otro valor que permita una mejor interpretación de esa variable.

### Utilidad de los metadatos

En algunos casos, incluso si carecemos de metadatos, resulta posible interpretar correctamente los datos, como sucede si trabajamos con un Modelo Digital de Elevaciones (MDE) y valores de elevación en metros. Es fácil saber que los valores de elevación se encuentran en esas unidades aplicando cierta lógica, y procesarlos correspondientemente aunque no exista un dato explicito que así nos los indique. 

En otras circunstancias, los metadatos son necesarios, pues contienen información que no puede inferirse directamente desde los propios datos. Si varias capas están en sistemas de coordenadas distintos y deseamos aplicar las transformaciones correspondientes para unificarlos en uno único y procesarlas de manera conjunta, estas transformaciones no se pueden llevar a cabo si no conocemos el sistema de origen del que partimos en cada capa. En este supuesto, el trabajo con los datos viene condicionado a que existan los metadatos correspondientes.

Los metadatos:

* *Ayudan a ordenar y a mantener la inversión en los datos*. Los usuarios potenciales de los datos podrán no utilizar los datos porque no conocen las características de los mismos.
* *Ayudan a la transferencia de los datos*. Aportan información sobre el formato del archivo, el volumen en megabytes, la localización de los datos, etc. lo cual permite a un usuario procesar correctamente los datos.
* *Se pueden utilizar para permitir la distribución en línea de los datos*. Podrán incorporar direcciones para descargar archivos, ya sea gratuitamente o previo pago, mediante unas descripciones de cómo realizar estos procesos.
* *Facilitan la búsqueda de datos en múltiples bases de datos*. Unos metadatos estándares permiten a un usuario hacer una consulta, que es redirigida a los diferentes catálogos de metadatos grabados en el servidor principal. El resultado es un listado de metadatos procedentes de diferentes servidores.
* *Pueden ayudar a evitar el uso erróneo de los datos*. Incluyen unas descripciones de cómo hay que utilizar estos datos y para qué finalidad y objetivos fueron creados.

### Proceso de creación de metadatos

La creación de los metadatos no es tarea de un único grupo de profesionales ni se lleva a cabo en un único momento dentro del ciclo de vida de los datos. Por el contrario, distintas entidades o grupos pueden crear o editar los metadatos, y pueden hacerlo a lo largo de todo el tiempo de existencia de dichos datos.

En resumen, los metadatos pueden ser creados o modificados en los siguientes puntos dentro de la vida de los datos:

* Cuando se crean los datos.
* Cuando se organizan o catalogan los datos.
* Cuando se modifican o editan los datos.
* Cuando se archivan o descatalogan los datos.

Durante este proceso de descripción de los datos es importante seguir unos pasos básicos:

* *Organizar la información*; es importante saber qué tenemos y como está estructurado.
* *Redactar el metadato*; hay que tener presente que lo pueden leer usuarios no expertos, por lo que tiene que ser redactada de forma clara y sencilla. Si por eso el texto tiene que ser más largo, no hay problema. El título es muy importante por localizar la información. Habría que incluir Qué, Dónde, Cuándo, Quién y Escala.
* *Revisar el metadato*; entregar el documento a otro para que se lo lea. Si sólo hay la persona que los ha redactado, que los deje una temporada y los vuelva a leer.

La elaboración de estos metadatos se hace sobre la base de unos estándares internacionales, que especifican qué información se tiene que dar en cada apartado. De esta manera, todo el mundo describe los datos del mismo modo.

Un vez creados y revisados los metadatos son importados a un servidor de catálogo y se utilizan para localizar, evaluar y acceder a la información geográfica disponible.

En circunstancias ideales, todo dato debería tener asociados unos metadatos, y estos últimos deberían crearse siempre que se creen dichos datos y actualizarse siempre que estos se modifiquen. La realidad, sin embargo, es que una gran parte de los datos geográficos que existen no tiene metadatos asociados, o bien estos no son lo suficientemente detallados.

### Contenido de los metadatos

Los valores que pueden incorporarse a los metadatos son muy abundantes, tantos como tipos distintos de información se considere necesario registrar respecto a un dato geográfico particular.

Las características de los metadatos asociados a los datos dependerán directamente de estos y de algunos factores como los siguientes:

* El tipo de dato y, en particular, el modelo de representación empleado. Los datos vectoriales tendrán asociados unos metadatos distintos que los correspondientes a datos ráster. 
* La organización, entidad o individuo responsable de la creación de los datos y el uso que se pretende dar a estos.
* El elemento al que se asocian los metadatos. Como veremos en el siguiente apartado, podemos asociar metadatos a un juego de capas, una capa o una entidad aislada dentro de una capa.
* El estándar empleado para crear los metadatos.

Algunos de los elementos comunes que se incorporan a los metadatos geográficos son los siguientes:

* **Información de identificación.** Este tipo de información permite identificar de forma única un dato geográfico y distinguirlo de otros. Esta información ayuda a catalogar los datos, e incluye el nombre, palabras claves, una descripción básica o la ya mencionada extensión geográfica de los datos. 
* **Información sobre la calidad de los datos.** La información sobre la calidad de los datos puede incluir, entre otros elementos, aquellos relativos a la completitud de estos, los procesos que se han empleado en su creación y mantenimiento, o las operaciones de validación y verificación a las que se han sometido.
* **Información sobre la representación del dato espacial.** Se incluyen en este grupo la precisión y exactitud de los datos, la escala de trabajo o la resolución en el caso de capas ráster. Este tipo de metadatos están también íntimamente ligados con la calidad de los datos.
* **Información sobre la componente no espacial.** Información relacionada con los atributos que acompañan a las capas vectoriales, o bien relativas a las variables que se recogen en capas ráster. Esto incluye explicaciones sobre el significado de los nombres de cada uno de los atributos, el rango de valores válidos para cada uno de ellos o los métodos empleados para recoger estos datos.
* **Información sobre la distribución.** Esta información sirve para definir el acceso a los datos y las posibilidades de distribución de estos, especificando quiénes pueden acceder a ellos y quiénes no, o en qué condiciones pueden hacerlo. También puede recoger elementos como la fecha en que fueron publicados los datos o bien cuándo fueron puestos a disposición del público.

### Granularidad de los metadatos

Habitualmente, los metadatos están asociados a un conjunto de datos al completo. Este conjunto de datos que sirve como unidad a la hora de crear metadatos coincide en general con la idea de capa en un SIG. Es decir, cada capa tiene asociado un bloque de metadatos.

Esto no quiere decir, no obstante, que no puedan registrarse metadatos a un nivel distinto. Dependiendo del tipo de datos con los que se trabaje, puede resultar de interés o incluso necesario asociar metadatos a unidades distintas.

Algunos metadatos como el sistema de coordenadas serán compartidos por todos los elementos de una capa, y por tanto es lógico en su caso emplear la capa como unidad básica en lo que a metadatos se refiere. Otro metadatos, sin embargo, hacen referencia a elementos particulares dentro de la capa.

Se podría llegar a crear metadatos con una granularidad muy grande a nivel de elemento. Por ejemplo en una capa vectorial se podrían identificar los siguientes datos:

* Quién ha creado ese elemento.
* Quién ha modificado ese elemento.
* Cuándo fue creado originalmente.
* Cuándo ha sido modificado por ultima vez.
* Cuántas veces ha sido modificado.
* Una descripción del objeto real que este elemento representa. 

También podemos encontrar el caso opuesto, en el que varias capas comparten los mismos metadatos, y por tanto estos pueden asociarse a escala de toda una familia de datos. Ese es el caso cuando se tiene un conjunto de capas generadas por una misma entidad y para un mismo fin, las cuales cubren una amplia zona geográfica y debido a ello se encuentran divididas horizontalmente. Estas circunstancias se dan de forma habitual en series de datos de carácter nacional o autonómico, y conforman una de las situaciones en las que el registro de metadatos puede hacerse para toda la serie en su conjunto, al menos para algunos de esos metadatos.

### Ejemplos de metadatos

La mejor forma de entender el contenido de los metadatos es ver algunos sencillos ejemplos reales.

http://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/metadata/spaJEXtmexTerminosMunicipales

https://ide.cat/geonetwork/srv/cat/catalog.search#/metadata/base-municipal-5k-v2r1

En ellas pueden verse verse los metadatos con un formato de página Web sencilla compuesta de una lista de apartados y campos, así como su valores correspondientes.

Si se comparan los campos y apartados que aparecen en ambas páginas, puede verse que no coinciden completamente. Eso es debido a que esos metadatos han sido generados por distintos organismos, que no utilizan una única metodología.

### Perfiles de metadatos

Con el objetivo de formalizar y homogeneizar los metadatos, los organismos responsables de las IDEs redactan unas guías que definen las directrices (requisitos y recomendaciones) a seguir a la hora de generar metadatos, de acuerdo a los estándares de metadatos de conjuntos de datos (ISO 19115) y de servicios (ISO 19119). Entre otros, fijan el contenido de información mínimo y obligatorio que han de incluir, así como los posibles contenidos opcionales. Estos documentos se conocen como Perfiles de metadatos.

#### Ejemplos de perfiles de metadatos

##### Perfil IDEC
http://www.cartocat.cat/geoportal/cas/documentacio/manuals/Perfil_IDEC_v4.0_cas.pdf

##### Núcleo español de metadatos (NEM)
https://idee.es/resources/presentaciones/JIDEE05/sesion_04_02.pdf

##### INSPIRE
https://inspire.ec.europa.eu/documents/inspire-metadata-implementing-rules-technical-guidelines-based-en-iso-19115-and-en-iso-1

## Qué es un catálogo de metadatos

El catálogo de metadatos, es quizá la pieza más importante dentro de una IDE y se trataría de un registro, que contendría el inventario de la información geográfica disponible en el territorio “administrado” por la IDE.

El proceso para implementar un catálogo puede resultar tedioso y poco gratificante pero es parte importante en el éxito de una IDE.

Básicamente implica identificar y convencer a todos los posibles productores de datos cartográficos, llámese departamento, agencia, empresa o incluso universidad que haga un inventario de toda su información geográfica y la describa siguiendo una ficha estándar. Esto es lo que se llama, crear metadatos.

Estos metadatos, que son ficheros con codificación XML que siguen el estándar ISO 19115, son cargados dentro del catálogo de metadatos para poder ser interrogados por todos los usuarios.

Cabe decir que la confección del metadato no es tarea fácil y que en el se describen campos como por ejemplo: creador de la cartografía, fecha de creación, fecha revisión, accesibilidad, formatos de la información, calidad, distribución o caja de coordenadas de la información descrita.

Una particularidad de los catálogos de metadatos, es que permiten ser interrogados espacialmente (ej. Dime toda la información geográfica existente que intercepte con el trazado de este rio) y algunos de ellos, por ejemplo el de la IDEC, van más allá de un simple repositorio de metadatos y permiten registrar plantillas de transformación entre móldelos de datos geográficos, peticiones a objetos geográficos o estilos de representación cartográficas, todos ellos utilizados como parte de lo geoservicios distribuidos.

Una vez descrita e inventariada la información geográfica se les pide a los entes integrantes de la IDE que permitan la visualización, básicamente a través de un navegador web, de la información descrita. Para ello se utilizan los servidores de mapas.

### Ejemplos de catálogos de metadatos

https://ide.cat/geonetwork/srv/cat/catalog.search#/home

http://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/home

## Herramientas para trabajar con metadatos

**Editores de texto.** Los metadatos pueden almacenarse en un fichero de texto plano, y por tanto pueden editarse con cualquier programa que permita la creación y edición de tales ficheros. Lo habitual en este caso es disponer de un fichero plantilla que contenga los distintos campos que se han de registrar para cada conjunto de datos geográficos, y la creación del metadato consiste simplemente en apoyarse en esa plantilla y a continuación de cada nombre de campo añadir el valor correspondiente.

**Editores de metadatos.** Herramientas más elaboradas que presenten una interfaz gráfica con distintas cajas de texto o listas desplegables. Estas aplicaciones, además de ser más agradables para el usuario, permiten incorporar elementos de validación en el proceso, evitando que en algún campo se introduzcan valores incorrectos o avisando al usuario en caso de que un campo presente un valor sospechoso.

**Utilidades.** Existen aplicaciones que no se emplean directamente para introducir los valores de los metadatos, pero que pueden intervenir en el proceso. Entre ellas están aquellas que chequean y validan los metadatos o las que lo preprocesan dándole un formato adecuado según unas reglas establecidas de antemano. 

**Herramientas de creación automática de metadatos.** Algunos de los valores que se incorporan a los metadatos pueden extraerse de los propios datos. Por ello, el proceso de creación de metadatos puede automatizarse en cierta medida, y existen aplicaciones específicamente diseñada para realizar esa tarea.

Para facilitar la tarea de creación y edición de metadatos existen en el mercado diversos editores de metadatos de libre acceso. Estos editores permiten editar metadatos en un entorno amigable al usuario, ocultando la complejidad que puede suponer su edición manual y proporcionando la conformidad a los estándares aplicables.

## Referencias

[^1]: https://es.wikipedia.org/wiki/Metadatos
[^2]: http://volaya.github.io/libro-sig/chapters/Metadatos.html

# Catálogo de Metadatos

Uno de los principales objetivos de las Infraestructuras de Datos Espaciales (IDEs) es facilitar la búsqueda y consulta de la información espacial existente. Para ello es necesaria la catalogación de dichos datos espaciales, y su posterior carga en un servicio de catálogo de metadatos.

## Qué es un catálogo de metadatos

El catálogo de metadatos, es quizá la pieza más importante dentro de una IDE y se trataría de un registro, que contendría el inventario de la información geográfica disponible en el territorio “administrado” por la IDE.

El proceso para implementar un catálogo puede resultar tedioso y poco gratificante pero es parte importante en el éxito de una IDE.

Básicamente implica identificar y convencer a todos los posibles productores de datos cartográficos, llámese departamento, agencia, empresa o incluso universidad que haga un inventario de toda su información geográfica y la describa siguiendo una ficha estándar. Esto es lo que se llama, crear metadatos.

Estos metadatos, que son ficheros con codificación XML que siguen el estándar ISO 19115, son cargados dentro del catálogo de metadatos para poder ser interrogados por todos los usuarios.

Cabe decir que la confección del metadato no es tarea fácil y que en el se describen campos como por ejemplo: creador de la cartografía, fecha de creación, fecha revisión, accesibilidad, formatos de la información, calidad, distribución o caja de coordenadas de la información descrita.

Una vez descrita e inventariada la información geográfica se les pide a los entes integrantes de la IDE que permitan la visualización, básicamente a través de un navegador web, de la información descrita. Para ello se utilizan los servidores de mapas.

## Funciones del Catálogo de Metadatos

Mediante el catálogo los usuarios podrán realizar búsquedas, a través de opciones como nombre, área geográfica, coordenadas, categoría temática ó tipo de dato, ofreciendo adicionalmente un mapa de referencia para interactuar con el usuario y facilitar la búsqueda de información, además de visualizar los mapas y obtener información geográfica.

Una particularidad de los catálogos de metadatos, es que permiten ser interrogados espacialmente (ej. Dime toda la información geográfica existente que intercepte con el trazado de este rio) y algunos de ellos, por ejemplo el de la IDEC, van más allá de un simple repositorio de metadatos y permiten registrar plantillas de transformación entre modelos de datos geográficos, peticiones a objetos geográficos o estilos de representación cartográficas, todos ellos utilizados como parte de lo geoservicios distribuidos.

También se puede descargar la ficha de metadatos de los distintos recursos, o descargar directamente el dato mediante un enlace. 

Algunos de los datos georeferenciados se pueden consultar y visualizar mediante servicios de mapas interoperables del OGC como por ejemplo Web Map Services (WMS), Web Feature Services (WFS) y Web Coverage Services (WCS).

### Ejemplos de catálogos de metadatos

https://ide.cat/geonetwork/srv/cat/catalog.search#/home

http://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/home

## Ejercicio

!!! question "Ejercicio 0.5 pts"
    En un documento de texto poner:

    * La url de una IDE
    * Realiza una búsqueda de datos sobre un tema específico (Ej. vegentación)
    * Realizar consultas usando filtros de atributos y/o espaciales para afinar los resultados
    * Hacer una captura de una búsqueda en el catálogo de la IDE de servicios WMS relacionados al tema específico seleccionado.

# WFS

El WFS (Web Feature Service) es una especificación que sirve para lanzar consultas sobre objetos geográficos.

Los WFS implementan también la especificación OGC FILTER encoding que permite dotar a WFS de un gran potencial ya que le permite realizar tanto consultas alfanuméricas y espaciales.

WFS básico permite hacer consultas y recuperación de elementos geográficos. Por el contrario WFS-T (Web Feature Service Transactional) permite además la creación, eliminación y actualización de estos elementos geográficos del mapa. 

Para realizar estas operaciones se utiliza el lenguaje GML (Geography Markup Language) que deriva del XML, que es el estándar a través del que se transmiten las órdenes WFS. el GML También es el formato de retorno de las consultas.

| Operadores espaciales | Operadores lógicos |
|-----------------------|--------------------|
| BBOX                  | LessThan           |
| Intersects            | LessThanEqualTo    |
| Within                | GreaterThanEqualTo |
| Beyond                | NotEqualTo         |
| Equals                | Like               |
| Disjoint              | GreaterThan        |
| Touches               | EqualTo            |
| Crosses               | Between            |
| Contains              |                    |
| Overlaps              |                    |

Se puede ver la especificación en [https://www.ogc.org/standards/wfs](https://www.ogc.org/standards/wfs)

## Tipos de peticiones WFS

### GetCapabilities

Nos permite descubrir cuales son las capacidades del servidor. Como respuesta va a obtener un archivo en formato xml dónde podremos saber cuales son las características del servicio, las versiones de WFS soportadas por el servidor, las operaciones que soporta, cual es su sistema de referencia, sus coordenadas y metadatos de las capas de información que contiene.

#### Parámetros del GetCapabilities

| Parámetro | Obligatoriedad | Descripción                                                            |
|-----------|----------------|------------------------------------------------------------------------|
| VERSION   | Obligatorio    | Versión de la especificación OGC (1.0.0, 1.1.0, 1.1.3, 2.0, 2.0.2)          |
| SERVICE   | Obligatorio    | Tipo de servicio al que va dirigida la petición (**WFS**)                  |
| REQUEST   | Obligatorio    | Nombre de la operación (**GetCapabilities**)                               |

Ejemplo: http://www.juntadeandalucia.es/institutodeestadisticaycartografia/geoserver-ieca/grid/wfs?REQUEST=GetCapabilities&SERVICE=WFS&VERSION=2.0.0

### DescribeFeatureType

Devuelve la descripción de los tipos de objetos geográficos (XML schema de los feature types) que el servicio puede ofrecer. El servidor devuelve como respuesta un archivo XML. En la descripción del tipo de objeto geográfico se indica cómo hay que codificar los objetos geográficos para enviarlos como datos de entrada en operaciones de inserción, actualización o sustitución, y cómo se codifican cuando son datos de salida (en las respuestas de las operaciones GetPropertyValue, GetFeature o GetFeatureWithLock). Es una operación obligatoria.

#### Parámetros del DescribeFeatureType

| Parámetro    | Obligatoriedad | Descripción                                                                                                                                                           |
|--------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VERSION      | Obligatorio    | Versión de la especificación OGC (1.0.0, 1.1.0, 1.1.1, 1.3.0)                                                                                                         |
| SERVICE      | Obligatorio    | Tipo de servicio al que va dirigida la petición (**WFS**)                                                                                                             |
| REQUEST      | Obligatorio    | Nombre de la operación (**DescribeFeatureType**)                                                                                                                         |
| TYPENAME     | Opcional       | Lista los nombres de los tipos de objeto geográfico que se van a describir, separados por comas. Si no se indica ninguno, devuelve la descripción de todos los tipos. |
| OUTPUTFORMAT | Opcional       | Formato de salida para describir los tipos de objetos. Por defecto GML3.2 (text/xml;subt ype=gml/3.2)                                                                                             |

Ejemplo: http://www.ign.es/wfs/redes-geodesicas?REQUEST=DescribeFeatureType&SERVICE=WFS&VERSION=1.1.0&TYPENAME=RED_ROI

### GetFeature

Esta operación devuelve una selección de objetos geográficos en formato GML. Además, debe ser posible realizar un filtro en función de sus propiedades para obtener los objetos geográficos que desea y de realizar tanto consultas espaciales como no espaciales. Es una operación obligatoria.

Para definir el tipo de objeto geográfico a consultar, qué propiedades obtener y las restricciones a aplicar se utilizan el elemento Query

Para ver más operaciones y ejemplos https://www.idee.es/resources/documentos/RD_wfs_v2_0.pdf

#### Parámetros del GetFeature

| Parámetro       | Obligatoriedad | Descripción                                                                                                                                                                                                                                                                                                             |
|-----------------|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VERSION         | Obligatorio    | Versión de la especificación OGC (1.0.0, 1.1.0, 1.1.1, 1.3.0)                                                                                                                                                                                                                                                           |
| SERVICE         | Obligatorio    | Tipo de servicio al que va dirigida la petición (**WFS**)                                                                                                                                                                                                                                                               |
| REQUEST         | Obligatorio    | Nombre de la operación (**GetFeature**)                                                                                                                                                                                                                                                                           |
| TYPENAME        | Obligatorio    | Lista los nombres de los tipos de objeto geográfico que se van a describir, separados por comas. (Excepto cuando el parámetro RESOURCE_ID es especificado)                                                                                                                                                              |
| RESOURCEID      | Opcional       | Lista los identificadores únicos de los objetos geográficos que se quieren obtener. Mutuamente excluyente con FILTER y BBOX.                                                                                                                                                                                            |
| FILTER          | Opcional       | Describe un conjunto de características sobre las que operar. Se debe establecer un filtro por cada tipo de objeto geográfico listado en el parámetro TYPENAME                                                                                                                                                          |
| BBOX            | Opcional       | Solicitud mediante una bounding box (rectángulo envolvente). Mutuamente excluyente con RESOURCEID y FILTER.                                                                                                                                                                                                             |
| SORTBY          | Opcional       | Indica los nombres de las propiedades cuyos valores se van a utilizar para ordenar el resultado de la consulta. Se puede indicar si el orden es ascendente o descendente, valor ASC o DESC (Valor por defecto: orden descendente DESC). Ejemplo: SORTBY=Apellido ASC,Nota DESC                                          |
| FILTER_LANGUAGE | Opcional       | Indica el lenguaje que se emplea para codificar la expresión (valor de FILTER). Valor por defecto urn:ogc:def:queryLanguage:OGC-FES:Filter.                                                                                                                                                                             |
| SRSNAME         | Opcional       | Sistema de referencia que debe aplicarse en la geometría de los objetos geográficos resultantes de la petición. Si no se indica, el servicio devuelve las geometrías en el sistema que posea por defecto. El servidor debe ser capaz de transformar las geometrías en los distintos sistemas de referencia que soporta. |

Ejemplos: 

*Solicitud para obtener todos los vértices geodésicos entre los paralelos 38 y 39 entre las latitudes 0 y 2 (parámetro BBOX) de la Red de Orden Inferior (parámetro typeName) del servicio de redes geodésicas del Instituto Geográfico Nacional. Los resultados los pedimos en proyección UTM huso 30 (parámetro srsNAME) y en el formato XML (parámetro outputFormat)*

http://www.ign.es/wfs/redes-geodesicas?SERVICE=WFS&REQUEST=GetFeature&TYPENAME=RED_ROI&srsNAME=urn:ogc:def:crs:EPSG::25830&BBOX=38,0,39,2&outputFormat=text/xml;%20subtype=gml/3.1.1

*Solicitud del objeto geográfico denominado “Teide” del Nomenclátor Geográfico Básico de España usando el parámetro FILTER*

http://www.ign.es/wfs-inspire/ngbe?SERVICE=WFS&VERSION=2.0.0&REQUEST=GetFeature&COUNT=10&TYPENAME=gn:NamedPlace&FILTER=%3cFilter%20xmlns:gn=%22http://inspire.ec.europa.eu/schemas/gn/4.0%22%3e%3cPropertyIsEqualTo%3e%3cValueReference%3egn:name/gn:GeographicalName/gn:spelling/gn:SpellingOfName/gn:text%3c/ValueReference%3e%3cLiteral%3eTeide%3c/Literal%3e%3c/PropertyIsEqualTo%3e%3c/Filter%3e

# Estándares OCG
    
## Qué es OGC?

El OGC (Open Geospatial Consortium fué creada en 1994 y está formada por más de 500 empresas, agencias gubernamentales y universidades. Es una organización internacional sin ánimo de lucro comprometida con la elaboración de estándares abiertos e interoperables de calidad para la comunidad geoespacial global. 

Estos estándares se elaboran a través de un proceso de consenso y están disponibles de forma gratuita para que cualquier persona pueda utilizarlos para mejorar el intercambio de los datos geoespaciales del mundo.

Estas especificaciones tienen como objetivo, fomentar la interoperabilidad geoespacial. El éxito de estas especificaciones radica en el hecho de que son impulsadas y creadas por las mismas empresas, que después las implementan en sus productos comerciales. 

### Interoperabilidad

Se puede definir la interoperabilidad como la habilidad de dos o más sistemas para intercambiar información y poderla utilizar, sin ningún esfuerzo por parte del usuario. Las modalidades de interoperatividad dependen de los agentes que interaccionan. Dicho de otra manera, los datos producidos en un entorno operativo tienen que poder ser leídos e interpretados por otro entorno sin que el usuario tenga que hacer una conversión de formatos.

La interoperabilidad permite:

* Acceder a más y mejor información (topográficos, ortoimágenes, callejeros, catastro, medio ambiente...), sin tener que disponer de un software específico o directamente desde el navegador. Esto permite que el usuario pueda acceder a cartografía de varias fuentes, con arquitecturas diferentes, de una forma fácil y transparente.

* Facilita el acceso a geoservicios.

## Estándares OGC

Un estándar es un modelo, un patrón que tiene como finalidad la fijación de unas normas comunes para garantizar la homogeneidad en el proceso de producción. Pero para que tenga éxito tiene que tener un uso mayoritario. 

![estandares](img/standards.png)
*Estándares*

Para conseguir que, tanto la documentación de los datos como la creación de servicios sea comprensible y accesible para todo el mundo, es decir, para hacer que todos “hablemos el mismo idioma”, se han diseñado estándares de metadatos y de servicios que pretenden poner en común los puntos de vista de los diferentes productores. Por lo tanto, la estandarización consiste en hacer que, tanto la documentación de datos como la creación de geoservicios, así como su acceso, se hagan conforme a unas norma previamente establecidas. 

Los estándares de la OGC son documentos de carácter técnico dónde se describen las interfaces de comunicación entre servidores y la forma de implementarlos.

En estas especificaciones no se menciona ni la arquitectura, plataforma o lenguajes de programación a utilizar. 

Los documentos, antes de ser consideradas como una OpenGIS Implementation Specification, son elaborados y probados por diferentes grupos de trabajo dentro de OGC y finalmente sometidas a votación.

Los servicios de cartografía online o web de OGC (OWS) son estándares de OGC creados para su uso en aplicaciones de la World Wide Web (WWW). Estos permiten formular petiones al servidor para: enviar preguntas, obtener datos vectoriales o ráster, hacer geoprocesos, etc.   

Todos los estándares creados por OGC se pueden consultar en [https://www.ogc.org/docs/is](https://www.ogc.org/docs/is)

![Evolución de servicios OWS](img/ows.png)
*Evolución de servicios OWS*

### WMS

La intención de WMS (Web Map Service) es la de permitir la superposición visual de información geográfica compleja y distribuida en diferentes servidores. Un cliente puede hacer peticiones a otros servidores también basados en esta especificación para descubrir información geográfica deseada. Una vez encontrada el cliente puede recurrir a ella de forma simultánea y puede visualizar diferentes datos geográficos de diferentes servidores en un mismo entorno.

Cada petición está compuesta por unos parámetros concretos definidos por la especificación WMS y que es entendida por todos los servidores de mapas que cumplen con la especificación.

Por lo tanto, cuando se dice que un Servidor de Mapas es estándar y cumple con WMS, significa que es capaz de dar respuesta a estas peticiones.

El estándar WMS proporciona una interfaz HTTP simple para solicitar imágenes de mapas georegistrados desde una o más bases de datos geoespaciales distribuidas. 

#### Tipos de peticiones WMS

#### GetCapabilities

Nos permite descubrir cuales son las capacidades del servidor. Como respuesta va a obtener un archivo en formato xml dónde podremos saber cuales son las características del servicio, las versiones de WMS soportadas por el servidor, las operaciones que soporta, cual es su sistema de referencia, sus coordenadas, que formato de imagen soporta y metadatos de las capas de información que contiene.

##### Parámetros del GetCapabilities

| Parámetro | Obligatoriedad | Descripción                                                            |
|-----------|----------------|------------------------------------------------------------------------|
| VERSION   | Obligatorio    | Versión de la especificación OGC (1.0.0, 1.1.0, 1.1.1, 1.3.0)          |
| SERVICE   | Obligatorio    | Tipo de servicio al que va dirigida la petición (**WMS**)                  |
| REQUEST   | Obligatorio    | Nombre de la operación (**GetCapabilities**)                               |
| LANGUAGE  | Opcional       | Se obtiene el fichero de salida en el idioma solicidado                |
| FORMAT    | Opcional       | Formato de salida del metadato del servicio.   (Por defecto text/xml)  |

Ejemplos: 

http://www.ign.es/wms-inspire/ign-base?VERSION=1.3.0&REQUEST=GetCapabilities&SERVICE=WMS

http://geoserveis.icc.cat/icc_bt5m/wms/service?REQUEST=GetCapabilities&SERVICE=WMS

##### Aspectos prácticos

###### Tamaño máximo de la imágen

Si se pide una imagen mayor que el tamaño máximo permitodo retornará un error

``` xml
<Service>
    <Name>icc_bt5m</Name>
    <Title>
    ICC - Base topogràfica de Catalunya 1:5 000 (BT-5M) - Capes WMS 96dpi (píxel 0,26458333 mm)
    </Title>
    ...
    <MaxWidth>2048</MaxWidth>
    <MaxHeight>2048</MaxHeight>
</Service>
```

###### OnlineResource

En algunos software de escritorio utiliza esta url para hacer las peticiones de las operaciones GetMap.

``` xml
<GetMap>
    <Format>image/jp2;subtype="gmljp2"</Format>
    <Format>image/gif</Format>
    <Format>image/png</Format>
    <Format>image/bmp</Format>
    <Format>image/jpeg</Format>
    <Format>image/tiff</Format>
    <DCPType>
        <HTTP>
            <Get>
                <OnlineResource xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="http://shagrat.icc.cat/lizardtech/iserv/ows" xlink:type="simple"/>
            </Get>
        </HTTP>
    </DCPType>
</GetMap>
```

###### Layer

El atributo queryable indica si la capa es consultable (1 =  consultable, 0 = no consultable)

Name es indentificador de la capa. Es el valor que se debe usar en el parámetro LAYERS de las peticiones GetMap

Title es nombre descriptivo de la capa

LegendURL hace referencia a una url de una imagen externa que contiene la leyenda de la capa

Min y Max(ScaleDenominator) factor de escala. Limita la visualización de la capa a estas escalas. Si se pide una capa fuera de esa escala retorna en blanco.

``` xml
<Layer queryable="1">
    <Name>02_ALTI_PA</Name>
    <Title>[BT5M] (02) (x) ALTIMETRIA: talussos, marges (àrees)</Title>
    <Abstract>02_ALTI_PA</Abstract>
    <CRS>EPSG:25831</CRS>
    <CRS>EPSG:4326</CRS>
    <BoundingBox CRS="EPSG:25831" minx="254904.96" miny="4484796.89" maxx="530907.30" maxy="4749795.10"/>
    ...
    <Style>
    ...
    <LegendURL width="328" height="64">
        <Format>image/png</Format>
        <OnlineResource xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="http://geoserveis.icc.cat/icc_bt5m/wms/service?request=GetLegendGraphic%26version=1.3.0%26format=image/png%26layer=02_ALTI_PA" xlink:type="simple"/>
    </LegendURL>
    </Style>
    <MinScaleDenominator>472.470238</MinScaleDenominator>
    <MaxScaleDenominator>7087.053571</MaxScaleDenominator>
</Layer>
```

###### GetFeatureInfo

Formatos de salida de la consulta

``` xml
<GetFeatureInfo>
    <Format>application/vnd.esri.wms_raw_xml</Format>
    <Format>application/vnd.esri.wms_featureinfo_xml</Format>
    <Format>application/vnd.ogc.wms_xml</Format>
    <Format>text/xml</Format>
    <Format>text/html</Format>
    <Format>text/plain</Format>
    <DCPType>
        <HTTP>
            <Get>
                <OnlineResource xmlns:xlink="http://www.w3.org/1999/xlink" xlink:type="simple" xlink:href="http://geoserveis.icc.cat/icc_bt5m/wms/service?"/>
            </Get>
        </HTTP>
    </DCPType>
</GetFeatureInfo>
```

#### GetMap

Petición GetMap devolverá un mapa en formato imagen, ya sea un PNG, JPEG, GIF, etc.

##### Parámetros del GetMap

| Parámetro   | Obligatoriedad | Descripción                                                                                                    |
|-------------|----------------|----------------------------------------------------------------------------------------------------------------|
| VERSION     | Obligatorio    | Versión de la especificación OGC (1.0.0, 1.1.0, 1.1.1, 1.3.0)                                                  |
| SERVICE     | Obligatorio    | Tipo de servicio al que va dirigida la petición (**WMS**)                                                      |
| REQUEST     | Obligatorio    | Nombre de la operación (**GetMap**)                                                                            |
| LAYERS      | Obligatorio    | Lista de nombres de las capas separadas por coma                                                               |
| FORMAT      | Obligatorio    | Formato de salida de la imagen.  (image/png, image/jpeg, ...)                                                  |
| STYLES      | Obligatorio    | Lista de estilos separados por coma. Si no hay estilo se puede dejar en blanco                                 |
| SRS o CRS   | Obligatorio    | Código ESPG del sistema de referencia                                                                          |
| BBOX        | Obligatorio    | Caja de coordenadas del mapa (minx,miny,maxx,maxy)                                                             |
| WIDTH       | Obligatorio    | Número píxeles del ancho de la imágen                                                                          |
| HEIGHT      | Obligatorio    | Número píxeles del alto de la imágen                                                                           |
| TRANSPARENT | Opcional       | Indica si el fondo del mapa debe ser transparente (true ,false)                                                |
| BGCOLOR     | Opcional       | Color de fondo para la imagen del mapa. El valor está en la formato RRGGBB hexadecimal                         |
| SLD         | Opcional       | Una URL que hace referencia a un archivo XML StyledLayerDescriptor que controla el estilo de las capas de mapa |
| EXCEPTIONS  | Opcional       | Formato excepciones                                                                                            |

Ejemplo: http://www.ign.es/wms-inspire/ign-base?SERVICE=WMS&REQUEST=GetMap&VERSION=1.3.0&LAYERS=IGNBaseTodo&STYLES=&FORMAT=image/png&BGCOLOR=0xFFFFFF&TRANSPARENT=TRUE&SRS=EPSG:4258&BBOX=26.4764705882353,-19,44.5235294117647,5&WIDTH=1020&HEIGHT=767

#### GetFeatureInfo

Petición GetFeatureInfo sirve para mostrar los atributos de los objetos del mapa, vuelve la información en formato de tabla o XML. Si una capa está marcada como “consultable” (queryable), se puede solicitar datos sobre una coordenada de la imagen del mapa.

##### Parámetros del GetFeatureInfo

| Parámetro     | Obligatoriedad | Descripción                                                                    |
|---------------|----------------|--------------------------------------------------------------------------------|
| VERSION       | Obligatorio    | Versión de la especificación OGC (1.0.0, 1.1.0, 1.1.1, 1.3.0)                  |
| SERVICE       | Obligatorio    | Tipo de servicio al que va dirigida la petición (**WMS**)                      |
| REQUEST       | Obligatorio    | Nombre de la operación (**GetFeatureInfo**)                                    |
| LAYERS        | Obligatorio    | Lista de nombres de las capas separadas por coma                               |
| FORMAT        | Obligatorio    | Formato de salida de la imagen.  (image/png, image/jpeg, ...)                  |
| STYLES        | Obligatorio    | Lista de estilos separados por coma. Si no hay estilo se puede dejar en blanco |
| SRS o CRS     | Obligatorio    | Código ESPG del sistema de referencia                                          |
| BBOX          | Obligatorio    | Caja de coordenadas del mapa (minx,miny,maxx,maxy)                             |
| WIDTH         | Obligatorio    | Número píxeles del ancho de la imágen                                          |
| HEIGHT        | Obligatorio    | Número píxeles del alto de la imágen                                           |
| QUERY_LAYERS  | Obligatorio    | Lista de nombres de las capas que se quieren consultar separadas por coma      |
| X o I            | Obligatorio    | Valor del píxel a consultar                                                    |
| Y o J           | Obligatorio    | Valor del píxel a consultar                                                    |
| INFO_FORMAT   | Opcional       | Formato de la respuesta (por defecto text/xml)                                 |
| FEATURE_COUNT | Opcional       | Número máximo de elementos a devolver                                          |
| EXCEPTIONS    | Opcional       | Formato excepciones                                                            |

Ejemplo:

http://geoserveis.icc.cat/icgc_bm5m/wms/service?REQUEST=GetFeatureInfo&SERVICE=WMS&VERSION=1.1.1&LAYERS=10_MUNICIPI_PC&QUERY_LAYERS=10_MUNICIPI_PC&INFO_FORMAT=text/html&STYLES=&SRS=EPSG:25831&BBOX=257904,4484796,680304,4907196&WIDTH=768&HEIGHT=768&X=295&Y=580

#### GetLegendGraphic

Petición que devuelve una imagen de la imagen de la leyenda del mapa de una capa, proporcionando una guía visual de los elementos del mapa.

| Parámetro | Obligatoriedad | Descripción                                                    |
|-----------|----------------|----------------------------------------------------------------|
| VERSION   | Obligatorio    | Versión de la especificación OGC (1.0.0, 1.1.0, 1.1.1, 1.3.0)  |
| SERVICE   | Obligatorio    | Tipo de servicio al que va dirigida la petición (**WMS**)      |
| REQUEST   | Obligatorio    | Nombre de la operación (**GetLegendGraphic**)                  |
| LAYER     | Obligatorio    | Nombre de la capa                                              |
| FORMAT    | Obligatorio    | Formato de salida de la imagen.  (image/png, image/jpeg, ...)  |
| WIDTH     | Opcional       | Número píxeles del ancho de la imágen                          |
| HEIGHT    | Opcional       | Número píxeles del alto de la imágen                           |

Ejemplo:

http://wms.guifi.net/cgi-bin/mapserv?map=/home/guifi/maps.guifi.net/guifimaps/GMap.map&version=1.3.0&service=WMS&request=GetLegendGraphic&sld_version=1.1.0&layer=Nodes&format=image/png&STYLE=default

#### Aspector prácticos WMS

##### Principales diferencias entre las versiones 1.1.1 y 1.3.0 
* En la operación GetMap, el parámetro SRS se llama CRS en 1.3.0
* En la operación GetFeatureInfo, los parámetros X e Y se llaman I y J en 1.3.0.
* En 1.1.1, los sistemas de coordenadas geográficas especificados con el espacio de nombres EPSG se definen para tener un orden de ejes de longitud / latitud. En 1.3.0 el orden es la latitud / longitud.

Por ejemplo, considere la solicitud WMS 1.1 utilizando el SRS WGS84 (EPSG: 4326):
    
    server/wms?VERSION=1.1.1&REQUEST=GetMap&SRS=epsg:4326&BBOX=-180,-90,180,90&...
La solicitud equivalente WMS 1.3.0 es:
    
    server/wms?VERSION=1.3.0&REQUEST=GetMap&CRS=epsg:4326&BBOX=-90,-180,90,180&...

##### Problemas comunes
* Tamaño de la imagen (pantallas grandes y/o de mucha resolución)
* Capas no visibles por el control de escala
* Capas no consultables
* Formato de salida del GetFeatureInfo
* No están pensados para peticiones teseladas (velocidad) 
* No tienen caché. Las imágenes se generan al vuelo 
* Lista restringida de SRS soportados
* En software de escritorio el onlineResource (QGis tiene la opción de ignorar el onlineResource )
* Modificar el estilo (SLD poco soportado)
* SLD difícil de entender y hacer  

## WMTS

## WFS

## SLD

## SOS

## GML

## CSW

## Otros estándares OGC
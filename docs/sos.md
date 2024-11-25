## SOS

El estándar SOS (Sensor Observation Service) es un servicio de datos. Define un interface estandarizado y operaciones para el acceso a observaciones desde sensores y sistemas de sensores que es consistente con todos los sistemas, incluyendo remoto, in-situ, fijos y sensores móviles. SOS proporciona resultados de consultas en el formato estándar de observación y medida (en inglés Observation and Mesurements, O&M) para modelizar observaciones de sensores y la especificación SensorML para modelizar sensores y sistemas sensor.

Una observación es un evento cuyo resultado es una estimación del valor de alguna propiedad de la característica de interés, obtenida usando un procedimiento específico. 

Las observaciones se definen por

* eventTime – Cuando se tomó la medida
* featureOfInterest – La entidad que se mide
* observedProperty - La característica que se midió
* procedure - cómo se midió

Operaciones SOS requeridas incluyen: 
* GetObservation - acceso a datos de observación y medida del sensor a través de una consulta espacio-temporal que se puede filtrar por un fenómeno 
* GetCapabilities - Metadatos del servicio SOS 
* DescribeSensor - información sobre los sensores, sus procesos y plataformas en SensorML

Operaciones opcionales incluyen: 
* GetResult 
* GetFeatureOfInterest 
* GetFeatureOfInterestTime 
* DescribeFeatureofInterest 
* DescribeObservationType
* DescribeResultModel
* Register Sensor
* InsertObservation

Algunos conceptos de interés para trabajar con sensores [^1]

### Offering

Los datos servidos por un servicio SOS se agrupan en diferentes offerings. Por ejemplo, un servicio SOS “meteo” podría tener los siguientes offerings: imágenes de satélite, datos de radar, medidas de estaciones meteorológicas, mapas de predicción, etc. Cada offering expone datos de un sensor o una red de sensores, descritos como un procedure.

Se pueden considerarlos distintos Offerings como secciones co cajones que clasifican los diferentes datos según su origen o naturaleza.

### Procedure

Una procedure describe un sensor, una colección de sensores, or un proceso que produce un conjunto de observaciones. Proporciona metadatos sobre las entradas y salidas del sensor, datos de calibración y procesado, información de contacto, y la disponibilidad de datos (extensiones espacial y temporal), etc.

Normalmente viene descrito en el formato SensorML.

Se puede considerar una Procedure como una ficha de metadatos acerca del (los) sensor(es) o proceso(s) a cargo de generar los datos que ofrece el servicio.

Un Offering está relacionado con una sola Procedure, mientras que una Procedure puede ser usada en diferentes Offerings. Por ejemplo, una Procedure podría ser una “Red de Estaciones Meteorológicas”, y ésta misma red de estaciones ser usada en diferentes Offerings, por ejemplo para diferentes períodos de tiempo. El Offering sería “Medidas de la Red de Estaciones Meteorológicas para el año 2015”.

### Feature of Interest

Cada observación en un servicio SOS está ligada a una Feature Of Interest (FoI), que habitualmente determina el lugar donde el fenómeno observado tuvo lugar. Por ejemplo, para imágenes satélite, la FoI podría ser su footprint (polígono que determina el área fotografiada sobre la superficie de la tierra), o para una medición de temperatura, la FoI podría ser la ubicación del termómetro (punto).

Las FoI pueden considerarse como el conjunto de lugares a los que están referidos los datos.

### Observed Property

La propiedad que se mide, tal que: Temperatura, Dirección del viento, Nubosidad, Número de vehículos... puede ser un valor numérico (una cantidad y una unidad de medida), lógico (toma los valores verdadero o falso), categórico (un valor de entre una lista: soleado, nublado, lluvioso), o descriptivo (un texto).

### Observation

Finalmente, una Observation es el valor que toma una Observed Property en un momento (Phenomenon Time) y un lugar (Feature Of Interest) dados. Por ejemplo: “La temperatura en Barcelona el 22/09/2015 a las 11:52 es de 23 grados centígrados”.

Se puede ver la especificación en [https://www.ogc.org/standards/sos](https://www.ogc.org/standards/sos)

## Referencias

[^1]: https://sensor-widgets.readthedocs.io/es/latest/sos.html#
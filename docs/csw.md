## CSW

La especificación (CSW Catalog Service for the Web) establece cómo deben estructurarse e implementarse los servicios de catalogación y de búsqueda de metadatos geospaciales, estableciendo el subconjunto mínimo de metadatos que deben ser interrogables.

#### Tipos de peticiones CSW

Las operaciones que se definen en este estándar OGC son 7, siendo 4 obligatorias y 3 opcionales.

| Operación       | Obligatoriedad | Descripción                                                                                                                                                                                                                                          |
|-----------------|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GetCapabilities | Obligatorio    | Solicitud de las características del CSW. Devuelve el documento Capabilities, en XML                                                                                                                                                                 |
| DescribeRecord  | Opcional       | Permite realizar búsquedas de elementos del modelo de datos implementado en el servicio de catálogo. Con esta operación se pueden obtener las descripciones de todos los elementos del modelo datos o sólo de algunos                                |
| GetDomain       | Opcional       | Permite a los usuarios consultar los valores permitidos de un parámetro o propiedad determinados. Se utiliza para obtener información acerca del rango de valores que puede poseer un elemento del registro de metadatos o un parámetro de consulta. |
| GetRecords      | Obligatorio    | Envía una consulta(query) al catálogo y devuelve todos los registros de metadatos de los recursos catalogados que satisfacen los requisitos de la consulta                                                                                           |
| GetRecordById   | Obligatorio    | Obtiene los registros de metadatos de los recursos catalogados mediante los identificadores de dichos registros de metadatos                                                                                                                         |
| Harvest         | Opcional       | Esta operación indica la URI que apunta al recurso de metadatos a insertar o actualizar en el catálogo. El servicio de catálogo se encarga de analizarlo y de crear o modificar registros de metadatos en el catálogo                                |
| Transaction     | Opcional       | Define una interfaz para crear, actualizar y borrar registros del catálogo de metadatos                                                                                                                                                              |

Se puede ver la especificación en [https://www.ogc.org/standards/cat](https://www.ogc.org/standards/cat)

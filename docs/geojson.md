# GeoJSON

GeoJSON es un formato de intercambio de datos espaciales basado en JSON (JavaScript Object Notation). Ha sido adoptado ampliamente en el ámbito de los Sistemas de Información Geográfica debido a su simplicidad, compatibilidad con aplicaciones web y facilidad de lectura tanto por personas como por máquinas.

Especificacion: https://datatracker.ietf.org/doc/html/rfc7946 o https://geojson.org/

El estándar GeoJSON permite representar:

* **Objetos geométricos**: puntos, líneas, polígonos, y sus variantes múltiples.

* Entidades geográficas (**Features**) con atributos asociados.

* Colecciones de entidades (**FeatureCollection**).

GeoJSON trabaja exclusivamente en coordenadas **WGS84 (EPSG:4326)**, usando el orden **[longitud, latitud]**, lo cual es especialmente relevante para evitar errores comunes.

## Estructura Básica de GeoJSON

Todo documento GeoJSON tiene uno de varios tipos principales. El más sencillo es un objeto geométrico.

### Point

``` json
{
  "type": "Point",
  "coordinates": [-0.127758, 51.507351]
}
```

Interpretación:

* type: identifica el tipo de geometría.

* coordinates: un array(matriz) con [longitud, latitud].

#### MultiPoint

``` json
{
  "type": "MultiPoint",
  "coordinates": [
    [-3.70379, 40.41678],
    [2.35222, 48.85661]
  ]
}
```

### LineString

Representación de una ruta simple:

```json
{
  "type": "LineString",
  "coordinates": [
    [-3.70379, 40.41678],
    [-0.127758, 51.507351],
    [2.35222, 48.85661]
  ]
}
```

* coordinates: un array de puntos.

### Polygon

Representa un área. El primer anillo es el contorno exterior; los siguientes, posibles agujeros internos.

```json
{
  "type": "Polygon",
  "coordinates": [
    [
      [0, 0],
      [3, 0],
      [3, 3],
      [0, 3],
      [0, 0]
    ]
  ]
}
```

* coordinates: un array de lineas. Las lineas deben ser cerradas

Ejemplo con un agujero interior:

```json
{
  "type": "Polygon",
  "coordinates": [
    [
      [0, 0], [6, 0], [6, 6], [0, 6], [0, 0]
    ],
    [
      [2, 2], [4, 2], [4, 4], [2, 4], [2, 2]
    ]
  ]
}
```

## Entidades (Features) y Colecciones (FeatureCollection)

Los datos no se componen únicamente de geometrías. Necesitamos atributos asociados a cada objeto espacial. Para ello se emplea el tipo **Feature**.

### Feature con propiedades

```json
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [-74.006, 40.7128]
  },
  "properties": {
    "nombre": "Nueva York",
    "poblacion": 8804190,
    "pais": "Estados Unidos"
  }
}
```

Componentes:

* geometry: el objeto geométrico.

* properties: un diccionario con atributos descriptivos.

### FeatureCollection

Las bases de datos geográficas suelen agrupar múltiples entidades.

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [-3.70379, 40.41678] },
      "properties": { "nombre": "Madrid" }
    },
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [2.35222, 48.85661] },
      "properties": { "nombre": "París" }
    }
  ]
}
```

## Consideraciones de Coordinadas y Sistemas de Referencia

Según la especificación oficial, GeoJSON debe emplear WGS84 (EPSG:4326) con coordenadas en el orden:

```
[longitud, latitud]  →  [x, y]
```

Errores comunes:

* Invertir latitud y longitud.

* Asumir que GeoJSON puede incluir otros CRS; en la práctica, se considera deprecado.

!!! tip
    Cuando se importen datos de otras fuentes, es esencial verificar el sistema de referencia y reproyectar si es necesario antes de exportar a GeoJSON.
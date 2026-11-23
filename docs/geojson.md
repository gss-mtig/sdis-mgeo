# GeoJSON: leer y usar datos geográficos en la Web

**GeoJSON** es un formato para representar datos geográficos usando la sintaxis de JSON (JavaScript Object Notation). Es habitual en mapas web, portales de datos abiertos y API geográficas porque puede transportar geometrías junto con información descriptiva.

GeoJSON es un **formato**, no un servicio. Un archivo, una respuesta de una API o una descarga pueden estar en GeoJSON. Para saber si una respuesta JSON contiene información geográfica, comprueba si incluye tipos como `Feature`, `FeatureCollection` o una geometría.

## La estructura básica

Este ejemplo sintético representa una parada de transporte. No son datos reales:

```json
{
  "type": "Feature",
  "id": "parada-001",
  "geometry": {
    "type": "Point",
    "coordinates": [2.1734, 41.3851]
  },
  "properties": {
    "nombre": "Parada de ejemplo",
    "linea": "L1",
    "accesible": true,
    "validacion": null
  }
}
```

Una `Feature` tiene tres componentes principales:

- **`type`** identifica el tipo de objeto. En este caso, `Feature`.
- **`geometry`** contiene la geometría: su tipo y sus coordenadas. Puede ser `null` si el recurso no tiene una geometría conocida.
- **`properties`** contiene los atributos que describen la entidad. Aquí son texto, un valor lógico y un valor nulo. También pueden aparecer números y otros valores JSON.

El identificador `id` es opcional. Los nombres de tipos y propiedades distinguen mayúsculas de minúsculas: `Feature` y `feature` no son lo mismo.

## Una colección de entidades

Para representar varias entidades se usa `FeatureCollection`. Sus elementos aparecen dentro del array `features`:

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [2.1734, 41.3851]
      },
      "properties": {
        "nombre": "Parada A",
        "linea": "L1"
      }
    },
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [2.181, 41.389]
      },
      "properties": {
        "nombre": "Parada B",
        "linea": "L2"
      }
    }
  ]
}
```

## Tipos de geometría y coordenadas

GeoJSON define siete tipos de geometría. La forma de `coordinates` indica cuántas posiciones y agrupaciones hay:

| Geometría            | Qué representa                                                | Forma orientativa de las coordenadas |
| -------------------- | ------------------------------------------------------------- | ------------------------------------ |
| `Point`              | Una posición                                                  | `[x, y]`                             |
| `MultiPoint`         | Varias posiciones                                             | `[[x, y], [x, y]]`                   |
| `LineString`         | Una línea formada por posiciones ordenadas                    | `[[x, y], [x, y], ...]`              |
| `MultiLineString`    | Varias líneas                                                 | `[[[x, y], ...], [[x, y], ...]]`     |
| `Polygon`            | Un área: anillo exterior y, opcionalmente, anillos interiores | `[[[x, y], ...]]`                    |
| `MultiPolygon`       | Varias áreas                                                  | `[[[[x, y], ...]], ...]`             |
| `GeometryCollection` | Una colección de geometrías                                   | Usa `geometries`, no `coordinates`   |

En un `Polygon`, el primer anillo describe el contorno exterior; los siguientes pueden representar agujeros. Cada anillo debe estar cerrado: su primera y última posición coinciden. La [RFC 7946](https://www.rfc-editor.org/rfc/rfc7946) especifica la estructura completa y las reglas de cada geometría.

## Coordenadas y sistema de referencia

La RFC 7946 establece coordenadas geográficas WGS 84 en grados decimales y el orden **longitud, latitud**:

```text
[longitud, latitud] = [x, y]
```

Por ejemplo, `[2.1734, 41.3851]` representa aproximadamente Barcelona. La latitud no va primero. GeoJSON conforme a RFC 7946 no incluye un miembro `crs` para declarar otro sistema; si los datos de origen están en un sistema proyectado, reproyéctalos a WGS 84 antes de exportarlos. La RFC admite una tercera coordenada opcional para la altura en metros. ([RFC 7946, coordenadas](https://www.rfc-editor.org/rfc/rfc7946))

## Cómo abrirlo y comprobarlo

- **En un navegador o editor de texto:** puedes leer la estructura y comprobar sus valores.
- **En QGIS:** puedes abrir un archivo `.geojson` como capa vectorial, ver su geometría y consultar su tabla de atributos.
- **En una API web:** una respuesta GeoJSON puede visualizarse en un mapa web o procesarse desde una aplicación.

Antes de usarlo, revisa que el JSON esté bien formado, que `type` tenga el valor esperado, que las coordenadas estén en el orden correcto y que los atributos tengan sentido. Para polígonos, comprueba además que los anillos estén cerrados.

## Actividades prácticas en clase

Son actividades breves para hacer en parejas. Se pueden realizar con los ejemplos de esta página, el [GeoJSON didáctico local](ejemplos/ogcapi_features/feature-ejemplo.geojson), papel y lápiz, navegador o QGIS; no requieren programar.

### 1. ¿JSON o GeoJSON? — 5 minutos

**Objetivo:** distinguir un objeto JSON corriente de una estructura GeoJSON.

**Pasos:**

1. Comparad `{"nombre": "Parada A", "linea": "L1"}` con el ejemplo de `Feature` de esta página.
2. Localizad las claves que indican que el segundo objeto incluye información espacial.
3. Decidid si el primer objeto es GeoJSON por sí solo.

**Resultado:** nombrad las claves que permiten reconocer una `Feature`.

### 2. ¿Dónde cae el punto? — 5 minutos

**Objetivo:** interpretar correctamente el orden de coordenadas.

**Pasos:**

1. Buscad `[2.1734, 41.3851]` en un mapa o interpretadla con un mapa de coordenadas.
2. Intercambiad los valores y buscad `[41.3851, 2.1734]`.
3. Explicad por qué el segundo punto aparece en un lugar distinto.

**Resultado:** indicad qué par sitúa el punto en Barcelona y cuál es el orden correcto.

### 3. Adivina la geometría por sus arrays — 8 minutos

**Objetivo:** relacionar la estructura de coordenadas con el tipo de geometría.

**Pasos:**

1. Abrid el archivo [geometrias-para-clasificar.geojson](ejemplos/geojson/geometrias-para-clasificar.geojson) en un editor de texto. Los valores de `geometry.type` están vacíos a propósito.
2. Deducid el tipo de cada geometría observando la estructura de `coordinates` y escribidlo en el campo `geometry.type` correspondiente.
3. Comparad los casos `MultiPoint` y `LineString`: tienen arrays parecidos, pero representan cosas distintas. Explicad qué diferencia hay entre ellos.

**Resultado:** el archivo completado con los tipos de geometría correctos y una explicación de la diferencia entre `MultiPoint` y `LineString`. El archivo original no es GeoJSON completo hasta rellenar esos campos.

### 4. Lee una entidad — 8 minutos

**Objetivo:** interpretar la geometría, el identificador y los atributos de una `Feature`.

**Pasos:**

1. Abrid el archivo [inventario-de-servicios.geojson](ejemplos/geojson/inventario-de-servicios.geojson) en un editor de texto o cargadlo en QGIS.
2. Señalad `type`, `id` (si existe), `geometry` y `properties`.
3. Elegid una entidad, anotad dos propiedades e indicad qué tipo de valor contiene cada una.
4. Explicad qué entidad representa la geometría y en qué lugar aproximado se encuentra.

**Resultado:** una descripción de una entidad en una frase, incluyendo una propiedad y su geometría.

### 5. Encuentra y corrige los errores — 10 minutos

**Objetivo:** detectar errores frecuentes de coordenadas y geometría.

**Pasos:**

1. Abrid [geojson-con-errores.geojson](ejemplos/geojson/geojson-con-errores.geojson) en un editor de texto.
2. Corregid la posición del punto para que corresponda a Barcelona y cerrad el anillo del polígono repitiendo su primera posición al final.
3. Guardad una copia corregida y explicad cómo comprobaríais ambos cambios en un mapa o en QGIS.

**Resultado:** dos correcciones y una comprobación visual.

### 6. ¿Cuándo elegir GeoJSON? — 5 minutos

**Objetivo:** reconocer para qué tareas resulta útil el formato.

**Pasos:** elegid si GeoJSON sería una opción adecuada para cada caso y explicad la decisión:

- compartir unas pocas paradas de autobús para mostrarlas en un mapa web;
- distribuir un ráster de elevación muy grande;
- enviar una imagen de mapa ya dibujada para verla como fondo.

**Resultado:** una decisión para cada caso.

## Para recordar

- JSON es la sintaxis; GeoJSON añade tipos y estructura para datos geográficos.
- `Feature` combina geometría y propiedades; `FeatureCollection` agrupa entidades.
- Las coordenadas de RFC 7946 van en orden longitud-latitud y usan WGS 84.
- GeoJSON es útil para intercambio y mapas web, pero no reemplaza todos los formatos geoespaciales.

## Fuentes

- [RFC 7946: The GeoJSON Format](https://www.rfc-editor.org/rfc/rfc7946).
- [Sitio oficial del formato GeoJSON](https://geojson.org/).

## Soluciones orientativas

Consulta esta sección después de intentar las actividades.

1. **¿JSON o GeoJSON?** Una `Feature` tiene `type`, `geometry` y `properties`. El objeto con solo nombre y línea es JSON válido, pero no expresa una geometría GeoJSON.
2. **¿Dónde cae el punto?** `[2.1734, 41.3851]` sitúa el punto aproximadamente en Barcelona: primero longitud y luego latitud. Al invertirlas, el punto queda muy lejos.
3. **Adivina la geometría por sus arrays.** `[x, y]` es una posición de `Point`. `[[x, y], [x, y]]` puede describir un `MultiPoint` o un `LineString`; el miembro `type` distingue puntos separados de posiciones ordenadas que forman una línea. La estructura con un nivel adicional agrupa posiciones en anillos de un `Polygon`.
4. **Lee una entidad.** `geometry` indica dónde está y qué forma tiene; `properties` describe la entidad. El archivo local es sintético y lo indica en sus propiedades.
5. **Encuentra y corrige los errores.** En el archivo, el punto que se pretende situar en Barcelona tiene las coordenadas invertidas: deben quedar como `[2.1734, 41.3851]`. El anillo debe terminar repitiendo exactamente su primera posición.
6. **¿Cuándo elegir GeoJSON?** Es apropiado para intercambiar entidades vectoriales en la Web. No representa directamente un ráster, y una imagen de mapa no conserva las geometrías ni los atributos de las entidades.

**Siguiente:** [Clientes de mapas](clientes_de_mapa.md).

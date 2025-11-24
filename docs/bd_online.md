# Publicar datos en una base de datos online

Para esto uilizaremos el servicio de [Supabase](https://supabase.com/)

## Descargar datos de accidentes de Barcelona (2024)

Usaremos los datos abiertos del Ajuntament de Barcelona:

Ir al portal de datos abiertos: https://opendata-ajuntament.barcelona.cat

Buscar: `Vehicles implicats en accidents `

Descargar el dataset en formato CSV.
Alternativamente, puedes usar este enlace directo (si ya está publicado para 2024):

https://opendata-ajuntament.barcelona.cat/data/ca/dataset/accidents-vehicles-gu-bcn

## Crear un nuevo proyecto en Supabase

1. Ve a https://supabase.com/ y crea una cuenta.

1. En tu dashboard, haz clic en **"New Project"**.

1. Configura:

  * Nombre del proyecto (ej. accidents-bcn)

  * Password

  * Región

  * Base de datos: PostgreSQL (por defecto)

1. Espera unos segundos mientras se provisiona.

## Activar PostGIS en Supabase

1. Abre la pestaña de **Database**

1. Seleccionar **extensions**

1. Buscar *postgis*

1. Activar PostGIS para el esquema **public**

1. Abre la pestaña **SQL Editor** desde el menú lateral izquierdo.

1. Ejecuta esta sentencia para activar PostGIS:

    ```
    create extension if not exists postgis;
    ```

1. Espera la confirmación

## Subir CSV a Supabase

1. Crear una nueva tabla con el nombre `accidents_bcn`

1. Seleccionar **Import Data from CSV**

1. Sube el archivo CSV y mapea las columnas correctamente.

### Crear la calve primaria

1. Abre la pestaña **SQL Editor** desde el menú lateral izquierdo.

```sql
alter table accidents_bcn
add column id serial primary key;
```

### Crear la geometría POINT usando lat/lon

```sql
alter table accidents_bcn
add column geom geometry(Point, 4326);

update accidents_bcn
set geom = ST_SetSRID(ST_MakePoint("Longitud_WGS84", "Latitud_WGS84"), 4326)
where "Latitud_WGS84" is not null and "Longitud_WGS84" is not null;
```

## Crear endpoint GeoJSON desde Supabase

1. Crear una función que devuelva un `FeatureCollection`. Desde el **SQL Editor**, ejecuta:

```sql
create or replace function public.get_accidents_geojson()
returns json
language sql
as $$
select json_build_object(
  'type', 'FeatureCollection',
  'features', json_agg(
    json_build_object(
      'type', 'Feature',
      'geometry', ST_AsGeoJSON(geom)::json,
      'properties', json_build_object(
        'id', id,
        'data', to_char(make_date("NK_Any"::integer, "Mes_any"::integer, "Dia_mes"::integer), 'YYYY-MM-DD'),
        'hora', "Hora_dia",
        'tipus_vehicle', "Descripcio_tipus_vehicle"
      )
    )
  )
)
from accidents_bcn
where geom is not null;
$$;
```

## Hacer el endpoint público

### Dar permisos públicos

En la pestaña **Auth → Policies**, selecciona la tabla `accidents_bcn` y crea una nueva policy:

* Select: Enabled

* Policy: `Allow read access to everyone`

* Condición: `true`

### Activar acceso a la función

Supabase expone funciones (RPC) como endpoints REST automáticamente.

Para que sea accesible públicamente:

1. Ve a la sección **SQL Editor → Run SQL** y ejecuta:

```sql
grant execute on function get_accidents_geojson() to anon;
```

## Probar el endpoint GeoJSON

1. Ve a la sección **Project overview → Project API**

```
https://<TU-PROYECTO>.supabase.co/rest/v1/rpc/get_accidents_geojson
```

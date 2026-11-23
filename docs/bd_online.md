# Publicar datos desde una base de datos con Supabase

En la práctica anterior publicamos un archivo GeoJSON estático. En esta lección guardaremos registros en una base de datos PostgreSQL y ofreceremos una **API de solo lectura** para que otra aplicación consulte esos datos.

Supabase ofrece PostgreSQL como servicio, una interfaz web para gestionar tablas y una Data API que expone tablas y funciones seleccionadas. Usaremos PostGIS para guardar puntos y una función que devuelve el conjunto como GeoJSON.

!!! note "Configuración revisada"
    Procedimiento revisado en noviembre de 2026. La interfaz del panel puede cambiar; consulta la documentación oficial enlazada si los nombres de los menús difieren.

!!! warning "Entorno gratuito y acceso público"
    La cuenta gratuita de Supabase permite hasta dos proyectos activos por cuenta y pausa automáticamente proyectos con poca actividad durante siete días. Para una clase con muchos alumnos, conviene preparar un proyecto común de demostración y repartir el acceso de lectura, o comprobar previamente las condiciones de las cuentas del alumnado. No dependas de que un proyecto gratuito permanezca activo durante todo el curso. [Detalles del plan gratuito](https://supabase.com/docs/guides/platform/free-project-pausing)

    En esta práctica publicaremos datos sintéticos. No subas datos personales, sensibles o cuya licencia no permita su redistribución. Solo habilitaremos lectura pública; no uses una clave secreta ni `service_role` en una página web.

## 1. Preparar los datos

Descarga el [CSV sintético de ejemplo](ejemplos/supabase/puntos_demo.csv). Contiene cuatro puntos inventados para la práctica, con un `id` numérico único para usar como clave primaria, nombre, tema y coordenadas en grados decimales.

Si quieres hacer una ampliación con datos reales, puedes explorar el conjunto de [vehículos implicados en accidentes de la Guardia Urbana de Barcelona](https://opendata-ajuntament.barcelona.cat/data/ca/dataset/accidents-vehicles-gu-bcn). Revisa antes la licencia, el año disponible y los nombres de los campos; el archivo puede cambiar con el tiempo. La práctica principal no depende de que ese recurso externo esté disponible.

## 2. Crear un proyecto y activar PostGIS

1. Inicia sesión en [Supabase](https://supabase.com/) y crea un proyecto de prueba.
2. Abre **Database → Extensions**, busca `postgis` y actívala.
3. En el diálogo de confirmación, deja el esquema recomendado `extensions`.

PostGIS añade tipos espaciales, como `geometry`, y funciones para trabajar con coordenadas. Supabase recomienda instalar la extensión en `extensions`, no en `public`. [Guía actual de PostGIS](https://supabase.com/docs/guides/database/extensions/postgis)

## 3. Importar el CSV

1. En **Table Editor**, pulsa **New table** y elige importar datos desde un CSV. También puedes abrir **Insert** dentro de una tabla vacía y seleccionar **Import Data from CSV**.
2. Sube `puntos_demo.csv` y crea una tabla llamada `puntos_demo` en el esquema `public`.
3. Comprueba que `id` es numérico (`int8`/`bigint`) y está marcado como clave primaria; `nombre` y `tema` son texto, y `longitud` y `latitud` son numéricos (`double precision` o `numeric`).
4. Termina la importación y confirma que aparecen cuatro filas con identificadores únicos.

La importación desde el panel está pensada para conjuntos pequeños; Supabase documenta un límite de 100 MB para esta vía. [Importar datos](https://supabase.com/docs/guides/database/import-data)

## 4. Crear la geometría espacial

En **SQL Editor**, ejecuta:

```sql
alter table public.puntos_demo
add column geom extensions.geometry(Point, 4326);

update public.puntos_demo
set geom = extensions.st_setsrid(
  extensions.st_makepoint(longitud, latitud),
  4326
)
where longitud is not null and latitud is not null;
```

`ST_MakePoint` recibe primero la longitud y después la latitud, igual que las coordenadas de GeoJSON: `[longitud, latitud]`. El identificador `4326` representa WGS 84.

## 5. Preparar una respuesta GeoJSON

Una columna `geometry` de PostGIS se almacena en un formato propio de la base de datos. La función siguiente transforma los puntos a objetos GeoJSON y los reúne en un `FeatureCollection`:

En el **SQL Editor** de Supabase, abre una consulta nueva, pega el bloque SQL siguiente y pulsa **Run**. Esto crea la función en la base de datos; no se crea en el editor de tablas ni en el archivo HTML.

```sql
create or replace function public.puntos_demo_geojson()
returns jsonb
language sql
stable
set search_path = ''
as $$
  select jsonb_build_object(
    'type', 'FeatureCollection',
    'features', coalesce(
      jsonb_agg(
        jsonb_build_object(
          'type', 'Feature',
          'geometry', extensions.st_asgeojson(p.geom)::jsonb,
          'properties', jsonb_build_object(
            'nombre', p.nombre,
            'tema', p.tema
          )
        )
      ),
      '[]'::jsonb
    )
  )
  from public.puntos_demo as p
  where p.geom is not null;
$$;
```

La función solo lee la tabla y devuelve geometrías y propiedades. Al publicar una API, es importante decidir qué columnas se exponen; no hay que devolver automáticamente todos los campos de una tabla.

La función ya se declara como `STABLE` en el bloque anterior. Esta propiedad permite que PostgREST la invoque mediante una petición `GET`. Si la función se creó anteriormente sin esa propiedad, en el **SQL Editor** ejecuta:

```sql
ALTER FUNCTION public.puntos_demo_geojson() STABLE;
```

## 6. Permitir lectura pública, sin permitir cambios

Para que cualquier persona pueda leer estos puntos, la base de datos necesita tres controles coordinados: exponer el recurso en la Data API, conceder permiso de lectura y crear una política RLS. Ejecuta este SQL:

```sql
alter table public.puntos_demo enable row level security;

drop policy if exists "Lectura pública de puntos de ejemplo"
on public.puntos_demo;

create policy "Lectura pública de puntos de ejemplo"
on public.puntos_demo
for select
to anon
using (true);

grant select on table public.puntos_demo to anon;

revoke all on function public.puntos_demo_geojson() from public;
revoke all on function public.puntos_demo_geojson() from anon;
revoke all on function public.puntos_demo_geojson() from authenticated;
grant execute on function public.puntos_demo_geojson() to anon;
```

La política permite leer las filas a la función que llama el rol `anon`; no permite insertar, actualizar ni borrar registros. El `grant` habilita la lectura de la tabla para ese rol, y los permisos de ejecución habilitan la función solo para lectura pública.

Por último, activa la exposición explícita desde el panel:

1. Abre **Integrations → Data API → Settings**.
2. Comprueba que `public` figura entre los esquemas expuestos.
3. Activa la exposición de la tabla `puntos_demo` y de la función `puntos_demo_geojson`.

En las configuraciones actuales, una tabla nueva no queda necesariamente disponible en la API por defecto. La exposición, los permisos `GRANT` y las políticas RLS son controles diferentes; hacen falta los tres. [Seguridad de la Data API](https://supabase.com/docs/guides/api/securing-your-api) · [Cambio de valores predeterminados de 2026](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically)

## 7. Consultar la API

La dirección del endpoint tiene esta forma:

```text
https://PROJECT_REF.supabase.co/rest/v1/rpc/puntos_demo_geojson
```

Sustituye `PROJECT_REF` por la referencia del proyecto, visible en su URL o en **Project Settings**. La petición necesita una clave de API. Normalmente se envía en el encabezado `apikey`; para probar la consulta desde el navegador, puedes añadirla como parámetro de URL:

Como alternativa para probarla directamente en el navegador, Supabase permite enviar la clave publicable como parámetro `apikey` en una petición `GET`. Sustituye ambos valores de ejemplo:

```text
https://PROJECT_REF.supabase.co/rest/v1/rpc/puntos_demo_geojson?apikey=sb_publishable_REEMPLAZA_CON_TU_CLAVE
```

Usa solo una clave publicable (`sb_publishable_…`) en esta URL. No pongas claves secretas en una dirección que pueda quedar en el historial del navegador o en registros del servidor. Para aplicaciones, es preferible enviar la clave mediante el encabezado `apikey`.

Abre el [comprobador de API de esta práctica](ejemplos/supabase/probar_api.html), pega la URL del proyecto y una **publishable key** (`sb_publishable_…`) y pulsa **Consultar**. La página envía una solicitud `POST` a la función, muestra la respuesta y no guarda los valores introducidos. La clave publicable está diseñada para usarse en clientes web; los permisos de la tabla y la política RLS limitan lo que permite hacer. [Tipos de claves de Supabase](https://supabase.com/docs/guides/getting-started/api-keys)

!!! danger "No uses la clave secreta"
    No introduzcas una clave `sb_secret_…`, `service_role` ni una contraseña de base de datos en el comprobador o en código web. Las claves secretas pueden omitir las políticas RLS y deben mantenerse solo en un entorno de servidor.

**Resultado esperado:** la respuesta es un `FeatureCollection` con cuatro objetos `Feature`, cada uno con su `geometry` y sus `properties`.

## Práctica guiada

**Objetivo:** pasar de un CSV con coordenadas a una tabla espacial consultable mediante una API de solo lectura.

**Materiales:** cuenta y proyecto de Supabase, navegador, [CSV sintético](ejemplos/supabase/puntos_demo.csv) y [comprobador de API](ejemplos/supabase/probar_api.html).

**Pasos:** importa el CSV, crea la geometría, configura la exposición y los permisos, y consulta la función. Comprueba que no se permiten modificaciones desde el endpoint público.

**Resultado esperado:** una URL de API que devuelve GeoJSON y una tabla en Supabase con geometrías PostGIS.

**Reflexión:** ¿qué aporta la base de datos y la API frente a publicar el mismo contenido como archivo estático? ¿Qué habría que cambiar si solo algunas personas pudieran acceder?

## Cómo se relaciona con el catálogo

La API publica y entrega datos; el catálogo describe el recurso y facilita encontrarlo. En una ficha de metadatos, enlaza al endpoint o a la página del recurso y explica qué consulta ofrece. No publiques la contraseña del proyecto ni una clave secreta en los metadatos.

## Referencias

- [PostGIS en Supabase](https://supabase.com/docs/guides/database/extensions/postgis).
- [Importar CSV en Supabase](https://supabase.com/docs/guides/database/import-data).
- [Seguridad de la Data API: exposición, permisos y RLS](https://supabase.com/docs/guides/api/securing-your-api).
- [Claves API publicables y secretas](https://supabase.com/docs/guides/getting-started/api-keys).
- [Supabase: crear una ruta de API](https://supabase.com/docs/guides/api/quickstart), incluye consulta en navegador mediante `apikey` en la URL.
- [Pausas de proyectos gratuitos](https://supabase.com/docs/guides/platform/free-project-pausing).

**Siguiente:** [Qué son las teselas vectoriales](teselas_vectoriales.md).

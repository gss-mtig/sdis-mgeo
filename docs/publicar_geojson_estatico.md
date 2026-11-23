# Publicar un archivo geográfico en GitHub Pages

Una forma sencilla de compartir datos geográficos es publicar un archivo estático: se guarda el archivo en un sitio web y otras personas acceden mediante una URL. Para esta práctica usaremos **GeoJSON**, porque puede contener geometrías y atributos y ya conocemos su estructura.

GitHub Pages publica sitios estáticos desde un repositorio. No ejecuta una base de datos ni permite modificar los datos mediante una API. Esta opción es adecuada para compartir un conjunto pequeño que se actualiza ocasionalmente; si necesitamos consultas dinámicas, edición o grandes volúmenes, conviene otra solución.

## Antes de publicar

Comprueba que:

- el GeoJSON está bien formado y usa coordenadas en orden longitud, latitud, conforme a RFC 7946;
- tienes permiso para redistribuir los datos y puedes indicar su licencia y atribución;
- el archivo no contiene datos personales, sensibles o que no deban hacerse públicos.

En GitHub Free, el repositorio que publica con GitHub Pages debe ser público. Todo lo que publiques en la página se podrá consultar en Internet. Para esta práctica, crea un repositorio separado que contenga solo los archivos del ejercicio. ([Requisitos de GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site))

## Preparar los archivos

Descarga el [GeoJSON sintético de ejemplo](ejemplos/publicacion_estatica/puntos.geojson) y la [página de entrada](ejemplos/publicacion_estatica/index.html). Los puntos y sus atributos son inventados para la práctica.

También puedes abrir la [vista previa del ejemplo](ejemplos/publicacion_estatica/index.html) desde los materiales del curso.

La estructura del repositorio será:

```text
mi-publicacion/
├── index.html
└── puntos.geojson
```

`index.html` contiene un enlace al archivo. El GeoJSON es el recurso de datos; la página sirve como entrada y explica cómo encontrarlo. También puedes sustituir `puntos.geojson` por un conjunto propio, siempre que sea pequeño, válido y publicable.

## Publicar con GitHub Pages

1. Inicia sesión en GitHub y crea un repositorio nuevo llamado, por ejemplo, `mi-publicacion-geografica`.
2. Configura el repositorio como **público**.
3. Sube `index.html` y `puntos.geojson` a la raíz del repositorio. Puedes hacerlo desde la interfaz web con **Add file → Upload files**.
4. Abre **Settings → Pages**.
5. En **Build and deployment**, selecciona **Deploy from a branch**.
6. Elige la rama `main` y la carpeta `/ (root)` como origen y guarda los cambios.
7. Cuando termine la publicación, abre el enlace que aparece en la página de configuración de Pages.

La guía oficial describe este método de publicación desde una rama. ([Configurar el origen de publicación](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site))

## Comprobar y compartir el recurso

La página principal tendrá una dirección parecida a esta:

```text
https://USUARIO.github.io/REPOSITORIO/
```

La URL directa del GeoJSON tendrá esta forma:

```text
https://USUARIO.github.io/REPOSITORIO/puntos.geojson
```

Sustituye `USUARIO` y `REPOSITORIO` por los valores reales. Abre ambas direcciones:

- La primera debe mostrar la página de entrada con un enlace al archivo.
- La segunda debe devolver el contenido GeoJSON. Esa es la dirección que se puede compartir o añadir como recurso en una ficha de metadatos.

Si no aparece todavía, revisa el estado de publicación en **Settings → Pages → Visit site**. La primera publicación puede tardar unos minutos.

## ¿Qué se ha publicado?

En este flujo el repositorio almacena el archivo y Pages lo entrega por HTTP. No hemos instalado un servidor geográfico ni convertido el archivo en una API: la respuesta es el archivo tal cual. Si cambias el GeoJSON y subes una nueva versión, la URL seguirá apuntando al archivo actualizado.

| Necesidad | ¿Es adecuado un archivo estático? |
|---|---|
| Compartir un GeoJSON pequeño y consultarlo en un mapa | Sí |
| Reemplazar manualmente el archivo cuando cambia | Sí |
| Filtrar entidades por un parámetro enviado en la URL | No, eso requiere una API o lógica adicional |
| Editar registros en línea con varias personas | No, conviene una base de datos o una plataforma de edición |
| Publicar un ráster grande o millones de entidades | No, hay que valorar otros formatos y servicios |

GitHub Pages tiene límites de tamaño, tráfico y uso; no está pensado como alojamiento de grandes conjuntos de datos o como servidor de bases de datos. Consulta los [límites actuales de GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits).

## Práctica guiada

**Objetivo:** publicar un conjunto GeoJSON estático y compartir su URL directa.

**Materiales:** cuenta de GitHub, navegador y los dos archivos de ejemplo descargados arriba.

**Pasos:** sigue las instrucciones de publicación, abre el sitio y luego abre la URL directa del GeoJSON. Comprueba que el nombre del archivo aparece en la ruta y que la respuesta contiene `FeatureCollection`.

**Resultado esperado:** una página pública con enlace al GeoJSON y una URL directa que se pueda compartir.

**Reflexión:** si los datos cambian cada día o deben poder filtrarse por municipio, ¿seguirías publicando un único archivo estático? ¿Qué necesitarías añadir?

## Conexión con los metadatos

La publicación de los datos y la publicación de su ficha son tareas diferentes. En un catálogo como GeoNetwork, la ficha describe el conjunto de datos y puede enlazar a la URL directa del GeoJSON. La URL de GitHub Pages no sustituye a la ficha: permite acceder al archivo, mientras que el catálogo ayuda a encontrarlo y entenderlo.

## Referencias

- [GitHub Pages: crear un sitio](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).
- [GitHub Pages: configurar el origen de publicación](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
- [GitHub Pages: límites de uso](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits).
- [RFC 7946: formato GeoJSON](https://www.rfc-editor.org/rfc/rfc7946).

**Siguiente:** [Publicar datos en una base de datos online con Supabase](bd_online.md).

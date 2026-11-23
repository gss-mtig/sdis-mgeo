# Servir un COG por HTTP

Para que un cliente aproveche el acceso parcial de un COG remoto, el servidor debe aceptar peticiones HTTP por rangos de bytes. En esta práctica iniciaremos un servidor estático en el ordenador usando `http-server`, un paquete de Node.js que admite peticiones `Range`.

## Prepara los archivos

Pon `imagen_cog.tif` —creado en la [lección anterior](crear_cog.md)— en una carpeta de trabajo. Abre una terminal en esa carpeta. Necesitas Node.js y npm, los mismos requisitos básicos usados en la práctica de TileServer GL Light.

## Inicia un servidor temporal

Ejecuta el servidor sin instalación global:

```bash
npx --yes http-server@14.1.1 . -a 127.0.0.1 -p 8081 -c-1 --cors
```

La primera vez, `npx` descarga el paquete desde npm. `-a 127.0.0.1` lo limita a tu propio ordenador, `-p 8081` elige el puerto, `-c-1` desactiva la caché y `--cors` permite que otros clientes locales hagan peticiones al servidor desde el navegador.

Deja la terminal abierta. El archivo estará en:

```text
http://127.0.0.1:8081/imagen_cog.tif
```

## Comprueba las peticiones parciales

En una segunda terminal, solicita un tramo pequeño del archivo:

```bash
curl -sS -D - -o /dev/null -H "Range: bytes=0-15" http://127.0.0.1:8081/imagen_cog.tif
```

En Windows, escribe `curl.exe` en lugar de `curl` si PowerShell interpreta `curl` como un alias.

La respuesta debe incluir `206 Partial Content` y un encabezado `Content-Range`. Si devuelve `200 OK` con el archivo completo o no reconoce `Range`, ese servidor no está demostrando el acceso por partes que buscamos.

Cuando acabes, vuelve a la primera terminal y pulsa **Ctrl+C**. Este servidor solo es para la práctica local, no para publicar datos en Internet.

## Publicación en Internet

Para distribuir un COG, se puede alojar el archivo en un servidor web o almacenamiento de objetos público. Antes de enlazarlo, comprueba que el alojamiento:

- sirve el archivo por HTTPS;
- responde a peticiones `Range` con contenido parcial;
- permite las solicitudes entre dominios si un visor web las necesita;
- conserva metadatos, licencia y atribución del dato.

El formato del archivo por sí solo no garantiza estas capacidades del alojamiento.

## Fuente

- [Paquete `http-server` y su soporte de peticiones `Range`](https://github.com/http-party/http-server/releases), consultado el 14 de noviembre de 2026.
- [Estándar HTTP: peticiones por rangos](https://httpwg.org/specs/rfc9110.html).

**Siguiente:** [abrir el COG en QGIS](consumir_cog.md).

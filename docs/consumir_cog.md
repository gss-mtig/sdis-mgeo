# Consumir un COG en QGIS

Abrirás desde QGIS el COG que está sirviendo el servidor HTTP local. Así podrás observar la diferencia entre leer un archivo local y acceder a un ráster alojado en una URL.

## 1. Comprueba que el servidor sigue activo

La terminal que ejecuta `http-server` debe seguir abierta. En el navegador, abre:

```text
http://127.0.0.1:8081/imagen_cog.tif
```

El navegador puede mostrar una descarga o intentar abrir la imagen. Lo importante es que la dirección responda.

## 2. Abre el COG remoto en QGIS

En QGIS, abre el **Administrador de fuentes de datos**, selecciona **Ráster** e introduce la ruta remota en el campo de origen:

```text
/vsicurl/http://127.0.0.1:8081/imagen_cog.tif
```

Pulsa **Añadir**. `/vsicurl/` indica a GDAL que lea el archivo mediante HTTP y solicite las partes que necesita. Si la versión de QGIS no acepta la ruta en ese campo, prueba **Capa → Añadir capa → Añadir capa ráster** o usa la dirección HTTP directa.

Acércate y aléjate. El ráster debe seguir cubriendo la zona de Catalunya de la imagen sintética. Como el archivo es pequeño, la diferencia de velocidad puede no ser perceptible; el ejercicio demuestra el mecanismo, no una mejora de rendimiento medible.

## Actividad breve

**En parejas, 5–10 minutos:** comparad la capa abierta desde el archivo local con la capa añadida mediante `/vsicurl/`. Revisad qué devuelve la prueba `Range` de la lección anterior y explicad por qué un servidor que entrega solo el archivo completo reduce la ventaja del COG.

**Resultado esperado:** la misma imagen en QGIS y una explicación de la relación entre COG, servidor compatible con rangos y cliente.

**Para pensar:** ¿qué consultarías en la ficha de un COG remoto antes de usarlo como dato analítico (fecha, resolución, bandas, sistema de referencia, licencia)?

## Fuentes

- [Documentación GDAL: acceder a archivos remotos con `/vsicurl/`](https://gdal.org/en/stable/user/virtual_file_systems.html), consultada el 14 de noviembre de 2026.
- [Manual de QGIS 3.44](https://docs.qgis.org/3.44/en/docs/user_manual/), consultado el 14 de noviembre de 2026.

**Siguiente:** [Qué es GeoParquet](geoparquet.md).

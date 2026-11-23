# Crear un COG con GDAL

En esta práctica convertirás a Cloud Optimized GeoTIFF (COG) un recorte real de la ortofoto territorial en color de Catalunya, publicada por el Institut Cartogràfic i Geològic de Catalunya (ICGC) y descrita en el catálogo de la IDEC. Descargarás una pequeña zona en formato GeoTIFF y la optimizarás con GDAL, incluido en QGIS.

## Materiales

- QGIS instalado y una terminal donde funcione GDAL. En Windows, puedes usar **OSGeo4W Shell**.
- Una pequeña imagen GeoTIFF descargada desde la ficha de la IDEC y el visor de descargas del ICGC.

La ortofoto territorial en color de 25 cm representa Catalunya a partir de fotografías aéreas. La ficha de la IDEC identifica la cobertura de 2024, el ICGC como productor y la licencia CC BY 4.0.

## 1. Descarga una pequeña área

1. Abre la [ficha de la ortofoto territorial en color de 2024 en la IDEC](https://catalegs.ide.cat/geonetwork/srv/api/records/ortofoto-25cm-v4r0-color-2024?language=cat). Revisa el productor, la resolución, las fechas de las fuentes y las condiciones de uso.
2. Desde la ficha, abre el enlace del ICGC o accede al [visor de descargas del ICGC](https://visors.icgc.cat/appdownloads/).
3. Selecciona **Ortoimagenes → Ortofoto Territorial 25 cm**, delimita un área pequeña (por ejemplo, un recuadro de unos cientos de metros) y elige **GeoTIFF** como formato. Si el visor permite seleccionar la cobertura temporal, usa 2024 para mantener la correspondencia con la ficha consultada.
4. Descarga y extrae el archivo. Guárdalo en una carpeta de trabajo con el nombre `ortofoto_idec.tif`.

No descargues la cobertura completa de Catalunya para esta práctica: el recorte pequeño es suficiente para convertir y revisar la estructura. El visor ofrece descargas de imágenes por área y varios formatos ráster.

## 2. Comprueba que GDAL puede crear COG

En la terminal ejecuta:

```bash
gdalinfo --format COG
```

Si aparece la información del controlador `COG`, puedes continuar. El controlador de GDAL crea un GeoTIFF con la organización de un COG. Está disponible desde GDAL 3.1.

Antes de convertir, inspecciona la imagen descargada:

```bash
gdalinfo ortofoto_idec.tif
```

Anota el tamaño, número de bandas, sistema de referencia y extensión. La imagen descargada debe estar georreferenciada; no uses una captura de pantalla del visor ni una imagen exportada sin georreferenciación.

## 3. Convierte el GeoTIFF

Sitúate en la carpeta donde guardaste `ortofoto_idec.tif` y ejecuta:

```bash
gdal_translate -of COG ortofoto_idec.tif imagen_cog.tif -co COMPRESS=DEFLATE
```

`-of COG` selecciona el formato de salida. `COMPRESS=DEFLATE` conserva exactamente los valores de la imagen y reduce el tamaño cuando los datos lo permiten. La compresión adecuada depende del tipo de ráster: no conviene usar una compresión con pérdida en datos analíticos sin evaluar sus efectos.

## 4. Revisa el resultado

Abre `imagen_cog.tif` en QGIS y confirma que conserva la extensión, el sistema de referencia y la visualización de la ortofoto original. También puedes ejecutar:

```bash
gdalinfo imagen_cog.tif
```

Busca la estructura de bloques y las overviews. En versiones de GDAL 3.13 o posteriores también puedes validar la estructura con `gdal driver cog validate imagen_cog.tif`; si tu QGIS incluye una versión anterior, este subcomando puede no estar disponible.

!!! question "Comprueba tu comprensión"

    ¿Qué información de la ortofoto permanece en el archivo COG y qué parte de la optimización depende del servidor donde se publique?

**Resultado esperado:** `imagen_cog.tif`, un COG basado en una ortofoto real, georreferenciada y procedente de la IDEC. Conserva la atribución al ICGC y la licencia CC BY 4.0 al reutilizarla.

## Fuentes

- [IDEC: ficha de la Ortofoto en color de Catalunya 25 cm, cobertura 2024](https://catalegs.ide.cat/geonetwork/srv/api/records/ortofoto-25cm-v4r0-color-2024?language=cat), consultada el 22 de noviembre de 2026.
- [ICGC: visor de descargas](https://visors.icgc.cat/appdownloads/), consulta del 22 de noviembre de 2026.
- [ICGC: información de la Ortofoto Territorial](https://www.icgc.cat/ca/Geoinformacio-i-mapes/Dades-i-productes/Imatge/Ortofoto-Territorial).
- [Documentación GDAL: crear COG y opciones disponibles](https://gdal.org/en/stable/drivers/raster/cog.html), consultada el 14 de noviembre de 2026.

**Siguiente:** [Servir un COG por HTTP](servir_cog.md).

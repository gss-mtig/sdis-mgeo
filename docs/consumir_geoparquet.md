# Consumir GeoParquet en QGIS

Abrirás en QGIS el archivo Parquet creado en la práctica anterior. El resultado es una capa vectorial: puedes dibujarla, consultar sus atributos y combinarla con otras capas compatibles.

## Abre el archivo

1. Descarga `puntos.parquet` desde la ubicación donde lo publicaste o usa el que creaste en la lección anterior.
2. En QGIS selecciona **Capa → Añadir capa → Añadir capa vectorial**.
3. Selecciona el archivo `.parquet` y pulsa **Añadir**.
4. Comprueba que aparecen tres puntos. Abre la tabla de atributos y revisa `nombre`, `tema` y `dato_sintetico`.

Si quieres intentar abrir un archivo remoto, GDAL y la compilación de QGIS deben soportar acceso HTTP al controlador Parquet. Para que el ejercicio no dependa de esa función, descarga primero el archivo y ábrelo localmente.

## Interpreta el resultado

GeoParquet conserva las geometrías y atributos, pero no define la simbología del mapa. QGIS aplica una representación y permite explorar la tabla. El formato está orientado al almacenamiento e intercambio eficiente de datos, no a servir un mapa ya dibujado.

!!! question "Comprueba tu comprensión"

    Si otra persona recibe el archivo, ¿qué debe saber para interpretar correctamente las geometrías? ¿Qué diferencia hay entre abrir este archivo y consumir un WMS?

## Actividad de clase

**En parejas, 5–10 minutos:** comparad `puntos.geojson` y `puntos.parquet` en QGIS. Localizad una geometría, un campo que se mantiene y cualquier diferencia que dependa de la herramienta. Decidid cuál compartiríais con un equipo de análisis y cuál con una aplicación web sencilla.

**Resultado esperado:** comparación breve que relacione estructura, compatibilidad y uso previsto, sin asumir que un formato es mejor para todas las tareas.

## Fuentes

- [Documentación GDAL: leer conjuntos Parquet y GeoParquet](https://gdal.org/en/stable/drivers/vector/parquet.html), consultada el 14 de noviembre de 2026.
- [Manual de QGIS 3.44](https://docs.qgis.org/3.44/en/docs/user_manual/), consultado el 14 de noviembre de 2026.

**Siguiente:** [Ejercicio final: descubre y publica datos geográficos](ejercicio_final_ide.md).

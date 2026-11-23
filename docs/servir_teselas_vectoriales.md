# Servir teselas con TileServer GL Light

Ahora pondrás a disposición de un cliente web las teselas vectoriales que has generado. TileServer GL Light sirve archivos MBTiles y estilos compatibles con clientes como MapLibre GL JS. En esta lección configurarás el servicio para publicar tanto los 10.000 puntos sintéticos como, si has completado la ampliación anterior, los vehículos implicados en accidentes de Barcelona.

> Este ejercicio inicia un servidor **local** para aprender y comprobar el flujo. Para que otras personas accedan desde Internet, haría falta desplegar el servicio en un servidor accesible y mantenerlo; esta práctica no realiza ese despliegue.

## Requisitos

- Haber completado [la generación de `puntos.mbtiles`](crear_teselas_vectoriales.md). La capa de accidentes es opcional: para servirla también, completa la ampliación del CSV y crea `accidentes_barcelona.mbtiles`.
- Node.js y npm. La documentación actual de TileServer GL indica soporte para Node.js 20, 22 y 24. Si vas a preparar la actividad para un aula, instala y comprueba Node.js antes de la sesión.
- Descarga [config_solo_puntos.json](ejemplos/vector_tiles/config_solo_puntos.json) y [estilo_puntos.json](ejemplos/vector_tiles/estilo_puntos.json) para servir solo los puntos. Para servir ambos conjuntos, descarga además [config.json](ejemplos/vector_tiles/config.json) y [estilo_accidentes.json](ejemplos/vector_tiles/estilo_accidentes.json).

La versión consultada para esta guía es `tileserver-gl-light` **5.7.0**. Hay dos formas de instalarlo. En ambos casos necesitas que Node.js y npm estén disponibles y que el equipo pueda descargar el paquete desde npm.

### Opción A: instalación global

Es la opción más cómoda si tienes permisos para instalar paquetes globales:

```bash
npm install --global tileserver-gl-light@5.7.0
tileserver-gl-light --version
```

### Opción B: instalación local, sin permisos de administrador

Abre la terminal dentro de tu carpeta `teselas-clase` e instala el programa solo en esa carpeta:

```bash
npm install --no-save tileserver-gl-light@5.7.0
```

Para comprobarlo y arrancarlo, usa `npx` desde esa misma carpeta:

```bash
npx tileserver-gl-light --version
npx tileserver-gl-light --config config_solo_puntos.json --port 8081
```

También puedes pedir a `npx` que descargue y ejecute la versión fijada sin instalarla globalmente ni guardarla como dependencia del proyecto:

```bash
npx --yes --package=tileserver-gl-light@5.7.0 tileserver-gl-light --config config_solo_puntos.json --port 8081
```

La primera ejecución necesita conexión a npm. Si el ordenador no tiene Node.js/npm o la red de la universidad bloquea la descarga, esta alternativa no podrá instalar el servidor: comprueba estos requisitos antes de la clase o prepara una demostración en un equipo donde esté permitido.

## Prepara la carpeta

Para la práctica básica, reúne estos archivos en una carpeta de trabajo:

```text
teselas-clase/
├── puntos.mbtiles
├── config_solo_puntos.json
└── estilo_puntos.json
```

Si también vas a servir los accidentes, coloca los archivos adicionales y ambos MBTiles en esa misma carpeta:

```text
teselas-clase/
├── puntos.mbtiles
├── accidentes_barcelona.mbtiles
├── config.json
├── estilo_puntos.json
└── estilo_accidentes.json
```

El GeoJSON y el CSV de origen no son necesarios para arrancar el servidor: TileServer GL lee los archivos MBTiles.

`config_solo_puntos.json` registra una fuente y un estilo. `config.json` registra las dos fuentes (`puntos` y `accidentes`) y ofrece una vista previa para cada estilo. Cada estilo usa el mismo nombre de capa interna que se indicó al crear los MBTiles (`puntos` o `accidentes`). Los estilos dibujan los datos sobre un fondo claro, sin depender de un mapa base externo.

## Inicia el servidor local

Abre una terminal en la carpeta de trabajo y ejecuta el comando correspondiente a la instalación elegida. El puerto predeterminado de TileServer GL es `8080`, que puede estar ocupado por otro programa. En estos ejemplos fijamos `8081`; puedes elegir otro puerto libre si también está ocupado. Para servir solo los puntos con la opción global:

```bash
tileserver-gl-light --config config_solo_puntos.json --port 8081
```

Para la instalación local con npm:

```bash
npx tileserver-gl-light --config config_solo_puntos.json --port 8081
```

Deja abierta la terminal mientras utilizas el servidor. En el navegador visita `http://localhost:8081/`. La portada de TileServer GL muestra la vista previa del estilo configurado. También puedes consultar los metadatos de la fuente de puntos en:

```text
http://localhost:8081/data/puntos.json
```

En ese documento identifica el nombre de la capa vectorial, los niveles de zoom y los campos que se publican. La ruta de teselas tiene la forma `/data/puntos/{z}/{x}/{y}.pbf`; el cliente solicita las teselas que necesita al navegar por el mapa.

### Sirve también los accidentes

Si has generado `accidentes_barcelona.mbtiles`, detén el servidor con **Ctrl+C** y vuelve a iniciarlo usando la configuración completa:

```bash
tileserver-gl-light --config config.json --port 8081
```

Con instalación local, usa `npx tileserver-gl-light --config config.json --port 8081`. Abre de nuevo `http://localhost:8081/`: la portada debe ofrecer las vistas previas de puntos y accidentes. Comprueba los metadatos de esta segunda fuente en:

```text
http://localhost:8081/data/accidentes.json
```

La ruta de teselas de accidentes tiene la forma `/data/accidentes/{z}/{x}/{y}.pbf`. Si el archivo MBTiles no está en la carpeta, usa `config_solo_puntos.json`; `config.json` necesita que existan los dos archivos. Si usas otro puerto, sustituye `8081` en las URL del navegador, QGIS y el ejemplo MapLibre.

Cuando termines, vuelve a la terminal y pulsa **Ctrl+C** para detener el servidor.

## Actividad de clase

**En parejas, 5–10 minutos:** abrid las vistas previas y los documentos `data/puntos.json` y `data/accidentes.json` (si generasteis esa capa). Comparad la distribución espacial y un atributo publicado. ¿En cuál de los dos conjuntos se concentra más la información en algunas zonas? ¿Qué os permite observar el mapa y qué información adicional podéis encontrar en los metadatos de la capa?

**Resultado esperado:** una vista previa local por cada conjunto servido, sus rutas de acceso identificadas y una observación sobre cómo varía la distribución espacial de los datos. Recordad que cada fila de accidentes representa un vehículo implicado, no necesariamente un accidente único.

Continúa con [consumir las teselas en QGIS y MapLibre GL JS](consumir_teselas_vectoriales.md).

## Si algo no funciona

- **`tileserver-gl-light` no se reconoce:** cierra y vuelve a abrir la terminal después de instalar el paquete; comprueba que Node.js y npm están instalados.
- **La instalación global falla por permisos:** sigue la [opción de instalación local](#opcion-b-instalacion-local-sin-permisos-de-administrador) y ejecuta el programa con `npx`.
- **npm no puede descargar el paquete:** comprueba la conexión a Internet y las restricciones de red del aula; la instalación local también necesita acceder a npm la primera vez.
- **El servidor no encuentra un archivo MBTiles:** comprueba que el archivo indicado en la configuración esté en la carpeta de trabajo. `config.json` requiere tanto `puntos.mbtiles` como `accidentes_barcelona.mbtiles`; para servir solo puntos, inicia con `config_solo_puntos.json`.
- **El mapa aparece vacío:** revisa que `source-layer` en el estilo coincide con el nombre de capa que informó `ogrinfo` (`puntos` o `accidentes`).
- **La vista previa de accidentes aparece vacía:** comprueba que `ogrinfo -ro -so accidentes_barcelona.mbtiles` muestra la capa `accidentes` y que el CSV tenía coordenadas válidas. Acerca el mapa si los puntos aparecen muy juntos.
- **El puerto 8081 también está ocupado:** elige otro puerto libre, por ejemplo `--port 8082`, y usa ese mismo número en todas las URL de la práctica.

## Fuentes

- [TileServer GL Light: instalación y uso](https://github.com/maptiler/tileserver-gl/blob/master/README_light.md), consultado el 14 de noviembre de 2026.
- [TileServer GL: instalación, incluido Node.js y la variante Light](https://github.com/maptiler/tileserver-gl/blob/master/docs/installation.rst).
- [TileServer GL: opciones de uso y configuración](https://github.com/maptiler/tileserver-gl/blob/master/docs/usage.rst).
- [TileServer GL: formato de `config.json` y fuentes MBTiles para estilos](https://github.com/maptiler/tileserver-gl/blob/master/docs/config.rst).

**Siguiente:** [Consumir teselas en QGIS y MapLibre GL JS](consumir_teselas_vectoriales.md).

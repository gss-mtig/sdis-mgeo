# SDIS-mgeo

Materiales docentes sobre infraestructuras de datos espaciales (IDEs) y estándares de geoservicios.

Sitio publicado: <https://gss-mtig.github.io/sdis-mgeo/>

## Temario

- Introducción a las IDE: antecedentes, definición, componentes, IDEC, IDEE, INSPIRE y otras IDE.
- Estándares OGC: WMS, WMTS, WFS, GML, SLD, SOS, CSW y OGC API.
- Instalación de programas: XAMPP, GeoNetwork y QGIS Server.
- Clientes de mapas: clientes web y prácticas con QGIS, Leaflet y ArcGIS Online.
- Estándares ISO y metadatos: creación, catalogación e intercambio de metadatos.
- Servidores de mapas y publicación de datos en bases de datos en línea.

## Requisitos

- Python 3.11 o posterior.
- Git para obtener el repositorio y enviar cambios a GitHub.

## Ejecutar y previsualizar en local

Desde la carpeta raíz del repositorio, crea y activa un entorno virtual e instala Zensical:

**Linux o macOS**

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install zensical
```

**Windows (PowerShell)**

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install zensical
```

Inicia la previsualización local con recarga automática:

```bash
zensical serve
```

Abre <http://localhost:8000>. Para generar el sitio estático sin iniciar el servidor:

```bash
zensical build
```

El sitio generado queda en `site/` (carpeta que no se versiona). Para salir del entorno virtual, ejecuta `deactivate`.

## Publicar en GitHub Pages

El sitio se construye y publica con GitHub Actions al enviar cambios a la rama `master`. El flujo está en [`.github/workflows/docs.yml`](.github/workflows/docs.yml).

1. En GitHub, abre **Settings → Pages** y selecciona **GitHub Actions** como fuente de publicación. Haz este cambio una vez que hayas revisado el sitio generado con Zensical.
2. Envía los cambios a `master`:

   ```bash
   git add .
   git commit -m "Migrar documentación a Zensical"
   git push origin master
   ```

3. En la pestaña **Actions**, revisa la ejecución del flujo **Publicar documentación**. Al terminar, GitHub Pages actualizará <https://gss-mtig.github.io/sdis-mgeo/>.

La configuración actual de `mkdocs.yml` y la estructura `docs/` se conservan para facilitar la migración gradual. Zensical utiliza esa configuración para generar el sitio; el flujo de GitHub Actions instala Zensical y publica la carpeta `site/`.

## Estructura

```text
mkdocs.yml                  # Configuración del sitio y navegación
docs/                       # Páginas Markdown e imágenes
.github/workflows/docs.yml  # Construcción y publicación en GitHub Pages
```

## Licencia

Consulta [LICENSE](LICENSE).

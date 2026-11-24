# Descargar conjuntos de datos con ATOM

Un servicio de descarga permite obtener los datos geográficos para abrirlos en un SIG, analizarlos o transformarlos. El servicio **ATOM de Catastro** organiza enlaces a descargas de conjuntos INSPIRE predefinidos, como las parcelas catastrales de un municipio.

Esto es distinto de un WMS: con WMS recibes una imagen de mapa; con ATOM accedes a un archivo descargable con entidades y atributos. En el ejemplo del Catastro, la descarga es un ZIP con datos en GML y un archivo XML de metadatos.

## Qué significa ATOM en este servicio

**Atom Syndication Format** es un formato XML estandarizado por IETF para publicar listas de entradas con títulos, fechas y enlaces. La guía técnica de INSPIRE para servicios de descarga predefinidos describe cómo utilizar feeds Atom para ofrecer enlaces a conjuntos de datos ya preparados. Esa guía técnica no es una norma legal y su versión publicada es de 2013; aquí nos interesa entender el servicio del Catastro, que sigue ofreciéndose en el portal. El formato Atom no es un estándar OGC ni una API de consulta espacial: el feed ayuda a descubrir descargas, pero no permite pedir entidades mediante un filtro espacial.

En el servicio del Catastro, el proveedor organiza las descargas por tipo de datos y municipio. El usuario recorre los enlaces del feed hasta el archivo que necesita. El portal indica que los conjuntos se actualizan dos veces al año.

En un feed Atom, el documento raíz contiene entradas (`entry`) y cada entrada puede enlazar a otro feed o a un archivo. Este esquema reducido es solo ilustrativo:

```xml
<feed xmlns="http://www.w3.org/2005/Atom">
  <title>Parcelas catastrales</title>
  <entry>
    <title>Gerencia territorial</title>
    <updated>AAAA-MM-DDThh:mm:ssZ</updated>
    <link rel="alternate" href="enlace-al-siguiente-feed-o-archivo" />
  </entry>
</feed>
```

El título ayuda a identificar el recurso, `updated` indica una fecha asociada a la entrada y `href` contiene el enlace que se sigue. El valor concreto de esos campos depende del feed.

## Ejemplo: parcelas catastrales INSPIRE del Catastro

La Dirección General del Catastro ofrece servicios ATOM para tres conjuntos INSPIRE: parcelas catastrales (CP), direcciones (AD) y edificios (BU). En esta lección utilizaremos el de parcelas.

1. Abre la página oficial de [Servicios INSPIRE de Cartografía Catastral](https://www.catastro.hacienda.gob.es/webinspire/index.html) y localiza la sección **Servicios ATOM de conjuntos de datos predefinidos INSPIRE**.
2. Abre el feed de [Parcelas catastrales (CP)](https://www.catastro.hacienda.gob.es/INSPIRE/CadastralParcels/ES.SDGC.CP.atom.xml). Según el navegador, verás una lista con formato propio o el XML sin formato visual.
3. En la primera lista, sigue el enlace de la gerencia territorial correspondiente. En su feed, busca el municipio que te interesa. Si la lista aparece como XML, usa **Ctrl+F** para buscar el nombre y sigue el enlace asociado a esa entrada.
4. Descarga el ZIP del municipio y descomprímelo. Para parcelas, el paquete incluye el GML de parcelas catastrales, otro GML de zonas catastrales y un XML con metadatos.
5. Abre en QGIS el GML de parcelas catastrales. Revisa la extensión, los atributos y el sistema de referencia; compara la geometría con una capa de referencia disponible en QGIS.

El [documento de descripción del servicio](https://www.catastro.hacienda.gob.es/webinspire/documentos/inspire-ATOM.pdf) explica esta estructura: un primer nivel de feeds de gerencias territoriales y un segundo nivel con enlaces a los archivos municipales. El contenido de los feeds puede cambiar cuando se actualizan los datos, así que sigue los enlaces que aparecen en el servicio en vez de reutilizar una URL de descarga municipal guardada.

## Qué contiene la descarga y qué no

- El ZIP contiene un conjunto municipal predefinido; no seleccionas una caja del mapa ni envías una consulta por atributos.
- Los datos de parcelas se entregan en GML 3.2.1, junto con un fichero XML de metadatos.
- Cada municipio puede tener un volumen de datos distinto. Si solo necesitas una zona pequeña, el servicio ATOM puede descargar más información de la necesaria.
- La licencia del Catastro se aplica al acceso y al uso de los datos. Permite determinados usos de los datos transformados, pero no autoriza redistribuir en Internet los datos originales sin transformar. Lee la [licencia de acceso y uso](https://www.catastro.hacienda.gob.es/webinspire/documentos/Licencia.pdf) antes de publicar o compartir resultados.

## Actividad práctica en clase

**En parejas, 10–15 minutos.** Elegid un municipio y seguid el feed de parcelas del Catastro hasta localizar su archivo.

1. Anotad el nombre del feed inicial y el enlace del feed de la gerencia territorial.
2. Localizad la entrada del municipio y anotad el nombre del ZIP y la fecha indicada en el feed.
3. Descargad y descomprimid el ZIP. Identificad el GML de parcelas y el XML de metadatos.
4. Cargad el GML en QGIS y comprobad si muestra entidades y atributos.

**Resultado esperado:** una tabla breve con municipio, ZIP, fecha del feed, nombre del GML y dos atributos observados. No publiquéis ni redistribuyáis el ZIP original: la licencia del Catastro establece condiciones específicas para difundir información transformada.

**Reflexiona:** ¿cuándo te conviene una descarga municipal completa y cuándo sería mejor un servicio que permita consultar entidades para un área menor?

## Si el feed no se abre como una página

ATOM es XML. Si el navegador muestra código, sigue los enlaces `href` de las entradas; no es necesario que el navegador convierta el feed en una interfaz. También puedes consultar la [guía de ATOM del Catastro](https://www.catastro.hacienda.gob.es/webinspire/documentos/inspire-ATOM.pdf), que incluye capturas del recorrido y describe los archivos incluidos en cada ZIP. Si el servicio está temporalmente fuera de línea, el docente puede usar esas capturas para reconocer la estructura y retomar la descarga cuando vuelva a estar disponible.

## Fuentes

- [Dirección General del Catastro: Servicios INSPIRE de Cartografía Catastral](https://www.catastro.hacienda.gob.es/webinspire/index.html), consultado el 24 de noviembre de 2026.
- [Feed ATOM de parcelas catastrales INSPIRE](https://www.catastro.hacienda.gob.es/INSPIRE/CadastralParcels/ES.SDGC.CP.atom.xml).
- [Catastro: descripción de los servicios de descarga ATOM](https://www.catastro.hacienda.gob.es/webinspire/documentos/inspire-ATOM.pdf).
- [Catastro: licencia de acceso y uso](https://www.catastro.hacienda.gob.es/webinspire/documentos/Licencia.pdf).
- [INSPIRE: guía técnica para la implementación de servicios de descarga](https://knowledge-base.inspire.ec.europa.eu/publications/technical-guidance-implementation-inspire-download-services_en).
- [IETF RFC 4287: Atom Syndication Format](https://www.rfc-editor.org/rfc/rfc4287).

**Siguiente:** [Pirámides de teselas ráster: XYZ, WMTS y OGC API – Tiles](piramides_teselas.md).

# SLD

EL SLD (Style Layer Descriptor) es una codificación xml para permitir al usuario ampliar las especificaciones (WMS) y definir símbolos de objetos.

El usuario puede aplicar estilos a los objetos de forma diferentes de cómo han sido configurados en el servidor.

Los servidores WMS que soportan SLD permiten añadir los parámetros SLD dónde como valor se describe la url dónde se encuentra el documento xml o SLDBODY, dónde se pasan los valores SLD de forma directa (método poco recomendado) a las peticiones WMS GetMap.

Ejemplos: 

*Petición sin SLD*
http://servicios.idee.es/wms-inspire/hidrografia?VERSION=1.1.1&SERVICE=WMS&REQUEST=GetMap&SRS=EPSG:25830&FORMAT=image/png&BBOX=419685.23094987,4082028.7934849,582245.81538657,4201830.8601227&WIDTH=1247&HEIGHT=919&LAYERS=HY.Network

*Petición con SLD*
http://servicios.idee.es/wms-inspire/hidrografia?VERSION=1.1.1&SERVICE=WMS&REQUEST=GetMap&SRS=EPSG:25830&FORMAT=image/png&BBOX=419685.23094987,4082028.7934849,582245.81538657,4201830.8601227&WIDTH=1247&HEIGHT=919&SLD=http://betaserver.icgc.cat/dades/sld.xml

http://servicios.idee.es/wms-inspire/hidrografia?VERSION=1.1.1&SERVICE=WMS&REQUEST=GetMap&SRS=EPSG:25830&FORMAT=image/png&BBOX=419685.23094987,4082028.7934849,582245.81538657,4201830.8601227&WIDTH=1247&HEIGHT=919&SLD_BODY=%3CStyledLayerDescriptor+version%3D%221.0.0%22+xmlns%3D%22http%3A%2F%2Fwww.opengis.net%2Fsld%22+xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22+xmlns%3Axsi%3D%22http%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchemainstance%22+xsi%3AschemaLocation%3D%22http%3A%2F%2Fschemas.opengis.net%2Fsld%2F1.0.0%2FStyledLayerDescriptor.xsd%22+xmlns%3Ase%3D%22http%3A%2F%2Fwww.opengis.net%2Fse%22+xmlns%3Abcn%3D%22http%3A%2F%2Fwww.ign.es%2Fbcn25%22%3E%3CNamedLayer%3E%3CName%3EHY.Network%3C%2FName%3E%3CUserStyle%3E%3CFeatureTypeStyle%3E%3Cse%3AFeatureTypeName%3EHY.Network%3C%2Fse%3AFeatureTypeName%3E%3CRule%3E%3CLineSymbolizer%3E%3CStroke%3E%3CCssParameter+name%3D%22stroke%22%3E%23ffaaff%3C%2FCssParameter%3E%3CCssParameter+name%3D%22strokewidth%22%3E5.0%3C%2FCssParameter%3E%3C%2FStroke%3E%3C%2FLineSymbolizer%3E%3C%2FRule%3E%3C%2FFeatureTypeStyle%3E%3C%2FUserStyle%3E%3C%2FNamedLayer%3E%3C%2FStyledLayerDescriptor%3E

Se puede ver la especificación en [https://www.ogc.org/standards/sld](https://www.ogc.org/standards/sld)

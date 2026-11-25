# Ejercicio final: descubre y publica datos geográficos

## Propósito

En este ejercicio individual recorrerás el ciclo de trabajo de una infraestructura de datos espaciales (IDE): localizarás una IDE, buscarás datos en su catálogo, interpretarás la ficha, descargarás un conjunto y lo volverás a publicar acompañado de una visualización y una ficha breve.

Elige una problemática que te interese: por ejemplo, movilidad, agua, incendios, contaminación, equipamientos, usos del suelo, biodiversidad o riesgos naturales. Formula una pregunta concreta que los datos puedan ayudar a explorar.

Debes utilizar una IDE distinta de la IDEC empleada en el [caso práctico de clase](caso_idec_inundaciones.md). Puedes escoger una IDE local, regional, estatal o europea, siempre que el catálogo permita encontrar un conjunto de datos apropiado.

!!! question "Buscar, publicar y visualizar datos de una IDE — 3 puntos"

    Completa las fases siguientes y presenta las evidencias indicadas en la entrega.

    ### 1. Plantea una pregunta

    Describe brevemente el problema que te interesa, el territorio al que se refiere y qué quieres averiguar. Evita temas demasiado amplios: convierte, por ejemplo, “movilidad” en una pregunta que especifique un lugar y una necesidad.

    ### 2. Encuentra y evalúa los datos en una IDE

    1. Identifica una IDE distinta de la IDEC y enlaza su geoportal o catálogo.
    2. Busca conjuntos relacionados con tu pregunta. Anota los términos que has probado.
    3. Selecciona un conjunto y enlaza su ficha de metadatos.
    4. A partir de la ficha, identifica quién produce los datos, qué territorio y periodo cubren, su fecha o actualización, las condiciones de uso y cómo se accede a ellos. Si algún dato no consta o no está claro, indícalo.
    5. Descarga los datos y comprueba que puedes abrirlos. Si el formato no se puede publicar o visualizar directamente en la práctica, puedes transformarlo con QGIS a un formato adecuado, explicando qué conversión has hecho.

    ### 3. Publica los datos y crea una visualización

    Publica el conjunto descargado —o una versión transformada— en un sitio accesible mediante una URL. Para un conjunto pequeño puedes utilizar GitHub Pages siguiendo la práctica de [publicación de un archivo GeoJSON](publicar_geojson_estatico.md). Si utilizas otro método, explica dónde has alojado los datos y cómo se accede.

    Crea una visualización web sencilla que permita ver la información geográfica. Puedes partir del ejemplo de Leaflet de los materiales y adaptarlo a tus datos. La visualización debe indicar qué conjunto muestra y enlazar a la descarga publicada. No es necesario desarrollar una aplicación compleja.

    Antes de publicar, comprueba que la licencia permite redistribuir los datos y que no expones información personal, sensible o restringida. No subas datos si no puedes confirmar que es adecuado hacerlos públicos; en ese caso, elige otro conjunto.

    ### 4. Redacta una ficha breve

    Añade a la página de publicación o al documento de entrega una ficha con:

    - **Título** del conjunto.
    - **Descripción**: qué representa y para qué puede servir.
    - **Productor** y enlace a la ficha del catálogo original.
    - **Territorio** y **fecha o periodo** de los datos.
    - **Formato publicado** y enlace directo al archivo.
    - **Licencia o condiciones de uso**, con atribución si corresponde.
    - **Limitaciones conocidas**, por ejemplo cobertura incompleta, fecha antigua o campos que requieren interpretación.

    Esta ficha es una presentación breve del recurso publicado. No sustituye el ejercicio de creación de un registro formal de metadatos en GeoNetwork.

    ### Entrega

    Entrega un documento individual en PDF, DOCX u ODT de unas **3–5 páginas**, con:

    1. La pregunta, el problema y el territorio elegidos.
    2. El nombre y enlace de la IDE, los términos de búsqueda y el enlace a la ficha seleccionada.
    3. Una síntesis de lo que averiguaste en los metadatos y una breve justificación de por qué elegiste ese conjunto.
    4. Evidencia de la descarga y de la publicación: enlace al sitio, enlace directo al archivo y enlace a la visualización. Incluye capturas suficientes para que se entienda el resultado.
    5. La ficha breve del recurso y una reflexión final: ¿qué parte de tu pregunta permiten explorar estos datos y qué limitación importante encontraste?

    Incluye la fecha en que consultaste el catálogo. Los enlaces publicados deben ser accesibles para su corrección durante el periodo de evaluación. Si la IDE o el recurso dejan de estar disponibles, aporta capturas y enlaces alternativos cuando sea posible.

    ### Criterios de evaluación

    - **0,5 puntos:** pregunta concreta, con problemática y territorio definidos.
    - **0,75 puntos:** búsqueda trazable en una IDE distinta de la IDEC, selección justificada y lectura pertinente de la ficha de metadatos.
    - **0,75 puntos:** descarga y publicación accesible del conjunto, con formato utilizable, licencia y atribución tratadas correctamente.
    - **0,5 puntos:** visualización funcional, relacionada con los datos y enlazada desde la entrega.
    - **0,5 puntos:** ficha breve completa, fuentes enlazadas y reflexión sobre el uso y las limitaciones de los datos.

    **Total: 3 puntos.**

## Consejos para elegir un conjunto de datos

Antes de comprometerte con un conjunto, comprueba que:

- la descarga funciona y el archivo tiene un tamaño razonable;
- la ficha identifica al productor y ofrece información sobre fecha, cobertura y condiciones de uso;
- el formato puede abrirse en QGIS y convertirse, si hace falta, a GeoJSON;
- las geometrías y atributos tienen sentido para la pregunta que has formulado;
- puedes redistribuir los datos en un sitio público.

Si un servicio falla, prueba otro enlace de descarga ofrecido por la ficha o escoge otro conjunto. El objetivo es completar el flujo con datos utilizables y explicar tus decisiones, no depender de un servicio externo concreto.

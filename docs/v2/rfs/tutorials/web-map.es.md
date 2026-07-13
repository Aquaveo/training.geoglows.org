# Capa de Esri Living Atlas

Esri alberga un **ArcGIS Living Atlas of the World**. Incluye mapas, aplicaciones y capas de datos que pueden ayudar a los investigadores a acceder fácilmente a los datos. Hospedan una capa de GEOGLOWS como parte de este programa. Esto permite que los datos de caudal de RFS se carguen en ArcGIS o QGIS sin necesidad de descargar todo el conjunto de datos. La imagen a continuación muestra la capa de caudal cargada en QGIS.

Puedes añadirlo a mapas web como una capa web sin necesidad de descargar los datos adicionales ni la red de drenaje. Si estás intentando descargar el *hydrofabric*, encontrarás instrucciones sobre cómo hacerlo en la sección de [datos disponibles](../datasets/catalog.md).

![captura de pantalla](../../static/images/imagen.png)

La capa es una capa de animación que muestra los primeros 10 días de los datos de pronóstico de 15 días de RFS. Los arroyos están coloreados según si superan un período de retorno dado y, por lo tanto, están en un flujo alto.

Algunas cosas que un usuario puede hacer con esta capa:

- Los datos de pronóstico se pueden ver secuencialmente a lo largo del tiempo gracias al control deslizante incorporado en la aplicación. Un usuario puede observar los arroyos en ventanas de 3 horas. El color de los arroyos cambiará si el arroyo experimenta un flujo alto durante este tiempo.
- Las características se pueden identificar haciendo clic en el mapa. Los pop-ups preconfigurados mostrarán nombres de ríos provenientes de OpenStreetMap.

[Más información](https://www.arcgis.com/home/item.html?id=8f0573e0c0b9491dbeafde9c72ccf02b) sobre la capa del mapa web se puede encontrar en el sitio de web de ArcGIS. La información sobre cómo cargar capas de Living Atlas en ArcGIS se encuentra [aquí](https://enterprise.arcgis.com/en/portal/10.5/use/add-living-atlas-layers.htm).

Para cargar este mapa en QGIS, haz lo siguiente:

**Paso 1:** En la parte inferior de la página de información de la capa del mapa de Esri, en el lado derecho, se encuentra el enlace URL para acceder a la capa del mapa:  
https://livefeeds3.arcgis.com/arcgis/rest/services/GEOGLOWS/GlobalWaterModel_Medium/MapServer  
Copia este enlace en tu portapapeles.

**Paso 2:** En tu software GIS, ve a *Capa* → *Añadir capa* → *Añadir capa de servicio ArcGIS REST*.

![screenshot](../../static/images/qgis.png)

**Paso 3:** Haz clic para añadir una nueva capa de servicio REST. Introduce un nombre para la capa y pega la URL copiada en la ventana.

La capa también se puede utilizar en [Esri Instant Apps](https://www.esri.com/en-us/arcgis/products/arcgis-instant-apps/overview).


# Novedades

Este sitio de capacitación se centra en la versión 3 de RFS (River Forecast System, Sistema de Pronóstico de Ríos). Se realizaron muchos cambios importantes entre esta versión del modelo y la versión anterior. Esta página ofrece algunos detalles sobre las mejoras y los cambios realizados al modelo. Si solo busca información sobre el modelo, puede omitir esta página.

1. **Datos de hidrografía**
    1. **Número de ríos** - RFSv2 tenía alrededor de 6.8 millones de ríos, pero RFSv3 se redujo a aproximadamente 4.9 millones. Estos recortes provienen principalmente de la eliminación de ríos en grandes desiertos; se eliminaron ríos del desierto del Sahara, del desierto de Gobi y de los desiertos del centro de Australia. También se eliminaron los segmentos de río ubicados dentro de lagos o en pequeñas cuencas costeras (o en el océano). Además, algunos ríos más pequeños se fusionaron. Los identificadores (IDs) de los ríos se mantuvieron iguales en el modelo. Si el ID de su río ya no está disponible y no se encuentra en una zona eliminada, puede relacionarlo con el nuevo río de RFSv3. La correspondencia entre los IDs de río antiguos y nuevos está disponible en el archivo [tdxhydro_to_v3_id_map.parquet](https://v3.s3.riverforecastsystem.com/hydrography/global/tdxhydro_to_v3_id_map.parquet) (aproximadamente 87 MB).
    2. **Regiones** - Los datos de hidrografía ya no están organizados en 125 VPUs. En su lugar, ahora están organizados en 47 regiones numeradas a partir de sus cuencas de nivel 2 de HydroSHEDS.
    3. **Lagos** - El conjunto de datos de hidrografía muestra un nuevo conjunto de lagos. Este es diferente de los lagos que estaban disponibles en RFSv2.
2. **Formatos de almacenamiento de datos** - Los archivos zarr ahora utilizan la versión 3 de zarr en lugar de la versión 2. Se agregaron más metadatos a los archivos y el almacenamiento se optimizó aún más.
3. **Cambios en los procesos de enrutamiento** - El proceso que enruta el agua a través de los ríos se actualizó para depender completamente de un paquete de Python llamado river-route, desarrollado por el Dr. Riley Hales. El proceso se actualizó para ejecutarse más rápido y se hicieron algunas correcciones menores a algunas de las entradas del modelo.
4. **Nuevos buckets de AWS** - Un nuevo bucket de AWS contiene todos los datos de la versión 3 del modelo. Se puede encontrar aquí: [https://v3.s3.riverforecastsystem.com](https://v3.s3.riverforecastsystem.com).
5. **Nuevo Hydroviewer** - El Hydroviewer se ha actualizado para la versión 3, con nuevas funciones como el mapeo de inundaciones, herramientas para seleccionar ríos y cuencas completas, y la búsqueda de ríos por nombre. Consulte la página del [Hydroviewer](web-apps/hydroviewer.md) para aprender a usarlo.
6. **Productos de mapeo de inundaciones** - RFS ahora produce mapas de inundación que muestran el área que se inundaría a lo largo de un río, y la profundidad que alcanzaría el agua, para un caudal determinado. Se pueden ver y descargar en el [Hydroviewer](web-apps/hydroviewer.md), y los distintos productos de mapas de inundación se describen en [Datos Disponibles](data/available-data.md#mapas-de-inundacion).
7. **Almacén de datos** - Hay un nuevo almacén de datos disponible para descargar los productos de RFSv3: [https://apps.geoglows.org/previews/rfs-data-store/](https://apps.geoglows.org/previews/rfs-data-store/). Este sitio proporciona metadatos e información sobre los datos disponibles y permite a los usuarios explorar y descargar los productos de datos de su interés. Consulte [El Almacén de Datos](data/accessing-data/datastore.md) para obtener instrucciones sobre cómo usarlo.
8. **Cambios en este sitio** - Este sitio se actualizó y reorganizó. Parte de la información más avanzada se trasladó a una sección avanzada. También se agregó información sobre aguas subterráneas.

## Mejora del Modelo

RFS obtiene sus entradas de datos meteorológicos globales. Los datos globales tienen un sesgo inherente. Los desarrolladores de RFS trabajan
constantemente para minimizar los sesgos y corregir los errores que se producen en el sistema. Estamos trabajando para aplicar la corrección
de sesgo a las entradas del modelo como un paso para mejorar los resultados.

La [corrección de sesgo local](../v2/rfs/bias-correction/bias-correction.md) fue una opción disponible en las versiones 2 y 1. Se desarrolló como parte de un proyecto de
investigación y la realizaban los usuarios finales como un paso de posprocesamiento. La corrección de sesgo local permitía aplicar
correcciones solo a los segmentos de río que tenían una estación de aforo. Aunque el código sigue disponible para que los usuarios finales
utilicen esta opción, se está dando más importancia a opciones que permitan mejorar los ríos más allá de una sola ubicación. Con este fin,
en la versión 2 se probó una corrección de sesgo global, [SABER](../v2/rfs/bias-correction/bias-correction.md#saber-analisis-de-corrientes-para-estimacion-y-reduccion-de-sesgo).

De cara al futuro, se está investigando para que esta corrección y calibración se integren en la formulación del modelo, en lugar de ser un
paso de posprocesamiento. Esto permite que todo el modelo se beneficie de los datos de las estaciones de aforo y evita tener dos versiones
separadas de los datos: con corrección de sesgo y sin corrección de sesgo.

GEOGLOWS ha estado recopilando una base de datos de estaciones de aforo para mejorar RFS. Los datos de aforo que se aporten mejorarán el
desempeño en los ríos cercanos y en el modelo en su conjunto. Los datos de una estación podrían beneficiar los valores de toda una cuenca o
de ríos similares, y no solo en su ubicación. Los datos se usarían para que el modelo sea lo más preciso posible.

Todos los datos aportados pueden mantenerse privados. Se utilizarán con fines de investigación y validación, pero los valores originales de
las estaciones no se publicarán sin permiso. Aportar datos locales puede ayudar a que las zonas locales tengan un mejor desempeño, lo que
hace que el modelo sea más preciso en las áreas con datos de aforo aportados.

Si dispone de datos de caudal o de nivel de agua, nos encantaría incluirlos en nuestro proceso de calibración y validación. Complete este
formulario de Google y nos pondremos en contacto con usted sobre los datos.
<!-- TODO: add the link to the Google form for contributing gauge data -->

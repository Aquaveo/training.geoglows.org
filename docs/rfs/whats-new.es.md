# Novedades

Este sitio de capacitación se centra en la versión 3 de RFS (River Forecast System, Sistema de Pronóstico de Ríos). Se realizaron muchos cambios importantes entre esta versión del modelo y la versión anterior. Esta página ofrece algunos detalles sobre las mejoras y los cambios realizados al modelo. Si solo busca información sobre el modelo, puede omitir esta página.

1. **Datos de hidrografía**
    1. **Número de ríos** - RFSv2 tenía alrededor de 6.8 millones de ríos, pero RFSv3 se redujo a aproximadamente 4.9 millones. Estos recortes provienen principalmente de la eliminación de ríos en grandes desiertos; se eliminaron ríos del desierto del Sahara, del desierto de Gobi y de los desiertos del centro de Australia. También se eliminaron los segmentos de río ubicados dentro de lagos o en pequeñas cuencas costeras (o en el océano). Además, algunos ríos más pequeños se fusionaron. Los identificadores (IDs) de los ríos se mantuvieron iguales en el modelo. Si el ID de su río ya no está disponible y no se encuentra en una zona eliminada, puede relacionarlo con el nuevo río de RFSv3. La correspondencia entre los IDs de río antiguos y nuevos está disponible en el archivo [tdxhydro_to_v3_id_map.parquet](https://v3.s3.riverforecastsystem.com/hydrography/global/tdxhydro_to_v3_id_map.parquet) (aproximadamente 87 MB).
    2. **Regiones** - Los datos de hidrografía ya no están organizados en 125 VPUs. En su lugar, ahora están organizados en 47 regiones numeradas a partir de sus cuencas de nivel 2 de HydroSHEDS.
    3. **Lagos** - El conjunto de datos de hidrografía muestra un nuevo conjunto de lagos. Este es diferente de los lagos que estaban disponibles en RFSv2.
2. **Formatos de almacenamiento de datos** - Los archivos zarr ahora utilizan la versión 3 de zarr en lugar de la versión 2. Se agregaron más metadatos a los archivos y el almacenamiento se optimizó aún más.
3. **Cambios en los procesos de enrutamiento** - El proceso que enruta el agua a través de los ríos se actualizó para depender completamente de un paquete de Python llamado riverroute, desarrollado por el Dr. Riley Hales. El proceso se actualizó para ejecutarse más rápido y se hicieron algunas correcciones menores a algunas de las entradas del modelo.
4. **Nuevos buckets de AWS** - Un nuevo bucket de AWS contiene todos los datos de la versión 3 del modelo. Se puede encontrar aquí: [https://v3.s3.riverforecastsystem.com](https://v3.s3.riverforecastsystem.com).
5. **Nuevas Aplicaciones Web**
    1. HydroSOS
    2. FEWS
6. **Productos de mapeo de inundaciones**
7. **Almacén de datos** - Hay un nuevo almacén de datos disponible para descargar los productos de RFSv3: [https://apps.geoglows.org/previews/rfs-data-store/](https://apps.geoglows.org/previews/rfs-data-store/). Este sitio proporciona metadatos e información sobre los datos disponibles y permite a los usuarios explorar y descargar los productos de datos de su interés. Consulte [El Almacén de Datos](what-is-it/using-datastore.md) para obtener instrucciones sobre cómo usarlo.
8. **Cambios en este sitio** - Este sitio se actualizó y reorganizó. Parte de la información más avanzada se trasladó a una sección avanzada. También se agregó información sobre aguas subterráneas.

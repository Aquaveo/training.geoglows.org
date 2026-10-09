## Términos y Vocabulario

- **Hidrografía**: Conjuntos de datos SIG de elementos hidrológicos como ríos, puntos de confluencia, límites de cuencas, límites de cuencas hidrográficas, límites
  de lagos y otros elementos.
- **Hydrofabric**: hidrografía.
- **TanDEM-X**: Misión satelital SAR del Centro Aeroespacial Alemán (DLR) y Airbus Defence and Space. Se utiliza para producir un modelo digital de
  elevación de 12 metros, que es el producto global de su tipo con la mayor precisión y resolución. No está disponible públicamente, pero sí lo están los productos
  Copernicus Glo30 y FABDEM derivados de él.
- **TDX-Hydro**: Conjunto de datos de líneas centrales de ríos y límites de cuencas producido por la Agencia Nacional de Inteligencia Geoespacial (NGA) en 2023. Los ríos se
  delinearon a partir de datos de elevación TanDEM-X de 12 metros usando TauDEM, con un extenso preprocesamiento de la elevación y un posprocesamiento de corrección
  de la ubicación de las líneas centrales de los ríos.
- **TauDEM**: Herramienta de análisis de terreno utilizada para delinear ríos y cuencas a partir de datos de elevación.
- **Región**: Grupo de una o más cuencas hidrográficas completas agrupadas para dividir el conjunto de datos global de hidrografía en partes más pequeñas y facilitar
  la distribución de datos, la división de los cálculos y la elaboración de mapas. Las regiones se numeran según su ID de cuenca de nivel 2 de HydroBASINS. RFS V2 utilizaba en su lugar 125 partes
  más pequeñas llamadas VPUs (Vector Processing Units, Unidades de Procesamiento Vectorial).
- **River ID**: Identificador único para cada línea central de río en el conjunto de datos de hidrografía de RFS. Los programas SIG e hidrológicos suelen tener diferentes
  nombres para este ID. Por ejemplo, TauDEM y TDX-Hydro lo llaman "link number" (LINKNO) y el software de Esri lo llama "common identifier" (COMID). En
  RFS, se denomina River ID y se almacena en el atributo riverId. Cualquier referencia a LINKNO, COMID, ReachID, StreamID, RiverID o cualquier
  término similar debe entenderse como lo mismo.
- **Orden de Strahler**: Número para clasificar ríos topológicamente. Los ríos más pequeños son de orden 1 y, cuando dos ríos de orden 1 se unen,
  forman un río de orden 2. Cuando dos ríos de orden 2 se unen, forman un río de orden 3, y así sucesivamente. En TDX-Hydro, el orden máximo es 9.

---

## Descripción General

La hidrografía de RFS es una modificación del conjunto de datos de ríos y cuencas TDX-Hydro. Proviene de datos de elevación propietarios de TanDEM-X con una resolución de 12 metros. Puede
descargar el conjunto de datos completo y revisar el documento técnico completo que describe su creación en https://earth-info.nga.mil/, en la pestaña "Geosciences". El conjunto completo de datos TDX-Hydro contiene aproximadamente 16 millones de segmentos de río y cubre todo el planeta en 62 partes que corresponden al nivel 2 de
HydroBASINS. Omitimos 12 regiones que representan islas o las zonas terrestres más al norte. Además, muchas revisiones para reducir la cantidad de elementos de río
y optimizar la red para el enrutamiento en canales redujeron el número total de ríos a 4.9 millones. Esta versión utilizada en RFS está
disponible para que los usuarios la descarguen y la usen para sus propios fines. Este conjunto de datos se conoce como hidrografía, hydrofabric o red de ríos. Son
datos vectoriales con puntos y líneas con coordenadas, no datos en cuadrícula, e incluyen cuatro componentes principales:

- Las **líneas centrales de los ríos** exactas utilizadas en RFS. Cada río tiene un ID único de 9 dígitos, denominado reachID, número de enlace (link number) o ID de río.
  Este es el archivo llamado "streams_{region}.geo.parquet".
- Los **límites de las cuencas** utilizados en RFS. Son los límites alrededor de cada línea central de río y representan el área conectada a esa línea.
  Se identifican usando el mismo ID de río que las líneas centrales de los ríos. Este es el archivo llamado "catchments_{region}.geo.parquet". Cada línea
  central de río corresponde exactamente a un límite de cuenca único.
- Los **puntos de conexión** utilizados en RFS donde se conectan diferentes líneas centrales de río. Cada punto tiene un atributo llamado riverId, que representa
  el único ID del río aguas abajo de cada punto. Tiene otro atributo llamado upstream_ids, que es una lista de los IDs de los ríos
  aguas arriba del punto de conexión. Este es el archivo llamado "confluences_{region}.geo.parquet".
- Las **cuencas de lagos fusionadas** utilizadas en RFS para representar la ubicación de los lagos. Las cuencas de los ríos que, mediante búsquedas en SIG, se identificaron como
  parte de un lago se fusionaron para representar los lagos. Por lo tanto, su forma será diferente del límite real del lago, ya que depende de las formas de las
  cuencas de los ríos fusionadas.

---

## Regiones

Los datos SIG están divididos en 47 partes más pequeñas, llamadas regiones. Esto facilita la gestión y el acceso a la gran cantidad de datos. Cada región representa una o
más cuencas hidrográficas completas y se numera según su ID de cuenca de nivel 2 de HydroBASINS.

Los límites de las regiones también están disponibles para su descarga (el archivo "regions.geo.parquet", o "boundary_{region}.geo.parquet" para una sola región) para ayudar a
identificar qué región incluye el área de interés de un usuario. Los demás conjuntos de datos SIG deben descargarse según la región de interés y se
descargan como una región completa.

---

## Metadatos Disponibles

Los ríos de V3 tienen los siguientes atributos, muchos de los cuales provienen del proceso de delineación de TauDEM. Para obtener más explicación sobre estos atributos, consulte
la [Documentación de TauDEM](https://hydrology.usu.edu/taudem/taudem5/help53/StreamReachAndWatershed.html){:target="_blank"}.

| Atributo        | Fuente    | Descripción                                                                                                         |
|-----------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| riverId         | TDX-Hydro | Un número de ID de 9 dígitos, único a nivel mundial, para ese río (el LINKNO de TDX-Hydro).                         |
| nextRiverId     | TDX-Hydro | El ID (riverId) del río inmediatamente aguas abajo de ese río, o -1 en una salida.                                  |
| outletRiverId   | RFS V3    | El ID del río de salida final al que drena la cuenca de este río.                                                   |
| riverIndex      | RFS V3    | La posición del río en el orden topológico (de la cabecera a la salida). Los archivos retrospectivos y de pronóstico usan el mismo orden. |
| upstreamCount   | RFS V3    | El número total de ríos aguas arriba de ese río. Todos ellos se encuentran desde riverIndex − upstreamCount hasta riverIndex. |
| strahlerOrder   | TDX-Hydro | El orden de Strahler.                                                                                               |
| shreveOrder     | RFS V3    | La magnitud de Shreve.                                                                                              |
| USContArea      | TDX-Hydro | El área de drenaje total aguas arriba del punto más aguas arriba, en metros cuadrados.                              |
| DSContArea      | TDX-Hydro | El área de drenaje total aguas arriba del punto más aguas abajo, en metros cuadrados.                               |
| areaM2          | RFS V3    | El área de la cuenca propia del río, en metros cuadrados.                                                           |
| Length          | RFS V3    | La longitud del río, en metros.                                                                                     |
| TDXHydroRegion  | RFS V3    | La región de nivel 2 de HydroBASINS a la que pertenece el río.                                                      |
| musk_k          | RFS V3    | El parámetro k de Muskingum utilizado para el enrutamiento fluvial.                                                 |
| musk_x          | RFS V3    | El parámetro x de Muskingum utilizado para el enrutamiento fluvial.                                                 |
| velocity_factor | RFS V3    | El factor de escala de velocidad utilizado para calcular musk_k.                                                    |

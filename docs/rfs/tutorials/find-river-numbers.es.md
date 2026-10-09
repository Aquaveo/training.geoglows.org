## Visión General

Hay 4.9 millones de segmentos de río modelados en los conjuntos de datos de RFS V3. Estos números provienen del conjunto de datos TDX-Hydro y son diferentes de los números de cualquier otro conjunto de datos de ríos. RFS V3 utiliza los mismos IDs de río que RFS V2, pero algunos ríos de V2 se eliminaron o se fusionaron en V3 (consulte
[Novedades](../whats-new.md) para obtener más detalles y un archivo que relaciona los IDs antiguos con los nuevos). Todos los números de ID tienen 9 dígitos. Como referencia, esta tabla proporciona los IDs de algunos
ríos principales y sus ubicaciones generales.

| Número de ID | Ríos seleccionados y ubicaciones generales |
|--------------|--------------------------------------------|
| 760021611    | Mississippi, EE. UU.                       |
| 160064246    | Nilo, África Oriental                      |
| 710462910    | Colorado, EE. UU. y México                 |
| 441057380    | Ganges, India                              |
| 430157411    | Mekong, Vietnam                            |
| 210406913    | Tíber, Italia                              |
| 621010293    | Amazonas, Brasil                           |
| 130747391    | Congo, República Democrática del Congo     |
| 640255644    | Paraná, Argentina                          |

Los números de ID de RFS tienen 9 dígitos. Aunque los números grandes a menudo se delimitan, comúnmente con una coma o un punto según el idioma, cualquier código que escriba
para obtener datos ***no debe*** incluir delimitadores. Estos IDs son números enteros. La mayoría de los lenguajes de programación interpretarán las comillas, los puntos, las comas
u otros caracteres como algo distinto a un entero, lo que hará que el proceso de obtención falle. Por ejemplo, el número `123456789` ***no debe***
escribirse como `123,456,789` ni `123.456.789` ni `"123456789"` ni `"123,456,789"` ni ninguna otra variación. Solo la representación entera `123456789`
funcionará.

## Uso de la Aplicación Web

La forma más fácil de encontrar el ID de un río es utilizar la [aplicación web de RFS](https://apps.geoglows.org/rfs){:target="_blank"}. Haga clic en un río en
el mapa. Para asegurarse de hacer clic exactamente en el río que desea, el mapa se acercará a un nivel de detalle mayor si está demasiado alejado. Después de
hacer clic en un río, el mapa identificará el segmento de río en el que hizo clic y el ID se le presentará en la ventana emergente con gráficos
y otra información.

## Uso de los Datos de Hidrografía

Los datos de hidrografía están disponibles en el [almacén de datos de RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}. Puede descargar y ver
los ríos o las cuencas en un software SIG como ArcGIS o QGIS. Puede hacer clic en los elementos o usar herramientas de análisis espacial para seleccionar muchos ríos. Los
números de ID de esos ríos se almacenan en el atributo riverId.

## Encontrar Ríos con Lat/Lon

Existen muchos métodos para intentar encontrar el ID de un río a partir de una latitud y una longitud. Ninguno es perfecto para todos los casos. Los métodos automatizados pueden presentar varios
errores potenciales debido a la exactitud y precisión de sus puntos lat/lon, la exactitud de las líneas de los ríos en esa ubicación específica,
si desea ajustarse a la salida más cercana o al arco de río más cercano, si su punto lat/lon está cerca de una confluencia donde el SIG podría confundirse al tener
varias opciones cercanas, etc. Los métodos automatizados deben considerarse imperfectos y su exactitud debe verificarse con otras fuentes, como un área de drenaje aguas arriba
conocida en el lat/lon de un punto de aforo, el nombre del río, comparaciones con mapas base de imágenes u otros medios.

Un método para comenzar es cargar en un software SIG los archivos SIG de los ríos de su área de interés. Puede ajustar sus puntos al arco de río más cercano. 
En QGIS, la herramienta se llama "Snap geometries to layer" (Ajustar geometrías a capa). Use el algoritmo para encontrar el punto más cercano e insertar vértices adicionales si es necesario.

Otro método es descargar los polígonos de las cuencas e intersecarlos con una capa que contenga sus puntos lat/lon. El trabajo en SIG es sencillo, 
pero en ocasiones es menos preciso y requiere descargar archivos más grandes.

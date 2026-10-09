## Descargar datos de pronóstico de RFS para mi río

Si solo necesita descargar datos de algunos ríos o no desea escribir código, ¡use la aplicación web! Nuestras aplicaciones le permiten explorar gráficamente
un mapa de ríos, ver y descargar datos de pronóstico o retrospectivos, comparar pronósticos con las imágenes satelitales más recientes y
encontrar enlaces a más información. Visite [apps.geoglows.org/rfs](https://apps.geoglows.org/rfs){:target="_blank"} para comenzar.

## Obtener una lista de IDs en mi cuenca

Cada río del modelo RFS tiene un atributo llamado "TerminalLink". El TerminalLink es el número de ID del río en la salida de la
cuenca en la que se encuentra un río de interés determinado. Todos los ríos de la cuenca tienen la misma salida. Puede filtrar la tabla de ríos para seleccionar solo aquellos
que drenan hacia el mismo río. Puede usar los conjuntos de datos SIG y realizar esta operación en ArcGIS o QGIS. Puede encontrar enlaces para obtener los archivos SIG
de los ríos en la página de Datos Disponibles y en el tutorial sobre cómo Encontrar Números de Río. Alternativamente, puede hacerlo mediante código utilizando las tablas de
metadatos de RFS, a través de la tabla de metadatos del modelo. Necesitará descargar esa tabla (aproximadamente 250 MB) para resolver este problema mediante código.

<script src="https://gist.github.com/rileyhales/e94f0c51090f26bc396e2289d41edefd.js"></script>

## Obtener el pronóstico de muchos ríos

El paquete de Python geoglows le permite solicitar datos de muchos ríos simultáneamente. No necesita usar bucles for en su código para hacer
solicitudes secuenciales de datos de un solo río. Prepare una lista con todos los números de ID de los ríos de los que desea obtener datos. Por ejemplo, podría obtener una
lista de todos los ríos de una cuenca (consulte el tutorial en esta página). Al usar el paquete de Python geoglows, puede pasar esa lista completa de ríos a las
funciones para obtener los datos.

<script src="https://gist.github.com/rileyhales/963be8a9cbbc179d99ed82fd5c61bf46.js"></script>

## Guardar el conjunto de datos de registros de pronóstico

Se generan nuevos pronósticos diariamente. Los caudales promedio del ensamble que se predice que ocurrirán en las 24 horas entre un pronóstico y el siguiente se archivan cada día al
inicio de una nueva simulación de pronóstico. Este conjunto de datos se conoce como el registro de pronóstico. Se actualiza continuamente cada día. Este conjunto de datos no se
archiva en un bucket de AWS. Solo está disponible a través del servicio REST para facilitar la creación de gráficos sobre la marcha. Sin embargo, la predicción completa de caudal
del ensamble se guarda todos los días.

No escriba código que recorra una lista de ríos y descargue los registros de pronóstico cada día. Esto supone una carga para el servicio REST y
no es tan rápido ni eficiente si el número de ríos es grande. Si desea descargar una copia de estos registros, puede obtenerlos desde AWS, donde se guarda cada día el pronóstico
completo del ensamble, y calcularlos utilizando las herramientas disponibles en el paquete de Python geoglows.

<script src="https://gist.github.com/rileyhales/11ac6df64593dabb641ad9f044b23e37.js"></script>

## Guardar una copia local de los datos de pronóstico o retrospectivos

Muchos usuarios desean mantener copias de los nuevos pronósticos en sus propios dispositivos. En particular, algunos usuarios necesitan descargar los datos para poder moverlos a
un entorno de cómputo seguro o a un centro de cómputo de alto rendimiento. Puede usar el paquete de Python geoglows para obtener datos de pronóstico o retrospectivos
y guardar una copia.

<script src="https://gist.github.com/rileyhales/ec78fa1c1d6453c407faee8d9c72acea.js"></script>

De forma predeterminada, los datos se descargan como un DataFrame (datos tabulares). Tiene muchas opciones para guardar DataFrames en disco, como Parquet, CSV o Excel. Si
almacena tablas grandes de datos, como caudales retrospectivos o de pronóstico por ensamble para muchos ríos, recomendamos el formato Parquet. Será
más rápido de leer y escribir, además de estar más comprimido que muchos otros formatos.

Los usuarios más avanzados también pueden obtener los datos como un Dataset de Xarray, adecuado para datos de mayor dimensión y formatos de archivo como netCDF o Zarr.
También puede guardar conjuntos de datos de Xarray en disco en varios formatos. El formato adecuado depende del caso de uso previsto. Para especificar el formato de los datos a
descargar, use format='df' para obtener tablas de datos (DataFrames) o format='xarray' para obtenerlos como un conjunto de datos
multidimensional. La mayoría de los usuarios debería usar el formato predeterminado, DataFrame.

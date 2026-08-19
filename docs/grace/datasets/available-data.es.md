## Componentes de Almacenamiento

Hay cuatro componentes de almacenamiento disponibles para visualizar y descargar. Todos son anomalías —una desviación respecto a un promedio de largo
plazo— y no cantidades absolutas.

| Nombre | Abreviatura | Fuente |
|--------|-------------|--------|
| Anomalía del Almacenamiento Total de Agua | TWSa | GRACE |
| Anomalía del Equivalente de Agua en Nieve | SWEa | GLDAS |
| Anomalía de la Humedad del Suelo | SMa | GLDAS |
| Anomalía del Almacenamiento de Agua Subterránea | GWSa | Calculada |

Se enumeran aquí en el orden en que aparecen en el balance de masa: el total de GRACE, los componentes superficiales que se le restan y el resultado
de agua subterránea. La Anomalía del Almacenamiento de Agua Subterránea se calcula en lugar de observarse; consulte
[Derivación del Agua Subterránea](../understanding/computational-algorithm.md#derivacion-del-agua-subterranea).

## Resolución de la Cuadrícula

Los componentes se calculan sobre celdas de balance hídrico, que son de 1.0 grado de forma predeterminada. En la configuración de la aplicación está
disponible una opción de medio grado. Al cambiar entre ellas, el mapa y el análisis actual se recargan a partir del otro conjunto de datos, y las
celdas más finas tardan más en prepararse.

Los datos de GRACE se proporcionan originalmente en celdas de 3 grados conocidas como mascons, antes de ser reducidos de escala a las celdas de
anomalía de 1.0 y 0.5 grados. Tanto las huellas de los mascons como los límites de las celdas de anomalía pueden mostrarse en el mapa desde la
configuración de la aplicación.

Para conocer cómo se cuadriculan y se reducen de escala los datos brutos, consulte
[Derivación del Agua Subterránea](../understanding/computational-algorithm.md#derivacion-del-agua-subterranea).

## Unidades y Línea Base

Los valores son anomalías expresadas en altura de agua equivalente. Cada componente de GLDAS se convierte a formato de anomalía restando la media
centrada en los valores de 2004 a 2009.

## Cobertura Temporal

GRACE ha generado soluciones mensuales del campo gravitatorio desde abril de 2002. El recorte regional produce una serie temporal desde 2002 hasta el
presente para cada componente, con un paso de tiempo mensual.

## Vacíos en los Datos

Si se inspecciona con atención el archivo de la serie temporal de almacenamiento de agua subterránea, se observará que faltan varios meses o hay
vacíos en los datos. Por ejemplo, falta el mes de junio de 2003. Esto se debe a que hubo periodos en los que los satélites GRACE no produjeron datos
utilizables.

El vacío más grande es un periodo de 12 meses en 2017-2018, entre el final de la misión GRACE original en 2017 y el momento en que los satélites
GRACE-FO posteriores fueron lanzados y entraron en operación en 2018.

En los años con vacíos grandes puede resultar difícil identificar tendencias estacionales y aplicar el método de Fluctuación del Nivel Freático. Una
manera de resolver este problema es utilizar un algoritmo estadístico para detectar patrones estacionales en los datos e imputar datos sintéticos en
los vacíos; ese método y la herramienta para aplicarlo se describen en
[Relleno de Vacíos en los Datos](../applications/water-table-fluctuation.md#vacios-en-los-datos-de-grace).

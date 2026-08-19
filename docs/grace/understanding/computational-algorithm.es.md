## Descripción General

Las anomalías de almacenamiento derivadas de GRACE se basan en los datos de observación de la Tierra recopilados por la NASA mediante satélites que
cartografían el campo gravitatorio terrestre. Los cambios en la gravedad están impulsados por cambios en el almacenamiento de agua, lo que ofrece una
oportunidad poco común de monitorear el nivel del agua subterránea mediante satélites, combinada con estimaciones del agua superficial.

Esta página describe cómo se separa el componente de agua subterránea de esa medición mediante un enfoque de balance de masa, y cómo el resultado se
recorta a una región de interés. Para conocer el contexto de los datos y la aplicación que los ofrece, consulte
[Descripción General](overview.md).

## Cómo Funciona la Medición

La misión GRACE se lanzó en marzo de 2002. Consiste en un par de satélites situados a 400 km sobre la Tierra y separados entre sí por 200 km. A medida
que los satélites pasan sobre distintas regiones de la Tierra, el satélite delantero y el trasero son atraídos ligeramente hacia adelante y hacia
atrás en respuesta a cambios sutiles en el campo gravitatorio terrestre provocados por variaciones de la masa superficial. Esto hace que la distancia
entre los satélites varíe, y los cambios se registran mediante un sistema de microondas de banda K con una precisión de hasta 10 micras.

![Representación artística de los satélites gemelos, con el enlace de medición de distancia entre ellos](../../static/images/grace-satellites.jpg)

*Crédito de la imagen: NASA/JPL-Caltech*

Los satélites GRACE siguen una trayectoria variable que cubre toda la Tierra aproximadamente una vez al mes. Estos datos son procesados luego por la
NASA para producir un mapa del campo gravitatorio terrestre. Cada mes se genera un mapa nuevo y se calculan las diferencias para producir un mapa de
anomalías de gravedad. Se asume que los cambios de masa se deben principalmente a la variación del almacenamiento de agua.

Cada mes la NASA genera un mapa cuadriculado de la anomalía del almacenamiento total de agua con una resolución de 3 grados. Ese mapa se reduce luego
de escala mediante un algoritmo de conservación de masa a una resolución de 0.5 grados y se pone a disposición para su descarga en formato ráster
multidimensional netCDF.

## Derivación del Agua Subterránea

El componente de agua subterránea de los datos brutos de GRACE puede separarse mediante un enfoque de balance de masa, utilizando los modelos del
Sistema Global de Asimilación de Datos Terrestres (GLDAS) de la NASA para calcular el componente de agua superficial de los datos. Para calcular el
almacenamiento total de agua superficial, se suman los componentes de los modelos GLDAS que representan el almacenamiento de agua superficial y se
restan del conjunto de datos de GRACE, con el fin de estimar un conjunto de datos de anomalía del almacenamiento de agua subterránea.

La aplicación utiliza cuatro conjuntos de datos:

- El conjunto de datos TWSa de GRACE
- El conjunto de datos de almacenamiento en el dosel vegetal de GLDAS (CAN)
- El equivalente de agua en nieve de GLDAS (SWE)
- La humedad del suelo de GLDAS (SM)

Cada componente de GLDAS se convierte a formato de anomalía restando la media centrada en los valores de 2004 a 2009, y luego se promedia entre los
tres modelos GLDAS para producir un conjunto de datos de anomalías por componente: CANa, SWEa y SMa. La desviación estándar de los tres modelos GLDAS
se utiliza para ayudar a estimar la incertidumbre.

Los datos de GLDAS se obtienen normalmente en formato cuadriculado con una resolución de 1 grado de latitud por 1 grado de longitud, mientras que la
TWSa de GRACE se distribuye a 0.5 grados. La conciliación de ambas cuadrículas se realiza mediante un promedio ponderado por área de las cuatro celdas
de la cuadrícula de GRACE que coinciden con cada celda de la cuadrícula de GLDAS.

Los componentes pueden calcularse sobre celdas de 1 grado, que es la opción predeterminada, o sobre celdas de medio grado, seleccionadas en la
configuración de la aplicación. Consulte [Resolución de la Cuadrícula](../datasets/available-data.md#resolucion-de-la-cuadricula).

La anomalía del agua subterránea es la diferencia entre la TWSa y la suma de las anomalías de los componentes de agua superficial:

```
GWa = TWSa - (SWEa + CANa + SMa)
```

El resultado de este cálculo es la anomalía del almacenamiento de agua subterránea, un método probado y aprobado para predecir cambios a largo plazo
en el almacenamiento de agua subterránea.

## Recorte de la Cuadrícula

Para el recorte regional, el usuario proporciona un límite que define la región de interés. La aplicación selecciona las celdas cuyo centro se
encuentra dentro del límite definido y calcula la anomalía media de almacenamiento para cada uno de los componentes —TWSa, SWEa, CANa y SMa—, lo que
da como resultado una serie temporal desde 2002 hasta el presente para cada componente, con un paso de tiempo mensual.

La siguiente figura muestra la cuenca del Chad en Níger recortada y representada junto con el límite de la región. Solo se incluyen en el promedio las
celdas cuyos centros caen dentro del límite.

![La cuenca del Chad en Níger, recortada y representada con el límite de la región](../../static/images/grace-subsetted-region.png)

Para el almacenamiento de agua, el promedio de cada componente se multiplica por el área de la región, lo que da como resultado anomalías de volumen.

### Tamaño de la Región

Se recomienda que una región tenga al menos 3x3 grados de tamaño. Se pueden procesar regiones más pequeñas, pero la incertidumbre de los resultados
aumenta. Esto se debe a que las celdas nativas de la cuadrícula de GRACE tienen una resolución de 3x3 grados antes de reducirse de escala a 0.5x0.5
grados. Las celdas de la cuadrícula de GLDAS son de 1x1 grado y, por lo tanto, las celdas resultantes de la Anomalía del Almacenamiento de Agua
Subterránea (GWSa) tienen una resolución de 1x1 grado.

El algoritmo examina las celdas globales de las cuadrículas de GRACE y GLDAS para encontrar aquellas cuyo centroide cae dentro del límite de la
región. Si la región es tan pequeña que no se encuentra ninguna celda, se muestra un mensaje de error.

### Análisis en un Solo Punto

Además de analizar el cambio del almacenamiento de agua subterránea promediado sobre una región, la aplicación puede utilizarse para realizar un
análisis en la ubicación de un solo punto. Esto sirve para generar rápidamente una serie temporal en un punto de interés, o en los casos en que la
región de interés es demasiado pequeña para procesarse como región.

Para un análisis puntual, la aplicación localiza las celdas de las cuadrículas de GRACE y GLDAS que contienen el punto seleccionado y devuelve la
serie temporal del conjunto de datos elegido para esa celda. Si se está visualizando una región, el punto seleccionado debe estar dentro de los
límites de dicha región.

## Estimaciones de Incertidumbre

Es fundamental comprender que los resultados de estas predicciones tienen incertidumbres y limitaciones.

Para calcular la incertidumbre del componente de almacenamiento de agua subterránea, las estimaciones de incertidumbre de GRACE y de GLDAS se combinan
calculando la raíz cuadrada de la suma de los cuadrados de la incertidumbre de cada componente, medida a través de sus desviaciones estándar.

```
σGWa = √[(σTWSa)² + (σSWEa)² + (σCANa)² + (σSMa)²]
```

<!-- NOTE: the GGST source states this in prose as "the square root of the sum of the squares", but its
     rendered equation shows the terms SUBTRACTED:
     \sigma GWa = \sqrt {(\sigma TWSa)^2 - (\sigma SWEa)^2 - (\sigma CANa)^2 - (\sigma SMa)^2}
     The prose and the equation contradict each other in the source. We have written the sum-of-squares
     form here because it matches the prose and is the physically standard result; the subtracted form
     can go negative. Confirm with Norm Jones before publishing. -->

Las estimaciones resultantes de los datos de agua subterránea no son adecuadas para aplicaciones de alta precisión o de carácter local, como la
ubicación de pozos; más bien, estos datos sirven como una estimación de las tendencias generales del almacenamiento de agua subterránea.

## Curva de Agotamiento del Almacenamiento

La aplicación ofrece la opción de visualizar los datos de la serie temporal en forma de curva de agotamiento del almacenamiento, que es la integral en
el tiempo de la anomalía de almacenamiento.

La curva de agotamiento del almacenamiento presenta los cambios acumulados en el almacenamiento de los componentes de agua respecto a los niveles
existentes cuando las misiones GRACE comenzaron a distribuir datos en abril de 2002. Esta curva se utiliza en la gestión del agua subterránea porque
ofrece una visualización sencilla de cuánto almacenamiento han ganado o perdido los acuíferos desde un momento determinado.

Para calcular el agotamiento, la aplicación suma la GWSa a lo largo del tiempo con el fin de determinar los cambios en el volumen de almacenamiento de
agua subterránea de la región. Estos datos muestran si una región está agotando su almacenamiento o si el agua subterránea se está recargando, lo que
aporta información valiosa sobre la sostenibilidad del agua subterránea.

Una ilustración del norte de África y la península arábiga de 2002 a 2021 muestra que el agua subterránea de esa región se ha ido agotando desde
principios de 2009 en adelante.

![Curva de agotamiento del almacenamiento para la región árabe, 2002 a 2021](../../static/images/grace-depletion-curve.png)

## Limitaciones

Los datos de GRACE presentan limitaciones que los usuarios deben conocer y comprender. Los datos se proporcionan con una resolución relativamente baja
(1 grado de latitud por 1 grado de longitud), que representa aproximadamente un cuadrado de 100 km x 100 km. Con una resolución tan baja, basar
decisiones en una sola celda conlleva incertidumbres altas y desconocidas. Los datos brutos de GRACE tienen una resolución aún más gruesa (3 grados de
latitud por 3 grados de longitud), que luego se procesa para obtener datos TWSa de mayor resolución.

Incluso con estas limitaciones, los datos de GRACE aportan información valiosa sobre los acuíferos, como qué regiones se están agotando y cuáles se
están recargando, lo que permite a los gestores utilizar de forma sostenible sus recursos de agua subterránea. El mejor uso de la aplicación es
identificar tendencias generales en los acuíferos, y no seleccionar la ubicación de un pozo.

También se recomienda que, siempre que sea posible, estos datos se validen con datos locales. La aplicación muestra las incertidumbres de los cálculos
como bandas de error en las series temporales, aportando contexto sobre distintas regiones y periodos de tiempo.

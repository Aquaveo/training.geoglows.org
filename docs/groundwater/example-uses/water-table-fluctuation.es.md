## Descripción General

Además de obtener la anomalía del almacenamiento de agua subterránea derivada de GRACE, es posible analizar la serie temporal de anomalías de
almacenamiento para extraer una estimación de la recarga anual mediante una técnica denominada método de Fluctuación del Nivel Freático (WTF, por sus
siglas en inglés).

El método WTF se desarrolló originalmente para estimar la recarga a partir de las fluctuaciones estacionales de los niveles de agua subterránea
medidos directamente en pozos de monitoreo. Cuando una serie temporal de niveles de agua presenta fluctuaciones estacionales como las que se muestran
a continuación, se asume que el periodo de descenso durante la parte seca del año se debe al bombeo y a la descarga de agua subterránea, y que el
ascenso durante la parte húmeda del año es resultado de la recarga.

![Fluctuación estacional en una serie temporal de nivel de agua subterránea](../../static/images/wtf-seasonal-fluctuation.png)

Utilizando los niveles de agua obtenidos de un pozo de monitoreo, la recarga puede estimarse de la siguiente manera:

```
R = Sy × (Δh / t)
```

donde Δh es el ascenso del nivel de agua, t es el periodo de tiempo (normalmente un año) y Sy es el rendimiento específico o el coeficiente de
almacenamiento correspondiente.

El coeficiente de almacenamiento es necesario porque el ascenso del nivel de agua en el acuífero circundante se produce en el espacio de poros, y el
coeficiente lo convierte al componente de equivalente de agua líquida apropiado, en las unidades de tasa de infiltración [longitud]/[tiempo] que se
utilizan para la recarga. Si este análisis se realiza utilizando la curva de anomalías del almacenamiento de agua subterránea derivada de GRACE, no es
necesario utilizar un coeficiente de almacenamiento, ya que la anomalía se expresa de por sí en equivalente de agua líquida, y la recarga puede
estimarse directamente como:

```
R = ΔGWSa / Δt
```

donde ΔGWSa es el ascenso del agua subterránea extraído de la curva de anomalías del almacenamiento de agua subterránea derivada de GRACE.

## Métodos para Estimar el Componente de Recarga

Existen dos enfoques generales para determinar la magnitud del ascenso asociado a la recarga:

![Definición de Sp, SB y SL en un ciclo estacional, con los componentes RS y RD](../../static/images/wtf-rs-rd-fig.png)

Con el método más conservador, el ascenso se mide desde el valle hasta el siguiente pico, de la siguiente manera:

```
R_método_1 = ΔGWSa / Δt = (Sp - SB) / Δt = RS
```

Otro método consiste en suponer que el descenso del agua subterránea provocado por el bombeo y la descarga continúa al mismo ritmo durante la
temporada húmeda y que, por lo tanto, el ascenso debe calcularse a partir de una extrapolación lineal de la línea de descenso, de la siguiente manera:

```
R_método_2 = ΔGWSa / Δt = (Sp - SL) / Δt = RS + RD
```

Las tasas de recarga obtenidas con estas dos ecuaciones pueden considerarse una estimación baja y una alta, aunque según la experiencia de los autores
el método 1 parece ser el más preciso. Un ejemplo de aplicación del método WTF para estimar la recarga en el sur de Níger puede consultarse en
[Evaluating Groundwater Storage Change and Recharge Using GRACE Data: A Case Study of Aquifers in Niger, West Africa](https://www.mdpi.com/2072-4292/14/7/1532){:target="_blank"}.

## Descarga de la Serie Temporal del Nivel de Agua

Para aplicar el método WTF y estimar la recarga con datos de GRACE, primero es necesario descargar la serie temporal de anomalías del almacenamiento
de agua subterránea. Cargue la región, seleccione el componente Anomalía del Almacenamiento de Agua Subterránea y descargue el CSV. Los pasos y el
formato del archivo se describen en
[Visualización y Descarga de Resultados](../accessing-data/web-app.md#visualizacion-y-descarga-de-resultados).

## Vacíos en los Datos de GRACE

Si se inspecciona con atención el archivo CSV de la serie temporal de almacenamiento de agua subterránea, se observará que faltan varios meses o hay
vacíos en los datos. Por ejemplo, falta el mes de junio de 2003:

![Un mes faltante en la serie temporal descargada](../../static/images/grace-excel-download.png)

Esto se debe a que hubo periodos en los que los satélites GRACE no produjeron datos utilizables. El vacío más grande es un periodo de 12 meses en
2017-2018, entre el final de la misión GRACE original en 2017 y el momento en que los satélites GRACE-FO posteriores fueron lanzados y entraron en
operación en 2018. A continuación se muestra un gráfico de ejemplo para un acuífero del sur de Níger con los vacíos señalados:

![Serie temporal de un acuífero del sur de Níger con los vacíos señalados](../../static/images/wtf-niger-gaps.png)

En los años con vacíos grandes puede resultar difícil identificar tendencias estacionales y aplicar el método WTF. Una manera de resolver este
problema es utilizar un algoritmo estadístico para detectar patrones estacionales en los datos e imputar datos sintéticos en los vacíos. Esto puede
lograrse con un modelo sencillo de descomposición estacional (`statsmodels.tsa.seasonal.seasonal_decompose`) implementado en el paquete de Python
statsmodels. Este modelo elimina primero la tendencia mediante un filtro de convolución (el componente de tendencia), luego calcula el valor promedio
de cada periodo (el componente estacional), en este caso los meses, siendo el componente residual la diferencia entre el promedio mensual (componente
estacional) y las mediciones mensuales reales. Con este enfoque, la serie temporal de GWSa se descompone en tres componentes: la tendencia, el
estacional y el aleatorio:

```
Y[t] = T[t] + S[t] + e[t]
```

Donde Y[t] es la GWSa, T[t] es la tendencia de la GWSa, S[t] es el componente estacional de la GWSa y e[t] es el componente residual de la GWSa. Los
componentes de la descomposición para los datos mostrados arriba se ilustran a continuación:

![Descomposición estacional en componentes de tendencia, estacional y residual](../../static/images/wtf-decomposed.png)

Para imputar los datos faltantes se utiliza la tendencia obtenida de la descomposición y se le suma el promedio de los valores mensuales y residuales
de ese mes, con el fin de estimar el valor faltante. Este modelo puede expresarse como:

```
Y[t] = y(T[t]) + mean(S[t] + e[t])
```

La siguiente figura muestra la serie temporal original en negro, con los valores imputados en rojo:

![Serie temporal original en negro con los valores imputados en rojo](../../static/images/wtf-imputed.png)

## Herramientas de Imputación de Datos

Para ayudar a los usuarios a aplicar el método de statsmodels descrito anteriormente y así imputar los vacíos en los datos de GRACE, el código de
Python que realiza la imputación está implementado en un cuaderno de Google Colab. Después de abrir el cuaderno, siga las instrucciones incluidas en
el código.

[Abrir el cuaderno de imputación de vacíos en Colab](https://colab.research.google.com/github/BYU-Hydroinformatics/ggst-notebooks/blob/main/impute_gaps_GRACE.ipynb){:target="_blank"}

Antes de ejecutar el código, deberá preparar y cargar un archivo CSV con los datos originales que contienen los vacíos. Este archivo debe contener
únicamente dos columnas, que puede copiar y pegar desde el CSV completo y guardar después como un archivo CSV independiente (`base_file.csv`, por
ejemplo).

![Un CSV de dos columnas preparado para el cuaderno de imputación](../../static/images/wtf-two-col-csv.png)

Aquí tiene un archivo de ejemplo que puede utilizar con el script:
[west-gwsa-raw-clean.csv](../../static/files/west-gwsa-raw-clean.csv)

## Análisis de Tendencias Multilineales

En el método de descomposición estacional descrito anteriormente para la imputación de vacíos se utilizó una única tendencia lineal. Esta es la
tendencia resultante del archivo de ejemplo enlazado arriba, con una sola línea de tendencia:

![Descomposición con una única tendencia lineal](../../static/images/wtf-trend-1.png)

Sin embargo, muchos conjuntos de datos presentan múltiples tendencias lineales. Para este conjunto de datos existen cuatro tendencias distintas. El
script de Python cuenta con una opción para realizar un análisis de regresión multilineal. Para este conjunto de datos se fijó la variable
`number_breakpoints` en 3 y se ejecutó un algoritmo de regresión multilineal que ajusta los datos de la siguiente manera:

![Ajuste de regresión multilineal con tres puntos de quiebre interiores](../../static/images/wtf-trend-4-scatter.png)

Tenga en cuenta que 3 puntos de quiebre interiores dan lugar a cuatro tendencias lineales. Esta opción produce las siguientes tendencias:

![Descomposición con cuatro tendencias lineales](../../static/images/wtf-trend-4.png)

Y, por último, la imputación de vacíos con 4 líneas de tendencia da el siguiente resultado:

![Imputación de vacíos utilizando cuatro líneas de tendencia](../../static/images/wtf-trend-4-results.png)

## Ejemplos de Procesamiento de Datos

Una vez rellenados los vacíos, el último paso consiste en graficar y analizar las curvas de una temporada a la vez, extraer los valores de GWSa de la
curva y calcular la estimación de recarga utilizando el método 1 o el método 2, o ambos.

![Procesamiento de una sola temporada en el libro de trabajo de ejemplo](../../static/images/wtf-excel-example.png)

El siguiente archivo de Excel ilustra cómo examinar y procesar cada temporada de datos de una serie temporal de anomalías del almacenamiento de agua
subterránea derivada de GRACE e imputada:
[west-gwsa-wtf.xlsx](../../static/files/west-gwsa-wtf.xlsx)

Después de abrir el archivo, copie y pegue los valores de GWSa generados por el algoritmo de imputación como se muestra aquí. Observe que los valores
imputados tienen más dígitos que los originales. Las fórmulas de las columnas C y D separan los datos imputados de la columna B para permitir un
gráfico multicolor en el que las secciones imputadas originales puedan visualizarse con claridad.

![Pegado de los valores imputados en el libro de trabajo](../../static/images/wtf-excel-paste.png)

En este punto puede recorrer cada una de las pestañas correspondientes a los años a partir de 2002. En cada página, los valores estacionales se
extraen automáticamente de la hoja principal mediante una fórmula VLOOKUP. En cada página, ajuste manualmente las líneas roja y verde para que se
adapten a la rama descendente y a la base. Luego lea manualmente los valores SP, SB y SL en cm sobre el eje vertical e introdúzcalos en las tres
celdas indicadas en el diagrama. Los valores RS, RD, R1 y R2 se calcularán entonces automáticamente.

![Ajuste de la rama descendente y de la base para un año](../../static/images/wtf-excel-fitting.png)

![Definición de Sp, SB y SL en un ciclo estacional, con los componentes RS y RD](../../static/images/wtf-rs-rd-fig.png)

A medida que examine el gráfico de cada año, es posible que necesite ajustar el rango del eje vertical antes de poder ajustar correctamente las
líneas. Para ello, haga doble clic en el eje vertical, abra la pestaña de opciones del eje y ajuste manualmente los límites mínimo y máximo para
encuadrar bien el gráfico.

![Ajuste de los límites del eje vertical](../../static/images/wtf-excel-axis.png)

Si necesita añadir años adicionales, copie una de las hojas anuales, cámbiele el nombre y modifique el año en la parte superior de la hoja. Después de
procesar todos los años y calcular todos los valores R1 y R2, podrá ver un resumen en la hoja Summary.

![Hoja de resumen con los resultados de todos los años](../../static/images/wtf-excel-summary.png)

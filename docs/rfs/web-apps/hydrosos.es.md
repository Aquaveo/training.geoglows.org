# Aplicación HydroSOS

## Descripción General y Objetivos

Esta aplicación busca ofrecer una visualización de las condiciones hídricas actuales en todo el mundo, así como de las posibles condiciones futuras de ríos individuales.

Contar con datos hídricos confiables es clave para informar a los tomadores de decisiones sobre las condiciones hidrológicas actuales, de modo que puedan tomar las medidas necesarias para gestionar sus recursos hídricos.
Disponer de información precisa y confiable sobre las condiciones hídricas locales, tanto del estado actual como de las perspectivas proyectadas, es esencial para orientar las decisiones de gestión en el abastecimiento de agua, la energía hidroeléctrica y la operación de embalses. Al combinar registros históricos con pronósticos de modelos, las herramientas de estado y perspectiva presentan las tendencias actuales y esperadas dentro de su contexto histórico adecuado. Estos productos combinan indicadores clave con mapas y gráficos interactivos, lo que ayuda a los gestores a comparar rápidamente los patrones hidrológicos actuales y futuros con las condiciones normales de referencia para apoyar una toma de decisiones eficaz.

HydroSOS (Hydrologic Status and Outlook, Estado y Perspectiva Hidrológica) es una iniciativa creada por la OMM (Organización Meteorológica Mundial) que presenta un método estándar para comparar las condiciones actuales y pronosticadas con el promedio histórico para la misma época del año. Sus métodos se aplican a varias variables hidrológicas, pero para las contribuciones de RFS nos enfocamos en el caudal, porque esa es la variable que proporciona RFS. Para obtener más información, consulte las páginas de la OMM: [https://wmo.int/activities/hydrosos/global-hydrological-status-and-outlook-system-hydrosos](https://wmo.int/activities/hydrosos/global-hydrological-status-and-outlook-system-hydrosos) y [https://wmohydrosos.ceh.ac.uk/](https://wmohydrosos.ceh.ac.uk/). También han creado un [portal de HydroSOS](https://wmohydrosos.ceh.ac.uk/portal/) diseñado para mostrar HydroSOS con base en información de varias fuentes diferentes. RFS aporta datos de caudal al portal, y esa misma información se muestra en esta aplicación.

## Cómo Usar la Aplicación

### Vista Global

Explore el mapa global para ver el estado hidrológico actual de las cuencas. Cada cuenca se colorea según su categoría de HydroSOS para el mes que se muestra en la esquina superior derecha. Puede seleccionar el botón del calendario para mostrar un mes diferente.

![La aplicación web HydroSOS Water Monitor](../../static/images/hydrosos-app.png)

### Seleccionar una Cuenca

Puede seleccionar una cuenca haciendo clic directamente sobre ella en la aplicación o buscándola en la barra de búsqueda. Para buscar una cuenca, puede hacerlo por su nombre (por ejemplo: Mississippi) o por su ID de HydroBASINS para una cuenca de nivel 4. Una vez que seleccione una cuenca, puede haber un periodo de carga y luego un panel lateral mostrará gráficos e información sobre esa cuenca específica.

### Interpretación de los Gráficos

En la parte superior del panel lateral verá el nombre de la cuenca, su estado y alguna información básica sobre ella.

A continuación verá un gráfico del estado mensual de HydroSOS. Las bandas de color muestran los rangos de cada una de las categorías de HydroSOS. La línea negra muestra los promedios mensuales del año en curso, indicando en qué categorías ha estado el caudal a lo largo de este año. Luego hay una predicción de cómo podrían ser los próximos meses, con un rango de posibilidades.

![Gráfico del estado mensual de HydroSOS](../../static/images/hydrosos-monthly-status.png)

El siguiente gráfico muestra el caudal como un volumen acumulado a lo largo del año. Tanto las categorías de HydroSOS como los valores de caudal de RFS se convierten a volúmenes. Luego, los volúmenes históricos se utilizan para mostrar una predicción de cuál podría ser el volumen total dentro de tres meses, con base en los volúmenes observados en esos meses en el pasado.

![Gráfico de perspectiva estacional a tres meses](../../static/images/hydrosos-seasonal-outlook.png)

El siguiente gráfico muestra el volumen acumulado del río. Cada línea gris representa un año diferente. La línea azul muestra el año mediano.

![Gráfico de volumen acumulado](../../static/images/hydrosos-cumulative-volume.png)

El último gráfico muestra la escorrentía histórica. Muestra el volumen anual total de cada año (en gris) y lo compara con un promedio móvil de 5 años.

![Gráfico de escorrentía anual histórica](../../static/images/hydrosos-annual-runoff.png)

## Comprender el Estado de las Cuencas

Los colores de las cuencas representan el percentil de la escorrentía acumulada actual en relación con el periodo histórico de referencia. Se obtienen clasificando los promedios mensuales. Cada mes solo se compara consigo mismo: enero se compara con enero, febrero con febrero, etc. Luego se etiquetan según el percentil en el que se encuentran.

| Estado       | Rango de percentiles         |
|--------------|------------------------------|
| Muy seco     | Por debajo del percentil 10  |
| Seco         | Percentil 10–30              |
| Normal       | Percentil 30–70              |
| Húmedo       | Percentil 70–90              |
| Muy húmedo   | Por encima del percentil 90  |

## Límites de las Cuencas

La aplicación utiliza el nivel 4 de HydroBASINS para definir los límites de las cuencas y asociar la información hidrológica con cuencas individuales. Cada cuenca se identifica mediante un ID único de HydroBASINS. Para cada cuenca se identificó y seleccionó el río de RFS en su salida para representar las condiciones de caudal de esa cuenca. Los valores de caudal de ese río se usaron para colorear toda la cuenca. Si la cuenca no estaba bien representada por un solo río, se dejó en blanco.

## Datos con Corrección de Sesgo

Esta aplicación web ofrece la opción de usar datos hidrológicos con corrección de sesgo global. Esta opción carga los datos de RFS con corrección de sesgo global mediante el método SABER. Consulte la [sección avanzada](../advanced/bias-correction/saber-method.md) para obtener más información sobre qué es y cómo usarlo. La clasificación de cada cuenca no cambiará, pero los valores absolutos sí. Por lo tanto, el mapa mostrado no cambiará al activar esta opción, pero los valores en los gráficos de cada cuenca sí lo harán. Como los datos con corrección de sesgo se obtienen por separado, activar esta opción puede aumentar el tiempo de carga.

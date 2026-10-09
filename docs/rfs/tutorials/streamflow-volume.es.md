## Visión General

Un uso común de los datos de RFS consiste en obtener el volumen de agua en el río. Esto es útil especialmente para la gestión de embalses, porque permite al usuario saber cuánta agua entra al embalse durante un periodo de tiempo determinado y, por lo tanto, qué volumen de agua debe liberarse para evitar la falla de la presa.

Los datos de RFS se reportan como un caudal en metros cúbicos por segundo. Este valor se reporta para un intervalo de tiempo determinado. Por ejemplo, en los pronósticos, representa el caudal promedio durante el paso de tiempo de 3 horas.

Para convertir el valor de caudal en un volumen, puede multiplicar el caudal por el número de segundos del periodo de tiempo. Para los pronósticos de 3 horas, multiplicaría cada valor de caudal por 10800 (3 horas × 60 minutos por hora × 60 segundos por minuto). Esto le daría el volumen total durante ese periodo de tres horas. Luego puede sumar los valores a lo largo del tiempo para obtener el volumen total en ese periodo.

## Ejemplo en Excel

A continuación se muestra un ejemplo de cómo se pueden hacer los cálculos de volumen en Excel.

1. Descargue los datos de pronóstico de su río.

    ![Datos de pronóstico descargados para el río](../../static/images/volume_example1.png)

2. Abra los datos en Excel. Elimine la columna adicional para que solo quede la columna `flow_median`.

    ![Datos en Excel con solo la columna flow_median](../../static/images/volume_example2.png)

3. Introduzca la fórmula para calcular el volumen en cada paso de tiempo. Tome el caudal promedio y multiplíquelo por el número de segundos del periodo de tiempo.

    ![Fórmula de volumen introducida en el primer paso de tiempo](../../static/images/volume_example3.png)

4. Copie la fórmula hacia abajo para rellenar automáticamente todos los valores.

    ![Fórmula copiada hacia abajo para rellenar automáticamente todos los valores](../../static/images/volume_example4.png)

5. Ahora tiene el volumen de entrada proyectado a lo largo del tiempo. Cada número se expresa en metros cúbicos. Puede sumarlos para obtener el volumen total durante el pronóstico de 15 días.

## Ejemplo en Código

Todos estos cálculos también se pueden realizar en un notebook de Python. El siguiente script muestra un ejemplo de este tipo de cálculos.

[VolumeStatistics.ipynb](https://colab.research.google.com/drive/1UmIyMWsbpOcPjFGO0F2YhBbX9nV3dGlm?usp=sharing)

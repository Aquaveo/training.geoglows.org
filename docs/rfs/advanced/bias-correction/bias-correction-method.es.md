# Método de Corrección de Sesgo

RFS presenta sesgos que pueden limitar su precisión, lo que llevó al desarrollo de un enfoque de corrección de sesgo. Para corregir estos sesgos sistemáticos en
ubicaciones instrumentadas, proponemos el método de Curva de Duración de Caudal Mensual con Mapeo de Cuantiles (MFDC-QM). Este método se enfoca en los sesgos relacionados con la
variabilidad del caudal y la correlación. RFS no asimila datos de caudal observados en su cálculo inicial. Sin embargo, la técnica de corrección de sesgo
permite aplicar los datos globales a nivel local. Los usuarios locales pueden tener más confianza en sus datos porque saben que sus datos observados
pueden utilizarse para mejorar los datos modelados en su ubicación.

Después de aplicar la corrección de sesgo, observamos una mejora significativa en la distribución de las relaciones de sesgo y variabilidad, con una ligera
mejora en los valores de correlación en las estaciones, lo que resultó en simulaciones más confiables y en mejores métricas de Eficiencia de Kling-Gupta (KGE): sesgo,
variabilidad y correlación.

La siguiente presentación explica cómo se ha validado RFS y ofrece detalles sobre los métodos de corrección
de sesgo.

[GEOGLOWS - Corrección de Sesgo.pdf](https://drive.google.com/file/d/1-GyWh_lY2AjRTXM7aRknqmJiIEh_BqMd/view?usp=sharing)

RFS aplica la corrección de sesgo a sus datos de pronóstico asumiendo que el pronóstico comparte los mismos sesgos que la simulación retrospectiva. Este proceso
consiste en asignar los valores de caudal pronosticados a una probabilidad de no excedencia utilizando la curva de duración de caudal de la simulación histórica y luego reemplazar
los valores pronosticados por los valores correspondientes de la curva de duración de caudal observada.

![pronósticos](../../../static/images/forecast-bias-correction.png)

Este método ayuda a mejorar la precisión de los pronósticos, particularmente en los primeros horizontes de pronóstico, alineando los datos más estrechamente con las observaciones
históricas. Sin embargo, las mejoras están limitadas por la suposición de que los sesgos en los datos de pronóstico son idénticos a los de la simulación
retrospectiva. Las siguientes imágenes muestran cómo mejoraron los valores de KGE del modelo de pronóstico después de aplicar las técnicas de corrección de sesgo.

![kge](../../../static/images/global_kge1.png)

![kge](../../../static/images/global_kge2.png)

Para más información, consulte esta presentación: [Bias_Correction_Forecast_Data.pdf](https://drive.google.com/file/d/1Fu4KhqhW6lW1eI8U2pcuHJFyCTqw5Qrn/view?usp=sharing)

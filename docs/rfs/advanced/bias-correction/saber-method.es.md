# SABER (Análisis de Corrientes para Estimación y Reducción de Sesgo)

El método SABER es una herramienta de corrección de sesgo diseñada para grandes modelos hidrológicos como RFS, que aborda específicamente el problema de los sesgos del modelo en
cuencas tanto aforadas como no aforadas. SABER utiliza curvas de duración de caudal (FDC) para comparar el caudal observado con los valores simulados por los
modelos hidrológicos, identificando y corrigiendo los sesgos. Para las ubicaciones no aforadas, donde no hay observaciones directas disponibles, SABER utiliza la curva de duración
de caudal escalar (SFDC).

A diferencia de la corrección de sesgo, que cada institución realiza localmente, SABER lo realiza el equipo de RFS y no lo ejecutan los usuarios finales. Usamos los
datos de las estaciones de aforo que se nos proporcionan para mejorar todos los resultados del modelo. Este proceso todavía está en fase de experimentación y actualmente no
se aplica a los datos a los que acceden los usuarios finales. Esperamos que se aplique en futuras versiones de RFS.

SABER permite extender el proceso de corrección de sesgo a cuencas no aforadas mediante el análisis de comportamientos similares de las cuencas, con base en la proximidad espacial y
la agrupación de regímenes de caudal. Este método es particularmente útil en regiones donde la escasez de datos limita la calibración tradicional, como en los modelos
globales como RFS, y asegura pronósticos de caudal más precisos en grandes dominios espaciales.

SABER funciona comparando los datos de caudal simulados con los valores observados en las ubicaciones aforadas para detectar sesgos altos o bajos. Aplica técnicas de agrupamiento
(clustering) de aprendizaje automático para agrupar cuencas con características de caudal similares, lo que ayuda a extender la corrección de sesgo de cuencas aforadas a no aforadas. El
proceso de SABER incluye el cálculo de las SFDC para diferentes probabilidades de excedencia y la división de los caudales simulados entre los valores correspondientes de la SFDC, incluso en
regiones afectadas por presas o embalses.

![saber](../../../static/images/saber.png)

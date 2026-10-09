# Corrección de Sesgo en un Río de Interés

Puede realizar la corrección de sesgo en cualquier río de RFS siempre que conozca su LINKNO y disponga de datos observados que correspondan a ese río. La forma más sencilla de realizar la corrección de sesgo es usar la función del [paquete de Python] (https://geoglows.readthedocs.io/en/latest/api-documentation/bias.html). Hay una función para corregir los datos históricos y otra para corregir los datos de pronóstico.

## Corrección de Sesgo - Ejemplo de Pronóstico

Este notebook de Colab ofrece una guía paso a paso para realizar la corrección de sesgo en los valores de pronóstico de RFS. Muestra cómo ajustar los valores de caudal
pronosticados utilizando observaciones históricas, lo que mejora la precisión de las predicciones y alinea los datos con mediciones reales para un mejor
análisis hidrológico:

[Bias_Correction_GEOGloWS_ECMWF_Hydrological_Model_Forecast Colab.ipynb](https://colab.research.google.com/drive/1AWwF60XP_6GKhl1fe9KDhhndT802cHUq?usp=sharing)

## Corrección de Sesgo - Ejemplo Retrospectivo

Para profundizar en el análisis de la corrección de sesgo y la evaluación del desempeño, hemos preparado un notebook interactivo de Google Colab. Este notebook
proporciona una guía paso a paso para realizar estos análisis utilizando datos reales del río Magdalena en El Banco, Colombia. Cubre tanto la
corrección de sesgo como la evaluación del desempeño, lo que le permite trabajar con los datos y los métodos descritos en esta
guía: [Bias_Correction_GEOGloWS_ECMWF_Hydrological_Model_Retrospective_Simulation Colab.ipynb](https://colab.research.google.com/drive/19gr9icMEUwZdT6ae6DPG-IwGeWTS3mKk?usp=sharing).

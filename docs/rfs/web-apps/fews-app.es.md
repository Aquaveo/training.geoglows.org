# Aplicación FEWS

Esta aplicación web está diseñada para mostrar rápidamente alertas de inundación. Utiliza datos del modelo RFS y de [Flood Hub de Google](https://sites.research.google/floods/l/0/0/3) para mostrar las cuencas que presentan un alto riesgo de inundación. Los lugares con mayor riesgo de inundación se resaltan en el mapa.

![La aplicación web FEWS4All](../../static/images/fews-app.png)

Se pueden seleccionar cuencas y se abrirá un panel lateral que muestra qué modelo(s) indican un riesgo de inundación, así como el riesgo de inundación que presenta cada modelo.

![Alertas de inundación de cada modelo para una cuenca seleccionada](../../static/images/fews-warnings.png)

La tarjeta de cada modelo muestra el ID del río o de la estación de aforo que utilizó, junto con los detalles del pronóstico. Debajo de esta información se muestran datos sobre la población total y la infraestructura de la cuenca. Esto proporciona contexto sobre los impactos que podría tener la inundación.

![Impactos en la población y la infraestructura para una cuenca seleccionada](../../static/images/fews-impact.png)

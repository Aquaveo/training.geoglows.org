## Descripción General

La misión GRACE (Gravity Recovery And Climate Experiment) de la NASA proporciona datos que pueden utilizarse para analizar los cambios a largo plazo
en el almacenamiento de agua subterránea en regiones seleccionadas. Los datos permiten identificar y caracterizar las condiciones en zonas con pocos
datos, o identificar tendencias en otras regiones donde estas pueden quedar ocultas por el ruido de los datos de pozos.

GRACE proporciona estimaciones mensuales de las anomalías de almacenamiento de agua en altura de agua equivalente, y ha generado soluciones mensuales
del campo gravitatorio desde abril de 2002. Las estimaciones de la variabilidad de masa y los errores de observación asociados están disponibles en
una cuadrícula global de 300 km.

![Mapa global de las anomalías de gravedad medidas por GRACE](../../static/images/grace-globe.png){ width="388" }

## Anomalías de Almacenamiento Derivadas de GRACE

GRACE mide el agua total almacenada en una columna de la Tierra: nieve, agua superficial, humedad del suelo, agua en el dosel vegetal y agua
subterránea en conjunto. Se utiliza un enfoque de balance de masa para separar el componente de agua subterránea de ese total y presentarlo para un
área de interés.

Al integrar los datos de las misiones GRACE y GRACE-FO, y utilizar los datos de agua superficial de GLDAS de la NASA, es posible observar los cambios
en el almacenamiento de agua subterránea. La naturaleza global de estos datos permite a los usuarios definir regiones que representan países,
cuencas o acuíferos, agregar los cambios de volumen de agua en esas regiones y obtener resultados como gráficos de series temporales para toda la
región o en puntos seleccionados.

El algoritmo utilizado para procesar los datos de GRACE y GLDAS y producir anomalías de agua subterránea a escala global y regional se describe en
detalle en la página [Algoritmo de Cálculo](computational-algorithm.md).

## La Aplicación Web

GRACE Regional Analyst es una aplicación web que ofrece las anomalías de almacenamiento derivadas de GRACE. Aunque se han desarrollado varias
herramientas para procesar y visualizar los datos de GRACE, esta está diseñada específicamente para apoyar la gestión de los recursos de agua
subterránea por parte de las partes interesadas y los tomadores de decisiones a nivel regional. Esto se logra procesando cuidadosamente los datos
brutos de GRACE para eliminar anomalías y mejorar la resolución: separando el componente de agua subterránea de los demás componentes del
almacenamiento de agua mediante GLDAS, recortando los datos a regiones de interés específicas y presentando los resultados en una interfaz sencilla e
intuitiva.

Permite a los usuarios cargar archivos JSON o dibujar una región en el mapa para sus áreas de interés. También muestra un mapa animado de las
anomalías de cambio de almacenamiento.

![GRACE Regional Analyst mostrando la anomalía global del almacenamiento de agua subterránea](../../static/images/web-app-overview.png)

La aplicación está disponible en
[apps.geoglows.org/grace-anomalies](https://apps.geoglows.org/grace-anomalies){:target="_blank"}. Consulte
[Uso de la Aplicación Web](../accessing-data/web-app.md).

## Lecturas Adicionales

GRACE ha demostrado ser una herramienta eficaz para caracterizar los cambios en el almacenamiento de agua subterránea en regiones extensas:

- [J. Famiglietti et al., 2011](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2010GL046442){:target="_blank"}
- [J. S. Famiglietti, 2014](https://www.nature.com/articles/nclimate2425){:target="_blank"}
- [Rodell, Velicogna, & Famiglietti, 2009](https://www.nature.com/articles/nature08238){:target="_blank"}
- [Thomas, Reager, Famiglietti, & Rodell, 2014](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1002/2014GL059323){:target="_blank"}

<!-- TODO: decide whether these citations belong here or on the top-level Publications page. -->

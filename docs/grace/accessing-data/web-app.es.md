## Descripción General

GRACE Regional Analyst es una aplicación web que ofrece una interfaz de mapa para visualizar los componentes de almacenamiento a escala global,
animarlos a lo largo del tiempo, generar series temporales y descargar los resultados.

La aplicación está disponible en
[apps.geoglows.org/grace-anomalies](https://apps.geoglows.org/grace-anomalies){:target="_blank"}.

Esta página abarca todo lo que se hace dentro de la aplicación. Los conceptos que sustentan estos pasos —cómo se derivan los datos, cómo se recortan
las regiones y qué significan los resultados— se explican en [Algoritmo de Cálculo](../understanding/computational-algorithm.md).

## La Interfaz del Mapa

Al abrir la aplicación web, lo primero que se ve es el mapa. El control deslizante de tiempo, en la parte inferior izquierda, cambia el mes que se
muestra y permite animar el registro de un mes al siguiente. Las herramientas de dibujo, en la esquina superior derecha, se utilizan para definir una
región de interés, lo que se describe con más detalle a continuación.

![La interfaz del mapa, indicando dónde dibujar una región, cambiar el mes y elegir la capa mostrada](../../static/images/web-app-interface.png)

También en la esquina superior derecha, el usuario puede decidir qué capa desea visualizar. Las opciones son Anomalía del Almacenamiento de Agua
Subterránea (GWSa), Anomalía del Almacenamiento Total de Agua (TWSa), Anomalía de la Humedad del Suelo (SMa) y Anomalía del Equivalente de Agua en
Nieve (SWEa). Cada una se describe en [Datos Disponibles](../datasets/available-data.md).

![El menú de capa mostrada, con GWSa, TWSa, SMa y SWEa](../../static/images/display-layer-options.png)

En el lado izquierdo hay una opción para seleccionar un mapa base. Existen varias opciones distintas para elegir.

![La galería de mapas base, con opciones de Imágenes, Calles, Topográfico y otros fondos](../../static/images/base-maps.png){ width="420" }

## Selección de un Área o Punto

Para seleccionar un área o un punto, el usuario tiene varias opciones.

La primera opción es cargar un geojson del área de interés. Para ello, seleccione el botón de carga en la esquina superior derecha. Se abrirá una
ventana emergente donde se puede cargar el archivo. Se aceptan tanto archivos `.geojson` como `.json`.

![El cuadro de diálogo Cargar Polígono, que acepta un archivo .geojson o .json arrastrándolo o mediante el explorador de archivos](../../static/images/upload-json.png){ width="440" }

La siguiente opción es utilizar las herramientas de dibujo para trazar una región de interés en el mapa. Haga doble clic para finalizar el polígono.

![Trazado de una región de interés en el mapa con las herramientas de dibujo](../../static/images/region-of-interest.png)

Otra manera de elegir dónde visualizar los datos es utilizar las herramientas de dibujo para seleccionar un solo punto de interés. Un análisis puntual
devuelve la serie temporal de las celdas de la cuadrícula que contienen ese punto, lo cual se explica en
[Análisis en un Solo Punto](../understanding/computational-algorithm.md#analisis-en-un-solo-punto).

La última manera de elegir una región es seleccionar un acuífero existente. Para ello, seleccione "Aquifer Scale" en el menú superior derecho. Esto
cargará los límites de los acuíferos en el mapa, y luego se puede seleccionar uno.

![Límites de acuíferos cargados en el mapa en la vista Aquifer Scale](../../static/images/aquifer-scale.png)

Una vez seleccionado, el mapa mostrará únicamente ese acuífero junto con sus datos asociados.

Cómo se convierte la región en una serie temporal —qué celdas de la cuadrícula se incluyen y el tamaño mínimo de región recomendado— se explica en
[Recorte de la Cuadrícula](../understanding/computational-algorithm.md#recorte-de-la-cuadricula).

## Visualización y Descarga de Resultados

Una vez que se ha seleccionado un punto o una región en el mapa, el gráfico de la serie temporal de la selección se cargará en la mitad inferior de la
aplicación. El gráfico muestra el componente seleccionado como una línea, con su incertidumbre como una banda sombreada, en equivalente de agua
líquida (cm).

![Serie temporal de la anomalía del almacenamiento de agua subterránea con la banda de incertidumbre y el botón Download CSV](../../static/images/groundwater-plot.png)

En la esquina superior derecha del gráfico hay un botón para descargar el CSV. Los datos que se muestran actualmente en el gráfico serán los datos que
se descarguen. Cambie la capa mostrada en el lado derecho del mapa para modificar qué variable se grafica.

Cada componente de almacenamiento se descarga como su propio archivo con cuatro columnas. Las unidades de almacenamiento son equivalente de agua
líquida en cm.

| Columna | Contenido |
|---------|-----------|
| `Date` | Mes del valor, en un formato de fecha estándar |
| `GWS` | Anomalía del almacenamiento de agua subterránea, en cm |
| `GWS_upper` | Límite superior del rango de error |
| `GWS_lower` | Límite inferior del rango de error |

Las columnas de valores llevan el nombre del componente descargado: un archivo de equivalente de agua en nieve tiene `SWE`, `SWE_upper` y
`SWE_lower`. Las fechas ya están en un formato de fecha estándar y no requieren conversión.

## Configuración

La aplicación cuenta con algunas opciones de configuración que el usuario puede ajustar. Se encuentran seleccionando la configuración en el menú
superior derecho. Esto abrirá una ventana emergente con las opciones enumeradas.

![Configuración de visualización: opacidad de la capa, celdas de balance hídrico, huellas de mascons y límites de las celdas de anomalía](../../static/images/groundwater-settings-1.png){ width="440" }

**Opacidad de la capa** controla con qué intensidad se dibuja la capa de anomalías sobre el mapa base. Al reducirla, el mapa base se hace visible por
debajo.

**Celdas de balance hídrico** alterna entre las celdas de 1.0 grado usadas de forma predeterminada y celdas más finas de medio grado. Al cambiar, el
mapa y el análisis actual se recargan a partir del otro conjunto de datos, y las celdas más finas tardan más en prepararse. Consulte
[Resolución de la Cuadrícula](../datasets/available-data.md#resolucion-de-la-cuadricula).

**Huellas de mascons de GRACE** dibuja los contornos de las celdas originales de 3 grados en las que se entregan los datos. Un control deslizante
ajusta el grosor de la línea.

**Límites de las celdas de anomalía** dibuja los contornos de las celdas de 1.0 o 0.5 grados en las que se reportan las anomalías. Un control
deslizante ajusta el grosor de la línea.

![Configuración continuación: paleta de colores, barra de color y datos en caché](../../static/images/groundwater-settings-2.png){ width="440" }

**Paleta de colores** establece el esquema de colores utilizado para la capa de anomalías. Red-White-Blue es la opción predeterminada, y hay
disponibles cuatro opciones seguras para personas con daltonismo: Viridis, Cividis, Brown-Teal y Purple-Green.

**Barra de color** muestra u oculta la leyenda en el mapa.

**Escala dinámica** está activada de forma predeterminada y ajusta la escala de colores a los valores mínimo y máximo de la región seleccionada,
mostrando siempre el 0 como color central. Al desactivarla se utiliza un rango fijo de -30 a +30 cm.

**Borrar datos en caché** elimina las coordenadas y la animación global almacenadas localmente. La siguiente actualización de la página volverá a
cargar todo desde la red, simulando una primera visita.

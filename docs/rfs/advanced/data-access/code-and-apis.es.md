!!! note
    Los métodos descritos aquí son los medios preferidos para obtener datos del River Forecast System (RFS).

## Estructuras de Datos

La mayoría de los datos de RFS se almacenan en formato Zarr y están fragmentados (chunked) de manera que se pueden consultar eficientemente como series temporales. Puede leer esos archivos Zarr
directamente desde AWS S3 utilizando cualquier lenguaje de programación que tenga una biblioteca cliente de Zarr. La forma más fácil de hacerlo es en Python, utilizando el paquete `geoglows`.

Para obtener datos, necesitará conocer el número de ID de los ríos que le interesan. Revise
el [tutorial sobre cómo encontrar los números de río](../../tutorials/find-river-numbers.es.md) antes de continuar.

## Paquete de Python geoglows

La forma más sencilla de descargar datos del servicio de datos es utilizando el paquete cliente oficial de Python llamado "geoglows". Para ver tutoriales completos,
consulte la [documentación del paquete de Python geoglows](https://geoglows.readthedocs.io){:target="_blank"}.

Para ver fragmentos de código para tareas comunes, consulte el [Recetario](code-snippets.md).

## Ejemplo en Python

Para escribir su propio código en Python que lea directorios Zarr, necesitará los siguientes paquetes:

- [zarr](https://zarr.readthedocs.io/en/stable/){:target="_blank"} >= 3
- [s3fs](https://s3fs.readthedocs.io/en/latest/){:target="_blank"} >= 2025
- [xarray](http://xarray.pydata.org/en/stable/){:target="_blank"} >= 2025

!!! warning
    Las versiones anteriores de estas dependencias también funcionan, pero no se han probado para este sitio de capacitación.

Para encontrar las rutas de los directorios Zarr, consulte el [catálogo de datos](catalog.md){:target="_blank"}. Puede pasar
el URI que comienza con `s3://` directamente a la función `xr.open_dataset()`. No necesita una cuenta de AWS para acceder a los datos, pero debe asegurarse de configurar la consulta para que sea anónima estableciendo storage_options={'anon': True}. 

```python
import xarray as xr

retro_hourly_zarr_uri = 's3://river-forecast-system-v3/retrospective/hourly.zarr'
ds = xr.open_dataset(retro_hourly_zarr_uri, engine='zarr', storage_options={'anon': True})

# now select the 1 or more rivers you want to get data for
rivers = [621054340, ]

df = ds.sel(riverId=rivers)["Q"].to_dataframe()

# save the dataframe as csv, do some analysis, make a plot, etc
df.to_csv('./my_river_data.csv')
```

## Ejemplo en JavaScript

Para escribir su propio código en JavaScript, necesitará una dependencia que lea directorios Zarr. Algunas opciones son:

- [zarrita.js](https://zarrita.dev/){:target="_blank"}
- [zarr.js](https://guido.io/zarr.js/){:target="_blank"}

```javascript
import * as zarr from "https://cdn.jsdelivr.net/npm/zarrita/+esm";

const baseZarrUrl = "https://river-forecast-system-v3.s3.us-west-2.amazonaws.com/retrospective/daily.zarr"

// open the riverId variable
const idStore = new zarr.FetchStore(`${baseZarrUrl}/riverId`);
const idNode = await zarr.open(idStore, {kind: "array"});
// open the discharge variable
const qStore = new zarr.FetchStore(`${baseZarrUrl}/Q`);
const qNode = await zarr.open(qStore, {kind: "array"});
// open the time variable
const tStore = new zarr.FetchStore(`${baseZarrUrl}/time`);
const tNode = await zarr.open(tStore, {kind: "array"});

// get the time values and convert from "time since origin" values to ISO strings
const tUnits = tNode.attrs.units
const tArray = await zarr.get(tNode, [null])
const originTime = tUnits.split("since")[1].trim()
const conversionFactor = {
  seconds: 1,
  minutes: 60,
  hours: 60 * 60,
  days: 60 * 60 * 24,
}[tUnits.split("since")[0].trim()]
const times = [...tArray.data].map(t => {
  let origin = new Date(originTime)
  origin.setSeconds(origin.getSeconds() + (t * conversionFactor))
  return origin.toISOString()
})

// determine the index of the river with your ID of interest
const idArray = await zarr.get(idNode, [null])
const idx = idArray.data.indexOf(760127992)

// get the discharge values for the river with your ID of interest
const qArray = await zarr.get(qNode, [idx, null])

// do something with your arrays of data
console.log("preview of data retrieved:")
console.log("times:", times.slice(0, 50))
console.log("discharge:", qArray.data.slice(0, 50))
```

## Notebooks de Ejemplo

Los siguientes notebooks interactivos de Google Colab recorren análisis comunes utilizando datos reales de ríos.

### Periodos de retorno, curvas de duración de caudal y caudales promedio

Para explorar más a fondo el análisis de periodos de retorno, curvas de duración de caudal y promedios estacionales, lo invitamos a seguir nuestra demostración interactiva
en el notebook de Google Colab proporcionado. Este notebook práctico lo guiará a través del proceso, utilizando datos reales del río Tensift
en Marruecos. Puede acceder al notebook y ejecutarlo directamente en su navegador:

[Return_Periods-FDC-Average_Flows Colab.ipynb](https://colab.research.google.com/drive/1pcB6VEXgT8MMy0MiL9iek0cviDzebxNB?usp=sharing)

---

#### Datos Retrospectivos

Para profundizar en el análisis de datos retrospectivos, periodos de retorno, curvas de duración de caudal y promedios estacionales, hemos preparado un notebook interactivo
de Google Colab. Este notebook proporciona una guía paso a paso para realizar estos análisis utilizando datos reales del río San Juan en
Rancho La Trinidad, Costa Rica. Cubre tanto los datos retrospectivos como el análisis estadístico de caudales, lo que le permite trabajar con los datos y los métodos
descritos en estas guías.

- [Tutorial de Datos de la Simulación Retrospectiva](https://colab.research.google.com/drive/1BRn7cJ8a1KbiLUqou3h7hv7QNW4FTjQI?usp=sharing)
- [Tutorial Extendido](https://colab.research.google.com/drive/1K9-O53eZqGV0mrznoRt0jHuEPnCR9elr?usp=sharing)

---

### Simulación de Pronóstico

El notebook de Colab proporciona una guía interactiva sobre cómo acceder a los datos de pronóstico de RFS y visualizarlos. Muestra cómo obtener
pronósticos de caudal, graficar los datos utilizando bibliotecas de Python e interpretar estadísticas clave para una gestión y planificación eficaces
de los recursos hídricos.

- [Tutorial de Datos de la Simulación de Pronóstico](https://colab.research.google.com/drive/1KgcYNE2_GfBfUpjZiTIBIFlzxpRwq-vO?usp=sharing)
- [Tutorial Extendido](https://colab.research.google.com/drive/1nGDQ6Y4JclHz_kQW4y-rVKZjQF6FSPwb?usp=sharing)

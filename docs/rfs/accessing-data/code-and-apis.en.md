!!! note
    The methods described here are the preferred means of retrieving data from the River Forecast System.

## Data Structures

Most RFS data are stored in Zarr format and chunked in such a way that they can be efficiently queried for timeseries. You can read those Zarr files
directly from AWS S3 using any programming language with a Zarr client library. The easiest way to do this is in Python using the `geoglows` package.

In order to retrieve data, you will need to know the ID number of the rivers you are interested in. Please review
the [tutorial on finding river numbers](../tutorials/find-river-numbers.en.md) before proceeding.

## geoglows Python Package

The simplest way to download data from the data service is using the official Python client package titled "geoglows". For complete tutorials, please
refer to the [geoglows Python package documentation](https://geoglows.readthedocs.io){:target="_blank"}.

For snippets of code for commonly needed tasks, see the [Cookbook](code-snippets.md).

## Python Example

To write your own code Python which reads Zarr directories, you will need the following packages:

- [zarr](https://zarr.readthedocs.io/en/stable/){:target="_blank"} >= 3
- [s3fs](https://s3fs.readthedocs.io/en/latest/){:target="_blank"} >= 2025
- [xarray](http://xarray.pydata.org/en/stable/){:target="_blank"} >= 2025

!!! warning
    Earlier versions of these dependencies also work but are not tested for this training site.

To find the paths to the Zarr directories, you should refer to the [data catalog](../datasets/catalog.md){:target="_blank"}. You can pass
the URI starting with `s3://` directly to the `xr.open_dataset()` function. You do not need an aws account in order to access the data, but you must ensure that you are setting it to query anonymously by setting storage_options={'anon': True}. 

```python
import xarray as xr

retro_hourly_zarr_uri = 's3://geoglows-v2/retrospective/hourly.zarr'
ds = xr.open_dataset(retro_hourly_zarr_uri, engine='zarr', storage_options={'anon': True})

# now select the 1 or more rivers you want to get data for
rivers = [621054340, ]

df = ds.sel(river_id=rivers)["Q"].to_dataframe()

# save the dataframe as csv, do some analysis, make a plot, etc
df.to_csv('./my_river_data.csv')
```

## JavaScript Example

To write your own JavaScript code, you will need a dependency which reads from Zarr directories. Some options include:

- [zarrita.js](https://zarrita.dev/){:target="_blank"}
- [zarr.js](https://guido.io/zarr.js/){:target="_blank"}

```javascript
import * as zarr from "https://cdn.jsdelivr.net/npm/zarrita/+esm";

const baseZarrUrl = "http://geoglows-v2.s3-us-west-2.amazonaws.com/retrospective/daily.zarr"

// open the river_id variable
const idStore = new zarr.FetchStore(`${baseZarrUrl}/river_id`);
const idNode = await zarr.open(idStore, {mode: "r", format: 2});
// open the discharge variable
const qStore = new zarr.FetchStore(`${baseZarrUrl}/Q`);
const qNode = await zarr.open(qStore, {mode: "r", format: 2});
// open the time variable
const tStore = new zarr.FetchStore(`${baseZarrUrl}/time`);
const tNode = await zarr.open(tStore, {mode: "r", format: 2});

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
const qArray = await zarr.get(qNode, [null, idx])

// do something with your arrays of data
console.log("preview of data retrieved:")
console.log("times:", times.slice(0, 50))
console.log("discharge:", qArray.data.slice(0, 50))
```

## Example Notebooks

The following interactive Google Colab notebooks walk through common analyses using real river data.

### Return periods, flow duration curves, and average flows

To further explore the analysis of return periods, flow duration curves, and seasonal averages, we invite you to follow along with our interactive
demonstration in the provided Google Colab notebook. This hands-on notebook will guide you through the process, using real data from the Tensift River
in Morocco. You can access and run the notebook directly in your browser:

[Return_Periods-FDC-Average_Flows Colab.ipynb](https://colab.research.google.com/drive/1pcB6VEXgT8MMy0MiL9iek0cviDzebxNB?usp=sharing)

---

#### Retrospective Data

To dive deeper into the analysis of retrospective data, return periods, flow duration curves, and seasonal averages, we have prepared an interactive
Google Colab notebook. This notebook provides step-by-step guidance for conducting these analyses using real-world data from the San Juan River at
Rancho La Trinidad in Costa Rica. It covers both retrospective data and statistical flow analysis, allowing you to engage with the data and methods
discussed in these guides.

- [Retrospective Simulation Data Tutorial](https://colab.research.google.com/drive/1BRn7cJ8a1KbiLUqou3h7hv7QNW4FTjQI?usp=sharing)
- [Long Form Tutorial](https://colab.research.google.com/drive/1K9-O53eZqGV0mrznoRt0jHuEPnCR9elr?usp=sharing)

---

### Forecast Simulation

The Colab notebook provides an interactive guide on accessing and visualizing forecast data from RFS. It demonstrates how to retrieve
streamflow forecasts, plot the data using Python libraries, and interpret key statistics for effective water resource management and
planning.

- [Forecast Simulation Data Tutorial](https://colab.research.google.com/drive/1KgcYNE2_GfBfUpjZiTIBIFlzxpRwq-vO?usp=sharing)
- [Long Form Tutorial](https://colab.research.google.com/drive/1nGDQ6Y4JclHz_kQW4y-rVKZjQF6FSPwb?usp=sharing)

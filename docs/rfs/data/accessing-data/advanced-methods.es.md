# Métodos Avanzados de Acceso

Si desea acceder a los datos mediante programación, hay un par de formas de hacerlo.

Todos los datos de RFS están disponibles para que cualquier persona los descargue y utilice. Todos se almacenan en el bucket de AWS:
[https://v3.s3.riverforecastsystem.com/](https://v3.s3.riverforecastsystem.com/){:target="_blank"}. A partir de ahí, los datos se dividen en carpetas. Puede explorar el bucket y descargar los
datos que desee. Los datos de nuestras aplicaciones y del [almacén de datos](datastore.md) provienen todos de este bucket. El bucket es público, por lo que no se
necesita ninguna cuenta. Al usar herramientas como AWS CLI o Python, configúrelas para acceder a los datos de forma anónima
(por ejemplo, `--no-sign-request` o `anon=True`).

### Ejemplo: Lectura de Datos con Python

Este ejemplo lee el caudal retrospectivo diario de un río directamente desde el bucket. Requiere los paquetes de Python `xarray`, `zarr`
(versión 3 o posterior) y `s3fs`. Para encontrar el ID de un río, consulte [Encontrar Números de Río](../../tutorials/find-river-numbers.md).

```python
import xarray as xr

# open the daily retrospective discharge directly from the public bucket
ds = xr.open_dataset(
    's3://river-forecast-system-v3/retrospective/daily.zarr',
    engine='zarr',
    storage_options={'anon': True},  # access the public bucket anonymously
)

# select one or more rivers by river ID and convert to a table
df = ds.sel(riverId=[760021611])['Q'].to_dataframe()
df.to_csv('my_river_data.csv')
```

Además, hemos desarrollado un paquete de Python para facilitar el uso y el acceso a nuestros datos. La documentación del paquete de Python
se encuentra aquí: [https://geoglows.readthedocs.io/en/latest/](https://geoglows.readthedocs.io/en/latest/){:target="_blank"}. Puede usar estas funciones para obtener los datos que necesite.

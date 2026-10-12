# Advanced Accessing Methods

If you are looking to access data programmatically, there are a couple of ways to do this.

All of the RFS data is available to anyone to download and use. It is all stored in the AWS bucket: [https://v3.s3.riverforecastsystem.com/](https://v3.s3.riverforecastsystem.com/){:target="_blank"}.
From there, the data is divided further. Feel free to browse through the bucket and download whatever data you would like. The data on our
applications and at the [datastore](datastore.md) all come from this bucket. The bucket is public, so no account is needed. When using tools like the AWS CLI
or Python, set them to access the data anonymously (for example, `--no-sign-request` or `anon=True`).

### Example: Reading Data with Python

This example reads the daily retrospective discharge for one river directly from the bucket. It requires the `xarray`, `zarr` (version 3
or later), and `s3fs` Python packages. To find the ID of a river, see [Finding River Numbers](../../tutorials/find-river-numbers.md).

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

Furthermore, we have written a python package to make it easier to use and access our data. There is documentation for the python package
found here: [https://geoglows.readthedocs.io/en/latest/](https://geoglows.readthedocs.io/en/latest/){:target="_blank"}. Feel free to use these functions to get the data you need.

## Overview

The Python API for the GGST allows users to retrieve groundwater information about a point or region without having administrative privileges to the
GGST web application. You can also download a complete zip file of a region's netCDF raster files.

The GGST API has four functions. Each of these functions requires different inputs and returns different results as desired by the user:

- `getStorageOptions`
- `getPointValues`
- `getRegionTimeseries`
- `subsetRegionZipfile`

To run some of the functions listed above, the user will need an authentication token. The API can be implemented in many ways using a variety of
coding languages and platforms. An example implementation using Python in a Google Colaboratory notebook is described on the
[Colab Notebook](notebook.md) page.

## API Methods

All four GGST functions follow the same pattern. Each of the terms in brackets, along with the parameters and values, would be replaced by string
values:

```
https://apps.geoglows.org/apps/[parent-app]/api/[MethodName]/?param1=value1&param2=value2&...paramN=valueN
```

### getStorageOptions

| | |
|---|---|
| **Supported Methods** | GET |
| **Returns** | A JSON object with a list of storage options |
| **Parameters** | There are no parameters for the getStorageOptions function |

```
https://apps.geoglows.org/apps/ggst/api/getStorageOptions/
```

For simplicity, the options are given a variable name. For instance, "Total Water Storage (GRACE)" has a variable name of `grace`, and similarly
"Soil Moisture Storage (GLDAS)" is shortened to `sm`. See [Available Data](../datasets/available-data.md).

### getPointValues

| | |
|---|---|
| **Supported Methods** | GET |
| **Returns** | A JSON object with a timeseries for a given point |

| Name | Description | Valid Value | Required |
|------|-------------|-------------|----------|
| Longitude | long in WGS 84 Proj | Any value on land within the GRACE Explorer Domain (-60,180) | Yes |
| Latitude | lat in WGS 84 Proj | Any value on land within the GRACE Explorer Domain (-60,90) | Yes |
| `storage_type` | Storage type of interest | One of the abbreviated values from the first function, e.g. `grace`, `sw`, `sm` or `gw` | Yes |

```
https://apps.geoglows.org/apps/ggst/api/getPointValues/?latitude=20.7&longitude=80.2&storage_type=gw
```

<!-- TODO: the source documents the longitude domain as (-60,180), which appears to be an error for
     (-180,180). Confirm before publishing — this is reproduced as written in the source. -->

### getRegionTimeseries

The last two functions require an authentication token. It is best to call these two functions from Python.

| | |
|---|---|
| **Supported Methods** | POST |
| **Returns** | A JSON object with area of the region, depletion time series, error range timeseries and storage time series |

| Name | Description | Valid Value | Required |
|------|-------------|-------------|----------|
| Region name | Name for the subset region. All files will have this name as prefix | String | Yes |
| Storage type | Storage type of interest | One of the abbreviated values from the first function, e.g. `grace`, `sw`, `sm` or `gw` | Yes |
| files | A zipped folder | A zipped folder with `.shp`, `.shx`, `.prj` and `.dbf` files | Yes |
| API token | Token from the portal | Token from a user account on the portal | Yes |

Example query:

```python
files = {'shapefile': ("response.zip", uploaded["".join(uploaded)], 'application/zip')}
region_timeseries_request = requests.post(
    "https://apps.geoglows.org/apps/ggst/api/getRegionTimeseries/",
    headers={"Authorization": f"Token {api_token}"},
    data={"name": "api_test", "storage_type": "tws"},
    files=files,
)
```

Response, trimmed for clarity:

```
{'area': 437109427476.4769,
 'depletion': [['2000-01-01', 0.0], ['2000-02-01', -273831.117], ... ['2021-09-01', 4792246.794]],
 'error_range': [['2000-01-01', -6.045, -3.205], ... ['2021-09-01', 8.19, 11.796]],
 'success': 'success',
 'values': [['2000-01-01', -4.625], ['2000-02-01', -5.46], ... ['2021-09-01', 9.993]]}
```

### subsetRegionZipfile

| | |
|---|---|
| **Supported Methods** | POST |
| **Returns** | A zip file with regional netCDF files for each storage option clipped to the uploaded shapefile |

| Name | Description | Valid Value | Required |
|------|-------------|-------------|----------|
| Region name | Name for the subset region. All files will have this name as prefix | String | Yes |
| files | A zipped folder | A zipped folder with `.shp`, `.shx`, `.prj` and `.dbf` files | Yes |
| API token | Token from the portal | Token from a user account on the portal | Yes |

Example query:

```python
files = {'shapefile': ("response.zip", uploaded["".join(uploaded)], 'application/zip')}
subset_region_request = requests.post(
    "https://apps.geoglows.org/apps/ggst/api/subsetRegionZipfile/",
    headers={"Authorization": f"Token {api_token}"},
    data={"name": "api_test"},
    files=files,
)
z = ZipFile(BytesIO(subset_region_request.content))
z.extractall()
```

The result will be a folder with netCDF files.

## Obtaining an Authentication Token

The last two functions of the API require an authentication token. To obtain one, use one of the following two methods:

**1. Request a token.** You can request a token by contacting the administrator of the portal. For the `apps.geoglows.org` portal, please send a
request to Norm Jones (njones@byu.edu).

**2. Use an existing account.** If you have an account, you can obtain an authentication token by signing in and navigating to the User Settings.
After signing in, click on your username in the upper right corner, opening a panel, and then click on User Settings to reveal the API key. The
authentication token or API key will be in the third section.

<!-- TODO: The app interface has changed. Confirm the current path to the API key in user settings. -->

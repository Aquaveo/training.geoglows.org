## Summary

There are 4 primary kinds of river datasets provided by the River Forecast System. All these data are available for free.

1. **Hydrography**: GIS data for stream, catchment, and lake locations around the world.
2. **Retrospective Simulation**: Hourly river discharge data since January 1940.
3. **Forecasts**: 15-day streamflow forecasts generated every day at midnight.
4. **Flood Maps**: Flood extents and depths mapped from the forecasts and from return period flows.

[The GEOGLOWS River Forecast System V3](https://www.geoglows.org){:target="_blank"} © [Dr. Riley Hales](https://hales.app) 2025 is licensed
under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/){:target="_blank"}

## Table of datasets

The easiest way to find and download RFS V3 data is the [RFS Data Store](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"},
which describes each dataset and lets you download only the rivers and dates you need. See [The Datastore](../../what-is-it/using-datastore.md) for
instructions.

All RFS V3 datasets are stored in a single public AWS S3 bucket, `river-forecast-system-v3`, in the `us-west-2` region. You **do not need** an AWS
account, credit card, or a username and password to download data from it. You can browse the bucket in a web browser at
[https://v3.s3.riverforecastsystem.com](https://v3.s3.riverforecastsystem.com){:target="_blank"}.

When querying data from AWS, you may need to specify that you are accessing it anonymously if you don’t have an AWS account or prefer not to provide credentials.

| Dataset                                                                                                                                          | File Format(s)      | Bucket URI and Path                                                         |
|--------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|-----------------------------------------------------------------------------|
| [15-Day Ensemble Forecast](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/forecast-15day){:target="_blank"}                       | Zarr                | `s3://river-forecast-system-v3/forecasts15/`                                |
| [Stream Centerlines](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/streams){:target="_blank"}                                    | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Catchment Boundaries](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/catchments){:target="_blank"}                               | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Confluence Points](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/confluences){:target="_blank"}                                 | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Lakes](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/lakes){:target="_blank"}                                                   | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Retrospective - Hourly Discharge](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-hourly){:target="_blank"}         | Zarr                | `s3://river-forecast-system-v3/retrospective/hourly.zarr`                   |
| [Retrospective - Daily Discharge](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-daily){:target="_blank"}           | Zarr                | `s3://river-forecast-system-v3/retrospective/daily.zarr`                    |
| [Retrospective - Monthly Discharge](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-monthly){:target="_blank"}       | Zarr                | `s3://river-forecast-system-v3/retrospective/monthly.zarr`                  |
| [Retrospective - Yearly Discharge](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-yearly){:target="_blank"}         | Zarr                | `s3://river-forecast-system-v3/retrospective/yearly.zarr`                   |
| [Retrospective - Annual Maximums](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/annual-maximums-daily){:target="_blank"}         | Zarr                | `s3://river-forecast-system-v3/retrospective/maximums.zarr`                 |
| [Retrospective - Return Periods](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/return-periods){:target="_blank"}                 | Zarr                | `s3://river-forecast-system-v3/retrospective/return-periods.zarr`           |
| [Retrospective - Flow Duration Curves](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/flow-duration-curves){:target="_blank"}     | Zarr                | `s3://river-forecast-system-v3/retrospective/fdc.zarr`                      |
| [Forecast Flood Maps](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/forecast-flood-maps){:target="_blank"}                       | GeoParquet, GeoTIFF | `s3://river-forecast-system-v3/forecasts15/year=YYYY/month=MM/day=DD/`      |
| [Return Period Flood Maps](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/return-period-flood-maps){:target="_blank"}             | GeoTIFF             | `s3://river-forecast-system-v3/flood-maps/lat=YYY/lon=XXX/return-periods/`  |
| [FLDPLN Libraries](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/fldpln-libraries){:target="_blank"}                             | Zarr, PMTiles       | `s3://river-forecast-system-v3/flood-maps/lat=YYY/lon=XXX/fldpln.zarr/`     |

## Code and Technical References

- Forecast computation scripts: [https://github.com/geoglows/geoglows_ecflow](https://github.com/geoglows/geoglows_ecflow){:target="_blank"}
- Retrospective weekly update scripts: [https://github.com/geoglows/retrospective-update](https://github.com/geoglows/retrospective-update){:target="_blank"}

## Downloading data from the command line interface (recommended)

The fastest way to download RFS data using the AWS Command Line Interface. If you are not familiar with programming or command line tools, please
skip to the next section on downloading data with a web browser.

Using the CLI will download data faster than the through the browser and is recommended for downloading large amounts of data. Please refer to the AWS
instructions for downloading data from S3. You may need to add the `--no-sign-request` flag on your copy or sync commands. Each dataset's
**Download** tab in the [RFS Data Store](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"} also gives ready-to-use
commands for s5cmd and the AWS CLI.

## Downloading data with a web browser

The simplest way to browse the RFS V3 datasets is by using the [RFS Data Store](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}
or the [bucket browser](https://v3.s3.riverforecastsystem.com){:target="_blank"}. This is not the fastest way to download large amounts of data.
For better performance downloading data, you should use the command line interface instructions.

RFS allows users to download global streamflow data directly from AWS. This provides access to both retrospective simulation data and 15-day
streamflow forecasts. These datasets are hosted in S3 buckets, optimized for time series analysis and bulk downloads.

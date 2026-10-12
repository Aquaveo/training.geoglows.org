!!! danger "Bulk downloading is usually not necessary"
    Most users do not need this tutorial. All the forecast and retrospective simulation products are available for queries, bulk downloads,
    and via data service. However, the instructions for querying data are the fastest and most convenient (and cheapest for GEOGLOWS) for most uses.
    Please follow the tutorial on [querying river data](code-and-apis.en.md) before continuing to this section.

## References
Most users do not need to download the entire simulation result for the whole world. You can often be satisfied with a larger query/download. If you
proceed, you should be familiar with the awscli or a similar equivalent. A useful rule of thumb for estimating the disc space required is:

- 1 day of forecasts is about 150GB
- The hourly retrospective simulation zarr is about 6TB
- The daily retrospective simulation zarr is about 500GB
- The monthly retrospective simulation zarr is about 20GB
- The yearly retrospective simulation zarr is about 2GB

## awscli

The best way to bulk download data from s3 buckets is using a command line tool made for this purpose. These tools let you download multiple datasets
simultaneously and at higher speeds than is possible via the web browser. The basic tool for this is the awscli.
Use the [AWS S3 tutorials](https://docs.aws.amazon.com/AmazonS3/latest/userguide/download-objects.html){:target="_blank"} to get started.

!!! tip "Use `--no-sign-request`"
    Use the `--no-sign-request` flag to avoid errors, especially if you do not have aws credentials on your computer.

All RFS V3 data are stored in one bucket. When downloading data, the forecasts are under `s3://river-forecast-system-v3/forecasts15/` and the retrospective
simulation is under `s3://river-forecast-system-v3/retrospective/`. Each day's forecast is stored in its own folder by year, month, and day.

The general CLI command pattern for forecast datasets is:

```shell
aws s3 cp s3://river-forecast-system-v3/forecasts15/year=<YYYY>/month=<MM>/day=<DD>/discharge.zarr </local/save/path> --recursive --no-sign-request
```
The general CLI command pattern for retrospective datasets is:

```shell
aws s3 cp s3://river-forecast-system-v3/retrospective/daily.zarr </local/save/path> --recursive --no-sign-request
```

## s5cmd

`s5cmd` is a higher-performance alternative to `awscli`. Please consult the [s5cmd documentation](https://github.com/peak/s5cmd){:target="_blank"}.
The general CLI command pattern for forecast datasets is:

```shell
s5cmd --no-sign-request cp "s3://river-forecast-system-v3/forecasts15/year=<YYYY>/month=<MM>/day=<DD>/discharge.zarr/*" </local/save/path.zarr/>
```

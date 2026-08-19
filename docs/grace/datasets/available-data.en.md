## Storage Components

Four storage components are available to view and download. Every one is an anomaly — a departure from a long-term average — rather than an
absolute quantity.

| Name | Abbreviation | Source |
|------|--------------|--------|
| Total Water Storage Anomaly | TWSa | GRACE |
| Snow Water Equivalent Anomaly | SWEa | GLDAS |
| Soil Moisture Anomaly | SMa | GLDAS |
| Groundwater Storage Anomaly | GWSa | Calculated |

They are listed here in the order they appear in the mass balance: the GRACE total, the surface components subtracted from it, and the groundwater
result. Groundwater Storage Anomaly is calculated rather than observed — see
[Deriving Groundwater](../understanding/computational-algorithm.md#deriving-groundwater).

## Grid Resolution

The components are computed on water balance cells, which are 1.0 degree by default. A half degree option is available in the application
settings. Switching between them reloads the map and the current analysis from the other dataset, and the finer cells take longer to prepare.

GRACE is originally provided on 3 degree cells known as mascons, before being downscaled to the 1.0 and 0.5 degree anomaly cells. Both the mascon
footprints and the anomaly cell boundaries can be shown on the map from the application settings.

For how the raw data is gridded and downscaled, see
[Deriving Groundwater](../understanding/computational-algorithm.md#deriving-groundwater).

## Units and Baseline

Values are anomalies in equivalent water height. Each GLDAS component is converted to an anomaly format by subtracting the mean centered on values
from 2004 to 2009.

## Temporal Coverage

GRACE has provided monthly gravity field solutions since April 2002. Regional subsetting produces a time series from 2002 to the present for each
component on a monthly time step.

## Data Gaps

If you carefully inspect the groundwater storage time series file, you will see that there are several missing months or gaps in the data. For
example, the month of June is missing in 2003. This is because there were periods when the GRACE satellites did not produce usable data.

The largest gap is a 12-month period in 2017-2018, between the end of the original GRACE mission in 2017 and when the subsequent GRACE-FO satellites
were launched and became operational in 2018.

For the years with large gaps, it can be difficult to identify seasonal trends and apply the Water Table Fluctuation method. One way to resolve this
is to use a statistical algorithm to detect seasonal patterns in the data and impute synthetic data in the gaps; that method and the tool for
applying it are described under
[Filling Gaps in the Data](../applications/water-table-fluctuation.md#filling-gaps-in-the-data).

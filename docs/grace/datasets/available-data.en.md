## Overview

GGST serves several storage components. For simplicity, the options are given a variable name — for instance, "Total Water Storage (GRACE)" has a
variable name of `grace`, and similarly "Soil Moisture Storage (GLDAS)" is shortened to `sm`. These abbreviations are the values passed to the
`storage_type` parameter when using the [API](../accessing-data/api.md).

## Storage Options

| Name | Abbreviation | Source | Source Resolution |
|------|--------------|--------|-------------------|
| Total Water Storage | `grace` | GRACE | 0.5 degrees |
| Surface Water Storage | `sw` | GLDAS | 1.0 degrees |
| Soil Moisture Storage | `sm` | GLDAS | 1.0 degrees |
| Groundwater Storage | `gw` | Calculated | 1.0 degrees |
| Snow Water Equivalent | `swe` | GLDAS | 1.0 degrees |
| Terrestrial Water Storage | `tws` | GLDAS | 1.0 degrees |
| Canopy Storage | `canopy` | GLDAS | 1.0 degrees |

Groundwater Storage is calculated rather than observed. To learn more about how this is calculated, see
[Deriving Groundwater](../understanding/computational-algorithm.md#deriving-groundwater).

## Components Used in the Groundwater Calculation

Three of the GLDAS components are used to derive groundwater storage:

- The GLDAS canopy storage dataset (CAN)
- The GLDAS snow water equivalent (SWE)
- The GLDAS soil moisture (SM)

These are subtracted from the GRACE total water storage anomaly. See
[Deriving Groundwater](../understanding/computational-algorithm.md#deriving-groundwater).

## Selecting a Component in the App

The storage component options presented in the application include Total Water Storage (GRACE), Surface Water Storage (GLDAS), Soil Moisture Storage
(GLDAS), and Groundwater Storage (Calculated).

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

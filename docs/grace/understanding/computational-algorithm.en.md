## Overview

GRACE-derived storage anomalies rely on the Earth Observation data collected by NASA through satellites which map the gravitational field of the
Earth. Changes in gravity are driven by changes in water storage, offering a rare opportunity to monitor groundwater level through satellites
coupled with estimated surface water.

This page describes how the groundwater component is separated from that measurement using a mass balance approach, and how the result is subset to
a region of interest. For background on the data and the application that delivers it, see [Overview](overview.md).

## How the Measurement Works

The GRACE mission was launched in March 2002. It consists of a pair of satellites that are 400 km above the Earth and are separated by 200 km. As the
satellites pass over different regions of the Earth, the front and rear satellites are pulled slightly forward and backward in response to subtle
changes in the Earth's gravitational field caused by changes in surficial mass. This causes the distance between the satellites to vary, and the
changes are recorded by a k-band microwave whose accuracy is within 10 microns.

![Artist rendering of the twin satellites, with the ranging link between them](../../static/images/grace-satellites.jpg)

*Image credit: NASA/JPL-Caltech*

The GRACE satellites follow a varying path that covers the entire Earth about once per month. This data is then processed by NASA to produce a map of
the Earth's gravitational field. Each month a new map is generated and the differences are calculated to produce a gravity anomaly map. The changes
in mass are assumed to be primarily caused by the change in water storage.

Each month NASA generates a gridded map of total water storage anomaly at 3-degree resolution. This map is then down-scaled using a mass conservation
algorithm to 0.5-degree resolution and made available for download in netCDF multidimensional raster format.

## Deriving Groundwater

The groundwater component of the GRACE raw data can be separated using a mass balance approach, with NASA's Global Land Data Assimilation System
(GLDAS) models to compute the surface water component of the data. To compute total surface water storage, the components of the GLDAS models that
represent surface water storage are summed and subtracted from the GRACE dataset to estimate a groundwater storage anomaly dataset.

The application uses four sets of data:

- The GRACE TWSa dataset
- The GLDAS canopy storage dataset (CAN)
- The GLDAS snow water equivalent (SWE)
- The GLDAS soil moisture (SM)

Each GLDAS component is converted to an anomaly format by subtracting the mean centered on values from 2004 to 2009, then averaged across the three
GLDAS models to produce a component anomaly dataset: CANa, SWEa, and SMa. The standard deviation from the three GLDAS models is used to help estimate
uncertainty.

GLDAS data is normally acquired in a gridded format with a 1-degree latitude by 1-degree longitude resolution, while GRACE TWSa is served at
0.5 degrees. Reconciling the two grids is performed by an area-weighted average of the four GRACE grid cells coincident with each GLDAS grid cell.

The components can be computed on either 1-degree cells, which is the default, or on half degree cells, selected in the application settings. See
[Grid Resolution](../datasets/available-data.md#grid-resolution).

The groundwater anomaly is the difference between the TWSa and the sum of the surface water component anomalies:

```
GWa = TWSa - (SWEa + CANa + SMa)
```

The result of this computation is the groundwater storage anomaly, a tested and approved method to predict long-term changes in groundwater storage.

## Grid Subsetting

For regional subsetting, the user provides a boundary that defines the region of interest. The application selects the cells
that have cell centers within the defined boundary and calculates the average storage anomaly for each of the components — TWSa, SWEa, CANa, and
SMa — resulting in a time series from 2002 to the present for each component on a monthly time step.

The figure below shows the Chad Basin in Niger subsetted and displayed with the region boundary. Only the cells whose centers fall inside the
boundary are included in the average.

![Chad Basin in Niger, subsetted and displayed with the region boundary](../../static/images/grace-subsetted-region.png)

For water storage, the average of each component is multiplied by the area of the region, resulting in volume anomalies.

### Region Size

It is recommended that a region be at least 3x3 degrees in size. Smaller regions can be processed, but the uncertainty in the results increases. This
is because the native GRACE grid cells are 3x3 degrees in resolution before downscaling to 0.5x0.5 degrees. The GLDAS grid cells are 1x1 degree, and
therefore the resulting Groundwater Storage Anomaly (GWSa) cells are 1x1 degree resolution.

The algorithm searches the global GRACE and GLDAS grid cells to find cells where the centroid of the cells falls within the region boundary. If
the region is so small that no grid cells are found, an error message is displayed.

### Analysis at a Single Point

In addition to analyzing groundwater storage change averaged over a region, the application can be used to perform an analysis at a single point
location. This can be used to quickly generate a time series at a point of interest, or in cases where a region of interest is too small to be
processed as a region.

For a point analysis, the application finds the GRACE and GLDAS grid cells containing the selected point and returns the selected dataset time
series for the cell. If you are viewing a region, the selected point must be within the bounds of the region.

## Uncertainty Estimates

It is critical to understand that the results of these predictions have uncertainties and limitations.

To compute the uncertainty of the groundwater storage component, the uncertainty estimates from both the GRACE and GLDAS are combined by computing
the square root of the sum of the squares of the uncertainty of the individual components as measured by their standard deviations.

```
σGWa = √[(σTWSa)² + (σSWEa)² + (σCANa)² + (σSMa)²]
```

<!-- NOTE: the GGST source states this in prose as "the square root of the sum of the squares", but its
     rendered equation shows the terms SUBTRACTED:
     \sigma GWa = \sqrt {(\sigma TWSa)^2 - (\sigma SWEa)^2 - (\sigma CANa)^2 - (\sigma SMa)^2}
     The prose and the equation contradict each other in the source. We have written the sum-of-squares
     form here because it matches the prose and is the physically standard result; the subtracted form
     can go negative. Confirm with Norm Jones before publishing. -->

The resulting estimates of groundwater data are not suitable for highly precise or localized applications, such as the placement of wells; rather,
these data serve as an estimate of general trends in groundwater storage.

## Storage Depletion Curve

The application offers an option of viewing time series data in the format of a storage depletion curve, which is the time-integral of the
storage anomaly.

The storage depletion curve presents cumulative changes in water component storage relative to levels when the GRACE missions began distributing data
in April 2002. The storage depletion curve is used in groundwater management since it offers a simple visualization of how much storage aquifers have
gained or lost since a given point in time.

To compute the depletion, the application sums the GWSa over time to determine changes in groundwater storage volume over time for the region.
These data show if a region is depleting storage in the region, or if groundwater is recharging in the region, thereby providing valuable
information relative to groundwater sustainability.

An illustration of Northern Africa and the Arabian Peninsula from 2002 to 2021 shows that the groundwater in that region has been depleting since
early 2009 and onward.

![Storage depletion curve for the Arab region, 2002 to 2021](../../static/images/grace-depletion-curve.png)

## Limitations

GRACE data come with limitations that users need to know and understand. The data are provided at a relatively low resolution (1-degree latitude by
1-degree longitude) representing a 100 km x 100 km square, approximately. At such a low resolution, basing decisions on a single cell comes with high
and unknown uncertainties. Raw GRACE data is at an even coarser resolution (3-degrees latitude by 3-degrees longitude) which is then processed to
higher resolutions TWSa data.

Even with these limitations, GRACE data provide valuable insights into aquifers such as regions that are depleting and recharging, hence allowing
managers to sustainably use their groundwater resources. The best use of the application is to draw general trends in aquifers rather than selecting a
placement of a well.

It is also recommended that, whenever possible, these data be validated with local data. The application displays the uncertainties in the data
calculations as error bands on time series, providing context on regions and different time periods.

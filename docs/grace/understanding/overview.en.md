## Overview

The GRACE Groundwater Subsetting Tool (GGST) uses data from the NASA Gravity Recovery And Climate Experiment (GRACE) mission to analyze long-term
groundwater storage change for selected regions. GGST can be used to identify and characterize conditions in data-poor areas or identify trends in
other regions where trends can be obscured by noise from well data.

GGST integrates data from both the GRACE and GRACE-FO missions, and uses NASA GLDAS surface water data to derive groundwater storage changes. It
allows users to upload a geojson or json files to define regions representing countries, basins, or aquifers, aggregates the water volume changes in those regions, and displays
the results as time series plots for the whole region or at selected points. It also displays an animated map of the storage change anomalies.

GRACE provides monthly estimates of water storage anomalies in equivalent water height and has provided monthly gravity field solutions since April
2002. Estimates of mass variability and associated observational errors are available on a global 300 km grid.

While several tools have been developed for processing and visualizing GRACE data, GGST is designed specifically to support groundwater resource
management by regional stakeholders and decision-makers. This is accomplished by carefully processing the raw GRACE data to remove anomalies and
improve resolution: separating the groundwater component from the other water storage components using GLDAS, subsetting the data to specific regions
of interest, and presenting the results in a simple, intuitive interface.

The algorithm used to process the GRACE and GLDAS data to produce groundwater anomalies on both a global and regional scale is described in detail on
the [Computational Algorithm](computational-algorithm.md) page.

## How the Measurement Works

The GRACE mission was launched in March 2002. It consists of a pair of satellites that are 400 km above the Earth and are separated by 200 km. As the
satellites pass over different regions of the Earth, the front and rear satellites are pulled slightly forward and backward in response to subtle
changes in the Earth's gravitational field caused by changes in surficial mass. This causes the distance between the satellites to vary, and the
changes are recorded by a k-band microwave whose accuracy is within 10 microns.

The GRACE satellites follow a varying path that covers the entire Earth about once per month. This data is then processed by NASA to produce a map of
the Earth's gravitational field. Each month a new map is generated and the differences are calculated to produce a gravity anomaly map. The changes
in mass are assumed to be primarily caused by the change in water storage.

Each month NASA generates a gridded map of total water storage anomaly at 3-degree resolution. This map is then down-scaled using a mass conservation
algorithm to 0.5-degree resolution and made available for download in netCDF multidimensional raster format.

## Accessing GGST

GGST can be accessed through the [web application](../accessing-data/web-app.md), or by using the [API](../accessing-data/api.md) and the associated
[Google Colaboratory Notebook](../accessing-data/notebook.md) that makes the API intuitive to use.

## Further Reading

GRACE has proved an effective tool for characterizing groundwater storage changes in large regions:

- [J. Famiglietti et al., 2011](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2010GL046442){:target="_blank"}
- [J. S. Famiglietti, 2014](https://www.nature.com/articles/nclimate2425){:target="_blank"}
- [Rodell, Velicogna, & Famiglietti, 2009](https://www.nature.com/articles/nature08238){:target="_blank"}
- [Thomas, Reager, Famiglietti, & Rodell, 2014](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1002/2014GL059323){:target="_blank"}

<!-- TODO: decide whether these citations belong here or on the top-level Publications page. -->

## Acknowledgements

These tools were originally developed via funding from the National Aeronautics and Space Administration: 80NSSC20K0155; United States Agency for
International Development: Cooperative Agreement with SERVIR West Africa Hub.

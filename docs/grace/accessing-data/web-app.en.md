## Overview

GRACE Regional Analyst is a web application that provides a map interface for viewing storage components globally, animating
them over time, generating time series, and downloading results.

The application is available at
[apps.geoglows.org/grace-anomalies](https://apps.geoglows.org/grace-anomalies){:target="_blank"}.

This page covers everything you do inside the application. The concepts behind these steps — how the data is derived, how regions are subset, and
what the results mean — are covered in [Computational Algorithm](../understanding/computational-algorithm.md).

## The Map Interface

When opening the web app, the first thing visible is the map. The time slider on the bottom left changes which month is shown, and can animate the
record from one month to the next. The drawing tools in the upper right are used to define a region of interest, discussed in more detail below.

![The map interface, showing where to draw a region, change the month, and choose the displayed layer](../../static/images/web-app-interface.png)

Also in the upper right corner, the user can decide which layer they would like to view. The options are Groundwater Storage Anomaly (GWSa),
Total Water Storage Anomaly (TWSa), Soil Moisture Anomaly (SMa), and Snow Water Equivalent Anomaly (SWEa). Each is described under
[Available Data](../datasets/available-data.md).

![The Displayed Layer menu, listing GWSa, TWSa, SMa and SWEa](../../static/images/display-layer-options.png)

On the left side, there is an option to select a basemap. There are several different options to choose from.

![The basemap gallery, offering Imagery, Streets, Topographic and other backgrounds](../../static/images/base-maps.png){ width="420" }

## Selecting an Area or Point

To select an area or point, a user has a few options.

The first option is to upload a geojson of the area they are interested in. To do this, select the upload button in the upper right corner. A
pop-up will then open where the file can be uploaded. Both `.geojson` and `.json` files are accepted.

![The Upload Polygon dialog, accepting a .geojson or .json file by drag and drop or file browser](../../static/images/upload-json.png){ width="440" }

The next option is to use the drawing tools to draw a region of interest on the map. Double-click to finish the polygon.

![Tracing a region of interest on the map with the drawing tools](../../static/images/region-of-interest.png)

Another way to choose where to view the data is by using the drawing tools to select a single point of interest. A point analysis returns the time
series for the grid cells containing that point, which is covered under
[Analysis at a Single Point](../understanding/computational-algorithm.md#analysis-at-a-single-point).

The last way to choose a region is to select an existing aquifer. To do this, select "Aquifer Scale" from the upper right menu. This will load the
aquifer boundaries onto the map, and one can then be selected.

![Aquifer boundaries loaded on the map in Aquifer Scale view](../../static/images/aquifer-scale.png)

Once it is selected, the map will display just that aquifer along with its associated data.

How the region is turned into a time series — which grid cells are included, and the recommended minimum region size — is covered under
[Grid Subsetting](../understanding/computational-algorithm.md#grid-subsetting).

## Viewing and Downloading Results

Once a point or region has been selected on the map, the time series plot for the selection will load on the bottom half of the application. The
plot shows the selected component as a line with its uncertainty as a shaded band, in liquid water equivalent (cm).

![Groundwater storage anomaly time series with the uncertainty band, and the Download CSV button](../../static/images/groundwater-plot.png)

In the upper right corner of the graph is a button to download the CSV. The data that is currently displayed on the graph will be the data that is
downloaded. Change the displayed layer on the right-hand side of the map to change which variable is being graphed.

Each storage component downloads as its own file with four columns: the date, the value, and the upper and lower bounds of the error range. Dates
are in a standard date format, and the storage units are liquid water equivalent in cm.

The columns are described under
[Downloading the Water Level Time Series](../applications/water-table-fluctuation.md#downloading-the-water-level-time-series).

## Settings

The app has a couple settings that the user is able to adjust. These are found by selecting settings from the upper right menu. This will open a
pop-up with the listed settings.

![Display settings: layer opacity, water balance cells, mascon footprints, and anomaly cell boundaries](../../static/images/groundwater-settings-1.png){ width="440" }

**Layer opacity** controls how strongly the anomaly layer is drawn over the basemap. Lowering it lets the basemap show through.

**Water balance cells** switch between the 1.0 degree cells used by default and finer half degree cells. Switching reloads the map and the current
analysis from the other dataset, and the finer cells take longer to prepare. See
[Grid Resolution](../datasets/available-data.md#grid-resolution).

**GRACE mascon footprints** draw the outlines of the original 3 degree cells the data is delivered on. A slider sets the line width.

**Anomaly cell boundaries** draw the outlines of the 1.0 or 0.5 degree cells the anomalies are reported on. A slider sets the line width.

![Settings continued: color palette, color bar, and cached data](../../static/images/groundwater-settings-2.png){ width="440" }

**Color palette** sets the color scheme used for the anomaly layer. Red-White-Blue is the default, and four colorblind-safe options are available:
Viridis, Cividis, Brown-Teal, and Purple-Green.

**Color bar** shows or hides the legend on the map.

**Dynamic scale** is on by default, and fits the color scale to the minimum and maximum values in the selected region, with 0 always shown as the
center color. Turning it off uses a fixed range of -30 to +30 cm.

**Clear cached data** deletes the locally cached coordinates and global animation. The next page refresh will reload everything from the network,
simulating a first visit.

## Overview

There are 4.9 million river segments modeled in the RFS V3 datasets. These numbers come from the TDX-Hydro dataset and are different from
numbers in any other stream dataset. RFS V3 uses the same river IDs as RFS V2, but some V2 streams were removed or merged in V3 (see
[What's New](../whats-new.md) for details and a file that maps old IDs to new ones). All ID numbers are 9 digits. As a reference, this table provides IDs of some
major rivers and their general locations.

| ID Number | Select Rivers and General Locations |
|-----------|-------------------------------------|
| 760021611 | Mississippi, USA                    |
| 160064246 | Nile, East Africa                   |
| 710462910 | Colorado, USA & Mexico              |
| 441057380 | Ganges, India                       |
| 430157411 | Mekong, Vietnam                     |
| 210406913 | Tiber, Italy                        |
| 621010293 | Amazon, Brazil                      |
| 130747391 | Congo, D.R. Congo                   |
| 640255644 | Parana, Argentina                   |

The RFS ID numbers are 9 digits longs. While large numbers are often delimited, often with a comma or period in various languages, any code you write
to retrieve data ***should not*** include any delimiters. These IDs are integers. Most programming languages will interpret quotes, periods, commas,
or other characters as something besides an integer which will make the retrieval process fail. For example, the number `123456789` ***should not***
be written as `123,456,789` or `123.456.789` or `"123456789"` or `"123,456,789"` or any other variation. Only the integer representation `123456789`
will work.

## Using the Web App

The easiest way to find the ID of a river is to use the [RFS web app](https://apps.geoglows.org/rfs){:target="_blank"}. Click on a stream on
the map. To ensure you click on the exact stream you intended, the map will zoom in to a higher level of detail if you are zoomed out too far. After
clicking on a stream, the map will identify the river segment you clicked on and the ID will be presented to you in the pop-up window with charts
and other information.

## Using the Hydrography data

The Hydrography data is available in the [RFS datastore](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}. You can download and view either
the streams or catchments in a GIS software such as ArcGIS or QGIS. You can click on features or use spatial analysis tools to select many rivers. The
ID numbers for those rivers are stored in the riverId attribute.

## Find Rivers with Lat/Lon

There are many methods to attempt to find a river ID given a latitude and longitude. None are perfect for all cases. There are several potential
errors from automated methods due to the accuracy and precision of your lat/lon points, the accuracy of the stream lines in that specific location,
if you want to snap to the nearest outlet or nearest stream arc, is your lat/lon close to a confluence where the GIS would get confused by having
multiple close choices nearby, etc. Automated methods should be considered imperfect and verified for accuracy against other sources such as a known 
upstream drainage area at the lat/lon of a gauge point, the name of the river, comparisons to imagery basemaps, or other means.

One method to start with is to load the streams GIS files for your area of interest into a GIS software. You can snap them to the nearest stream arc. 
In QGIS, the tool is called "Snap geometries to layer”. Use the algorithm to find the nearest point and insert extra vertices if required.

Another method is to download the catchment polygons and intersect them with a layer containing your lat/lon points. The GIS work is straightforward 
but is occasionally less accurate and requires larger file downloads.

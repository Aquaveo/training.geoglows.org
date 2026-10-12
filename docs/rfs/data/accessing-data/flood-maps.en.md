# Accessing Flood Maps

There are 3 ways to access the flood maps.

### 1. Tool in the Hydroviewer

Flood maps are now integrated into the [Hydroviewer](../../web-apps/hydroviewer.md), and a user can view them by clicking on a stream and choosing an input
discharge value. These flood maps are computed based on this information and then displayed on the interface. A user can then download a
GeoTIFF of the flood map. This GeoTIFF can be loaded into GIS software to be viewed in other ways.

![A flood map in the Hydroviewer](../../../static/images/hydroviewer-flood-map.png)

### 2. Through the Datastore

Flood maps are available through the [datastore](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}. Code is given for creating and downloading the flood maps.
For more information on using the datastore, see [The Datastore](datastore.md).

![The Access tab for the return period flood maps in the datastore](../../../static/images/flood-maps-datastore.jpg)

### 3. On AWS

Return period flood maps are available on the [AWS bucket](https://v3.s3.riverforecastsystem.com/#flood-maps/){:target="_blank"}. They are indexed by their longitude and
latitude: each folder, such as `flood-maps/lon=-109/lat=39/`, covers one tile of 1 degree by 1 degree. Inside each tile, the
`return_period_maps` folder has one GeoTIFF for each return period (`rp2.tif`, `rp5.tif`, `rp10.tif`, `rp25.tif`, `rp50.tif`, and
`rp100.tif`). Each GeoTIFF is the flood map for a discharge equal to the flow for that return period.

![Return period flood maps in the AWS bucket](../../../static/images/flood-maps-aws-bucket.jpg)

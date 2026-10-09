# What's New?

This training site focuses on version 3 of RFS (River Forecast System). Many major changes were made between this version of the model and the previous version. This page provides some details of the upgrades and changes made to the model. If you are simply looking for information about the model, feel free to skip this page.

1. **Hydrography data**
    1. **Number of streams** - RFSv2 had about 6.8 million streams, but RFSv3 is down to about 4.9 million streams. These cuts came primarily from removing streams in major deserts; the Sahara Desert, the Gobi Desert, and the deserts of central Australia all had streams removed. Stream segments inside of lakes or in small coastal basins (or in the ocean) were also removed. Some smaller streams were merged together as well. River IDs all stayed the same in the model. If your river ID is no longer available and it is not in an area removed, you can map it to the new RFSv3 stream. The mapping between the old and new river IDs is available in the [tdxhydro_to_v3_id_map.parquet](https://v3.s3.riverforecastsystem.com/hydrography/global/tdxhydro_to_v3_id_map.parquet) file (about 87 MB).
    2. **Regions** - The hydrography data are no longer organized into 125 VPUs. Rather, they are now organized into 47 regions that are numbered from their HydroSHEDS level 2 basins.
    3. **Lakes** - A new set of lakes is shown in the hydrography dataset. This is different from the lakes that were available in RFSv2.
2. **Data storage formats** - The zarr files now use zarr version 3 rather than version 2. More metadata has been added to the files and storage has been optimized further.
3. **Changes in routing processes** - The process that routes the water through the rivers has been updated to rely entirely on a python package called riverroute and produced by Dr. Riley Hales. The process has been updated to be performed faster and some minor corrections were made to some of the model inputs.
4. **New AWS buckets** - A new AWS bucket contains all the data for version 3 of the model. It can be found here: [https://v3.s3.riverforecastsystem.com](https://v3.s3.riverforecastsystem.com).
5. **New Web Applications**
    1. HydroSOS
    2. FEWS
6. **Flood mapping products**
7. **Datastore** - A new datastore is available to download RFSv3 products: [https://apps.geoglows.org/previews/rfs-data-store/](https://apps.geoglows.org/previews/rfs-data-store/). This site provides metadata and information about the available data and allows users to browse through and download the data products of interest. See [The Datastore](what-is-it/using-datastore.md) for instructions on how to use it.
8. **Changes to this site** - This site has been updated and reorganized. Some of the more advanced information was moved to an advanced section. Information on groundwater was added as well.

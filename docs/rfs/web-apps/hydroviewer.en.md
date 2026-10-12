# Using the RFS Hydroviewer

## Overview
The [RFS Hydroviewer](https://apps.geoglows.org/previews/rfs-v3) is a web-based tool for visualizing and accessing streamflow forecasts and historical data globally. It allows users to:

- Explore real-time streamflow conditions  
- Analyze forecast trends  
- Review hydrological simulations for any river  
- Map potential flooding along a river  

The Hydroviewer supports informed decision-making in water resource management, disaster risk reduction, and climate resilience planning. Users can assess discharge values and identify potential flood or drought risks.

The interface is available in English, Spanish, and French. Use the language button at the top of the side panel to switch languages.

For more information, view the [webinar](../webinars/rfs-v2-webinar-4.md) on the Hydroviewer. Note that the webinar shows the version 2 Hydroviewer. The current Hydroviewer has more features, such as flood mapping and the hydrography explorer, that are described on this page.

![The Hydroviewer](../../static/images/hydroviewer-v3.png)

The Hydroviewer has 3 main sections - streamflow visualizations, flood maps, and hydrography explorer. Each of these sections will be explained in further detail below.

## 1. Streamflow Visualization

Streamflow visualization relates to how streams are displayed on the map. The streams are styled to allow for quick visualization based on the forecast data. The forecast initialization date defaults to show the most recent available data. However, if you would like to view the stream styles based on a forecast from a different day, you can change the forecast initialization date.

You can also choose from the drop down menu how the streams are styled. There are 5 different options available to display the streams:

1. **Standard**: No forecast coloring. Rivers are drawn by size only.
2. **Forecasted Max Flows**: Each river is colored by the highest return period it is expected to reach at any point during the forecast. This helps identify rivers experiencing high flows quickly.
3. **15 Day Timeseries**: The thickness (amount of flow) and color (return period exceeded) of each river are animated across the 3-hourly steps of the forecast. Use the time slider at the bottom of the map to play the animation or step through it.
4. **Time to Peak**: How long until each river reaches its highest flow. This is useful for seeing how much lead time there is before a peak.
5. **Below Q95 Flow**: Rivers forecast to flow below their 95th-percentile low flow, meaning they are unusually dry.

The legend in the corner of the map shows what each color means. The two buttons beside the stream style menu show or hide the legend and the time slider.

## 2. Flood Mapping

The flood mapping section computes flood maps on the fly and displays them on the map. To start using this section, begin by clicking where it says FIM Mode to make sure it is turned on.

You can choose from 5 different options for how your flood map is displayed under flood style. This determines what the discharge is for the flood map.

1. Synthetic Rating Curve Slider - If you select this option, a slider will appear. You can scroll on the slider to adjust the input streamflow for the flood map.
2. Return Period Indexed - Not currently operating
3. Manually Specified Flow - If this option is selected, you will have the option to enter in an input discharge value.
4. Forecast Timeseries - Not currently available
5. Forecast Maximum - Not currently available

Once the map style is selected, click on a stream segment on the map. You may need to zoom in to do this. Segments that are colored in red are not available. A flood map will then load. To map a longer stretch of river, click a second segment downstream; everything on the river between the two segments is selected. Click any flooded area to see the approximate water depth there.

![A flood map near Grand Junction, Colorado, for a flow of 5,000 m³/s](../../static/images/hydroviewer-flood-map.png)

This flood map can also be downloaded by selecting the download button next to the FIM menu. This will download a GeoTIFF of the drawn flood map. You can view this by loading it into a GIS software. The clear button next to it removes the selected segments so you can start again.

!!! note "About the flood maps"
    The flood maps are made with the ARC and FLDPLN methods, which map flooding from the terrain. They do not include 1D or 2D hydraulic physics, and they do not account for levees, culverts, bridges, drainage infrastructure, or current conditions. To learn more about how the flood maps are made, see the [Flood Mapping](../model-formulation/flood-mapping.md) page in the Model Formulation section.

## 3. Hydrography Explorer

This section is used to explore the hydrography (the river network) on the map. The options in this section control what happens when you click a river:

- **Data Browser**: Selects the river you click and opens its charts. This is the option the app starts in, and the only one that opens charts when you click a river.
- **River Select**: Selects only the river you click, without opening its charts.
- **Watershed Select**: Selects every river that drains to the river you click.
- **Multi Select**: Adds a whole watershed with every click, instead of replacing the last selection.
- **AOI Subsetter**: Selects an area within a watershed. Click the outlet first, then click each inlet to remove it and everything above it.

The row with the check mark is the option that is currently active. For example, with **Watershed Select** on, clicking the Gunnison River in Colorado selects it and every river upstream of it, which are highlighted in orange on the map. The number next to the option shows how many rivers are selected.

![Watershed Select highlighting the Gunnison River watershed](../../static/images/hydroviewer-watershed-select.jpg)

The buttons above the options are tools for working with the hydrography:

- **Search**: Find a river by name, or by its 9-digit river ID.
- **Styling options**: Filter which rivers are drawn and color the river network using your own rules.
- **Notable rivers**: A list of some of the largest or best-known rivers in the world, to use as examples.
- **Saved rivers**: The rivers you have saved (see Saving Rivers below).
- **Clear**: Clears the current selection.
- **Copy**: Copies the river IDs of the current selection, one per line.
- **Download**: Downloads the selected rivers and their catchments as GeoParquet files.

### Information About the Selected River

Below the selection options, the panel shows information about what is currently selected. It has two parts:

1. **A summary of the selection**: how many rivers are selected, the river ID and stream order of the outlet (the most downstream river in the selection), its region, and the range of river indexes it covers. The **Copy** and **Download** buttons use this selection.
2. **The attributes of the river you last clicked**: its river index, river ID, the ID of the outlet it drains to, the ID of the next river downstream, its TDX-Hydro region, the number of rivers upstream of it, its Strahler and Shreve stream orders, its length, the total area draining to it (contributing area), and the area of its own catchment.

![Information about a selected watershed of 530 rivers](../../static/images/hydroviewer-selection-readout.jpg)

### Searching for a River

To find a specific river:

1. Click the search button (magnifying glass) in the Hydrography Explorer.
2. Search by **River name** or by **River ID**:
    - **River name**: Start typing a name, such as "Colorado". A list of matching rivers appears, showing the country each one is in, so you can choose the right one when several rivers share a name.
    - **River ID**: Type the river's 9-digit ID, such as 760021611, and click **Search**.
3. The map zooms to the river and selects it.

The first time you search by ID, the app downloads an index of river IDs (about 17 MB). After that, searching by ID is instant.

![Searching for a river by name](../../static/images/hydroviewer-search.jpg)

### Filtering Rivers

The styling button (paintbrush) in the Hydrography Explorer opens the **Styling Options** panel, where you can choose which rivers are drawn on the map and how they are colored.

- **Presets**: Choose a ready-made style from the **Preset** menu, such as "Big rivers only", "Order ramp" (colored by stream order), or "By contributing area".
- **Filters**: Each river attribute in the list, such as stream order, contributing area, or TDX-Hydro region, has a **+ filter** button. Use it to show only the rivers that meet a condition, for example only rivers with a Strahler order of 5 or more. The filters you add are listed under **Global Visibility Filters**.
- **Styling rules**: Use the **+ rule** buttons to color rivers by an attribute. The rules are listed under **Attribute Styling Rules**, and the first rule that matches a river is the one used.
- **River names**: Check **River names** to color the river network using the table of named rivers.

![The Styling Options panel](../../static/images/hydroviewer-styling-options.jpg)

### Notable Rivers

The Hydroviewer includes a list of suggested rivers that are useful examples for exploring the app. Click the notable rivers button in the
Hydrography Explorer to open the list. Each river has two buttons: the chart icon opens the river's charts, and the location icon zooms the map
to the river. These river IDs can also be typed into the search to find the rivers directly.

![Notable rivers](../../static/images/hydroviewer-notable-rivers.png)

## Map Layers and Basemaps

Use the layer button in the top right of the map to turn on additional layers, and the basemap button below it to change the basemap. The layers include the flood inundation maps, catchments, region boundaries, HydroBASINS level 2 boundaries, and near-real-time satellite and flood observations such as the RIVER-FLD global flood composite, GOES / Himawari infrared imagery, and VIIRS true color imagery.

## Viewing Charts

Additionally, you may view charts from selected rivers. The charts display information about the forecast and retrospective data. To view these, make sure that FIM mode is turned off. Then select the chart icon at the top or if “Data Browser” is selected from the Hydrography Explorer, then a river’s charts should appear when clicked on. You can also open a river's charts by searching for it, or by choosing it from the notable rivers or saved rivers lists.

The charts open in the side panel and have three tabs:

- **Forecast**: The 15-day forecast for the selected forecast date.
- **Retrospective**: The simulated record for the river, back to 1940, and graphs derived from it.
- **Details**: Basic information about the river, such as its ID and location.

## Forecast Graphs

By default, the 15-day forecast from the current day will be displayed. However, if you would like, you can see a forecast from a previous day by choosing a different forecast initialization date in the Streamflow Visualization section.

![Forecast Graph](../../static/images/forecast.png)

An example of a forecast graph is shown here. The graph shows the median forecast, the spread of the ensemble members, and the return period thresholds for that river. More information on interpreting this plot is found in the [Forecast Data](../data/available-data.md#15-day-forecast-data) section of this training.

## Retrospective Graphs

You can view the retrospective data by selecting the **Retrospective** tab. Use the buttons above the graph to show the last 1, 5, 10, or 30 years, or the entire record. You can also drag a box on the graph to zoom in.

![Retro Data](../../static/images/retro_data.png)

This is the main retrospective plot, but other graphs exist that are derived from this retrospective data. They are designed to help interpret and analyze the data. They represent interpretations of the retrospective data, but are not all inclusive. Not all plots will be helpful in all use cases. The plots available are evolving based on current research.

### Yearly Cumulative Discharge

![Cumulative Discharge](../../static/images/cumulative_discharge.png)

This graph shows one value for each year in the retrospective simulation, representing the total discharge volume over that year for that stream. This is represented by the blue line on the graph. The red lines show 5 year averages of the volume to represent how the volume in the stream may be changing over time.

### Cumulative Volume by Year

![Cumulative Volume](../../static/images/cumulative_volume.png)

This graph shows the cumulative volume in millions of cubic meters throughout the year. The wettest and driest years are labeled to show an idea of the range of values that have been seen in the past. By hovering over a line on the hydroviewer it will tell you the specific year for each line. This graph also shows when the volume of water is most rapidly increasing, representing more streamflow.

### Monthly Average Flow with HydroSOS Categories

![Monthly Average Flow](../../static/images/monthly_average_flow.png)

This graph has features that can be toggled on and off to highlight different things.
The default view shows the monthly average flows from the entire period of record (the dotted blue line) and the year to date monthly averages (the black line). Additional years can be turned on and off to see how those monthly averages compare.
Additionally, the HydroSOS levels can be toggled on and off to show the range of streamflow conditions—very dry, dry, normal, wet, and very wet—throughout the year. It is based on methods developed by the WMO for their HydroSOS initiative. The category ranges are calculated using historical monthly averages. Each month's values are ranked separately and assigned a percentile. These percentiles are then used to define the thresholds for each category.
This graph helps users understand how river flow values in a given year compare to what is considered normal, and whether conditions were wetter or drier than usual for each month.

### Annual Peak Discharge

![Peak Discharge](../../static/images/peak_discharge.png)

This graph is designed to show information about the peak discharge of a river. The location tells about the time the discharge occurred and the color tells about the amount of water. The y-axis represents the different years. A dots location along the x-axis shows when in the year the peak discharge occurred. The colors represent the values of the peak discharge when it occurred. Outliers are highlighted in red.

### Raster Hydrograph

![Raster Hydrograph](../../static/images/raster_hydrograph.png)

A raster hydrograph is a grid-based visualization showing the temporal variation of streamflow for a single river. The x-axis represents months, the y-axis represents years, and the color of each cell indicates the streamflow magnitude. The point is that you can see all 85 years at once. Looking across a row shows the flow for one year, while looking up or down a column shows the same date across all years, for example every March 15th. This makes it easy to identify seasonal patterns, quickly see wet and dry periods, and spot outliers or years where the wet season was longer or shorter than normal.

### Flow Duration Curve

![FDC](../../static/images/fdc.png)

This graph displays streamflow on the y-axis and exceedance probability on the x-axis. Each point represents a monthly flow value, showing how often that level of flow is exceeded. In addition to the individual monthly values, the graph includes an overall flow duration curve based on the entire dataset. This allows users to compare monthly flow patterns with the long-term distribution of flows. By default only the overall curve is shown and the individual months must be toggled on to see them.

## Details

The **Details** tab shows basic information about the selected river:

- **riverId**: The river's unique 9-digit ID. Use this number to find the river again or to look up its data.
- **lat** and **lon**: The latitude and longitude of the river.
- **riverIndex**: The river's position in the river network order used by the RFS data files.
- **upstreamCount**: The number of river segments upstream of this river. A large number means the river drains a large network, such as a major river near its outlet.

![The Details tab](../../static/images/hydroviewer-details.jpg)

## Saving Rivers

To save a river, open its charts and click the heart icon next to the river's name, then give it a name. Saved rivers are outlined on the map and listed under the saved rivers button in the Hydrography Explorer, where they can be sorted by name or river ID. Saving rivers requires signing in (see Settings below).

## Forecast Reports

The reports button at the top of the side panel builds a printable document for a list of rivers, either your saved rivers or the notable rivers. There are two types of report:

- **Daily Forecast Report**: One page per river, with the 15-day forecast, a table of the chance of exceeding each return period on each day, and room for notes.
- **Flood Alerts Bulletin**: One page per river, headed by a color-coded flood alert, with the peak and mean flows and how the forecast compares with what the river normally carries at this time of year.

Choose the report type, the list of rivers, and the forecast date, then click **Generate**. When it is finished, use **Print / Save as PDF** to save it.

## Help, Language, and Display

The buttons at the top of the side panel include a few options for getting help and changing how the app looks:

- **Help** (question mark): Opens a panel that explains each part of the app in more detail, including the keyboard shortcuts.
- **Language**: Switches the app between English, Spanish, and French.
- **Theme** (sun icon): Switches between light and dark mode.

## Settings

You can sign in with the **Sign in** button at the top of the side panel. This is the same GEOGLOWS login used for the [datastore](../data/accessing-data/datastore.md), which requires a login to download data. Signing in allows you to join the GEOGLOWS mailing lists and to save rivers. Your saved rivers are stored in your profile, so they are available on any device you sign in from.

The settings menu (the gear icon at the top of the side panel) holds display options, such as shading the warning levels on the charts and outlining saved rivers on the map. It also lists the data the app has copied to your device to make it faster, such as the river ID index used for searching. These copies can be deleted at any time.

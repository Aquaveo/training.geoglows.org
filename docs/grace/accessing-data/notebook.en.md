## Overview

An example of calling the GGST API using Python is provided in a Google Colab Notebook. Google Colaboratory is a web based Python programming
environment hosted in the Google Cloud that is a component of the Google Drive environment.

You may implement the API on your own, but the Colab notebook is recommended: it is designed to run each of the API functions and help you download
and visualize the data.

[Open the GGST API notebook in Colab](https://colab.research.google.com/github/BYU-Hydroinformatics/ggst-notebooks/blob/main/ggst_api.ipynb){:target="_blank"}

You may wish to make a copy of the notebook in your own Google Drive.

## Running the Notebook

Run each cell of the notebook by hitting the play button on the left side of each cell and provide the necessary inputs by following the prompts. The
notebook runs through all four of the API functions.

To run some of the functions in this notebook, the user will have to sign up for an account and obtain an authentication token (API key). See
[Obtaining an Authentication Token](api.md#obtaining-an-authentication-token).

The notebook is divided into multiple sections and each section contains a set of cells, each of which contains Python code. When you first launch
the notebook, the sections are collapsed and you need to expand each section to view and run the code. The cells should be run sequentially. Some
cells require inputs, which you should enter before running the associated cells. Some cells produce outputs, displayed just below the cells.

## Notebook Sections

The code is divided into six sections designed to help the user understand how to call each of the four functions and how to plot and visualize them.

**Install Packages and Select your Portal.** Dependencies and other Python packages are installed and set up for the processing of the shapefile and
rendering of the graph in later cells.

**Function 1: getStorageOptions.** Lists all the available options and how to properly declare them in the appropriate cell.

**Function 2: getPointValues.** The user types in latitude and longitude coordinates and selects the desired storage option from a drop-down menu.
The next several cells create a dataframe, chart the timeseries, and plot a graph with estimated error bars.

**Requesting Info for Regional Functions 3 and 4.** The last two functions are regional functions and require more inputs to run. First, you will be
asked for your API token, which must match your declared portal to work. Second, you will be asked to give your region a name that will be used in
naming the files. Lastly, you will be asked to upload a zipped shapefile of the region of interest. This should contain four files — a `.shp`,
`.shx`, `.prj` and `.dbf` — zipped in a single folder.

**Function 3: getRegionTimeseries.** Asks for your desired storage option using a drop-down menu, calls the API, then displays an interactive table
and graph of the data returned.

**Function 4: getRegionZipfile.** Calls the API and returns a set of netCDF files which can be accessed from a tool bar on the left side of the
screen.

This section will also help you create a dataframe, plot your data, and visualize your data on an animated map.

## Exporting a Time Series

After generating and plotting the storage anomaly time series, run the line of code to export the Python Pandas data frame containing the time series
to a CSV file. This file will then appear in the files section of the Colab interface on the left. Click the three vertical dots to the right of the
file and select the Download option.

The resulting CSV file has the dates in the correct format and no changes are necessary. See
[Downloading Results](web-app.md#downloading-results).

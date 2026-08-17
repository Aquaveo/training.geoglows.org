## Overview

The GRACE Groundwater Subsetting Tool (GGST) is a web application that provides a map interface for viewing storage components globally, animating
them over time, generating time series, and downloading results.

The application is available at
[apps.geoglows.org/grace-anomalies](https://apps.geoglows.org/grace-anomalies){:target="_blank"}.

This page covers everything you do inside the application. The concepts behind these steps — how the data is derived, how regions are subset, and
what the results mean — are covered in [Overview](../understanding/overview.md).

## The Map Interface

<!-- TODO: The app interface has changed. Write this section against the current version of the app.
     Previously covered: storage component selector, region selector, time controls and animation,
     display options. Include screenshots once the interface is settled. -->

## Point Analysis

<!-- TODO: Write against the current version of the app.
     Previously covered: zoom to the area of interest, choose a storage component, activate the
     point selection tool, select a location, read the resulting time series plot, reopen a closed
     time series window, and clear selected points.
     The reasoning for when to use a point at all lives in
     ../understanding/computational-algorithm.md#analysis-at-a-single-point -->

## Region Analysis

<!-- TODO: Write against the current version of the app.
     Previously covered: choosing an existing region from the region selector, choosing a storage
     component, and viewing the resulting time series. -->

## Downloading Results

When exporting a time series, the data in the time series are saved to a tabular file with columns for the date, and each component of the time
series is exported as a separate column. Files can be exported as either a comma separated values (CSV) file or an Excel (XLS) file. The storage
units are liquid water equivalent in cm.

<!-- TODO: Write the export steps against the current version of the app.
     Previously covered: downloading plots and tables, and exporting a time series as CSV or Excel
     from the time series window menu. -->

### Fixing the Dates

<!-- WRITE ME (Rachel): Confirm the export format in the current version of the app.
     Everything below describes the old behavior — the date column arriving as epoch milliseconds.
     If the current version exports readable dates, delete this whole section; the conversion advice
     is then not just unnecessary but actively misleading. -->

The date column is saved in a unique format representing the number of milliseconds since January 1, 1970. This can be converted to a more typical
date format using a spreadsheet formula.

Create a new column and enter the conversion formula for the first date in the list. The formula converts the number from milliseconds to days and
then adds that number to the date value corresponding to January 1, 1970, thus creating a proper date value. To see this value, change the number
format to one of the standard date options. Whether it appears as month/day/year or day/month/year will depend on your regional settings.

<!-- TODO: the GGST documentation shows this formula only as an image (images-wtf/fixing_the_date.png),
     so the exact formula text is not available in the source. Obtain it and reproduce it here rather
     than reconstructing it. -->

Time series downloaded from the [Colab notebook](notebook.md) already have the dates in the correct format, and no changes are necessary.

## Administrative Functions

<!-- TODO: Write against the current version of the app.
     Previously covered: logging in, the Add a Region, Delete a Region, and Update Global Files
     configuration pages, automatic processing of each storage component, deleting a region, and
     which pages are visible when not logged in.
     NOTE: the old shapefile upload requirement (four unzipped files, EPSG:4326) no longer applies in
     the current version of the app. Document whatever replaced it. -->

!!! warning "Uploading affects every user"
    An uploaded region is not private to you, and deleting one removes it for everyone. Before adding a region, check that an equivalent boundary
    does not already exist.

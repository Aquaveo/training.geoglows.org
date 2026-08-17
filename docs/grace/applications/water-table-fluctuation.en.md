## Overview

In addition to obtaining the GRACE-derived groundwater storage anomaly, it is possible to analyze the storage anomaly time series to extract an
estimate of annual recharge using a technique called the Water Table Fluctuation (WTF) method.

The WTF method was originally developed to estimate recharge from seasonal fluctuations in groundwater levels measured directly in monitoring wells.
When a water level time series exhibits seasonal fluctuations, it is assumed that the declining period during the dry part of the year results from
pumping and groundwater discharge, and the rise during the wet part of the year is the result of recharge.

Using water levels derived from a monitoring well, recharge is estimated as follows:

```
R = Sy × (Δh / t)
```

where Δh is the rebound in water level, t is the time period (typically one year), and Sy is the specific yield or appropriate storage coefficient.

The storage coefficient is necessary because the water level rise in the surrounding aquifer occurs in the fractional void space, and the storage
coefficient converts it to the appropriate liquid water equivalent component in the [length]/[time] infiltration rate units used by recharge. If this
analysis is performed using the groundwater storage anomaly curve derived from GRACE, a storage coefficient is not needed, as the anomaly is already
in liquid water equivalent form and recharge can be estimated directly as:

```
R = ΔGWSa / Δt
```

where ΔGWSa is the rise in groundwater extracted from the GRACE-derived groundwater storage anomaly curve.

## Methods for Estimating Recharge Component

There are two general approaches for determining the height of the rise associated with recharge.

With the more conservative method, the rise is measured from the trough to the next peak as follows:

```
R_method_1 = ΔGWSa / Δt = (Sp - SB) / Δt = RS
```

Another method is to assume that the groundwater decline as a result of pumping and discharge continues at the same rate in the wet season, and
therefore the rise should be computed from a linear extrapolation of the declining line as follows:

```
R_method_2 = ΔGWSa / Δt = (Sp - SL) / Δt = RS + RD
```

The recharge rates extracted from these two equations could be considered a low and a high estimate, although in the experience of the GGST authors,
method 1 seems to be the most accurate.

<!-- TODO: reproduce the figure defining Sp, SB, and SL (images-wtf/rs_rd_fig.png). The method is
     very hard to follow without it. -->

An example of applying the WTF method to estimate recharge in Southern Niger can be found in
[Evaluating Groundwater Storage Change and Recharge Using GRACE Data: A Case Study of Aquifers in Niger, West Africa](https://www.mdpi.com/2072-4292/14/7/1532){:target="_blank"}.

## Downloading the Time Series

To apply the WTF method, first download the groundwater storage anomaly time series. Load the region and select the Groundwater Storage (Calculated)
storage component, then export the time series.

<!-- TODO: The app interface has changed. Write the download steps against the current version of
     the app. See ../accessing-data/web-app.md -->

The time series can also be downloaded directly from the Colab notebook, in which case the dates are already in the correct format. See
[Colab Notebook](../accessing-data/notebook.md) and [Downloading Results](../accessing-data/web-app.md#downloading-results).

## Filling Gaps in the Data

For the years with large gaps, it can be difficult to identify seasonal trends and apply the WTF method. See
[Data Gaps](../datasets/available-data.md#data-gaps).

One way to resolve this problem is to use a statistical algorithm to detect seasonal patterns in the data and impute synthetic data in the gaps. This
can be accomplished using a simple seasonal decomposition model (`statsmodels.tsa.seasonal.seasonal_decompose`) implemented in the statsmodels Python
package.

This model first removes the trend using a convolution filter (the trend component), then computes the average value for each period (the seasonal
component) — in this case months — with the residual component being the difference between the monthly average and the actual monthly measurements.
The GWSa time series is decomposed into three components: the trend, the seasonal, and the random components:

```
Y[t] = T[t] + S[t] + e[t]
```

where `Y[t]` is the GWSa, `T[t]` is the GWSa trend, `S[t]` is the seasonal GWSa component, and `e[t]` is the residual GWSa component.

To impute the missing data, the trend from the data decomposition is used, then the average of the monthly and residual values for that month is
added to estimate the missing value:

```
Y[t] = y(T[t]) + mean(S[t] + e[t])
```

## Data Imputation Tools

The Python code to perform the imputation is implemented in a Google Colab notebook. After launching the notebook, follow the instructions in the
code.

[Open the gap imputation notebook in Colab](https://colab.research.google.com/github/BYU-Hydroinformatics/ggst-notebooks/blob/main/impute_gaps_GRACE.ipynb){:target="_blank"}

Before running the code, you will need to prepare and upload a CSV file with the original data with the gaps. This file will need to contain only two
columns, which you can copy and paste from the full CSV and then save as a separate CSV file (`base_file.csv`, for example).

<!-- TODO: the GGST docs provide a sample file for this step (west-gwsa-raw-clean.csv). Decide whether
     to host a copy here or link to theirs. -->

## Multi-Linear Trend Analysis

In the seasonal decomposition method described above, a single linear trend was described. However, many data sets exhibit multiple linear trends.

The Python script has an option to perform a multi-linear regression analysis. For the sample dataset there are four distinct trends, set by giving
the `number_breakpoints` variable a value of 3 — note that 3 interior breakpoints result in four linear trends.

## Data Processing Examples

Once the gaps have been filled, the last step is to plot and analyze the curves one season at a time, extract the GWSa values from the curve, and
calculate the recharge estimate using either method 1 and/or method 2.

An Excel file provided by the GGST authors illustrates how to examine and process each season of data from a GRACE-derived and imputed groundwater
storage anomaly time series. After opening the file, copy and paste the GWSa values generated by the imputation algorithm. Note that the imputed
values have more digits than the original values. Formulas in columns C and D separate the imputed data in column B to allow a multi-colored plot
where the original imputed sections can be clearly visualized.

You can then browse through each of the tabs for the years starting in 2002. On each page, the seasonal values are automatically pulled from the main
sheet using a VLOOKUP formula. For each page, manually adjust the red and green lines to fit the descending branch and the base. Then manually scale
off the `Sp`, `SB`, and `SL` values in cm from the vertical axis and enter them into the three cells indicated in the diagram. The `RS`, `RD`, `R1`,
and `R2` values will then be automatically calculated.

As you examine the plot for each year, you may need to adjust the range of the vertical axis before you can properly fit the lines. To do this,
double-click on the vertical axis, click on the axis options tab, and manually adjust the minimum and maximum bounds to properly frame the plot.

If you need to add additional years, copy one of the yearly sheets, rename it, and change the year at the top of the sheet. After processing all of
the years and calculating all of the `R1` and `R2` values, you can see a summary in the Summary sheet.

<!-- TODO: the GGST docs provide the workbook (west-gwsa-wtf.xlsx). Decide whether to host a copy
     here or link to theirs. -->

# Performing Bias Correction on River of Interest

You are able to perform bias correction on any river from RFS given that you know the LINKNO and have observed data to match up with the river. The easiest way to perform bias-correction is by using the function in the [python package] (https://geoglows.readthedocs.io/en/latest/api-documentation/bias.html). There is a function to correct the historical data and another to correct the forecast data.

## Bias Correction - Forecast Example

This Colab notebook offers a step-by-step guide for performing bias correction on RFS forecast values. It shows how to adjust forecasted
streamflow values using historical observations, improving the accuracy of predictions and aligning the data with real-world measurements for better
hydrological analysis:

[Bias_Correction_GEOGloWS_ECMWF_Hydrological_Model_Forecast Colab.ipynb](https://colab.research.google.com/drive/1AWwF60XP_6GKhl1fe9KDhhndT802cHUq?usp=sharing)

## Bias Correction - Retrospective Example

To dive deeper into the analysis of bias correction and performance evaluation, we have prepared an interactive Google Colab notebook. This notebook
provides step-by-step guidance for conducting these analyses using real-world data from the Magdalena River at El Banco in Colombia. It covers both
bias correction and performance evaluation, allowing you to engage with the data and methods discussed in this
guide: [Bias_Correction_GEOGloWS_ECMWF_Hydrological_Model_Retrospective_Simulation Colab.ipynb](https://colab.research.google.com/drive/19gr9icMEUwZdT6ae6DPG-IwGeWTS3mKk?usp=sharing).
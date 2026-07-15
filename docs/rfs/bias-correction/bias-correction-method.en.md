# Bias Correction Method

RFS exhibits biases that can limit its precision, prompting the development of a bias correction approach. To correct these systematic biases at
instrumented locations, we propose the Monthly Flow Duration Curve Quantile-Mapping (MFDC-QM) method. This method targets biases related to flow
variability and correlation. RFS does not assimilate observed streamflow data into its initial calculation. However, the bias-correction technique
allows for the global data to be applied locally. Local users can have more confidence in their data because they can know that their observed data is
able to be used to improve the modeled data at their location.

After applying the bias correction, we observed a significant improvement in the distribution of bias and variability ratios, with a slight
improvement in correlation values across the stations, resulting in more reliable simulations and improved Kling-Gupta Efficiency (KGE) metrics: bias,
variability, and correlation.

The following presentation discusses how RFS has been validated and gives details of the methods of the bias-correction
methods.

[GEOGLOWS - Bias Correction.pdf](https://drive.google.com/file/d/1-GyWh_lY2AjRTXM7aRknqmJiIEh_BqMd/view?usp=sharing)

RFS applies bias correction to its forecast data by assuming the forecast shares the same biases as the retrospective simulation. This process
involves mapping forecasted streamflow values to a non-exceedance probability using the historical simulation's flow duration curve and then replacing
the forecasted values with corresponding values from the observed flow duration curve.

![forecasts](../../static/images/forecast-bias-correction.png)

This method helps improve forecast accuracy, particularly during earlier forecast lead times, aligning the data more closely with historical
observations. However, improvements are limited by the assumption that the biases in forecast data are identical to those in the retrospective
simulation. The following images show how the KGE values improved for the forecasted model after applying the bias correction techniques.

![kge](../../static/images/global_kge1.png)

![kge](../../static/images/global_kge2.png)

For more information see this powerpoint: [Bias_Correction_Forecast_Data.pdf](https://drive.google.com/file/d/1Fu4KhqhW6lW1eI8U2pcuHJFyCTqw5Qrn/view?usp=sharing)
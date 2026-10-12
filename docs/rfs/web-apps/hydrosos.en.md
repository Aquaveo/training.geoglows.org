# HydroSOS App

## Overview and Goals

This application aims to help provide a visualization of current water conditions around the world as well as potential future conditions for individual river conditions.

Reliable water data are key to inform decision makers about current hydrologic conditions so they can take necessary actions to manage their water resources.
Having accurate, dependable insights into local water conditions—both present status and projected outlooks—is essential for guiding management choices across water supply, hydroelectric power, and reservoir operations. By drawing on historical records alongside model forecasts, status and outlook tools present current and expected trends in their proper historical framework. These products combine key indicators with interactive maps and charts, helping managers quickly compare ongoing and future hydrologic patterns against normal baselines to support effective decision-making.

HydroSOS (Hydrologic Status and Outlook) is an initiative created by the WMO (World Meteorological Organization) which presents a standard method for comparing current and forecasted conditions to the historical average for the same time of year. Their methods apply to several hydrologic variables, but for the RFS contributions, we focus on streamflow because that is the variable provided by RFS. To learn more about it, look at the WMO’s pages: [https://wmo.int/activities/hydrosos/global-hydrological-status-and-outlook-system-hydrosos](https://wmo.int/activities/hydrosos/global-hydrological-status-and-outlook-system-hydrosos) and [https://wmohydrosos.ceh.ac.uk/](https://wmohydrosos.ceh.ac.uk/). They have also built a [HydroSOS portal](https://wmohydrosos.ceh.ac.uk/portal/) designed to display HydroSOS based on information from several different sources. RFS provides streamflow data into the portal, and that same information is displayed in this application.

## How to Use the App

### Global View

Explore the global map to see the current hydrologic status of river basins. Each basin is colored based on its HydroSOS category for the month displayed in the upper right hand corner. You can select the calendar button to choose to have a different month displayed.

![The HydroSOS Water Monitor web application](../../static/images/hydrosos-app.png)

### Select a Basin

You may select a basin either by clicking on it directly on the application or by searching it in the search bar. To search a basin you may either search by basin name (ex: Mississippi) or by its HydroBASINS ID for a level 4 river basin. Once you select a basin, there may be a period of loading and then a side panel will display graphs and information about that specific basin.

### Interpreting Charts

At the top of the side panel you will see the name of the basin, its status and some basic information about it.

Next you will see a chart for the Monthly HydroSOS status. The colored bands show what the ranges are for each of the categories in HydroSOS. Then the black line shows the current year monthly averages, displaying what categories the streamflow has been throughout this year. There is then a prediction for what the next couple months could look like with a range of possibilities.

![Monthly HydroSOS status chart](../../static/images/hydrosos-monthly-status.png)

The next graph shows streamflow as a cumulative volume throughout the year. The HydroSOS categories and the RFS streamflow values are both changed to volumes. The historical volumes are then used to show a prediction of what the total volume could be in three months from now based on what volumes were seen in those months in the past.

![Three-month seasonal outlook chart](../../static/images/hydrosos-seasonal-outlook.png)

The next graph displays the cumulative volume of the river. Each grey line represents a different year. The blue line displays the median year.

![Cumulative volume chart](../../static/images/hydrosos-cumulative-volume.png)

The last graph displays the historical runoff. It displays the total annual volume for each year (displayed in grey) and then compares that to a 5-year moving average.

![Historical annual runoff chart](../../static/images/hydrosos-annual-runoff.png)

## Understanding Basin Status

Basin colors represent the percentile of current cumulative runoff relative to the historical reference period. They are used by ranking monthly averages. Each month is only compared to itself - January is compared to January, February is compared to February, etc. Then they are labeled based on where they fall in the percentiles.

| Status   | Percentile range           |
|----------|----------------------------|
| Very Dry | Below the 10th percentile  |
| Dry      | 10th–30th percentile       |
| Normal   | 30th–70th percentile       |
| Wet      | 70th–90th percentile       |
| Very Wet | Above the 90th percentile  |

## Basin Boundaries

The application uses HydroBASINS level 4 to define river basin boundaries and associate hydrologic information with individual basins. Each basin is identified using a unique HydroBASINS ID. The outlet RFS stream for each basin was found and selected to represent the streamflow conditions in that basin. The streamflow values from that stream were used to color the entire basin. If the basin was not well represented by a single stream, then it was left blank.

## Bias-Corrected Data

This web application provides an option to use global bias-corrected hydrologic data. This loads the RFS globally bias corrected data using the SABER method. Please see the [advanced section](../advanced/bias-correction/saber-method.md) for more information about what this is and how to use it. The rankings for each basin will not change, but the absolute values will change. Therefore, the displayed map will not change by displaying this option, but the values in charts for each basin will. Because the bias-corrected data are retrieved separately, enabling this option may increase loading time.

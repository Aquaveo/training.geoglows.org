# FEWS App

This web application is designed to quickly display flood warnings. It uses data from the RFS model as well as [Google’s Flood Hub](https://sites.research.google/floods/l/0/0/3) to display basins that are experiencing a high risk for flooding. Places at most risk for flooding are highlighted on the map.

![The FEWS4All web application](../../static/images/fews-app.png)

Basins can be selected and a side panel will open to show which model(s) believe there is a flood risk as well as the flood risk presented from that model.

![Flood warnings from each model for a selected basin](../../static/images/fews-warnings.png)

Each model's card shows the river or gauge ID it used, along with the forecast details. Under this information is displayed information about total population and infrastructure in this basin. This provides context for what impacts the flood could have.

![Population and infrastructure impacts for a selected basin](../../static/images/fews-impact.png)

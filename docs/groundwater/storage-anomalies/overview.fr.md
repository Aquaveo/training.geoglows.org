## Vue d'Ensemble

La mission GRACE (Gravity Recovery And Climate Experiment) de la NASA fournit des données permettant d'analyser l'évolution à long terme du stockage
des eaux souterraines pour des régions sélectionnées. Ces données permettent d'identifier et de caractériser les conditions dans les zones pauvres en
données, ou de mettre en évidence des tendances dans d'autres régions où elles peuvent être masquées par le bruit des données de puits.

GRACE fournit des estimations mensuelles des anomalies de stockage en eau exprimées en hauteur d'eau équivalente, et produit des solutions mensuelles
du champ de gravité depuis avril 2002. Les estimations de la variabilité de masse et les erreurs d'observation associées sont disponibles sur une
grille globale de 300 km.

![Carte globale des anomalies de gravité mesurées par GRACE](../../static/images/grace-globe.png){ width="388" }

## Anomalies de Stockage Dérivées de GRACE

GRACE mesure l'eau totale stockée dans une colonne de la Terre : neige, eaux de surface, humidité du sol, eau interceptée par la végétation et eaux
souterraines réunies. Une approche de bilan de masse est utilisée pour isoler la composante souterraine de ce total et la restituer pour une zone
d'intérêt.

En intégrant les données des missions GRACE et GRACE-FO et en utilisant les données d'eaux de surface GLDAS de la NASA, il est possible d'observer
les variations du stockage des eaux souterraines. La nature globale de ces données permet aux utilisateurs de définir des régions représentant des
pays, des bassins ou des aquifères, d'agréger les variations de volume d'eau dans ces régions et d'obtenir les résultats sous forme de graphiques de
séries temporelles pour l'ensemble de la région ou en des points sélectionnés.

L'algorithme utilisé pour traiter les données GRACE et GLDAS afin de produire des anomalies d'eaux souterraines à l'échelle globale et régionale est
décrit en détail sur la page [Algorithme de Calcul](computational-algorithm.md).

## L'Application Web

GRACE Regional Analyst est une application web qui diffuse les anomalies de stockage dérivées de GRACE. Bien que plusieurs outils aient été
développés pour traiter et visualiser les données GRACE, celle-ci est conçue spécifiquement pour appuyer la gestion des ressources en eaux
souterraines par les acteurs et les décideurs régionaux. Cela est réalisé en traitant soigneusement les données brutes de GRACE afin d'éliminer les
anomalies et d'améliorer la résolution : en séparant la composante souterraine des autres composantes du stockage en eau à l'aide de GLDAS, en
découpant les données selon des régions d'intérêt précises et en présentant les résultats dans une interface simple et intuitive.

Elle permet aux utilisateurs de téléverser des fichiers JSON ou de dessiner une région sur la carte pour leurs zones d'intérêt. Elle affiche
également une carte animée des anomalies de variation du stockage.

![GRACE Regional Analyst affichant l'anomalie globale du stockage des eaux souterraines](../../static/images/web-app-overview.png)

L'application est disponible à l'adresse
[apps.geoglows.org/grace-anomalies](https://apps.geoglows.org/grace-anomalies){:target="_blank"}. Voir
[Utilisation de l'Application Web](../accessing-data/web-app.md).

## Pour Aller Plus Loin

GRACE s'est révélé un outil efficace pour caractériser les variations du stockage des eaux souterraines dans les grandes régions :

- [J. Famiglietti et al., 2011](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2010GL046442){:target="_blank"}
- [J. S. Famiglietti, 2014](https://www.nature.com/articles/nclimate2425){:target="_blank"}
- [Rodell, Velicogna, & Famiglietti, 2009](https://www.nature.com/articles/nature08238){:target="_blank"}
- [Thomas, Reager, Famiglietti, & Rodell, 2014](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1002/2014GL059323){:target="_blank"}

<!-- TODO: decide whether these citations belong here or on the top-level Publications page. -->

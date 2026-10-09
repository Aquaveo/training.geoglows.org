## Couche Living Atlas

Le meilleur moyen d'explorer les résultats du RFS est d'utiliser une carte web disponible gratuitement via l'**ArcGIS Living Atlas of the World**. Vous n'avez pas besoin d'une
licence ArcGIS pour utiliser cette couche. Vous pouvez visualiser la couche et interagir avec elle dans ArcGIS, QGIS, des applications JavaScript et la plupart des outils que vous utilisez habituellement pour exploiter des données SIG.

Vous pouvez l'ajouter à des cartes web en tant que couche web sans avoir besoin de télécharger les données supplémentaires ou le réseau de cours d'eau. Si vous souhaitez télécharger l'hydrofabric ou d'autres données, vous les trouverez dans le [magasin de données du RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3).

![capture d'écran](../../static/images/imagen.png)

La couche est dite « temporelle » (time-enabled), ce qui signifie qu'elle contient des données attributaires décrivant chaque segment de rivière sur les 10 premiers jours de chaque prévision quotidienne. À l'aide de
ces informations, les cours d'eau sont animés pour changer de couleur et de taille en fonction de la quantité d'eau prévue dans la rivière et selon que cette valeur dépasse ou non un
niveau de période de retour.

Quelques actions qu'un utilisateur peut effectuer avec cette couche :

- Les données de prévision peuvent être visualisées successivement dans le temps grâce au curseur intégré à l'application. Un utilisateur peut observer les cours d'eau par fenêtres de 3 heures.
  La couleur des cours d'eau change si le cours d'eau connaît un débit élevé pendant cette période.
- Les entités peuvent être identifiées en cliquant sur la carte. Des fenêtres contextuelles préconfigurées affichent les noms de rivières issus de la communauté OpenStreetMap.

[Plus d'informations](https://www.arcgis.com/home/item.html?id=8f0573e0c0b9491dbeafde9c72ccf02b) sur la couche de carte web sont disponibles sur le site ArcGIS. Des informations sur le chargement des couches Living Atlas dans ArcGIS sont disponibles [ici](https://enterprise.arcgis.com/en/portal/10.5/use/add-living-atlas-layers.htm).

Pour charger cette carte dans QGIS, procédez comme suit :

**Étape 1 :** Au bas de la page d'informations de la couche de carte Esri, sur le côté droit, se trouve le lien URL permettant d'accéder à la couche de carte :  
https://livefeeds3.arcgis.com/arcgis/rest/services/GEOGLOWS/GlobalWaterModel_Medium/MapServer  
Copiez ce lien dans votre presse-papiers.

**Étape 2 :** Dans votre logiciel SIG, allez dans *Couche* → *Ajouter une couche* → *Ajouter une couche ArcGIS REST Service*.

![capture d'écran](../../static/images/qgis.png)

**Étape 3 :** Cliquez pour ajouter une nouvelle couche de service REST. Saisissez un nom pour la couche et collez l'URL copiée dans la fenêtre.

La couche peut également être utilisée dans les [Esri Instant Apps](https://www.esri.com/en-us/arcgis/products/arcgis-instant-apps/overview).

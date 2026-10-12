# Accès aux Cartes d'Inondation

Il existe 3 façons d'accéder aux cartes d'inondation.

### 1. Outil dans le Hydroviewer

Les cartes d'inondation sont désormais intégrées au [Hydroviewer](../../web-apps/hydroviewer.md), et un utilisateur peut les afficher en cliquant sur une rivière et
en choisissant une valeur de débit d'entrée. Ces cartes d'inondation sont calculées à partir de ces informations, puis affichées dans
l'interface. L'utilisateur peut ensuite télécharger un GeoTIFF de la carte d'inondation. Ce GeoTIFF peut être chargé dans un logiciel SIG
pour être consulté autrement.

![Une carte d'inondation dans le Hydroviewer](../../../static/images/hydroviewer-flood-map.png)

### 2. Via le Magasin de Données

Les cartes d'inondation sont disponibles via le [magasin de données](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}. Du code est fourni pour créer et
télécharger les cartes d'inondation. Pour en savoir plus sur l'utilisation du magasin de données, consultez [Le Magasin de Données](datastore.md).

![L'onglet Access des cartes d'inondation par période de retour dans le magasin de données](../../../static/images/flood-maps-datastore.jpg)

### 3. Sur AWS

Les cartes d'inondation par période de retour sont disponibles dans le [bucket AWS](https://v3.s3.riverforecastsystem.com/#flood-maps/){:target="_blank"}. Elles sont indexées par
leur longitude et leur latitude : chaque dossier, comme `flood-maps/lon=-109/lat=39/`, couvre une tuile de 1 degré sur 1 degré. Dans chaque
tuile, le dossier `return_period_maps` contient un GeoTIFF pour chaque période de retour (`rp2.tif`, `rp5.tif`, `rp10.tif`, `rp25.tif`,
`rp50.tif` et `rp100.tif`). Chaque GeoTIFF est la carte d'inondation pour un débit égal au débit de cette période de retour.

![Cartes d'inondation par période de retour dans le bucket AWS](../../../static/images/flood-maps-aws-bucket.jpg)

## Télécharger les données de prévision du RFS pour ma rivière

Si vous n'avez besoin de télécharger des données que pour quelques rivières, ou si vous ne souhaitez pas écrire de code, utilisez l'application web ! Nos applications vous permettent de parcourir
graphiquement une carte des rivières, de visualiser et de télécharger des données de prévision ou rétrospectives, de comparer les prévisions avec les dernières images satellites et
de trouver des liens vers davantage d'informations. Rendez-vous sur [apps.geoglows.org/rfs](https://apps.geoglows.org/rfs){:target="_blank"} pour commencer.

## Obtenir la liste des ID de mon bassin versant

Chaque rivière du modèle RFS possède un attribut appelé « TerminalLink ». Le TerminalLink est le numéro d'ID de la rivière située à l'exutoire du
bassin versant dans lequel se trouve une rivière d'intérêt donnée. Toutes les rivières du bassin versant ont le même exutoire. Vous pouvez filtrer la table des rivières pour ne sélectionner que les
rivières qui se déversent toutes dans la même rivière. Vous pouvez utiliser les jeux de données SIG et effectuer cette opération dans ArcGIS ou QGIS. Vous trouverez les liens permettant de récupérer les fichiers SIG
des cours d'eau sur la page Données Disponibles et dans le tutoriel Trouver les Numéros de Rivière. Vous pouvez également effectuer cette opération en code, à l'aide des tables de
métadonnées du RFS, en utilisant la table de métadonnées du modèle. Vous devrez télécharger cette table (environ 250 Mo) pour résoudre ce problème par code.

<script src="https://gist.github.com/rileyhales/e94f0c51090f26bc396e2289d41edefd.js"></script>

## Récupérer les prévisions pour de nombreuses rivières

Le package Python geoglows vous permet de demander des données pour de nombreuses rivières simultanément. Vous n'avez pas besoin d'utiliser des boucles for dans votre code pour effectuer
des requêtes successives pour une seule rivière à la fois. Préparez une liste de tous les numéros d'ID des rivières pour lesquelles vous souhaitez obtenir des données. Par exemple, vous pourriez obtenir la
liste de toutes les rivières d'un bassin versant (voir le tutoriel sur cette page). Lorsque vous utilisez le package Python geoglows, vous pouvez passer cette liste complète de rivières aux
fonctions de récupération des données.

<script src="https://gist.github.com/rileyhales/963be8a9cbbc179d99ed82fd5c61bf46.js"></script>

## Sauvegarder le jeu de données des archives de prévision

De nouvelles prévisions sont générées chaque jour. Les débits moyens de l'ensemble prévus pour les 24 heures séparant deux prévisions sont archivés chaque jour au
début d'une nouvelle simulation de prévision. Ce jeu de données est appelé « forecast record » (archive des prévisions). Il est mis à jour en continu chaque jour. Ce jeu de données n'est pas
archivé dans un bucket AWS. Il est uniquement disponible via le service REST, pour faciliter la création de graphiques à la volée. Cependant, la prévision de débit d'ensemble
complète est sauvegardée chaque jour.

Veuillez ne pas écrire de code qui parcourt une liste de rivières pour télécharger chaque jour les archives de prévision. Cela surcharge le service REST et
n'est ni aussi rapide ni aussi efficace lorsque le nombre de rivières est important. Si vous souhaitez en télécharger une copie, vous pouvez les obtenir depuis AWS, où la prévision
d'ensemble complète est stockée chaque jour, et les calculer à l'aide des outils disponibles dans le package Python geoglows.

<script src="https://gist.github.com/rileyhales/11ac6df64593dabb641ad9f044b23e37.js"></script>

## Sauvegarder une copie locale des données de prévision ou rétrospectives

De nombreux utilisateurs souhaitent conserver des copies des nouvelles prévisions sur leurs propres appareils. En particulier, certains utilisateurs doivent télécharger les données afin de les transférer vers
un environnement de calcul sécurisé ou un centre de calcul haute performance. Vous pouvez utiliser le package Python geoglows pour récupérer des données de prévision ou rétrospectives
et en sauvegarder une copie.

<script src="https://gist.github.com/rileyhales/ec78fa1c1d6453c407faee8d9c72acea.js"></script>

Par défaut, les données sont téléchargées sous forme de DataFrame (données tabulaires). Vous disposez de nombreuses options pour sauvegarder les DataFrames sur disque, comme Parquet, CSV ou Excel. Si
vous stockez de grandes tables de données, comme les débits rétrospectifs ou les prévisions d'ensemble pour de nombreuses rivières, nous recommandons le format Parquet. Il est
plus rapide à lire et à écrire, et plus compressé que de nombreux autres formats.

Les utilisateurs plus avancés peuvent également récupérer les données sous forme de Dataset Xarray, adapté aux données multidimensionnelles et aux formats de fichiers tels que netCDF ou Zarr.
Vous pouvez également sauvegarder les datasets Xarray sur disque dans plusieurs formats. Le format approprié dépend de l'utilisation que vous prévoyez. Pour spécifier le format des données à
télécharger, utilisez format='df' pour récupérer des tables de données (DataFrames) ou format='xarray' pour les récupérer sous forme de jeu de données
multidimensionnel. La plupart des utilisateurs devraient utiliser le format par défaut, DataFrame.

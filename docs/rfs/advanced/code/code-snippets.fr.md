## Télécharger les données de prévision RFS pour ma rivière

Si vous n'avez besoin de télécharger des données que pour quelques rivières, ou si vous ne souhaitez pas écrire du code, utilisez l'application web ! Notre application vous permet de parcourir graphiquement une carte des rivières, de visualiser et télécharger des données de prévision ou rétrospectives, de comparer les prévisions avec les dernières images satellites et de trouver des liens vers plus d'informations. Visitez [hydroviewer.geoglows.org](https://hydroviewer.geoglows.org){:target="_blank"} pour commencer.

## Obtenir une liste d'ID dans mon bassin versant

Chaque rivière dans le modèle RFS possède un attribut appelé "TerminalLink". Le TerminalLink est le numéro d'ID de la rivière à l'exutoire du bassin versant dans lequel se trouve la rivière d'intérêt. Chaque rivière dans le bassin versant partage le même exutoire. Vous pouvez filtrer le tableau des rivières pour ne sélectionner que celles qui se jettent toutes dans la même rivière. Vous pouvez utiliser les ensembles de données SIG et effectuer cette opération dans ArcGIS ou QGIS. Vous pouvez trouver les liens pour récupérer les fichiers SIG pour les rivières en utilisant la page Available Data et le tutoriel sur la recherche de numéros de rivière. Alternativement, vous pouvez le faire en code en utilisant les tables de métadonnées de RFS. Vous devrez télécharger cette table (environ 250 Mo) pour résoudre ce problème par code.

<script src="https://gist.github.com/rileyhales/e94f0c51090f26bc396e2289d41edefd.js"></script>

## Récupérer les prévisions pour plusieurs rivières

Le package Python geoglows vous permet de demander des données pour plusieurs rivières simultanément. Vous n'avez pas besoin d'utiliser des boucles dans votre code pour faire des requêtes séquentielles pour une seule rivière. Préparez une liste de tous les numéros d'ID de rivière pour lesquels vous souhaitez obtenir des données. Par exemple, vous pourriez obtenir une liste de toutes les rivières d'un bassin versant (voir le tutoriel sur cette page). Lorsque vous utilisez le package Python geoglows, vous pouvez passer cette liste complète de rivières aux fonctions pour récupérer les données.

<script src="https://gist.github.com/rileyhales/963be8a9cbbc179d99ed82fd5c61bf46.js"></script>

## Sauvegarder le jeu de données des prévisions

De nouvelles prévisions sont générées quotidiennement. Les débits moyens de l'ensemble prédits pour les 24 heures suivant la nouvelle prévision sont archivés chaque jour au début d'une nouvelle simulation de prévision. Cet ensemble de données est appelé le “forecast record”. Il est continuellement mis à jour chaque jour. Cet ensemble de données n’est pas archivé sur un bucket AWS. Il est uniquement disponible via le service REST pour plus de commodité pour tracer les données à la volée. Cependant, la prédiction complète des débits de l’ensemble est sauvegardée chaque jour.

Veuillez ne pas écrire de code qui parcourt une liste de rivières pour télécharger chaque jour le “forecast record”. Cela surcharge le service REST et n’est pas aussi rapide ou efficace si le nombre de rivières est important. Si vous souhaitez télécharger une copie, vous pouvez les récupérer depuis AWS où la prévision complète de l'ensemble est stockée chaque jour et les calculer à l'aide des outils disponibles dans le package Python geoglows.

<script src="https://gist.github.com/rileyhales/11ac6df64593dabb641ad9f044b23e37.js"></script>

## Sauvegarder une copie locale des données de prévision ou rétrospectives

De nombreux utilisateurs souhaitent conserver des copies des nouvelles prévisions sur leurs propres appareils. En particulier, certains utilisateurs doivent télécharger des données afin de les déplacer vers un environnement de calcul sécurisé ou un centre de calcul haute performance. Vous pouvez utiliser le package Python geoglows pour récupérer des données de prévision ou rétrospectives et en sauvegarder une copie.

<script src="https://gist.github.com/rileyhales/ec78fa1c1d6453c407faee8d9c72acea.js"></script>

Par défaut, vous téléchargez les données sous forme de DataFrame (données tabulaires). Vous avez de nombreuses options pour sauvegarder les DataFrames sur disque, comme Parquet, CSV ou Excel. Si vous stockez de grandes tables de données, comme les prévisions ou les flux d’ensemble rétrospectifs pour plusieurs rivières, nous recommandons le format Parquet. Il sera plus rapide à lire et écrire et plus compressé que de nombreux autres formats.

Pour les utilisateurs avancés, vous pouvez également récupérer les données sous forme de Dataset Xarray, adapté aux données multidimensionnelles et aux formats de fichiers tels que netCDF ou Zarr. Vous pouvez également sauvegarder les datasets Xarray sur disque dans plusieurs formats. Le format approprié dépend de votre cas d'utilisation prévu. Pour spécifier le format des données à télécharger, utilisez format='df' pour récupérer des tables de données (DataFrames) ou format='xarray' pour récupérer un dataset multidimensionnel. La plupart des utilisateurs devraient utiliser le format par défaut, DataFrame.

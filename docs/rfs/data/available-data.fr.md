# Données Disponibles

Le RFS produit des valeurs de débit pour environ 4,9 millions de cours d'eau. Chaque segment de cours d'eau possède ses propres valeurs, qui peuvent être téléchargées et utilisées. Les données sont accessibles via le [magasin de données](accessing-data/datastore.md) ou via plusieurs [applications web](../web-apps/overview.md). Il existe également des options avancées pour consulter les données à l'aide de code ; consultez notre [section avancée](accessing-data/advanced-methods.md).

Il existe 3 grands ensembles de données :

1. Les données rétrospectives
2. Les données de prévision à 15 jours
3. Les cartes d'inondation

Chacun d'eux est expliqué plus en détail dans les sections suivantes. Vous trouverez également plus d'informations dans le [magasin de données](accessing-data/datastore.md).

## Données Rétrospectives

### Aperçu

La simulation rétrospective du RFS contient plus de 85 ans de données à résolution horaire à partir du 1er janvier 1940. Le modèle est déterministe, ce qui signifie qu'il n'y a qu'une seule valeur par pas de temps au lieu d'un ensemble de valeurs. La simulation rétrospective et de nombreux produits dérivés sont mis à jour chaque semaine.

![image](../../static/images/retro_data.png)

La simulation rétrospective fournit des débits moyens horaires, qui sont ensuite agrégés en moyennes journalières, mensuelles et annuelles. Les débits sont rapportés comme la moyenne sur l'intervalle suivant (heure, jour, mois ou année). La valeur indiquée représente le débit moyen à partir de ce moment jusqu'au pas de temps suivant. Toutes les valeurs sont en mètres cubes par seconde.

---

### Produits Dérivés

#### Périodes de Retour

Une période de retour est une estimation de la fréquence à laquelle un débit extrême élevé (crue) ou un épisode prolongé de faible débit (sécheresse) se produit. Les périodes de retour ont été pré-calculées en utilisant les distributions de Gumbel et Log Pearson Type 3, sur les débits moyens horaires maximaux de chaque année complète.
Les périodes de retour pré-calculées sont utilisées pour définir les niveaux d'alerte pour chaque segment de rivière dans le modèle. Les valeurs pré-calculées concernent les intervalles de retour de 2, 5, 10, 25, 50 et 100 ans. Vous pouvez calculer une période de retour avec votre méthode préférée en accédant au même jeu de données de maxima annuels.

#### Courbes de Durée de Débit

Les **Courbes de Durée de Débit (FDC)** représentent les régimes d'écoulement d'une rivière. Elles relient chaque débit à une probabilité de dépassement. La probabilité de dépassement est la probabilité qu'un débit échantillonné au hasard soit supérieur ou égal au débit correspondant à cette probabilité. Les grandes crues ont une faible probabilité de dépassement, tandis que les faibles débits ont une probabilité de dépassement élevée. La FDC est un outil utile pour comprendre la variabilité des débits et la probabilité de différents débits. Les FDC sont pré-calculées pour chaque mois (soit 12 courbes au total, une par mois) et pour toute la période d'enregistrement de la rivière. Elles permettent de comprendre le débit tout au long de l'année et ses variations saisonnières, ce qui est utile pour une gestion efficace des ressources en eau, la prévision des crues et la compréhension des régimes hydrologiques.

## Données de Prévision à 15 Jours

### Aperçu

Le RFS produit des prévisions de débit d'ensemble en utilisant les données IFS (Integrated Forecast System) de l'ECMWF. Les débits sont exprimés en mètres cubes par seconde. La prévision a un **pas de temps de 3 heures**, où chaque valeur de débit
représente le débit moyen survenu dans la rivière au cours des 3 heures précédentes. Ci-dessous, un exemple de graphique montrant tous les membres de l'ensemble.

![image](../../static/images/forecast_ensemble.png)

Chaque prévision comprend un **ensemble de 50+1 membres**, ce qui signifie qu'il y a **1 prédiction de référence (contrôle)** et **50 perturbations** (légères variations)
de l'état de référence.

La prévision de chaque jour est initialisée en utilisant comme condition initiale la valeur moyenne sur 24 heures des membres de l'ensemble du jour précédent.

### Interprétation d'une Prévision d'Ensemble

Chaque membre de l'ensemble a une probabilité égale de se produire. Par conséquent, il est préférable de comprendre les prévisions en examinant les résumés de l'ensemble
plutôt que les membres individuels.

Les graphiques de prévision sont conçus pour aider les utilisateurs à interpréter la plage des résultats possibles et les incertitudes. Le graphique de prévision le plus utilisé
comprend la médiane, le 20ᵉ percentile et le 80ᵉ percentile. Ceux-ci représentent 60 % de la distribution de probabilité parmi les membres de l'ensemble et donnent
un aperçu de la variabilité potentielle du débit futur. Cette approche permet aux utilisateurs de visualiser la gamme de scénarios probables pour leurs cours d'eau.

Dans l'exemple de graphique de prévision suivant, il y a 3 zones sur lesquelles se concentrer :

- **Ligne noire :** La médiane des 51 membres de l'ensemble. C'est la « meilleure estimation » du débit de la rivière.
- **Lignes bleues :** Les valeurs des 20ᵉ et 80ᵉ percentiles.
- **Zone bleue ombrée :** Représente l'incertitude de la prévision. Il s'agit des 60 % centraux de l'ensemble. Plus la zone bleue est étroite, plus le modèle est confiant.
  Le débit réel a plus de chances de se situer dans la zone bleue ombrée qu'en dehors.

![image](../../static/images/forecast.png)

<!-- Hidden for now: 45-day forecast section
## Données de Prévision à 45 Jours
Cette section est un espace réservé pour le contenu qui figurera ici si ces données sont produites.
-->

## Cartes d'Inondation

Les cartes d'inondation du RFS montrent la zone qui serait inondée le long d'une rivière, ainsi que la profondeur de l'eau, pour un débit
donné. Elles montrent uniquement les inondations dues au débordement des rivières, et non celles causées directement par la pluie. Les
cartes d'inondation sont actuellement en version préliminaire. Il existe trois produits de cartes d'inondation :

- **Cartes d'inondation prévues** : L'étendue et la profondeur de l'inondation prévues par chaque prévision quotidienne à 15 jours.
- **Cartes d'inondation par période de retour** : L'étendue et la profondeur de l'inondation pour les débits de chaque période de retour,
  comme le débit de 2 ans ou de 100 ans. Elles ne dépendent pas d'une prévision.
- **Bibliothèques d'inondation (FLDPLN)** : Les tables utilisées pour transformer n'importe quel débit en carte d'inondation. Elles
  peuvent servir à créer vos propres cartes d'inondation pour le débit de votre choix.

![Exemple de carte d'inondation près de Grand Junction, Colorado. Le bleu plus foncé indique une eau plus profonde.](../../static/images/flood-map-example.png)

Pour voir les cartes d'inondation, utilisez les outils de cartographie des inondations du [Hydroviewer](../web-apps/hydroviewer.md). Pour les télécharger,
consultez [Accès aux Cartes d'Inondation](accessing-data/flood-maps.md). Pour savoir comment elles sont produites, consultez
[Cartographie des Inondations](../model-formulation/flood-mapping.md) dans la section Formulation du Modèle.

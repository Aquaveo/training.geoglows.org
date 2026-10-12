# Données Disponibles

Le RFS produit des valeurs de débit pour environ 4,9 millions de cours d'eau. Chaque segment de cours d'eau possède ses propres valeurs, qui peuvent être téléchargées et utilisées. Les données sont accessibles via le [magasin de données](using-datastore.md) ou via plusieurs [applications web](../web-apps/overview.md). Il existe également des options avancées pour consulter les données à l'aide de code ; consultez notre [section avancée](../advanced/data-access/code-and-apis.md).

Il existe 3 grands ensembles de données :

1. Les données rétrospectives
2. Les données de prévision à 15 jours
3. Les données de prévision à 45 jours

Chacun d'eux est expliqué plus en détail dans les sections suivantes. Vous trouverez également plus d'informations dans le [magasin de données](using-datastore.md).

## Données Rétrospectives


### Aperçu

La simulation rétrospective du RFS contient plus de 85 ans de données à résolution horaire à partir du 1er janvier 1940. Le modèle est déterministe, ce qui signifie qu'il n'y a qu'une seule valeur par pas de temps au lieu d'un ensemble de valeurs. La simulation rétrospective et de nombreux produits dérivés sont mis à jour chaque semaine.

![image](../../static/images/retro_data.png)

La simulation rétrospective fournit des débits moyens horaires, qui sont ensuite agrégés en moyennes journalières, mensuelles et annuelles. Les débits sont rapportés comme la moyenne sur l'intervalle suivant (heure, jour, mois ou année). La valeur indiquée représente le débit moyen à partir de ce moment jusqu'au pas de temps suivant. Toutes les valeurs sont en mètres cubes par seconde.


| Propriété du modèle       | Simulation Rétrospective      |
|---------------------------|------------------------------|
| Date la plus ancienne     | 01 janvier 1940              |
| Type de simulation        | Déterministe                 |
| Membres de l'ensemble     | 1                            |
| Délai                     | 5-12 jours par rapport à aujourd'hui |
| Pas de temps              | Moyenne horaire              |
| Fréquence de mise à jour  | Hebdomadaire, le dimanche à 00:00 UTC |
| Téléchargement en masse disponible | Oui                 |
| Requête & sous-ensemble disponible | Oui                 |

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

| Propriété du modèle      | Simulation de Prévision |
|--------------------------|-------------------------|
| Type de simulation       | Ensemble                |
| Membres de l'ensemble    | 50+1                    |
| Horizon de prévision     | 15 jours                |
| Pas de temps             | Moyenne sur 3 heures    |
| Fréquence de mise à jour | Quotidienne à 00:00 UTC |
| Téléchargement en masse disponible | Oui           |
| Requête & sous-ensemble disponible | Oui           |

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

## Données de Prévision à 45 Jours
Cette section est un espace réservé pour le contenu qui figurera ici si ces données sont produites.

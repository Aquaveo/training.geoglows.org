# Données Disponibles

## Données Rétrospectives

### Termes et Vocabulaire

- **ERA5** : Cinquième génération de réanalyse atmosphérique globale du climat produite par l’ECMWF. Il s’agit du jeu de données de réanalyse le plus récent du Centre Européen pour les Prévisions Météorologiques à Moyen Terme (ECMWF). Disponible de 1940 à aujourd’hui et mis à jour quotidiennement avec un décalage de 5 jours.  
- **Réanalyse** : Produit modélisé intégrant des données in situ et/ou issues de la télédétection pour fournir la meilleure estimation possible des conditions hydrométéorologiques historiques. Les données de réanalyse sont utilisées comme entrées pour le modèle RFS.  

---

### Aperçu

La simulation rétrospective du RFS est une simulation déterministe sur plus de 85 ans avec une résolution horaire à partir du 1er janvier 1940. La simulation rétrospective et de nombreux produits dérivés sont mis à jour chaque semaine. Elle est basée sur le jeu de données ERA5.  

De nouvelles données ERA5 sont produites chaque jour avec un décalage de 5 jours par rapport au temps réel, donc le décalage minimal possible est de 5 jours. Une fois par semaine, toutes les nouvelles données ERA5 depuis la dernière simulation sont utilisées pour étendre la simulation rétrospective, ramenant le décalage à 5 jours.  

![image](../../static/images/retro_data.png)

Le jeu de données est déterministe et basé sur la modélisation de surface terrestre par réanalyse, ce qui signifie qu’il n’y a qu’une seule valeur par pas de temps, contrairement aux prévisions.  
La simulation rétrospective fournit des débits moyens horaires, qui sont ensuite agrégés en moyennes journalières, mensuelles et annuelles. Les débits sont rapportés comme la moyenne sur l’intervalle correspondant (heure, jour, mois ou année). Les dates sont indiquées au début de l’intervalle en UTC +00:00 (dates "alignées à gauche"). La valeur indiquée représente le débit moyen à partir de ce moment jusqu’au pas de temps suivant. Toutes les valeurs sont en mètres cubes par seconde.  

Les données mensuelles moyennes sont disponibles en deux formats différents. L’un est optimisé pour lire la série temporelle complète d’une seule rivière ou d’un groupe de rivières, ce qui est le cas d’utilisation le plus fréquent. L’autre est optimisé pour lire un grand nombre de rivières à un pas de temps donné.  

| Propriété du modèle       | Simulation Rétrospective      |
|---------------------------|------------------------------|
| Date la plus ancienne     | 01 janvier 1940              |
| Type de simulation        | Déterministe                 |
| Membres de l’ensemble     | 1                            |
| Délai                     | 5-12 jours par rapport à aujourd’hui |
| Pas de temps              | Moyenne horaire              |
| Fréquence de mise à jour  | Hebdomadaire, dimanche 00:00 UTC |
| Téléchargement en masse disponible | Oui                 |
| Requête & sous-ensemble disponible | Oui                 |

---

### Produits Dérivés

#### Périodes de Retour

Une période de retour est une estimation de la fréquence à laquelle un débit extrême élevé (crue) ou un épisode prolongé de faible débit (sécheresse) se produit. Les périodes de retour ont été pré-calculées en utilisant les distributions de Gumbel et Log Pearson Type 3, sur les débits moyens horaires maximum de chaque année complète.  

Les périodes de retour pré-calculées sont utilisées pour définir les niveaux d’alerte pour chaque segment de rivière dans le modèle. Les valeurs pré-calculées concernent les intervalles de retour de 2, 5, 10, 25, 50 et 100 ans. Vous pouvez calculer une période de retour avec votre méthode préférée en accédant aux mêmes données de maxima annuels.  

#### Courbes de Durée de Débit

Les **Courbes de Durée de Débit (FDCs)** représentent les schémas de débit dans une rivière. Elles relient chaque débit à une probabilité d’excédence. La probabilité d’excédence est la chance qu’un débit échantillonné au hasard soit supérieur ou égal au débit pour cette probabilité.  

Les grandes crues ont une faible probabilité d’excédence, tandis que les faibles débits ont une probabilité élevée. Les FDC sont un outil utile pour comprendre la variabilité des débits et la probabilité de différents débits.  

Les FDCs sont pré-calculées pour chaque mois (12 courbes au total représentant chaque mois) et pour toute la période historique de la rivière. Elles permettent de comprendre le débit tout au long de l’année et les variations saisonnières, ce qui est utile pour la gestion des ressources en eau, la prévision des crues et l’analyse des modèles hydrologiques.  

## Données de Prévision à 15 Jours

### Termes et Vocabulaire

- **IFS** : Integrated Forecast System. Nom du modèle couplé de météorologie et de surface terrestre utilisé pour générer les forçages pour les résultats du RFS.

---

### Aperçu

Le RFS produit des prévisions de débit fluvial en ensemble en utilisant les données IFS du ECMWF. Les prévisions quotidiennes sont calculées au centre de supercalcul de l’ECMWF à
Bologne, en Italie, et sont disponibles avant 12h UTC. Les débits sont exprimés en mètres cubes par seconde. La prévision a un **pas de temps de 3 heures**, où chaque valeur de débit
représente le débit moyen survenu dans la rivière au cours des 3 heures précédentes. Ci-dessous un exemple de graphique montrant tous les membres de l’ensemble.

![image](../../static/images/forecast_ensemble.png)

Chaque prévision inclut un **ensemble de 50+1 membres**, ce qui signifie qu’il y a **1 prédiction de référence (contrôle)** et **50 perturbations** (légères variations)
de l’état de référence.

La prévision de chaque jour est initialisée en utilisant la valeur moyenne sur 24 heures des membres de l’ensemble du jour précédent comme condition initiale.  
Les données IFS ont une résolution spatiale d’environ 9 kilomètres horizontalement à l’équateur. La grille des valeurs de débit IFS est mappée aux limites des bassins RFS
à l’aide de méthodes SIG de statistiques zonales.

| Propriété du modèle      | Simulation Rétrospective |
|--------------------------|-------------------------|
| Date la plus ancienne    | 01 juillet 1940         |
| Type de simulation       | Ensemble                |
| Membres de l’ensemble    | 50+1                    |
| Horizon de prévision     | 15 jours                |
| Pas de temps             | Moyenne 3 heures        |
| Fréquence de mise à jour | Quotidienne à 00:00 UTC|
| Téléchargement en masse disponible | Oui          |
| Requête & sous-ensemble disponible | Oui          |

### Interprétation d’une prévision en ensemble

Chaque membre de l’ensemble a une probabilité égale de se produire. Par conséquent, il est préférable de comprendre les prévisions en examinant les résumés de l’ensemble
plutôt que les membres individuels.

Les graphiques de prévision sont conçus pour aider les utilisateurs à interpréter la plage des résultats possibles et les incertitudes. Le graphique de prévision le plus utilisé
comprend la médiane, le 20ᵉ percentile et le 80ᵉ percentile. Ceux-ci représentent 60 % de la distribution de probabilité parmi les membres de l’ensemble et donnent
un aperçu de la variabilité potentielle du débit futur. Cette approche permet aux utilisateurs de visualiser la gamme de scénarios probables pour leurs rivières.

Dans l’exemple de graphique de prévision suivant, il y a 3 zones sur lesquelles se concentrer :

- **Ligne noire :** La médiane des 51 membres de l’ensemble. C’est la "meilleure estimation" du débit fluvial.  
- **Lignes bleues :** Les valeurs des 20ᵉ et 80ᵉ percentiles  
- **Zone bleue ombrée :** Représente l’incertitude de la prévision. Il s’agit des 60 % centraux de l’ensemble. Plus la zone bleue est étroite, plus le modèle est confiant.  
  Le débit réel est plus susceptible de se situer dans cette zone bleue ombrée.

![image](../../static/images/forecast.png)

## Données de Prévision à 45 Jours

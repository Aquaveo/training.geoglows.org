## Composantes de Stockage

Quatre composantes de stockage sont disponibles pour la visualisation et le téléchargement. Toutes sont des anomalies — un écart par rapport à une
moyenne de long terme — et non des quantités absolues.

| Nom | Abréviation | Source |
|-----|-------------|--------|
| Anomalie du Stockage Total en Eau | TWSa | GRACE |
| Anomalie de l'Équivalent en Eau de la Neige | SWEa | GLDAS |
| Anomalie de l'Humidité du Sol | SMa | GLDAS |
| Anomalie du Stockage des Eaux Souterraines | GWSa | Calculée |

Elles sont présentées ici dans l'ordre où elles apparaissent dans le bilan de masse : le total GRACE, les composantes de surface qui en sont
soustraites, puis le résultat souterrain. L'Anomalie du Stockage des Eaux Souterraines est calculée et non observée — voir
[Dérivation des Eaux Souterraines](../understanding/computational-algorithm.md#derivation-des-eaux-souterraines).

## Résolution de la Grille

Les composantes sont calculées sur des cellules de bilan hydrique, d'une résolution de 1.0 degré par défaut. Une option de demi-degré est disponible
dans les paramètres de l'application. Le passage d'une option à l'autre recharge la carte et l'analyse en cours à partir de l'autre jeu de données, et
les cellules plus fines sont plus longues à préparer.

Les données GRACE sont fournies à l'origine sur des cellules de 3 degrés appelées mascons, avant d'être désagrégées vers les cellules d'anomalie de
1.0 et 0.5 degré. Les emprises des mascons comme les limites des cellules d'anomalie peuvent être affichées sur la carte depuis les paramètres de
l'application.

Pour savoir comment les données brutes sont mises en grille et désagrégées, voir
[Dérivation des Eaux Souterraines](../understanding/computational-algorithm.md#derivation-des-eaux-souterraines).

## Unités et Période de Référence

Les valeurs sont des anomalies exprimées en hauteur d'eau équivalente. Chaque composante GLDAS est convertie en anomalie en soustrayant la moyenne
centrée sur les valeurs de 2004 à 2009.

## Couverture Temporelle

GRACE produit des solutions mensuelles du champ de gravité depuis avril 2002. Le découpage régional produit une série temporelle de 2002 à
aujourd'hui pour chaque composante, à pas de temps mensuel.

## Lacunes dans les Données

En examinant attentivement le fichier de la série temporelle du stockage des eaux souterraines, on constate que plusieurs mois sont manquants, ou
qu'il existe des lacunes dans les données. Le mois de juin 2003, par exemple, est absent. Cela s'explique par le fait que les satellites GRACE n'ont
pas produit de données exploitables pendant certaines périodes.

La plus grande lacune est une période de 12 mois en 2017-2018, entre la fin de la mission GRACE d'origine en 2017 et le moment où les satellites
GRACE-FO suivants ont été lancés et sont devenus opérationnels en 2018.

Pour les années comportant de larges lacunes, il peut être difficile de dégager les tendances saisonnières et d'appliquer la méthode de Fluctuation de
la Nappe Phréatique. Une façon de résoudre ce problème consiste à utiliser un algorithme statistique pour détecter les motifs saisonniers dans les
données et imputer des données synthétiques dans les lacunes ; cette méthode et l'outil qui permet de l'appliquer sont décrits dans
[Combler les Lacunes dans les Données](../applications/water-table-fluctuation.md#lacunes-dans-les-donnees-grace).

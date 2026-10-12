# Le Magasin de Données

Le [Magasin de Données du RFS](https://apps.geoglows.org/previews/rfs-data-store) (RFS Data Store) est l'endroit où trouver et télécharger les données du RFS. Il répertorie tous les jeux de données publiés par le modèle, décrit le contenu de chacun d'eux et vous permet de télécharger uniquement les rivières et les dates dont vous avez besoin.

## 1. Choisir une version du modèle

La page d'accueil répertorie chaque version du RFS. Sélectionnez **RFS v3**, la version actuelle, pour afficher ses jeux de données. RFS v2 et v1 sont des archives que vous pouvez parcourir, mais leurs données ne peuvent pas être téléchargées via cette application.

![La page d'accueil du Magasin de Données du RFS, répertoriant chaque version du modèle](../../static/images/datastore-versions.jpg)

## 2. Trouver un jeu de données

La liste des jeux de données affiche tout ce qui est disponible pour cette version, comme l'hydrographie, le débit rétrospectif, les prévisions et les cartes d'inondation.

- Utilisez la **barre de recherche** pour rechercher un jeu de données par son nom.
- Utilisez les **filtres** à gauche pour affiner la liste par catégorie, format de fichier ou résolution temporelle (par exemple, données horaires ou journalières).
- Utilisez **Sort by** (Trier par) pour classer la liste par titre ou par date de dernière mise à jour.

Sélectionnez un jeu de données pour ouvrir sa page.

## 3. En savoir plus sur le jeu de données

Chaque page de jeu de données comporte trois onglets :

- **Overview** (Aperçu) : une description du jeu de données et de ses métadonnées (voir ci-dessous).
- **Download** (Téléchargement) : des outils pour télécharger les données (voir ci-dessous).
- **Documentation** : des informations techniques plus détaillées.

![Une page de jeu de données avec ses onglets Overview, Download et Documentation](../../static/images/datastore-dataset-page.jpg)

### Métadonnées et informations sur le jeu de données

L'onglet **Overview** est un bon point de départ avant de télécharger quoi que ce soit. Il décrit le contenu du jeu de données et son organisation, notamment :

- **Description** : la nature des données et la façon dont elles ont été produites.
- **Couverture et résolution** : la période couverte, le pas de temps (par exemple, horaire ou journalier), la couverture spatiale et la résolution spatiale des données.
- **Variables** : le nom, les unités et les dimensions de chaque variable contenue dans les fichiers, comme `Q`, le débit en mètres cubes par seconde.
- **Détails du jeu de données** : le format de fichier, le système de coordonnées de référence, la version du modèle, le fournisseur, la fréquence de mise à jour, ainsi que les dates de création et de dernière mise à jour du jeu de données.
- **Licence et citation** : les conditions de partage des données et la manière de les citer dans vos travaux.
- **Stockage** : l'emplacement des données dans le bucket public du RFS.
- **Journal des modifications** : un historique des mises à jour du jeu de données.
- **Jeux de données associés** : des liens vers d'autres jeux de données souvent utilisés ensemble, comme les débits horaires, journaliers et mensuels.

![Métadonnées et variables du jeu de données dans l'onglet Overview](../../static/images/datastore-metadata.jpg)

## 4. Télécharger les données

Dans l'onglet **Download**, suivez les étapes numérotées :

1. **Zone d'intérêt** : choisissez ce que vous souhaitez télécharger, puis sélectionnez-le sur la carte. Vous pouvez choisir un bassin versant, les rivières situées entre deux points, des rivières individuelles, une ou plusieurs régions, ou le globe entier.
2. **Période** : choisissez des dates de début et de fin, ou utilisez un raccourci comme les 30 derniers jours ou l'ensemble de l'historique.
3. **Format** : choisissez le format de fichier à télécharger.
4. **Conditions d'utilisation** : lisez l'accord d'utilisation des données et cochez les deux cases pour l'accepter, ainsi que la licence du jeu de données.
5. **Demande** : connectez-vous, vérifiez le récapitulatif de votre demande (y compris sa taille estimée) et sélectionnez **Download**.

![Choix d'une zone d'intérêt dans l'onglet Download](../../static/images/datastore-area-of-interest.jpg)

### Télécharger les données vous-même

Si vous préférez télécharger les données avec vos propres outils, la section **Download it yourself** (Téléchargez-les vous-même), en bas de l'onglet Download, fournit des commandes prêtes à l'emploi pour s5cmd, l'AWS CLI, Python et JavaScript. Les données sont stockées dans un bucket public ; ces commandes ne nécessitent donc pas de compte.

![Commandes de téléchargement prêtes à l'emploi dans la section Download it yourself](../../static/images/datastore-download-yourself.jpg)

La page **Packages** du Magasin de Données renvoie également vers les deux bibliothèques de code maintenues pour lire les données du RFS : **geoglows** pour Python et **riverforecastsystem** pour JavaScript.

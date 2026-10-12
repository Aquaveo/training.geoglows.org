## Résumé

Le Système de Prévision Fluviale (RFS) fournit 4 principaux types de jeux de données fluviales. Toutes ces données sont disponibles gratuitement.

1. **Hydrographie** : données SIG sur l'emplacement des cours d'eau, des bassins versants et des lacs dans le monde entier.
2. **Simulation Rétrospective** : données horaires de débit des rivières depuis janvier 1940.
3. **Prévisions** : prévisions de débit à 15 jours générées chaque jour à minuit.
4. **Cartes d'Inondation** : étendues et profondeurs d'inondation cartographiées à partir des prévisions et des débits associés aux périodes de retour.

[Le Système de Prévision Fluviale GEOGLOWS V3](https://www.geoglows.org){:target="_blank"} © [Dr. Riley Hales](https://hales.app) 2025 est sous licence
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/){:target="_blank"}

## Tableau des jeux de données

Le moyen le plus simple de trouver et de télécharger les données du RFS V3 est le [Magasin de Données du RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"},
qui décrit chaque jeu de données et vous permet de télécharger uniquement les rivières et les dates dont vous avez besoin. Consultez [Le Magasin de Données](../../what-is-it/using-datastore.md) pour
les instructions.

Tous les jeux de données du RFS V3 sont stockés dans un seul bucket public AWS S3, `river-forecast-system-v3`, dans la région `us-west-2`. Vous **n'avez pas besoin** d'un compte
AWS, d'une carte bancaire, ni d'un identifiant et d'un mot de passe pour en télécharger des données. Vous pouvez parcourir le bucket dans un navigateur web à l'adresse
[https://v3.s3.riverforecastsystem.com](https://v3.s3.riverforecastsystem.com){:target="_blank"}.

Lorsque vous interrogez des données sur AWS, vous devrez peut-être préciser que vous y accédez de manière anonyme si vous n'avez pas de compte AWS ou si vous préférez ne pas fournir d'identifiants.

| Jeu de données                                                                                                                                   | Format(s) de fichier | URI et chemin dans le bucket                                                |
|--------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|-----------------------------------------------------------------------------|
| [Prévision d'ensemble à 15 jours](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/forecast-15day){:target="_blank"}                | Zarr                | `s3://river-forecast-system-v3/forecasts15/`                                |
| [Lignes centrales des cours d'eau](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/streams){:target="_blank"}                      | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Limites des bassins versants](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/catchments){:target="_blank"}                       | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Points de confluence](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/confluences){:target="_blank"}                              | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Lacs](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/lakes){:target="_blank"}                                                    | GeoParquet          | `s3://river-forecast-system-v3/hydrography/`                                |
| [Rétrospective - Débit horaire](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-hourly){:target="_blank"}            | Zarr                | `s3://river-forecast-system-v3/retrospective/hourly.zarr`                   |
| [Rétrospective - Débit journalier](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-daily){:target="_blank"}          | Zarr                | `s3://river-forecast-system-v3/retrospective/daily.zarr`                    |
| [Rétrospective - Débit mensuel](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-monthly){:target="_blank"}           | Zarr                | `s3://river-forecast-system-v3/retrospective/monthly.zarr`                  |
| [Rétrospective - Débit annuel](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-yearly){:target="_blank"}             | Zarr                | `s3://river-forecast-system-v3/retrospective/yearly.zarr`                   |
| [Rétrospective - Maxima annuels](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/annual-maximums-daily){:target="_blank"}          | Zarr                | `s3://river-forecast-system-v3/retrospective/maximums.zarr`                 |
| [Rétrospective - Périodes de retour](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/return-periods){:target="_blank"}             | Zarr                | `s3://river-forecast-system-v3/retrospective/return-periods.zarr`           |
| [Rétrospective - Courbes de durée des débits](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/flow-duration-curves){:target="_blank"} | Zarr             | `s3://river-forecast-system-v3/retrospective/fdc.zarr`                      |
| [Cartes d'inondation prévisionnelles](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/forecast-flood-maps){:target="_blank"}       | GeoParquet, GeoTIFF | `s3://river-forecast-system-v3/forecasts15/year=YYYY/month=MM/day=DD/`      |
| [Cartes d'inondation par période de retour](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/return-period-flood-maps){:target="_blank"} | GeoTIFF        | `s3://river-forecast-system-v3/flood-maps/lat=YYY/lon=XXX/return-periods/`  |
| [Bibliothèques FLDPLN](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/fldpln-libraries){:target="_blank"}                         | Zarr, PMTiles       | `s3://river-forecast-system-v3/flood-maps/lat=YYY/lon=XXX/fldpln.zarr/`     |

## Code et références techniques

- Scripts de calcul des prévisions : [https://github.com/geoglows/geoglows_ecflow](https://github.com/geoglows/geoglows_ecflow){:target="_blank"}
- Scripts de mise à jour hebdomadaire de la simulation rétrospective : [https://github.com/geoglows/retrospective-update](https://github.com/geoglows/retrospective-update){:target="_blank"}

## Téléchargement des données via l'interface en ligne de commande (recommandé)

Le moyen le plus rapide de télécharger les données du RFS est d'utiliser l'AWS Command Line Interface (CLI). Si vous n'êtes pas familier avec la programmation ou les outils en ligne de commande, veuillez
passer à la section suivante sur le téléchargement des données avec un navigateur web.

L'utilisation de la CLI permet de télécharger les données plus rapidement que via le navigateur et est recommandée pour télécharger de grandes quantités de données. Veuillez vous référer aux
instructions d'AWS pour le téléchargement de données depuis S3. Vous devrez peut-être ajouter l'option `--no-sign-request` à vos commandes copy ou sync. L'onglet
**Download** de chaque jeu de données dans le [Magasin de Données du RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"} fournit également des
commandes prêtes à l'emploi pour s5cmd et l'AWS CLI.

## Téléchargement des données avec un navigateur web

La manière la plus simple de parcourir les jeux de données du RFS V3 est d'utiliser le [Magasin de Données du RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}
ou le [navigateur du bucket](https://v3.s3.riverforecastsystem.com){:target="_blank"}. Ce n'est pas la méthode la plus rapide pour télécharger de grandes quantités de données.
Pour de meilleures performances de téléchargement, il est conseillé de suivre les instructions relatives à l'interface en ligne de commande.

Le RFS permet aux utilisateurs de télécharger les données mondiales de débit directement depuis AWS. Cela donne accès à la fois aux données de simulation rétrospective et aux prévisions
de débit à 15 jours. Ces jeux de données sont hébergés dans des buckets S3, optimisés pour l'analyse de séries temporelles et les téléchargements en masse.

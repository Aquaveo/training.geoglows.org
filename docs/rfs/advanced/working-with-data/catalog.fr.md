## Résumé

Il existe 3 principaux types de jeux de données fluviales fournis par le Système de Prévision Fluviale (RFS). Toutes ces données sont disponibles gratuitement.

1. **Hydrographie** : Données SIG pour les emplacements des cours d’eau et des bassins versants dans le monde entier.  
2. **Simulation Rétrospective** : Données horaires de débit des rivières depuis janvier 1940.  
3. **Prévisions** : Prévisions de débit sur 15 jours générées chaque jour à minuit.  

[Le Système de Prévision Fluviale GEOGLOWS V2](https://www.geoglows.org){:target="_blank"} © [Dr. Riley Hales](https://hales.app) 2025 est sous licence
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/){:target="_blank"}.

## Tableau des jeux de données

Tous les jeux de données RFS V2 sont sponsorisés par le Programme AWS Open Data Sponsorship. Cela rend les données publiquement disponibles gratuitement. Vous **n’avez pas besoin** d’un compte AWS, d’une carte bancaire, ni d’un identifiant ou mot de passe pour utiliser ce service AWS. Pour en savoir plus, consultez le [Registry of Open Data](https://registry.opendata.aws/geoglows-v2/) et
le [AWS Data Exchange](https://aws.amazon.com/marketplace/pp/prodview-aboaljwcz64zs).

Lors de l’accès aux données depuis AWS, vous devrez peut-être spécifier que vous y accédez de manière anonyme si vous n’avez pas de compte AWS ou préférez ne pas fournir vos identifiants.

Les données sont stockées dans 2 buckets. Le premier contient les fichiers de configuration du modèle, les données SIG, les simulations rétrospectives et d’autres données essentiellement statiques. Le second contient les prévisions quotidiennes produites par le RFS.

- Prévisions : [http://geoglows-v2-forecasts.s3-website-us-west-2.amazonaws.com/index.html](http://geoglows-v2-forecasts.s3-website-us-west-2.amazonaws.com/index.html){:target="_blank"}  
- SIG + Rétrospective : [http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html){:target="_blank"}

| Jeu de données                         | Format(s) de fichier | URI du Bucket et Chemin                                                                                                                                                           | Région AWS |
|----------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Prévisions quotidiennes                 | Zarr               | [s3://geoglows-v2-forecasts/](http://geoglows-v2-forecasts.s3-website-us-west-2.amazonaws.com/index.html){:target="_blank"}                                                      | us-west-2  |
| Hydrographie - VPUs                     | GeoPackage (sqlite)| [s3://geoglows-v2/hydrography/](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#hydrography/){:target="_blank"}                                                 | us-west-2  |
| Hydrographie - Global                   | GeoPackage (sqlite)| [s3://geoglows-v2/hydrography-global/](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#hydrography-global/){:target="_blank"}                                     | us-west-2  |
| Hydrographie - Tables Supplémentaires   | Parquet            | [s3://geoglows-v2/tables/](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#tables/){:target="_blank"}                                                             | us-west-2  |
| Rétrospective - Moyenne horaire        | Zarr               | [s3://geoglows-v2/retrospective/hourly.zarr](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#retrospective/hourly.zarr/){:target="_blank"}                          | us-west-2  |
| Rétrospective - Moyenne quotidienne    | Zarr               | [s3://geoglows-v2/retrospective/daily.zarr](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#retrospective/daily.zarr/){:target="_blank"}                            | us-west-2  |
| Rétrospective - Moyenne mensuelle      | Zarr               | [s3://geoglows-v2/retrospective/monthly-timeseries.zarr](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#retrospective/monthly-timeseries.zarr/){:target="_blank"} | us-west-2  |
| Rétrospective - Moyenne annuelle       | Zarr               | [s3://geoglows-v2/retrospective/yearly-timeseries.zarr](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#retrospective/yearly-timeseries.zarr/){:target="_blank"}    | us-west-2  |
| Rétrospective - Maximum annuel         | Zarr               | [s3://geoglows-v2/retrospective/yearly-maximums.zarr](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#retrospective/yearly-maximums.zarr/){:target="_blank"}        | us-west-2  |
| Rétrospective - Périodes de retour     | Zarr               | [s3://geoglows-v2/retrospective/return-periods.zarr](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#retrospective/return-periods.zarr/){:target="_blank"}          | us-west-2  |
| Rétrospective - Courbes de durée de débit | Zarr             | [s3://geoglows-v2/retrospective/fdc.zarr](http://geoglows-v2.s3-website-us-west-2.amazonaws.com/index.html#retrospective/fdc.zarr/){:target="_blank"}                                | us-west-2  |

## Références techniques et scripts

- Scripts de calcul des prévisions : [https://github.com/geoglows/geoglows_ecflow](https://github.com/geoglows/geoglows_ecflow){:target="_blank"}  
- Scripts de mise à jour hebdomadaire rétrospective : [https://github.com/geoglows/retrospective-update](https://github.com/geoglows/retrospective-update){:target="_blank"}

## Téléchargement des données via l’interface en ligne de commande (recommandé)

Le moyen le plus rapide de télécharger les données RFS est d’utiliser l’AWS Command Line Interface (CLI). Si vous n’êtes pas familier avec la programmation ou les outils en ligne de commande, passez à la section suivante sur le téléchargement via un navigateur web.

L’utilisation de la CLI permet de télécharger les données plus rapidement que via le navigateur et est recommandée pour de grandes quantités de données. Veuillez vous référer aux instructions AWS pour le téléchargement de données depuis S3. Vous devrez peut-être ajouter l’option `--no-sign-request` dans vos commandes `copy` ou `sync`.

## Téléchargement des données via un navigateur web

La manière la plus simple de parcourir les jeux de données RFS V2 est d’utiliser les sites web qui permettent de naviguer dans les datasets disponibles. Ce n’est pas la méthode la plus rapide.  
Pour un téléchargement plus performant, il est conseillé d’utiliser la CLI.

Le RFS permet aux utilisateurs de télécharger les données mondiales de débit fluvial directement depuis AWS. Cela donne accès à la fois aux données de simulation rétrospective et aux prévisions de débit sur 15 jours. Ces jeux de données sont hébergés dans des buckets S3, optimisés pour l’analyse des séries temporelles et les téléchargements en masse.

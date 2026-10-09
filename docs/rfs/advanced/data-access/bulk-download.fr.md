!!! danger "Le téléchargement en masse n'est généralement pas nécessaire"
    La plupart des utilisateurs n'ont pas besoin de ce tutoriel. Tous les produits de prévision et de simulation rétrospective sont disponibles via des requêtes, des téléchargements en masse
    et le service de données. Cependant, les instructions pour interroger les données sont les plus rapides et les plus pratiques (et les moins coûteuses pour GEOGLOWS) pour la plupart des usages.
    Veuillez suivre le tutoriel sur [l'interrogation des données fluviales](code-and-apis.fr.md) avant de poursuivre avec cette section.

## Références
La plupart des utilisateurs n'ont pas besoin de télécharger le résultat complet de la simulation pour le monde entier. Une requête ou un téléchargement plus large suffit souvent. Si vous
poursuivez, vous devez être familiarisé avec awscli ou un outil équivalent. Voici une règle empirique utile pour estimer l'espace disque nécessaire :

- 1 jour de prévisions représente environ 150 Go
- Le zarr de la simulation rétrospective horaire représente environ 6 To
- Le zarr de la simulation rétrospective journalière représente environ 500 Go
- Le zarr de la simulation rétrospective mensuelle représente environ 20 Go
- Le zarr de la simulation rétrospective annuelle représente environ 2 Go

## awscli

La meilleure façon de télécharger en masse des données depuis des buckets S3 est d'utiliser un outil en ligne de commande conçu à cet effet. Ces outils permettent de télécharger plusieurs jeux de données
simultanément et à des vitesses supérieures à celles possibles via un navigateur web. L'outil de base pour cela est awscli.
Utilisez les [tutoriels AWS S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/download-objects.html){:target="_blank"} pour commencer.

!!! tip "Utilisez `--no-sign-request`"
    Utilisez l'option `--no-sign-request` pour éviter les erreurs, en particulier si vous n'avez pas d'identifiants AWS sur votre ordinateur.

Toutes les données du RFS V3 sont stockées dans un seul bucket. Lors du téléchargement des données, les prévisions se trouvent dans `s3://river-forecast-system-v3/forecasts15/` et la simulation
rétrospective dans `s3://river-forecast-system-v3/retrospective/`. La prévision de chaque jour est stockée dans son propre dossier, organisé par année, mois et jour.

Le schéma général de commande CLI pour les jeux de données de prévision est :

```shell
aws s3 cp s3://river-forecast-system-v3/forecasts15/year=<YYYY>/month=<MM>/day=<DD>/discharge.zarr </local/save/path> --recursive --no-sign-request
```
Le schéma général de commande CLI pour les jeux de données rétrospectifs est :

```shell
aws s3 cp s3://river-forecast-system-v3/retrospective/daily.zarr </local/save/path> --recursive --no-sign-request
```

## s5cmd

`s5cmd` est une alternative plus performante à `awscli`. Veuillez consulter la [documentation de s5cmd](https://github.com/peak/s5cmd){:target="_blank"}.
Le schéma général de commande CLI pour les jeux de données de prévision est :

```shell
s5cmd --no-sign-request cp "s3://river-forecast-system-v3/forecasts15/year=<YYYY>/month=<MM>/day=<DD>/discharge.zarr/*" </local/save/path.zarr/>
```

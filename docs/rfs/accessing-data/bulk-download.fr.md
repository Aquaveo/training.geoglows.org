!!! danger "Le téléchargement en masse n'est généralement pas nécessaire"
    La plupart des utilisateurs n'ont pas besoin de ce tutoriel. Tous les produits de prévisions et de simulations rétrospectives sont disponibles pour les requêtes, les téléchargements en masse, et via le service de données. Cependant, les instructions pour interroger les données sont les plus rapides et les plus pratiques (et les moins coûteuses pour GEOGLOWS) pour la plupart des usages.
    Veuillez suivre le tutoriel sur [l'interrogation des données fluviales](code-and-apis.fr.md) avant de continuer cette section.

## Références
La plupart des utilisateurs n'ont pas besoin de télécharger le résultat complet de la simulation pour le monde entier. Vous pouvez souvent vous contenter d'une requête/téléchargement plus large. Si vous continuez, vous devez être familiarisé avec awscli ou un outil équivalent. Une règle pratique utile pour estimer l'espace disque nécessaire est :

- 1 jour de prévisions représente environ 150 Go
- Le Zarr de simulation rétrospective horaire représente environ 6 To
- Le Zarr de simulation rétrospective quotidienne représente environ 500 Go
- Le Zarr de simulation rétrospective mensuelle représente environ 20 Go
- Le Zarr de simulation rétrospective annuelle représente environ 2 Go

## awscli

La meilleure façon de télécharger en masse les données depuis les buckets S3 est d'utiliser un outil en ligne de commande conçu à cet effet. Ces outils permettent de télécharger plusieurs ensembles de données simultanément et à des vitesses supérieures à ce qui est possible via le navigateur web. L'outil de base pour cela est awscli.
Utilisez les [tutoriels AWS S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/download-objects.html){:target="_blank"} pour commencer.

!!! tip "Utilisez `--no-sign-request`"
    Utilisez le paramètre `--no-sign-request` pour éviter les erreurs, surtout si vous n'avez pas de credentials AWS sur votre ordinateur.

Lors du téléchargement de données depuis les buckets S3, les URI racines pour le bucket des prévisions est `s3://geoglows-v2-forecast/` et pour le bucket rétrospectif est `s3://geoglows-v2/`.

Le schéma général de commande CLI pour les ensembles de données de prévisions est :

```shell
aws s3 cp s3://geoglows-v2-forecast/<date>.zarr </local/save/path> --recursive --no-sign-request
```
Le schéma général de commande CLI pour les ensembles de données rétrospectifs est :

```shell
aws s3 cp s3://geoglows-v2/daily.zarr </local/save/path> --recursive --no-sign-request
```

## s5cmd

`s5cmd` est une alternative plus performante à `awscli`. Veuillez consulter la [documentation s5cmd](https://github.com/peak/s5cmd){:target="_blank"}.
Le schéma général de commande CLI pour les ensembles de données de prévision est :

```shell
s5cmd --no-sign-request cp "s3://geoglows-v2-forecast/<date>.zarr/*" </local/save/path.zarr/>
```


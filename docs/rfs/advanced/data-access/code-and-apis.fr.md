!!! note
    Les méthodes décrites ici sont les moyens privilégiés pour récupérer des données du River Forecast System.

## Structures de Données

La plupart des données du RFS sont stockées au format Zarr et découpées (chunked) de manière à pouvoir être interrogées efficacement sous forme de séries temporelles. Vous pouvez lire ces fichiers Zarr
directement depuis AWS S3 avec n'importe quel langage de programmation disposant d'une bibliothèque cliente Zarr. Le moyen le plus simple est d'utiliser Python avec le package `geoglows`.

Pour récupérer des données, vous devrez connaître le numéro d'ID des rivières qui vous intéressent. Veuillez consulter
le [tutoriel sur la recherche des numéros de rivière](../../tutorials/find-river-numbers.fr.md) avant de continuer.

## Package Python geoglows

Le moyen le plus simple de télécharger des données depuis le service de données est d'utiliser le package client Python officiel intitulé « geoglows ». Pour des tutoriels complets, veuillez
consulter la [documentation du package Python geoglows](https://geoglows.readthedocs.io){:target="_blank"}.

Pour des extraits de code répondant à des besoins courants, consultez le [Recueil de Recettes](code-snippets.md).

## Exemple en Python

Pour écrire votre propre code Python qui lit des répertoires Zarr, vous aurez besoin des packages suivants :

- [zarr](https://zarr.readthedocs.io/en/stable/){:target="_blank"} >= 3
- [s3fs](https://s3fs.readthedocs.io/en/latest/){:target="_blank"} >= 2025
- [xarray](http://xarray.pydata.org/en/stable/){:target="_blank"} >= 2025

!!! warning
    Les versions antérieures de ces dépendances fonctionnent également, mais elles n'ont pas été testées pour ce site de formation.

Pour trouver les chemins vers les répertoires Zarr, consultez le [catalogue de données](catalog.md){:target="_blank"}. Vous pouvez passer
l'URI commençant par `s3://` directement à la fonction `xr.open_dataset()`. Vous n'avez pas besoin d'un compte AWS pour accéder aux données, mais vous devez vous assurer que la requête est anonyme en définissant storage_options={'anon': True}.

```python
import xarray as xr

retro_hourly_zarr_uri = 's3://river-forecast-system-v3/retrospective/hourly.zarr'
ds = xr.open_dataset(retro_hourly_zarr_uri, engine='zarr', storage_options={'anon': True})

# maintenant sélectionnez la ou les rivières pour lesquelles vous souhaitez obtenir des données
rivers = [621054340, ]

df = ds.sel(riverId=rivers)["Q"].to_dataframe()

# enregistrez le DataFrame en CSV, faites des analyses, créez un graphique, etc.
df.to_csv('./my_river_data.csv')
```

## Exemple en JavaScript

Pour écrire votre propre code JavaScript, vous aurez besoin d'une dépendance capable de lire les répertoires Zarr. Voici quelques options :

- [zarrita.js](https://zarrita.dev/){:target="_blank"}
- [zarr.js](https://guido.io/zarr.js/){:target="_blank"}

```javascript
import * as zarr from "https://cdn.jsdelivr.net/npm/zarrita/+esm";

const baseZarrUrl = "https://river-forecast-system-v3.s3.us-west-2.amazonaws.com/retrospective/daily.zarr"

// ouvrir la variable riverId
const idStore = new zarr.FetchStore(`${baseZarrUrl}/riverId`);
const idNode = await zarr.open(idStore, {kind: "array"});
// ouvrir la variable de débit
const qStore = new zarr.FetchStore(`${baseZarrUrl}/Q`);
const qNode = await zarr.open(qStore, {kind: "array"});
// ouvrir la variable de temps
const tStore = new zarr.FetchStore(`${baseZarrUrl}/time`);
const tNode = await zarr.open(tStore, {kind: "array"});

// obtenir les valeurs de temps et convertir depuis "time since origin" vers des chaînes ISO
const tUnits = tNode.attrs.units
const tArray = await zarr.get(tNode, [null])
const originTime = tUnits.split("since")[1].trim()
const conversionFactor = {
  seconds: 1,
  minutes: 60,
  hours: 60 * 60,
  days: 60 * 60 * 24,
}[tUnits.split("since")[0].trim()]
const times = [...tArray.data].map(t => {
  let origin = new Date(originTime)
  origin.setSeconds(origin.getSeconds() + (t * conversionFactor))
  return origin.toISOString()
})

// déterminer l'indice de la rivière avec votre ID d'intérêt
const idArray = await zarr.get(idNode, [null])
const idx = idArray.data.indexOf(760127992)

// obtenir les valeurs de débit pour la rivière d'intérêt
const qArray = await zarr.get(qNode, [idx, null])

// faire quelque chose avec vos tableaux de données
console.log("preview of data retrieved:")
console.log("times:", times.slice(0, 50))
console.log("discharge:", qArray.data.slice(0, 50))
```

## Notebooks d'Exemple

Les notebooks Google Colab interactifs suivants présentent des analyses courantes à l'aide de données réelles de rivières.

### Périodes de retour, courbes de durée des débits et débits moyens

Pour approfondir l'analyse des périodes de retour, des courbes de durée des débits et des moyennes saisonnières, nous vous invitons à suivre notre
démonstration interactive dans le notebook Google Colab fourni. Ce notebook pratique vous guidera tout au long du processus en utilisant des données réelles de la rivière Tensift
au Maroc. Vous pouvez accéder au notebook et l'exécuter directement dans votre navigateur :

[Return_Periods-FDC-Average_Flows Colab.ipynb](https://colab.research.google.com/drive/1pcB6VEXgT8MMy0MiL9iek0cviDzebxNB?usp=sharing)

---

#### Données Rétrospectives

Pour approfondir l'analyse des données rétrospectives, des périodes de retour, des courbes de durée des débits et des moyennes saisonnières, nous avons préparé un notebook
Google Colab interactif. Ce notebook fournit des instructions étape par étape pour réaliser ces analyses à l'aide de données réelles de la rivière San Juan à
Rancho La Trinidad, au Costa Rica. Il couvre à la fois les données rétrospectives et l'analyse statistique des débits, ce qui vous permet de vous exercer avec les données et les méthodes
présentées dans ces guides.

- [Tutoriel sur les données de simulation rétrospective](https://colab.research.google.com/drive/1BRn7cJ8a1KbiLUqou3h7hv7QNW4FTjQI?usp=sharing)
- [Tutoriel détaillé](https://colab.research.google.com/drive/1K9-O53eZqGV0mrznoRt0jHuEPnCR9elr?usp=sharing)

---

### Simulation de Prévision

Le notebook Colab fournit un guide interactif pour accéder aux données de prévision du RFS et les visualiser. Il montre comment récupérer
les prévisions de débit, tracer les données à l'aide de bibliothèques Python et interpréter les statistiques clés pour une gestion et une planification efficaces
des ressources en eau.

- [Tutoriel sur les données de simulation de prévision](https://colab.research.google.com/drive/1KgcYNE2_GfBfUpjZiTIBIFlzxpRwq-vO?usp=sharing)
- [Tutoriel détaillé](https://colab.research.google.com/drive/1nGDQ6Y4JclHz_kQW4y-rVKZjQF6FSPwb?usp=sharing)

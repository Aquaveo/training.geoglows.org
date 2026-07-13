!!! note
    Les méthodes décrites ici sont les moyens préférés pour récupérer des données depuis le River Forecast System.

## Structures de données

La plupart des données RFS sont stockées au format Zarr et découpées de manière à pouvoir être interrogées efficacement pour des séries temporelles. Vous pouvez lire ces fichiers Zarr directement depuis AWS S3 en utilisant n'importe quel langage de programmation avec une bibliothèque cliente Zarr. Le moyen le plus simple pour le faire est en Python en utilisant le package `geoglows`.

Pour récupérer des données, vous devrez connaître le numéro d'ID des rivières qui vous intéressent. Veuillez consulter le [tutoriel sur la recherche des numéros de rivière](../tutorials/find-river-numbers.fr.md) avant de continuer.

## Package Python geoglows

Le moyen le plus simple de télécharger des données depuis le service de données est d'utiliser le package client officiel Python intitulé "geoglows". Pour des tutoriels complets, veuillez consulter la [documentation du package Python geoglows](https://geoglows.readthedocs.io){:target="_blank"}.

Pour des extraits de code pour des tâches couramment nécessaires, voir le [Cookbook](code-snippets.md).

## Exemple Python

Pour écrire votre propre code Python qui lit des répertoires Zarr, vous aurez besoin des packages suivants :

- [zarr](https://zarr.readthedocs.io/en/stable/){:target="_blank"} >= 3
- [s3fs](https://s3fs.readthedocs.io/en/latest/){:target="_blank"} >= 2025
- [xarray](http://xarray.pydata.org/en/stable/){:target="_blank"} >= 2025

!!! warning
    Les versions antérieures de ces dépendances fonctionnent également mais n'ont pas été testées pour ce site de formation.

Pour trouver les chemins vers les répertoires Zarr, vous devriez vous référer au [catalogue de données](../datasets/catalog.md){:target="_blank"}. Vous pouvez passer l'URI commençant par `s3://` directement à la fonction `xr.open_dataset()`. Vous n'avez pas besoin d'un compte AWS pour accéder aux données, mais vous devez vous assurer que la requête est anonyme en définissant `storage_options={'anon': True}`.

```python
import xarray as xr

retro_hourly_zarr_uri = 's3://geoglows-v2/retrospective/hourly.zarr'
ds = xr.open_dataset(retro_hourly_zarr_uri, engine='zarr', storage_options={'anon': True})

# maintenant sélectionnez la ou les rivières pour lesquelles vous souhaitez obtenir des données
rivers = [621054340, ]

df = ds.sel(river_id=rivers)["Q"].to_dataframe()

# enregistrez le DataFrame en CSV, faites des analyses, créez un graphique, etc.
df.to_csv('./my_river_data.csv')
```
## Exemple en JavaScript

Pour écrire votre propre code JavaScript, vous aurez besoin d'une dépendance capable de lire les répertoires Zarr. Quelques options incluent :

- [zarrita.js](https://zarrita.dev/){:target="_blank"}
- [zarr.js](https://guido.io/zarr.js/){:target="_blank"}

```javascript
import * as zarr from "https://cdn.jsdelivr.net/npm/zarrita/+esm";

const baseZarrUrl = "http://geoglows-v2.s3-us-west-2.amazonaws.com/retrospective/daily.zarr"

// ouvrir la variable river_id
const idStore = new zarr.FetchStore(`${baseZarrUrl}/river_id`);
const idNode = await zarr.open(idStore, {mode: "r", format: 2});
// ouvrir la variable de débit
const qStore = new zarr.FetchStore(`${baseZarrUrl}/Q`);
const qNode = await zarr.open(qStore, {mode: "r", format: 2});
// ouvrir la variable de temps
const tStore = new zarr.FetchStore(`${baseZarrUrl}/time`);
const tNode = await zarr.open(tStore, {mode: "r", format: 2});

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
const qArray = await zarr.get(qNode, [null, idx])

// faire quelque chose avec vos tableaux de données
console.log("aperçu des données récupérées :")
console.log("times:", times.slice(0, 50))
console.log("discharge:", qArray.data.slice(0, 50))
```

## Notebooks d'Exemple

Les notebooks Google Colab interactifs suivants présentent des analyses courantes à l'aide de données réelles de rivières.

### Périodes de retour, courbes de durée des débits et débits moyens

Pour approfondir l'analyse des périodes de retour, des courbes de durée des débits et des moyennes saisonnières, nous vous invitons à suivre notre démonstration interactive dans le notebook Google Colab fourni. Ce notebook pratique vous guidera tout au long du processus en utilisant des données réelles de la rivière Tensift au Maroc. Vous pouvez accéder au notebook et l'exécuter directement dans votre navigateur :

[Return_Periods-FDC-Average_Flows Colab.ipynb](https://colab.research.google.com/drive/1pcB6VEXgT8MMy0MiL9iek0cviDzebxNB?usp=sharing)

---

#### Données rétrospectives

Pour approfondir l'analyse des données rétrospectives, des périodes de retour, des courbes de durée des débits et des moyennes saisonnières, nous avons préparé un notebook interactif Google Colab. Ce notebook fournit des instructions étape par étape pour réaliser ces analyses en utilisant des données réelles de la rivière San Juan à Rancho La Trinidad au Costa Rica. Il couvre à la fois les données rétrospectives et l'analyse statistique des débits, vous permettant d’interagir avec les données et les méthodes décrites dans ces guides.

- [Retrospective Simulation Data Tutorial](https://colab.research.google.com/drive/1BRn7cJ8a1KbiLUqou3h7hv7QNW4FTjQI?usp=sharing)
- [Long Form Tutorial](https://colab.research.google.com/drive/1K9-O53eZqGV0mrznoRt0jHuEPnCR9elr?usp=sharing)

---

### Simulation de prévision

Le notebook Colab fournit un guide interactif pour accéder aux données de prévision RFS et les visualiser. Il montre comment récupérer les prévisions de débits, tracer les données à l'aide des bibliothèques Python et interpréter les statistiques clés pour une gestion et une planification efficaces des ressources en eau.

- [Forecast Simulation Data Tutorial](https://colab.research.google.com/drive/1KgcYNE2_GfBfUpjZiTIBIFlzxpRwq-vO?usp=sharing)
- [Long Form Tutorial](https://colab.research.google.com/drive/1nGDQ6Y4JclHz_kQW4y-rVKZjQF6FSPwb?usp=sharing)

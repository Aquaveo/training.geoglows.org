!!! note
    Les méthodes décrites ici sont les moyens préférés pour récupérer des données depuis le River Forecast System.

## Structures de données

La plupart des données RFS sont stockées au format Zarr et découpées de manière à pouvoir être interrogées efficacement pour des séries temporelles. Vous pouvez lire ces fichiers Zarr directement depuis AWS S3 en utilisant n'importe quel langage de programmation avec une bibliothèque cliente Zarr. Le moyen le plus simple pour le faire est en Python en utilisant le package `geoglows`.

Pour récupérer des données, vous devrez connaître le numéro d'ID des rivières qui vous intéressent. Veuillez consulter le [tutoriel sur la recherche des numéros de rivière](find-river-numbers.fr.md) avant de continuer.

## Package Python geoglows

Le moyen le plus simple de télécharger des données depuis le service de données est d'utiliser le package client officiel Python intitulé "geoglows". Pour des tutoriels complets, veuillez consulter la [documentation du package Python geoglows](https://geoglows.readthedocs.io){:target="_blank"}.

Pour des extraits de code pour des tâches couramment nécessaires, voir le [Cookbook](../accessing-data/code-snippets.md).

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

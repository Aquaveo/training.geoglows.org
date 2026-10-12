# Méthodes d'Accès Avancées

Si vous souhaitez accéder aux données par programmation, il existe plusieurs façons de le faire.

Toutes les données du RFS peuvent être téléchargées et utilisées par tous. Elles sont toutes stockées dans le bucket AWS :
[https://v3.s3.riverforecastsystem.com/](https://v3.s3.riverforecastsystem.com/){:target="_blank"}. Les données y sont ensuite réparties en dossiers. N'hésitez pas à parcourir le bucket et à
télécharger les données dont vous avez besoin. Les données de nos applications et du [magasin de données](datastore.md) proviennent toutes
de ce bucket. Le bucket est public, aucun compte n'est donc nécessaire. Lorsque vous utilisez des outils comme l'AWS CLI ou Python,
configurez-les pour accéder aux données de manière anonyme (par exemple, `--no-sign-request` ou `anon=True`).

### Exemple : Lecture des Données avec Python

Cet exemple lit le débit rétrospectif journalier d'une rivière directement depuis le bucket. Il nécessite les packages Python `xarray`,
`zarr` (version 3 ou ultérieure) et `s3fs`. Pour trouver l'identifiant d'une rivière, consultez
[Trouver les Numéros de Rivière](../../tutorials/find-river-numbers.md).

```python
import xarray as xr

# open the daily retrospective discharge directly from the public bucket
ds = xr.open_dataset(
    's3://river-forecast-system-v3/retrospective/daily.zarr',
    engine='zarr',
    storage_options={'anon': True},  # access the public bucket anonymously
)

# select one or more rivers by river ID and convert to a table
df = ds.sel(riverId=[760021611])['Q'].to_dataframe()
df.to_csv('my_river_data.csv')
```

De plus, nous avons développé un package Python pour faciliter l'utilisation de nos données et l'accès à celles-ci. La documentation du
package Python se trouve ici : [https://geoglows.readthedocs.io/en/latest/](https://geoglows.readthedocs.io/en/latest/){:target="_blank"}. N'hésitez pas à utiliser ces fonctions pour obtenir les données dont
vous avez besoin.

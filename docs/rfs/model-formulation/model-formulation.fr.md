Le but de cette page est de fournir un aperçu du Système de Prévision Fluviale (RFS), y compris ses entrées et sorties. Si votre intérêt principal est d’utiliser les données, vous pouvez passer cette page et aller directement à la section suivante.

Le graphique suivant donne un aperçu de la formation du RFS.
![Diagramme de la formulation du modèle RFS](../../static/images/rfs-v2-formulation.jpg)

## Entrées

Le Système de Prévision Fluviale (RFS) repose sur trois entrées principales, comme illustré dans le graphique :

1. **Hydrographie provenant de TDX-Hydro**  
   Le réseau fluvial utilisé par le RFS est basé sur l’hydrographie dérivée des données d’élévation numérique de TDX-Hydro. Pour préparer ces données pour le RFS, le réseau hydrographique subit plusieurs modifications et étapes de post-traitement, qui sont documentées dans le [répertoire TDX-Hydro Post-Processing](https://github.com/geoglows/tdxhydro-postprocessing).

2. **Modèles de surface terrestre rétrospectifs (ERA5)**  
   Les données historiques de débit sont fournies par ERA5, un produit de réanalyse global du Centre Européen pour les Prévisions Météorologiques à Moyen Terme (ECMWF).

3. **Modèles de surface terrestre de prévision (IFS)**  
   Les prévisions de débit futur sont générées à l’aide du Système de Prévision Intégrée (IFS) de l’ECMWF.

Les données de débit provenant à la fois d’ERA5 et de l’IFS sont converties en volumes d’écoulement à l’aide des outils du [répertoire basininflow](https://github.com/geoglows/basininflow).

Le tableau suivant résume les principaux jeux de données d’entrée utilisés par le RFS :

| Nom                             | DOI                                                                                | Type                            | Producteur | Licence                                                                                                                                                                         |
|---------------------------------|------------------------------------------------------------------------------------|---------------------------------|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ERA5                            | [DOI](https://doi.org/10.24381/cds.adbb2d47)                                       | Modèle de Surface Terrestre de Réanalyse | ECMWF      | [Licence Copernicus](https://cds.climate.copernicus.eu/api/v2/terms/static/licence-to-use-copernicus-products.pdf) - Gratuit pour usage commercial et non commercial avec attribution |
| TDX-Hydro                       | [Lien](https://earth-info.nga.mil/)                                                | Hydrographie des Rivières et Bassins | NGA        | [Licence TDX-Hydro](https://earth-info.nga.mil/php/download.php?file=tdx-hydro-license) - Publique, fournie "telle quelle" sans garantie                                        |
| Integrated Forecast System 48R1 | [Lien](https://confluence.ecmwf.int/display/FCST/Implementation+of+IFS+Cycle+48r1) | Modèle de Surface Terrestre de Prévision | ECMWF      | Licence payante requise                                                                                                                                                           |

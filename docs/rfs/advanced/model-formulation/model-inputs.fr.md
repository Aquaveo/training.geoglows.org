# Entrées du Modèle


Le Système de Prévision Fluviale (RFS) repose sur trois entrées principales :

## 1. **Hydrographie provenant de TDX-Hydro**  
Le réseau fluvial utilisé par le RFS est basé sur une hydrographie dérivée des données d'élévation numériques de TDX-Hydro. Pour préparer ces données pour le RFS, le réseau hydrographique subit plusieurs modifications et étapes de post-traitement.

### Modifications apportées à TDX-Hydro

Toutes les modifications que nous avons effectuées sur chaque région TDX-Hydro sont enregistrées dans 3 fichiers : 1) processing_options.xlsx, 2) tdx_header_numbers.json et 3)
terminal_node_vpu_list.csv. Le fichier JSON des numéros d'en-tête TDX associe chaque numéro de région TDX-Hydro à un numéro unique à 2 chiffres, dont le premier chiffre est
le premier chiffre du numéro de région, et le second chiffre correspond à l'indice dans l'ordre trié de toutes les régions qui partagent le même premier
chiffre. Le fichier CSV des nœuds terminaux associe chaque nœud terminal (l'identifiant associé à l'exutoire d'un bassin versant) à un numéro de VPU. Un aperçu de ces
modifications est présenté ici.

Les régions exclues comprennent celles situées le plus au nord et certaines des plus petites îles, où les jeux de données de ruissellement peuvent être moins précis et
où la population est clairsemée ou inexistante. Les versions futures pourraient réintroduire ces régions. De plus, nous avons corrigé des erreurs trouvées dans le jeu de données TDX-Hydro, qui
ont été signalées à la NGA pour être corrigées dans les versions futures. Ces erreurs comprennent :

1. Les cours d'eau sans longueur et sans segments amont/aval, c'est-à-dire les cours d'eau composés de seulement deux points situés exactement au même
   endroit. Ces cours d'eau, ainsi que les bassins versants associés, ont été supprimés.
2. Les cours d'eau sans longueur mais avec des segments amont ou aval. Ceux-ci ont été supprimés avec les bassins versants associés, et les attributs des
   segments amont et/ou aval ont été modifiés pour qu'ils se référencent mutuellement et préservent la connectivité du réseau hydrographique.
3. Les bassins versants dont l'identifiant de cours d'eau est « 0 », qui n'ont jamais eu de cours d'eau associé. Ceux-ci ont été supprimés.

Pour la plupart des régions, mais pas toutes, les cours d'eau de tête ont été fusionnés avec les segments situés en aval, jusqu'au segment aval
d'ordre de Strahler 2 ou 3 inclus. Il a été décidé que les régions largement côtières (Japon, îles des Caraïbes, Indonésie)
étaient plus sensibles aux modifications de leurs réseaux hydrographiques ; leurs cours d'eau de tête n'ont donc pas été modifiés. D'autres zones, comme le
désert du Sahara, ont été délimitées avec la même résolution que le reste du monde, souvent avec une résolution trop élevée. Dans ces zones, davantage d'entités pouvaient
être fusionnées sans modifier significativement le routage fluvial. Les cours d'eau de tête et les cours d'eau en aval ont donc été fusionnés en une seule entité avec
leurs bassins versants associés, et les attributs pertinents tels que la longueur et la pente ont été recalculés. L'ordre de cours d'eau jusqu'auquel les cours d'eau de tête
étaient fusionnés a également été choisi en fonction de ces considérations.

![image](../../../static/images/merged-tdxhydro-streams.png)

Les petits bassins versants d'une superficie allant jusqu'à 200 kilomètres carrés ont été supprimés du jeu de données TDX-Hydro pour toutes les régions. Cela a été fait pour des raisons similaires à
celles de la fusion différenciée des cours d'eau de tête. Dans les régions les plus côtières, les bassins versants de 25 à 75 kilomètres carrés au maximum ont été supprimés. Dans d'autres zones, comme
le désert du Sahara ou le nord du Canada, ce sont les bassins versants jusqu'à 200 kilomètres carrés qui ont été supprimés. Dans ces régions plus plates, la haute résolution de la
délimitation crée de petites « cuvettes » ou de petits ensembles de cours d'eau qui ne se déversent pas dans l'océan et ne représentent pas de véritables cours d'eau. Ils ont souvent
une superficie cumulée inférieure à 200 kilomètres carrés. Pour les régions moins côtières et plus plates ou plus sèches, des bassins versants plus grands ont été supprimés.

Les cours d'eau de tête se jetant directement dans un cours d'eau d'ordre de Strahler 2 ou plus ont été fusionnés avec le segment immédiatement en aval
pour la plupart des régions, mais pas toutes. Les raisons de l'élagage de ces cours d'eau sont les mêmes que ci-dessus.


   Aborder les entrées relatives aux cours d'eau et aux réservoirs ?

## 2. **Modèle de surface terrestre rétrospectif (ERA5)**  
Les bons modèles hydrologiques dépendent d'une bonne météorologie, car c'est la météorologie qui pilote l'hydrologie. Les modèles météorologiques reposent en grande partie sur des calculs de bilan énergétique pilotés par le rayonnement solaire incident, construits à partir de cellules de grille 3D de hauteurs variables.

L'ECMWF exécute un modèle de surface terrestre sur ces données météorologiques afin de produire des variables supplémentaires telles que le ruissellement, c'est-à-dire l'eau « restante » en hydrologie. Chaque cellule est traitée comme un seau indépendant, dans lequel les précipitations, l'infiltration, l'évapotranspiration, la fonte des neiges, les écoulements d'eau souterraine et l'humidité du sol interagissent. Le ruissellement est ce qui reste après ces processus.

![Modèle en seau d'une cellule de grille de surface terrestre](../../../static/images/bucket-model.png){ width="350" }

Pour la simulation rétrospective (historique), le RFS utilise le ruissellement d'ERA5, le produit de réanalyse mondiale de l'ECMWF. Comme il reconstitue les conditions passées à partir d'observations, ERA5 fournit l'historique long et cohérent que le RFS utilise pour construire ses débits historiques.

## 3. **Modèle de surface terrestre de prévision (IFS)**  
Le ruissellement prévu provient de l'Integrated Forecasting System (IFS, Système de Prévision Intégré) de l'ECMWF, qui exécute les mêmes calculs en seau de surface terrestre en avançant dans le temps afin de prédire le ruissellement futur. Plutôt qu'une prévision unique, l'IFS fonctionne sous forme d'ensemble : plusieurs simulations sont lancées à partir de conditions initiales légèrement différentes afin de représenter l'incertitude de la météo future. On obtient ainsi une plage de valeurs de ruissellement plutôt qu'une seule, que le RFS achemine pour produire un éventail de prévisions de débit traduisant la probabilité et l'ampleur possible des débits à venir.

Ce ruissellement alimente les prévisions du RFS et fournit des prédictions de débit à court terme qui complètent l'historique basé sur ERA5.

Les données de ruissellement provenant à la fois d'ERA5 et de l'IFS sont converties en volumes d'écoulement à l'aide des outils du [dépôt basininflow](https://github.com/geoglows/basininflow).

Le tableau suivant résume les principaux jeux de données d'entrée utilisés par le RFS :

| Nom                             | DOI                                                                                | Type                            | Producteur | Licence                                                                                                                                                                          |
|---------------------------------|------------------------------------------------------------------------------------|---------------------------------|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ERA5                            | [DOI](https://doi.org/10.24381/cds.adbb2d47)                                       | Modèle de Surface Terrestre de Réanalyse | ECMWF      | [Licence Copernicus](https://cds.climate.copernicus.eu/api/v2/terms/static/licence-to-use-copernicus-products.pdf) - Gratuit pour un usage commercial et non commercial avec attribution |
| TDX-Hydro                       | [Lien](https://earth-info.nga.mil/)                                                | Hydrographie des Rivières et des Bassins Versants | NGA        | [Licence TDX-Hydro](https://earth-info.nga.mil/php/download.php?file=tdx-hydro-license) - Disponible publiquement, fourni « tel quel » sans garantie                                  |
| Integrated Forecast System 48R1 | [Lien](https://confluence.ecmwf.int/display/FCST/Implementation+of+IFS+Cycle+48r1) | Modèle de Surface Terrestre de Prévision | ECMWF      | Licence payante requise                                                                                                                                 

En plus des entrées du modèle lui-même, des données observées sont utilisées dans le processus de calibration. Aborder brièvement la collecte et l'utilisation des données observées ?

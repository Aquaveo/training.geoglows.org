# Nouveautés

Ce site de formation porte sur la version 3 du RFS (River Forecast System, ou Système de Prévision Fluviale). De nombreux changements majeurs ont été apportés entre cette version du modèle et la version précédente. Cette page présente quelques détails sur les améliorations et les modifications apportées au modèle. Si vous cherchez simplement des informations sur le modèle, vous pouvez passer cette page.

1. **Données hydrographiques**
    1. **Nombre de cours d'eau** - Le RFSv2 comptait environ 6,8 millions de cours d'eau, tandis que le RFSv3 en compte environ 4,9 millions. Ces réductions proviennent principalement de la suppression des cours d'eau situés dans les grands déserts : des cours d'eau ont été supprimés dans le désert du Sahara, le désert de Gobi et les déserts du centre de l'Australie. Les segments de cours d'eau situés à l'intérieur des lacs ou dans de petits bassins côtiers (ou dans l'océan) ont également été supprimés. Certains petits cours d'eau ont aussi été fusionnés. Les identifiants de rivière sont tous restés les mêmes dans le modèle. Si votre identifiant de rivière n'est plus disponible et qu'il ne se trouve pas dans une zone supprimée, vous pouvez le faire correspondre au nouveau cours d'eau du RFSv3. La correspondance entre les anciens et les nouveaux identifiants de rivière est disponible dans le fichier [tdxhydro_to_v3_id_map.parquet](https://v3.s3.riverforecastsystem.com/hydrography/global/tdxhydro_to_v3_id_map.parquet) (environ 87 Mo).
    2. **Régions** - Les données hydrographiques ne sont plus organisées en 125 VPU. Elles sont désormais organisées en 47 régions numérotées d'après leurs bassins HydroSHEDS de niveau 2.
    3. **Lacs** - Un nouvel ensemble de lacs figure dans le jeu de données hydrographiques. Il est différent des lacs qui étaient disponibles dans le RFSv2.
2. **Formats de stockage des données** - Les fichiers zarr utilisent désormais la version 3 de zarr au lieu de la version 2. Davantage de métadonnées ont été ajoutées aux fichiers et le stockage a été encore optimisé.
3. **Modifications des processus de routage** - Le processus qui achemine l'eau à travers les rivières a été mis à jour pour reposer entièrement sur un package Python appelé river-route, développé par le Dr Riley Hales. Le processus a été mis à jour pour s'exécuter plus rapidement et quelques corrections mineures ont été apportées à certaines entrées du modèle.
4. **Nouveaux buckets AWS** - Un nouveau bucket AWS contient toutes les données de la version 3 du modèle. Il se trouve ici : [https://v3.s3.riverforecastsystem.com](https://v3.s3.riverforecastsystem.com).
5. **Nouveau Hydroviewer** - Le Hydroviewer a été mis à jour pour la version 3, avec de nouvelles fonctionnalités comme la cartographie des inondations, des outils pour sélectionner des rivières et des bassins versants entiers, et la recherche de rivières par leur nom. Consultez la page du [Hydroviewer](web-apps/hydroviewer.md) pour apprendre à l'utiliser.
6. **Produits de cartographie des inondations** - Le RFS produit désormais des cartes d'inondation qui montrent la zone qui serait inondée le long d'une rivière, ainsi que la profondeur de l'eau, pour un débit donné. Elles peuvent être consultées et téléchargées dans le [Hydroviewer](web-apps/hydroviewer.md), et les différents produits de cartes d'inondation sont décrits dans [Données Disponibles](data/available-data.md#cartes-dinondation).
7. **Magasin de données** - Un nouveau magasin de données est disponible pour télécharger les produits du RFSv3 : [https://apps.geoglows.org/previews/rfs-data-store/](https://apps.geoglows.org/previews/rfs-data-store/). Ce site fournit des métadonnées et des informations sur les données disponibles, et permet aux utilisateurs de parcourir et de télécharger les produits de données qui les intéressent. Consultez [Le Magasin de Données](data/accessing-data/datastore.md) pour savoir comment l'utiliser.
8. **Modifications de ce site** - Ce site a été mis à jour et réorganisé. Certaines des informations les plus avancées ont été déplacées dans une section avancée. Des informations sur les eaux souterraines ont également été ajoutées.

## Amélioration du Modèle

Le RFS reçoit ses entrées de données météorologiques mondiales. Ces données mondiales comportent un biais inhérent. Les développeurs du RFS
travaillent constamment à réduire ces biais et à corriger les erreurs qui se produisent dans le système. Nous travaillons à appliquer une
correction du biais aux entrées du modèle afin d'en améliorer les résultats.

La [correction locale du biais](../v2/rfs/bias-correction/bias-correction.md) était une option disponible dans les versions 2 et 1. Elle a été développée dans le cadre d'un
projet de recherche et était réalisée par les utilisateurs finaux comme étape de post-traitement. La correction locale du biais ne
permettait d'appliquer des corrections qu'aux segments de rivière équipés d'une station de jaugeage. Bien que le code reste disponible pour
les utilisateurs qui souhaitent utiliser cette option, l'accent est désormais mis sur des options permettant d'améliorer les rivières
au-delà d'un seul emplacement. Dans ce but, une correction globale du biais,
[SABER](../v2/rfs/bias-correction/bias-correction.md#saber-stream-analysis-for-bias-estimation-and-reduction), a été testée dans la version 2.

À l'avenir, des recherches sont menées pour que cette correction et cet étalonnage soient intégrés à la formulation du modèle plutôt qu'à
une étape de post-traitement. Cela permet à l'ensemble du modèle de bénéficier des données des stations de jaugeage et évite d'avoir deux
versions distinctes des données : avec et sans correction du biais.

GEOGLOWS constitue une base de données de stations de jaugeage pour améliorer le RFS. Les données de jaugeage partagées amélioreront les
performances sur les rivières voisines et sur l'ensemble du modèle. Les données d'une station pourraient profiter à tout un bassin versant
ou à des rivières similaires, et pas seulement à son emplacement. Les données seraient utilisées pour rendre le modèle aussi précis que
possible.

Toutes les données partagées peuvent rester privées. Elles seront utilisées à des fins de recherche et de validation, mais les valeurs
brutes des stations ne seront pas publiées sans autorisation. Le partage de données locales peut améliorer les performances dans les zones
concernées, ce qui rend le modèle plus précis dans les régions disposant de données de jaugeage partagées.

Si vous disposez de données de débit ou de niveau d'eau, nous serions ravis de les inclure dans notre processus d'étalonnage et de
validation. Veuillez remplir ce formulaire Google, et nous vous contacterons au sujet des données.
<!-- TODO: add the link to the Google form for contributing gauge data -->

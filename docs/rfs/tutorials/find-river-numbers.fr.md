## Vue d'ensemble

Les jeux de données du RFS V3 modélisent 4,9 millions de segments de rivière. Ces numéros proviennent du jeu de données TDX-Hydro et diffèrent des
numéros présents dans tout autre jeu de données de cours d'eau. Le RFS V3 utilise les mêmes identifiants de rivière que le RFS V2, mais certains cours d'eau de la V2 ont été supprimés ou fusionnés dans la V3 (consultez
[Nouveautés](../whats-new.md) pour plus de détails et pour obtenir un fichier qui fait correspondre les anciens identifiants aux nouveaux). Tous les numéros d'identification (ID) comportent 9 chiffres. À titre de référence, ce tableau fournit les ID de certaines
rivières majeures et leurs emplacements généraux.

| Numéro ID | Rivières sélectionnées et emplacements généraux |
|-----------|-------------------------------------------------|
| 760021611 | Mississippi, États-Unis                         |
| 160064246 | Nil, Afrique de l'Est                           |
| 710462910 | Colorado, États-Unis et Mexique                 |
| 441057380 | Gange, Inde                                     |
| 430157411 | Mékong, Vietnam                                 |
| 210406913 | Tibre, Italie                                   |
| 621010293 | Amazone, Brésil                                 |
| 130747391 | Congo, R.D. Congo                               |
| 640255644 | Paraná, Argentine                               |

Les numéros ID du RFS comportent 9 chiffres. Bien que les grands nombres soient souvent séparés par une virgule ou un point selon les langues, tout code que vous écrivez
pour récupérer des données ***ne doit pas*** inclure de séparateurs. Ces ID sont des entiers. La plupart des langages de programmation interpréteront les guillemets, points, virgules
ou autres caractères comme autre chose qu'un entier, ce qui fera échouer le processus de récupération. Par exemple, le numéro `123456789` ***ne doit pas***
être écrit `123,456,789` ou `123.456.789` ou `"123456789"` ou `"123,456,789"` ou sous toute autre variante. Seule la représentation entière `123456789`
fonctionnera.

## Utilisation de l'Application Web

Le moyen le plus simple de trouver l'ID d'une rivière est d'utiliser l'[application web du RFS](https://apps.geoglows.org/rfs){:target="_blank"}. Cliquez sur un cours d'eau sur
la carte. Pour vous assurer de cliquer sur le cours d'eau voulu, la carte effectue un zoom vers un niveau de détail plus élevé si vous êtes trop dézoomé. Après
avoir cliqué sur un cours d'eau, la carte identifie le segment de rivière sélectionné et l'ID vous est présenté dans la fenêtre contextuelle, avec des graphiques
et d'autres informations.

## Utilisation des Données Hydrographiques

Les données hydrographiques sont disponibles dans le [magasin de données du RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}. Vous pouvez télécharger et visualiser soit
les cours d'eau, soit les bassins versants dans un logiciel SIG comme ArcGIS ou QGIS. Vous pouvez cliquer sur les entités ou utiliser des outils d'analyse spatiale pour sélectionner de nombreuses rivières. Les
numéros ID de ces rivières sont stockés dans l'attribut riverId.

## Trouver des Rivières à partir de la Latitude/Longitude

Il existe de nombreuses méthodes pour essayer de trouver un ID de rivière à partir d'une latitude et d'une longitude. Aucune n'est parfaite dans tous les cas. Les méthodes automatisées peuvent produire plusieurs
erreurs potentielles, liées à l'exactitude et à la précision de vos points lat/lon, à l'exactitude des lignes de cours d'eau à cet endroit précis,
au fait que vous souhaitiez vous accrocher à l'exutoire le plus proche ou à l'arc de cours d'eau le plus proche, à la proximité de vos coordonnées avec une confluence où le SIG pourrait être induit en erreur par
plusieurs choix proches, etc. Les méthodes automatisées doivent être considérées comme imparfaites et leur exactitude doit être vérifiée par rapport à d'autres sources, telles qu'une superficie de
drainage amont connue à la latitude/longitude d'une station de mesure, le nom de la rivière, des comparaisons avec des fonds de carte d'imagerie ou d'autres moyens.

Une première méthode consiste à charger les fichiers SIG des cours d'eau de votre zone d'intérêt dans un logiciel SIG. Vous pouvez accrocher vos points à l'arc de cours d'eau le plus proche.
Dans QGIS, l'outil s'appelle « Snap geometries to layer ». Utilisez l'algorithme permettant de trouver le point le plus proche et d'insérer des sommets supplémentaires si nécessaire.

Une autre méthode consiste à télécharger les polygones des bassins versants et à les intersecter avec une couche contenant vos points lat/lon. Le travail SIG est simple,
mais il est parfois moins précis et nécessite des téléchargements de fichiers plus volumineux.

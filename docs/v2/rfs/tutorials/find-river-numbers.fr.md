## Vue d'ensemble

Il y a 6,25 millions de segments de rivière modélisés dans les jeux de données RFS V2. Ces numéros sont uniques au jeu de données TDX-Hydro et diffèrent des numéros présents dans tout autre jeu de données de cours d'eau et dans les versions précédentes du modèle. Tous les numéros d'identification (ID) sont à 9 chiffres. À titre de référence, ce tableau fournit les ID de certaines rivières majeures et leurs emplacements généraux.

| Numéro ID | Rivières sélectionnées et emplacements généraux |
|-----------|-----------------------------------------------|
| 760021611 | Mississippi, USA                              |
| 160064246 | Nil, Afrique de l'Est                          |
| 710462910 | Colorado, USA & Mexique                        |
| 441057380 | Gange, Inde                                   |
| 430157411 | Mékong, Vietnam                               |
| 210406913 | Tibre, Italie                                 |
| 621010293 | Amazone, Brésil                               |
| 130747391 | Congo, R.D. Congo                             |
| 640255644 | Paraná, Argentine                             |

Les numéros ID RFS comportent 9 chiffres. Bien que les grands nombres soient souvent séparés par une virgule ou un point dans différentes langues, tout code que vous écrivez pour récupérer des données ***ne doit pas*** inclure de séparateurs. Ces ID sont des entiers. La plupart des langages de programmation interpréteront les guillemets, points, virgules ou autres caractères comme autre chose qu’un entier, ce qui fera échouer le processus de récupération. Par exemple, le numéro `123456789` ***ne doit pas*** être écrit comme `123,456,789` ou `123.456.789` ou `"123456789"` ou `"123,456,789"` ou toute autre variation. Seule la représentation entière `123456789` fonctionnera.

!!! warning "Utilisateurs migrés depuis V1"
    RFS v2 est dérivé d'un modèle numérique de terrain (DEM) différent de v1 et comporte significativement plus de cours d'eau modélisés. En raison de la résolution plus élevée et des changements dans le placement des chenaux, il n'est pas possible de fournir une correspondance complète entre tous les numéros de la version 1 et les numéros v2. Nous avons décrit ci-dessous quelques étapes pour mapper un ancien ID vers un ID RFS 2.

## Utilisation de l'application Web

Le moyen le plus simple de trouver l'ID d'une rivière est d'utiliser l'[application web RFS](https://hydroviewer.geoglows.org){:target="_blank"}. Cliquez sur un cours d'eau sur la carte. Pour vous assurer que vous cliquez sur le cours d'eau exact voulu, la carte effectuera un zoom sur un niveau de détail plus élevé si vous êtes trop éloigné. Après avoir cliqué sur un cours d'eau, la carte identifiera le segment de rivière sélectionné et l'ID sera présenté dans la fenêtre pop-up avec les graphiques et autres informations.

## Utilisation des données hydrographiques

Les données hydrographiques sont disponibles dans le [catalogue de données](../datasets/catalog.md){:target="_blank"}. Vous pouvez télécharger et visualiser soit les cours d'eau, soit les bassins versants dans un logiciel SIG comme ArcGIS ou QGIS. Vous pouvez cliquer sur les entités ou utiliser des outils d'analyse spatiale pour sélectionner plusieurs rivières. Les numéros ID de ces rivières sont stockés dans l'attribut LINKNO.

## Trouver des rivières avec latitude/longitude

Il existe plusieurs méthodes pour essayer de trouver un ID de rivière à partir d'une latitude et d'une longitude. Aucune n'est parfaite pour tous les cas. Plusieurs erreurs potentielles peuvent survenir avec des méthodes automatisées en raison de la précision de vos points lat/lon, de la précision des lignes de cours d'eau à cet endroit précis, si vous souhaitez vous ajuster au point de sortie le plus proche ou à l'arc de cours d'eau le plus proche, si vos coordonnées sont proches d'une confluence où le SIG pourrait se tromper avec plusieurs choix proches, etc. Les méthodes automatisées doivent être considérées comme imparfaites et vérifiées pour leur exactitude par rapport à d'autres sources, telles qu'une zone de drainage amont connue à la latitude/longitude d’un point de jauge, le nom de la rivière, des comparaisons avec des cartes d'imagerie ou autres moyens.

Une méthode pour commencer consiste à charger les fichiers GIS des cours d'eau de votre zone d'intérêt dans un logiciel SIG. Vous pouvez les ajuster au segment de cours d'eau le plus proche. Dans QGIS, l'outil s'appelle "Snap geometries to layer”. Utilisez l'algorithme pour trouver le point le plus proche et insérer des sommets supplémentaires si nécessaire.

Une autre méthode consiste à télécharger les polygones des bassins versants et à les intersecter avec une couche contenant vos points lat/lon. Le travail SIG est simple mais parfois moins précis et nécessite des téléchargements de fichiers plus volumineux.

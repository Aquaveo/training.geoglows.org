## Termes et Vocabulaire

- **Hydrographie** : jeux de données SIG d'éléments hydrologiques tels que les cours d'eau, les points de confluence, les limites de bassins versants élémentaires, les limites de bassins versants, les limites
  de lacs et d'autres entités.
- **Hydrofabric** : hydrographie.
- **TanDEM-X** : mission satellitaire SAR du Centre Aérospatial Allemand (DLR) et d'Airbus Defence and Space. Elle sert à produire un modèle numérique
  d'élévation à 12 mètres, qui est le produit mondial de ce type le plus précis et à la plus haute résolution. Il n'est pas disponible publiquement, mais les produits Copernicus Glo30 et
  FABDEM qui en sont dérivés le sont.
- **TDX-Hydro** : jeu de données de lignes centrales de cours d'eau et de limites de bassins versants produit par la National Geospatial Intelligence Agency en 2023. Les cours d'eau sont
  délimités à partir des données d'élévation TanDEM-X à 12 mètres à l'aide de TauDEM, avec un prétraitement approfondi des élévations et un post-traitement de correction de
  l'emplacement des lignes centrales des cours d'eau.
- **TauDEM** : outil d'analyse de terrain utilisé pour délimiter les cours d'eau et les bassins versants à partir de données d'élévation.
- **Région** : groupe d'un ou plusieurs bassins versants complets réunis pour former des sous-ensembles plus petits du jeu de données hydrographiques mondial, afin de faciliter la
  distribution des données, la répartition des calculs et la création de cartes. Les régions sont numérotées d'après l'identifiant de leur bassin HydroBASINS de niveau 2. Le RFS V2 utilisait à la place 125
  sous-ensembles plus petits appelés VPU (Vector Processing Units).
- **River ID** : identifiant unique de chaque ligne centrale de cours d'eau dans le jeu de données hydrographiques du RFS. Les logiciels SIG et hydrologiques utilisent généralement des
  noms différents pour cet identifiant. Par exemple, TauDEM et TDX-Hydro utilisent « link number » (LINKNO) et les logiciels Esri l'appellent « common identifier » (COMID). Dans
  le RFS, on parle de River ID, et il est stocké dans l'attribut riverId. Toute référence à LINKNO, COMID, ReachID, StreamID, RiverID ou à tout
  terme similaire doit être comprise comme désignant la même chose.
- **Ordre de Strahler** : nombre servant à classer les rivières topologiquement. Les plus petites rivières sont d'ordre 1 et, lorsque deux rivières d'ordre 1 se rejoignent, elles
  forment une rivière d'ordre 2. Lorsque deux rivières d'ordre 2 se rejoignent, elles forment une rivière d'ordre 3, et ainsi de suite. Dans TDX-Hydro, l'ordre le plus élevé est 9.

---

## Aperçu

L'hydrographie du RFS est une modification du jeu de données de cours d'eau et de bassins versants TDX-Hydro. Elle provient des données d'élévation propriétaires TanDEM-X à 12 m. Vous pouvez
télécharger le jeu de données complet et consulter le document technique décrivant sa création sur https://earth-info.nga.mil/, sous l'onglet « Geosciences ». Le jeu de données TDX-Hydro complet contient environ 16 millions de segments de rivière et couvre l'ensemble du globe en 62 parties correspondant au niveau 2
de HydroBASINS. Nous avons exclu 12 régions représentant des îles ou les terres situées le plus au nord. De plus, de nombreuses révisions visant à réduire le nombre d'entités de cours d'eau
et à optimiser le réseau pour le routage dans les chenaux ont ramené le nombre total de rivières à 4,9 millions. Cette version utilisée dans le RFS est
mise à la disposition des utilisateurs, qui peuvent la télécharger et l'utiliser à leurs propres fins. Ce jeu de données est appelé hydrographie, hydrofabric ou réseau fluvial. Il s'agit de
données vectorielles composées de points et de lignes avec des coordonnées, et non de données en grille, et il comprend quatre composants principaux :

- Les **lignes centrales exactes des cours d'eau** utilisées dans le RFS. Chaque cours d'eau possède un identifiant unique à 9 chiffres, appelé reachID, link number ou stream ID.
  Il s'agit du fichier « streams_{region}.geo.parquet ».
- Les **limites des bassins versants** utilisées dans le RFS. Ce sont les limites entourant chacune des lignes de cours d'eau ; elles représentent la zone reliée à cette ligne.
  Elles sont identifiées par le même identifiant de rivière que les lignes centrales des cours d'eau. Il s'agit du fichier « catchments_{region}.geo.parquet ». Chaque ligne centrale
  de cours d'eau correspond exactement à une limite de bassin versant unique.
- Les **points de connexion** utilisés dans le RFS, là où différentes lignes centrales de cours d'eau se rejoignent. Chaque point possède un attribut appelé riverId, qui représente
  l'identifiant de l'unique rivière située en aval de ce point. Il possède un autre attribut appelé upstream_ids, qui est une liste des identifiants des rivières
  situées en amont du point de connexion. Il s'agit du fichier « confluences_{region}.geo.parquet ».
- Les **bassins versants de lacs fusionnés** utilisés dans le RFS pour représenter l'emplacement des lacs. Les bassins versants de cours d'eau identifiés par une recherche SIG comme faisant
  partie d'un lac ont été fusionnés pour représenter les lacs. Leur forme diffère donc de la limite réelle du lac, puisqu'elle dépend des formes des
  bassins versants fusionnés.

---

## Régions

Les données SIG sont divisées en 47 parties plus petites, les régions. Cela facilite la gestion et l'accès à cette grande quantité de données. Chaque région représente un ou
plusieurs bassins versants complets et est numérotée d'après l'identifiant de son bassin HydroBASINS de niveau 2.

Les limites des régions sont également disponibles en téléchargement (le fichier « regions.geo.parquet », ou « boundary_{region}.geo.parquet » pour une seule région) afin d'aider
à identifier la région qui contient la zone d'intérêt de l'utilisateur. Les autres jeux de données SIG doivent être téléchargés en fonction de la région d'intérêt et sont
téléchargés pour la région entière.

---

## Métadonnées Disponibles

Les cours d'eau de la V3 possèdent les attributs suivants, dont beaucoup proviennent du processus de délimitation TauDEM. Pour plus d'explications sur ces attributs, veuillez
consulter la [documentation TauDEM](https://hydrology.usu.edu/taudem/taudem5/help53/StreamReachAndWatershed.html){:target="_blank"}.

| Attribut        | Source    | Description                                                                                                         |
|-----------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| riverId         | TDX-Hydro | Numéro d'identification à 9 chiffres, unique à l'échelle mondiale, de cette rivière (le LINKNO de TDX-Hydro).        |
| nextRiverId     | TDX-Hydro | L'identifiant (riverId) de la rivière située immédiatement en aval de cette rivière, ou -1 à un exutoire.           |
| outletRiverId   | RFS V3    | L'identifiant de la rivière de l'exutoire final vers lequel s'écoule le bassin versant de ce cours d'eau.            |
| riverIndex      | RFS V3    | La position de la rivière dans l'ordre topologique (de la tête de bassin à l'exutoire). Les fichiers rétrospectifs et de prévision utilisent le même ordre. |
| upstreamCount   | RFS V3    | Le nombre total de rivières situées en amont de cette rivière. Elles se trouvent toutes entre riverIndex − upstreamCount et riverIndex. |
| strahlerOrder   | TDX-Hydro | L'ordre de Strahler du cours d'eau.                                                                                 |
| shreveOrder     | RFS V3    | La magnitude de Shreve du cours d'eau.                                                                              |
| USContArea      | TDX-Hydro | La superficie totale drainée en amont du point le plus en amont, en mètres carrés.                                  |
| DSContArea      | TDX-Hydro | La superficie totale drainée en amont du point le plus en aval, en mètres carrés.                                   |
| areaM2          | RFS V3    | La superficie du bassin versant propre de la rivière, en mètres carrés.                                             |
| Length          | RFS V3    | La longueur de la rivière, en mètres.                                                                               |
| TDXHydroRegion  | RFS V3    | La région HydroBASINS de niveau 2 à laquelle appartient la rivière.                                                 |
| musk_k          | RFS V3    | Le paramètre k de Muskingum utilisé pour le routage fluvial.                                                        |
| musk_x          | RFS V3    | Le paramètre x de Muskingum utilisé pour le routage fluvial.                                                        |
| velocity_factor | RFS V3    | Le facteur d'échelle de vitesse utilisé pour calculer musk_k.                                                       |

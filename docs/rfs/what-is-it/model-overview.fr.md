# Aperçu

Le système de prévision fluviale est conçu pour prédire la quantité d'eau présente dans les rivières à l'échelle mondiale. Ce calcul repose sur une équation de base selon laquelle toute l'eau sur Terre doit être conservée. Autrement dit, l'eau qui tombe sous forme de précipitations doit ensuite soit pénétrer dans le sol (infiltration), soit s'évaporer dans l'atmosphère, soit continuer à ruisseler à la surface du sol.

Cette idée est communément appelée le cycle de l'eau. L'eau circule sur la Terre : elle tombe sous forme de précipitations, puis s'évapore dans l'air, se condense et retombe à nouveau.

![Le cycle de l'eau](../../static/images/Water-Cycle-Art2A_medium.png)

*Crédit image : [NASA Global Precipitation Measurement](https://gpm.nasa.gov/education/water-cycle)*

Pour en savoir plus sur le cycle de l'eau, consultez la page [Water Cycle](https://gpm.nasa.gov/education/water-cycle) de la NASA.

Le ruissellement de surface est l'eau qui reste à la surface sans s'évaporer ni s'infiltrer dans le sol. C'est comme l'eau que l'on peut voir couler dans les rues ou sur les trottoirs après un orage.

Cette eau finit par s'accumuler à certains endroits, créant des cours d'eau et des lacs. L'eau continue ensuite à s'écouler vers l'aval sous forme de rivière jusqu'à ce qu'elle atteigne l'océan ou un lac sans exutoire.

Par conséquent, pour prédire l'eau présente dans les cours d'eau, nous devons connaître plusieurs éléments :

1. **Les données d'altitude.** Grâce à ces informations, nous pouvons déduire où les cours d'eau commenceront à se former. Nous savons que l'eau s'écoule vers le bas ; avec l'altitude de la surface terrestre, nous savons donc où l'eau ira lorsqu'il pleut.
2. **La quantité d'eau qui devient du ruissellement de surface.** Il existe des modèles météorologiques qui prédisent la quantité de pluie qui tombera à l'avenir et qui peuvent indiquer la quantité de pluie tombée dans le passé. Ce sont eux que nous utilisons lorsque nous consultons la météo pour savoir s'il pleuvra demain. Ces mêmes informations peuvent servir à savoir quel sera le débit demain. Elles nous permettent d'estimer la quantité d'eau qui va ruisseler et donc s'écouler dans les cours d'eau.
3. **La quantité d'eau en amont de chez moi.** Nous savons qu'une fois dans un cours d'eau, l'eau continue de s'écouler jusqu'à atteindre un lac sans exutoire ou un océan. Cela signifie que l'eau du ruisseau au fond de mon jardin dépend de la quantité de pluie tombée dans mon jardin, mais aussi de la quantité d'eau présente en amont qui s'est écoulée jusqu'à mon jardin. Nous pouvons le déterminer en déplaçant continuellement l'eau vers l'aval.
4. **La façon dont l'eau se déplace.** Nous devons savoir comment l'eau entre dans les cours d'eau, puis comment elle se déplace vers l'aval une fois dans la rivière. Par exemple, nous devons connaître la vitesse à laquelle cela se produit afin de savoir combien de temps il faut à une pluie qui entre dans le Mississippi, dans le nord des États-Unis, pour atteindre l'océan Atlantique.

Dans le système de prévision fluviale, ce sont les éléments nécessaires pour créer le modèle hydrologique. Le système de prévision fluviale utilise les données d'altitude de TDX-Hydro, construites à partir de données satellitaires, pour estimer l'emplacement des cours d'eau dans le monde entier. La quantité d'eau nous est fournie par l'ECMWF, une institution européenne qui exécute des modèles météorologiques. Ils modélisent la quantité de précipitations tombées dans le passé et prédisent celle qui tombera à l'avenir. Ils prédisent également quelle part des précipitations se transformera en ruissellement de surface et entrera dans les cours d'eau. C'est ainsi que l'on peut prédire la quantité d'eau qui entre dans les cours d'eau.

Les deux derniers éléments, la quantité d'eau en amont et la façon dont l'eau se déplace, sont liés. Ils sont calculés à l'aide d'un processus appelé routage. C'est là que nous calculons le déplacement de l'eau entre de petits segments de cours d'eau. Si ce calcul est effectué en continu, nous connaissons toujours la quantité d'eau en amont et nous pouvons la déplacer vers l'aval tandis que de l'eau supplémentaire s'ajoute à la rivière grâce aux précipitations locales. C'est le processus qu'exécute notre modèle. Il existe plusieurs méthodes pour effectuer ce calcul. Nous utilisons un processus appelé routage de Muskingum, du nom des équations que nous utilisons pour calculer comment l'eau se déplace à travers chaque petit segment de cours d'eau vers le segment situé en aval.

Nous avons créé cette application web pour mieux illustrer le fonctionnement de ce processus.

[https://cdn.apps.geoglows.org/webroute/live.html](https://cdn.apps.geoglows.org/webroute/live.html#map=1.6/21.3/-14.8)

Bien qu'il existe de nombreuses façons de l'explorer, une manière simple pour la démonstration consiste à sélectionner « pulse » comme pinceau.

<video controls muted playsinline width="100%">
  <source src="/static/videos/webroute-pulse-demo.mp4" type="video/mp4">
</video>

Cela revient à choisir d'injecter de l'eau à un endroit précis. Cliquez quelque part sur la carte du réseau hydrographique. Lorsque les cours d'eau changent de couleur, vous observez l'eau se déplacer dans votre rivière grâce à l'algorithme de routage utilisé par le RFS. La différence est qu'au lieu de sélectionner des emplacements au hasard comme dans cette démonstration, nous utilisons les prédictions mondiales pour injecter de l'eau dans toutes les rivières chaque fois qu'il pleut.

# Routage Fluvial

!!! warning "Avertissement"
    Le but de cette section sur la formulation du modèle est de fournir un aperçu du RFS, y compris ses entrées et ses sorties. Si votre intérêt principal est d'utiliser les données, vous pouvez passer cette section et aller directement à la section [Données](../data/available-data.md) de notre site.

Le routage est l'étape au cours de laquelle le RFS fait circuler l'eau dans le réseau hydrographique. Une fois le ruissellement du
bassin versant de chaque rivière calculé (voir l'[Aperçu](model-formulation.md)), le routage achemine cette eau vers l'aval, rivière par
rivière, pour créer un hydrogramme pour chaque rivière. Le RFS utilise [river-route](https://river-route.code.hales.app/){:target="_blank"}, un package Python
développé par le Dr Riley Hales pour router rapidement l'eau dans de très grands réseaux hydrographiques. Le code est disponible sur
[GitHub](https://github.com/rileyhales/river-route){:target="_blank"}.

## Comment l'Eau Circule dans le Réseau

À chaque pas de temps, le ruissellement du bassin versant d'une rivière est ajouté à cette rivière, ainsi que toute l'eau provenant des
rivières situées immédiatement en amont. Comme le débit d'une rivière dépend de tout ce qui se trouve en amont, les rivières sont
calculées dans l'ordre, de l'amont vers l'aval : d'abord les cours d'eau de tête, et l'exutoire en dernier. C'est l'ordre enregistré dans
l'attribut `riverIndex` de l'hydrographie du RFS.

![Les rivières sont routées dans l'ordre, de l'amont vers l'aval](../../static/images/river-routing-network.png)

## Routage de Muskingum

Le RFS utilise la méthode de Muskingum pour calculer la circulation de l'eau dans chaque rivière. Elle estime l'eau qui sort d'une rivière
au pas de temps suivant (\(Q_{t+1}\)) à partir de l'eau qui y entre au pas de temps suivant (\(I_{t+1}\)), de l'eau qui y entre
maintenant (\(I_t\)) et de l'eau qui en sort maintenant (\(Q_t\)) :

$$
Q_{t+1} = c_1 I_{t+1} + c_2 I_t + c_3 Q_t
$$

La somme des coefficients \(c_1\), \(c_2\) et \(c_3\) est égale à 1 : aucune eau n'est donc gagnée ni perdue. Ils sont calculés à
partir de la durée du pas de temps et de deux paramètres définis pour chaque rivière :

- **k** : le temps que met une onde de crue à parcourir la longueur de la rivière. Les rivières plus longues et plus lentes ont des
  valeurs de k plus élevées.
- **x** : dans quelle mesure l'onde de crue s'étale et s'aplatit en se déplaçant, de 0 (aplatissement maximal) à 0,5 (aucun).

Ensemble, ces paramètres retardent l'onde de crue et l'étalent à mesure qu'elle descend vers l'aval. Les valeurs de chaque rivière sont
incluses dans l'hydrographie du RFS sous les attributs `musk_k` et `musk_x`.

![Le routage de Muskingum retarde une onde de crue et aplatit son pic](../../static/images/river-routing-muskingum.png)

## Pas de Temps

river-route route l'eau avec un pas de temps égal ou inférieur à celui des données de ruissellement, afin que chaque valeur de
ruissellement soit routée au moins une fois. Les débits routés sont ensuite moyennés selon les pas de temps des résultats du RFS :

- **Simulation rétrospective** : des débits moyens horaires, qui sont ensuite regroupés en moyennes journalières, mensuelles et annuelles.
- **Prévisions** : des débits moyens sur 3 heures pour chacun des 15 jours de la prévision.

## En Savoir Plus

Pour voir le routage en action, essayez la démonstration interactive de la page [Aperçu du Modèle](../background/model-overview.md). Pour
tous les détails de la méthode, y compris les mathématiques, consultez la [documentation de river-route](https://river-route.code.hales.app/){:target="_blank"} et ses
[dérivations mathématiques](https://river-route.code.hales.app/references/math/){:target="_blank"}.

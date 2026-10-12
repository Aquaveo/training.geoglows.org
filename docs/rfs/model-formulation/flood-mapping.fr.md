# Cartographie des Inondations

!!! warning "Avertissement"
    Le but de cette section sur la formulation du modèle est de fournir un aperçu du RFS, y compris ses entrées et ses sorties. Si votre intérêt principal est d'utiliser les données, vous pouvez passer cette section et aller directement à la section [Données](../data/available-data.md) de notre site.

Les cartes d'inondation du RFS sont créées avec [NenCarta](https://nencarta.readthedocs.io/en/latest/configuration.html), un outil qui automatise la cartographie des inondations fluviales.
NenCarta utilise l'outil [Automated Rating Curve (ARC)](https://automated-rating-curve.readthedocs.io/en/latest/) pour estimer comment le niveau d'eau de chaque rivière varie avec le débit,
ainsi que la méthode FLDPLN pour transformer un débit en une carte de la zone inondée et de sa profondeur.

- **Pourquoi FLDPLN ?** FLDPLN est une version améliorée de la méthode HAND (Height Above Nearest Drainage), couramment utilisée. Ses
  résultats sont stockés sous forme de tables, ce qui rend les cartes d'inondation plus rapides et plus faciles d'accès et d'utilisation.
- **Inondations fluviales uniquement.** Les cartes montrent les inondations dues à la crue et au débordement des rivières. Elles ne montrent
  pas les inondations causées directement par de fortes pluies, comme l'eau qui s'accumule dans les zones basses ou dans les rues des villes.
- **Mises à jour au fil du temps.** Les cartes d'inondation peuvent être mises à jour et améliorées à mesure que de nouvelles données et
  méthodes deviennent disponibles.

Cette page ne présente pas la théorie de ces méthodes. Pour en savoir plus, consultez la [documentation de NenCarta](https://nencarta.readthedocs.io/en/latest/configuration.html) et la
[documentation d'ARC](https://automated-rating-curve.readthedocs.io/en/latest/). Pour voir les cartes d'inondation, utilisez les outils de cartographie des inondations du [Hydroviewer](../web-apps/hydroviewer.md).

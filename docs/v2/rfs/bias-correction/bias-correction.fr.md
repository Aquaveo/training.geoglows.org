# Correction de Biais et SABER

Le RFS présente des biais pouvant limiter sa précision, ce qui a conduit au développement d’une approche de correction de biais. Pour corriger ces biais systématiques aux emplacements instrumentés, nous proposons la méthode de **Quantile-Mapping avec Courbe de Durée de Débit Mensuelle (MFDC-QM)**. Cette méthode cible les biais liés à la variabilité du débit et à la corrélation. Le RFS n’assimile pas les données d’écoulement observées dans son calcul initial. Cependant, la technique de correction de biais permet d’appliquer les données globales localement. Les utilisateurs locaux peuvent ainsi avoir plus de confiance dans leurs données, car ils savent que leurs données observées peuvent être utilisées pour améliorer les données modélisées à leur emplacement.

Après application de la correction de biais, nous avons observé une amélioration significative de la distribution des ratios de biais et de variabilité, avec une légère amélioration des valeurs de corrélation entre les stations, aboutissant à des simulations plus fiables et à une meilleure performance selon l’**indice de Kling-Gupta (KGE)** : biais, variabilité et corrélation.

La présentation suivante explique comment le RFS a été validé et détaille les méthodes de correction de biais.

[GEOGLOWS - Correction de Biais.pdf](https://drive.google.com/file/d/1-GyWh_lY2AjRTXM7aRknqmJiIEh_BqMd/view?usp=sharing)

## Apprentissage interactif – Correction de Biais

Pour approfondir l’analyse de la correction de biais et de l’évaluation des performances, nous avons préparé un notebook interactif Google Colab. Ce notebook fournit un guide étape par étape pour réaliser ces analyses en utilisant des données réelles de la rivière Magdalena à El Banco en Colombie. Il couvre à la fois la correction de biais et l’évaluation des performances, vous permettant d’interagir avec les données et les méthodes présentées dans ce guide : [Bias_Correction_GEOGloWS_ECMWF_Hydrological_Model_Retrospective_Simulation Colab.ipynb](https://colab.research.google.com/drive/19gr9icMEUwZdT6ae6DPG-IwGeWTS3mKk?usp=sharing).

---

## SABER (Stream Analysis for Bias Estimation and Reduction)

La méthode **SABER** est un outil de correction de biais conçu pour de grands modèles hydrologiques comme le RFS, traitant spécifiquement les biais des modèles dans les bassins fluviaux jaugés et non jaugés. SABER utilise les **Courbes de Durée de Débit (FDC)** pour comparer les débits observés avec les valeurs simulées par les modèles hydrologiques, identifiant et corrigeant les biais. Pour les emplacements non jaugés, où les observations directes sont absentes, SABER utilise la **Courbe de Durée de Débit scalaire (SFDC)**.

Contrairement à la correction de biais, qui est effectuée localement par chaque institution, SABER est réalisé par l’équipe RFS et n’est pas appliqué par les utilisateurs finaux. Nous utilisons les données de jauges mises à notre disposition pour améliorer l’ensemble des résultats du modèle. Ce processus est encore en expérimentation et n’est pas appliqué aux données accessibles aux utilisateurs finaux. Nous espérons qu’il sera appliqué dans les futures versions du RFS.

SABER permet d’étendre la correction de biais aux bassins non jaugés en analysant les comportements similaires des bassins versants, sur la base de la proximité spatiale et du regroupement des régimes de débit. Cette méthode est particulièrement utile pour les régions où la rareté des données limite la calibration traditionnelle, comme dans les modèles globaux tels que le RFS, garantissant des prévisions de débit plus précises sur de larges domaines spatiaux.

SABER fonctionne en comparant les données de débits simulés avec les valeurs observées aux sites jaugés pour détecter les biais élevés ou faibles. Il applique des techniques de regroupement par apprentissage automatique pour regrouper les bassins ayant des caractéristiques de débit similaires, permettant d’étendre la correction de biais des bassins jaugés aux bassins non jaugés. Le processus SABER inclut le calcul des SFDC pour différentes probabilités d’excédence, en divisant les débits simulés par les valeurs SFDC correspondantes, même dans les régions affectées par des barrages ou réservoirs.

![saber](../../static/images/saber.png)

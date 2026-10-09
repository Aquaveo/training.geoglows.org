# Correction du Biais sur une Rivière d'Intérêt

Vous pouvez effectuer une correction du biais sur n'importe quelle rivière du RFS, à condition de connaître son LINKNO et de disposer de données observées correspondant à cette rivière. Le moyen le plus simple d'effectuer une correction du biais est d'utiliser la fonction du [package Python] (https://geoglows.readthedocs.io/en/latest/api-documentation/bias.html). Il existe une fonction pour corriger les données historiques et une autre pour corriger les données de prévision.

## Correction du Biais - Exemple de Prévision

Ce notebook Colab propose un guide étape par étape pour effectuer une correction du biais sur les valeurs de prévision du RFS. Il montre comment ajuster les valeurs de débit
prévues à l'aide des observations historiques, ce qui améliore la précision des prévisions et rapproche les données des mesures réelles pour une meilleure
analyse hydrologique :

[Bias_Correction_GEOGloWS_ECMWF_Hydrological_Model_Forecast Colab.ipynb](https://colab.research.google.com/drive/1AWwF60XP_6GKhl1fe9KDhhndT802cHUq?usp=sharing)

## Correction du Biais - Exemple Rétrospectif

Pour approfondir l'analyse de la correction du biais et de l'évaluation des performances, nous avons préparé un notebook Google Colab interactif. Ce notebook
fournit des instructions étape par étape pour réaliser ces analyses à l'aide de données réelles de la rivière Magdalena à El Banco, en Colombie. Il couvre à la fois
la correction du biais et l'évaluation des performances, ce qui vous permet de vous exercer avec les données et les méthodes présentées dans ce
guide : [Bias_Correction_GEOGloWS_ECMWF_Hydrological_Model_Retrospective_Simulation Colab.ipynb](https://colab.research.google.com/drive/19gr9icMEUwZdT6ae6DPG-IwGeWTS3mKk?usp=sharing).

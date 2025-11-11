# Stockage des données principales

## Statut
**Ce que doit contenir :**  
Le statut actuel de la décision (par exemple : Proposée, Acceptée, Rejetée, Supplantée).

Proposée

## Contexte
Le système d'information doit pouvoir stocker les données patient, les prescriptions et les résultats d'analyse de manière à y accéder avec une faible latence et en minimisant les coûts.

## Options Envisagées

1. SAN pour tous les laboratoires et pour le cloud privé
	- Latence très faible pour l'accès aux données 
	- Nécessite un CAPEX très élevé
2. DAS pour les laboratoires et SAN pour le cloud privé
	- Le DAS dans les laboratoires permet de garder de bonnes performances 
3. DAS pour les laboratoires et Stockage objet pour le cloud privé
	- Le stockage objet est plus simple à mettre en place
	- Performances très faibles (de l'ordre de la milliseconde)

## Décision
Nous avons choisi d'utiliser du DAS pour les laboratoires et un SAN pour le cloud privé. En effet, avoir du SAN pour tous les laboratoires résulterait en un CAPEX très élevé. Le stockage objet n'est pas acceptable car la latence est critique pour notre système. Cette solution permet un bon compromis entre performance et coût.


## Conséquences

- Accès aux données avec une très faible latence
- Coûts CAPEX relativement élevés
- Possibilité d'ajouter de nouvelles applications plus facilement à l'avenir.
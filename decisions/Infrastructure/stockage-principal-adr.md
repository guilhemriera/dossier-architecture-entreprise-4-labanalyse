# Stockage des données principales

## Statut

Proposée
## Contexte
Le système d'information doit pouvoir stocker les données patient, les prescriptions et les résultats d'analyse de manière à y accéder avec une faible latence et en minimisant les coûts. Les données seront principalement stockées sur le cloud privé mais les laboratoires doivent posséder une partie de ces données on-premise pour gérer l'activité quotidienne.

## Options Envisagées

1. SAN 
	- Latence très faible pour l'accès aux données 
	- Nécessite un CAPEX très élevé
2. DAS
	- Permet de garder de bonnes performances 
	- Scalabilité limitée
3. Stockage objet 
	- Plus simple à mettre en place
	- Performances très faibles (de l'ordre de 10-100 millisecondes)

## Décision
Nous avons choisi d'utiliser du DAS pour les laboratoires. En effet, avoir du SAN pour tous les laboratoires résulterait en un CAPEX très élevé. Le stockage objet n'est pas acceptable car la latence est critique pour notre système. Cette solution permet un bon compromis entre performance et coût.

## Conséquences

- Accès aux données avec une très faible latence
- Coûts CAPEX relativement élevés
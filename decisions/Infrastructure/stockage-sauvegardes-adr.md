# Stockage des sauvegardes

## Statut

Proposée
## Contexte
Les données principales doivent être sauvegardées pour garantir la continuité des opérations en cas de panne ou d'incident.

## Options Envisagées
1. Stockage sur bande
	- Permet de ne pas changer le système actuel
	- Récupération des données peu efficace
2. Stockage objet sur le cloud
	- Simple à mettre en place surtout si on utilise le même cloud que pour les données principales mais impossibilité de reprendre les activités en cas de panne du cloud
	- Performances faibles
	- Risques de coûts cachés lorsque l'on veut récupérer les données (egress)
3. Stockage sur disque dur on-premise
	- Plus cher et plus énergivore
	- Permet une récupération rapide des données en cas de défaillance du cloud

## Décision
Nous optons pour un stockage on-premise sur disque dur dans le laboratoire central pour les données de sauvegarde. En effet, l'intérêt des sauvegardes est de pouvoir assurer la disponibilité même en cas de panne du stockage principal, cela exclut un stockage sur bande trop lent à récupérer et un stockage objet lui aussi peu rapide.

## Conséquences

- Aménager un espace on-premise pour sauvegardes les données
- Récupération rapide en cas de panne pour assurer la continuité
- Maintenance des disques durs 
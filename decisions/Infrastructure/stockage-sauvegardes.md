# Stockage des sauvegardes

## Statut
**Ce que doit contenir :**  
Le statut actuel de la décision (par exemple : Proposée, Acceptée, Rejetée, Supplantée).

Proposée

## Contexte
Les données principales doivent être sauvegardées pour garantir la continuité des opérations en cas de panne ou d'incident.

## Options Envisagées
1. Stockage sur bande
Permet de ne pas changer le système actuel mais la récupération des données ne sera pas efficace
2. Stockage objet sur le cloud
Simple à mettre en place surtout si on utilise le même cloud que pour les données principales mais impossibilité de reprendre les activités en cas de panne du cloud
Le stockage objet n'est pas très rapide
Risques de coûts cachés lorsque l'on veut récupérer les données
3. Stockage sur disque dur on-premise
Plus cher et plus énergivore mais permet une récupération rapide des données en cas de défaillance du cloud

## Décision
Nous optons pour un stockage on-premise sur disque dur dans le laboratoire central pour les données de sauvegarde. En effet, l'intérêt des sauvegardes est de pouvoir assurer la disponibilité même en cas de panne du stockage principal, cela exclut un stockage sur bande trop lent à récupérer et un stockage objet lui aussi peu rapide.

## Conséquences

- Aménager un espace on-premise pour sauvegardes les données
- Récupération rapide en cas de panne pour assurer la continuité
- Maintenance des disques durs 
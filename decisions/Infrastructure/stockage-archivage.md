# Archivage

## Statut
**Ce que doit contenir :**  
Le statut actuel de la décision (par exemple : Proposée, Acceptée, Rejetée, Supplantée).

Proposée

## Contexte
Un système d'archivage doit être mis en place pour avoir accès aux données inactives à long terme pour des raisons juridiques ou analytiques.

## Options Envisagées
1. Stockage sur bande
	- Permet de recycler le système utilisé pour les sauvegardes donc facile à mettre en oeuvre 
	- Les données ne pourront pas être récupérées instantanément
	- Données hors-ligne (surface d'attaque moins élevée)
2. Stockage objet sur le cloud
	- Simple à mettre en place surtout si on utilise le même cloud que pour les données principales
	- Risques de coûts cachés lorsque l'on veut récupérer les données
3. Stockage sur disque dur on-premise
	- Récupération rapide des données 
	- Cher à mettre en place
	- Données hors-ligne

## Décision
Nous optons pour un stockage sur bande on-premise en réutilisant le système existant. Il n'est pas nécessaire d'avoir une récupération rapide pour les données archivées donc il vaut mieux choisir la solution qui minimise les coûts.

## Conséquences

- Facilité de mise en oeuvre et données hors-ligne moins accessibles aux pirates
- Très peu de coûts
- Récupération potentiellement lente
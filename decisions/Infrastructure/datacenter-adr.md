# Datacenter

## Statut

Proposée
## Contexte
Le système d'information doit posséder une infrastructure physique capable de stocker les données, avoir accès aux serveurs et d'héberger les applications nécessaires au bon fonctionnement des activités.

## Options Envisagées
1. Continuer à utiliser un datacenter on-premise
	- Pas de changement à mettre en place
	- Serveurs vieillissants et non virtualisés (complexes à gérer et à maintenir)
	- Contrôle total
2. Construire un datacenter on-premise plus adapaté
	- Coûts initiaux élevés
	- Contrôle total
	- Maintenance et sécurité à la charge de l'entreprise
3. Cloud privé
	- Grande flexibilité et scalabilité simplifiée
	- Plus grande résilience
	- Gestion, configuration et sécurité déléguée à un tiers spécialisé
4. Cloud en colocation
	- Coûts moins élevés que pour un cloud privé
	- Vecteur d'attaque plus grand car connecté à Internet et partagé avec d'autres entreprises
## Décision
Nous choisissons d'utiliser un cloud privé car LabAnalyse n'a pas les compétences en interne pour maintenir et gérer un datacenter on-premise de manière efficace. De plus, la croissance externe sera facilitée car le cloud est par nature très évolutif et scalable. Etant donné que les données médicales sont confidentielles, il est plus judicieux de ne pas utiliser un cloud en colocation même si les coûts sont plus élevés.

## Conséquences

- Scalabilité facile
- Coûts élevés
- Sécurité assurée
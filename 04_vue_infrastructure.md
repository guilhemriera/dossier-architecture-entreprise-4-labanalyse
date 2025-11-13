# 4. Vue infrastructure

## 4.1 Architecture technique cible

L'architecture technique actuelle on-premise repose sur seulement 4 serveurs physiques présents dans le laboratoire central, vieillissants et non virtualisés. Pour réduire les risques opérationnels et assurer la croissance externe, une autre architecture s'impose. 
### 4.1.1 Environnements et zones techniques

Environnements :
- Production
- Pré-production
- Sandbox technique (pour les tests d'intégrations)
- Pas besoin d'environnement de développement car les solutions ne sont pas développées par l'entreprise. 

Séparation logique avec des VPC et des ACL dinstincts

Zones : 
- DMZ
- Zone applicative
- Zone données (bases, caches)

### 4.1.2 Hébergement et topologie

Le système utilisera un cloud privé SaaS pour la gestion de ses opérations. Ce datacenter sera facilement scalable avec le volume croissant des opérations et les tâches de maintenance seront déléguées au prestataire étant donné le manque d'expertise de la DSI. Ce cloud privé sera préférentiellement choisi dans la région Auvergne-Rhônes-Alpes pour assurer une bonne connexion avec les laboratoires. De plus, il sera intéressant de demander un service iPaaS pour éviter une organisation en silos de l'organisation.

Les progiciels et toutes les applications du SI seront hébergés sur le cloud SaaS.

Les laboratoires de proximité (bords) utiliseront une petite infrastructure on-premise pour gérer les opérations quotidiennes qui seront synchronisées de manière asynchrone avec les bases de données centrales du cloud privé.

### 4.1.3 Réseaux et interconnexions

Le laboratoire central communiquera par une connexion internet sur fibre avec les serveurs du cloud privé. De même, les laboratoires de proximité accéderont aux données patients et aux prescriptions directement avec le cloud privé, sans passer par le laboratoire central.

Chaque laboratoire disposera d'un réseau VLAN dédié. Un SD-WAN est formé par la connexion de chaque laboratoire avec le cloud privé. Les laboratoires de proximité ne devraient pas être en mesure de communiquer directement les uns avec les autres.

De même, les tablettes mobiles peuvent communiquer uniquement par Internet au travers d'un VPN avec le laboratoire de proximité auquel il est attaché.

Une connexion VPN de secours est mise en place entre les laboratoires de proximité et le laboratoire central.

## 4.2 Composants d’infrastructure

### 4.2.1 Serveurs et virtualisation

Les laboratoires utiliseront une architecture hyperconvergée pour faciliter la gestion des équipements. En effet, utiliser une architecture traditionnelle nécessiterait des compétences techniques poussées pour choisir et configurer les meilleurs équipements, qui dépassent les capacités de la DSI. Une architecture convergée est plus simple mais représente des coûts initiaux très élevés. 

Pour éviter une sous-utilisation des ressources, les systèmes d'exploitation seront déployés avec une infrastucture virtualisé. En effet, la conteneurisation peut rapidement devenir compliquée à orchestrer.

### 4.2.2 Stockage et sauvegarde

DAS dans chacun des laboratoires de proximité pour assurer un accès rapide aux données locales sans avoir un CAPEX trop élevé.  Les données situées dans le cloud privé seront accessibles grâce au réseau datacenter.

Chaque laboratoire dispose donc d'une base de données relationnelle utilisée pour la prise de rendez-vous et la gestion des clients dudit laboratoire. Ces bases de données sont synchronisées quotidiennement avec les bases de données du cloud privé.

Les sauvegardes seront stockées sur disque dur on-premise dans le laboratoire central tandis que le système de bande sera réutilisé pour l'archivage des données.

### 4.2.3 Supervision et exploitation

Un système simple de dashboards qui affiche en continu les métriques des serveurs et des équipements du cloud pour permettre aux techniciens IT de LabAnalyse de superviser le bon déroulement des activités. 

Centralisation des logs avec un SIEM et système de corrélation d'alertes

## 4.3 Continuité et disponibilité

### 4.3.1 Plan de continuité d’activité (PCA)

Les sauvegardes seront stockées sur site en cas d'incident majeur au niveau du cloud privé. Ainsi, les laboratoires de proximité pourront utiliser une connexion de secours par VPN au laboratoire central pour continuer l'activité en attendant la reprise du cloud.

De même, les laboratoires de proximité seront équipés d'une base de données suffisante pour gérer l'activité quotidienne (voire sur 2 jours) en cas de problème de connexion avec le cloud et le laboratoire central. Une synchronisation sera effectuée chaque nuit avec le cloud pour assurer que les données sont à jour.

Une bascule réseau automatique pour basculer sur de la 4G-5G en cas de problèmes

Load balancers pour utiliser le système de redondance en cas de panne d'un des équipements.

### 4.3.2 Plan de reprise d’activité (PRA)

Stratégie actif/passif avec une réplication synchrone pour les données critiques mais asynchrone de manière générale

### 4.3.3 Niveaux de service

Le système doit garantir une haute disponibilité de 99,9% soit 8 heures d'indisponibilité maximum par an.

Délai de synchronisation en sortie du mode dégradé en moins de 10 minutes

Accès aux portails patients et médecins < 1s

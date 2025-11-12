# 4. Vue infrastructure

## 4.1 Architecture technique cible
Présente la structure technique du système : datacenters, cloud, réseaux, serveurs, stockage et sécurité périmétrique.

L'architecture technique actuelle on-premise repose sur seulement 4 serveurs physiques présents dans le laboratoire central, vieillissants et non virtualisés. Pour réduire les risques opérationnels et assurer la croissance externe, une autre architecture s'impose. 

### 4.1.1 Environnements et zones techniques
Décrit les environnements (développement, recette, production) et leurs séparations logiques et physiques.

### 4.1.2 Hébergement et topologie
Expose la répartition des composants entre cloud public, privé et on-premise, ainsi que la localisation géographique des ressources.

Le système utilisera un cloud privé pour la gestion de ses opérations. Ce datacenter sera facilement scalable avec le volume croissant des opérations et les tâches de maintenance seront déléguées au prestataire étant donné le manque d'expertise de la DSI. Ce cloud privé sera préférentiellement choisi dans la région Auvergne-Rhônes-Alpes pour assurer une bonne connexion avec les laboratoires.


### 4.1.3 Réseaux et interconnexions
Détaille les architectures réseau (LAN, WAN, VPN, SD-WAN) et les principes de segmentation et redondance.

Le laboratoire central communiquera par une connexion internet sur fibre avec les serveurs du cloud privé. De même, les laboratoires de proximité accéderont aux donnés patients et aux prescriptions directement avec le cloud privé, sans passer par le laboratoire central.

Chaque laboratoire disposera d'un réseau LAN dans lequel mais et. Un WAN est formé par la connexion de chaque laboratoire avec le cloud privé. Les laboratoires de proximité ne devraient pas être en mesure de communiquer directement les uns avec les autres.

De même, les tablettes mobiles peuvent communiquer uniquement par Internet au travers d'un VPN avec le laboratoire de proximité auquel il est attaché.

Une connexion VPN de secours est mise en place entre les laboratoires de proximité et le laboratoire central.


## 4.2 Composants d’infrastructure
Liste les principaux éléments techniques qui supportent le fonctionnement applicatif.

### 4.2.1 Serveurs et virtualisation
Décrit les types de serveurs, hyperviseurs, clusters et pools de ressources utilisés.

Le cloud privé utilisera une architecture hyperconvergée pour faciliter la gestion des équipements. En effet, utiliser une architecture traditionnelle nécessiterait des compétences techniques poussées pour choisir les meilleurs équipements et pour les configurer, qui dépassent les capacités de la DSI. Une architecture convergée est plus simple mais représente des coûts initiaux très élevés.

Pour éviter une sous-utilisation des ressources, les systèmes d'exploitation seront déployés avec une infrastructure virtualisée. La conteneurisation peut rapidement devenir compliquée.

### 4.2.2 Stockage et sauvegarde
Présente les solutions de stockage (SAN, NAS, objet), les stratégies de sauvegarde, restauration et archivage.

Direct Attached Stockage dans chacun des laboratoires de proximité pour assurer un accès rapide aux données locales sans avoir un CAPEX trop élevé.  Les données situées dans le cloud privé utiliseront un Storage Area Network pour minimiser la latence.

Chaque laboratoire dispose donc d'une base de données relationnelle qui est 

Les sauvegardes seront stockées sur disque dur on-premise dans le laboratoire central tandis que le système de bande sera réutilisé pour l'archivage des données.

### 4.2.3 Supervision et exploitation
Explique les outils et processus de monitoring, d’alerting et de pilotage des infrastructures.

## 4.3 Continuité et disponibilité
Définit les mesures pour garantir la continuité de service et la reprise après sinistre.

### 4.3.1 Plan de continuité d’activité (PCA)
Décrit les dispositifs permettant d’assurer la continuité des activités en cas d’incident majeur.

Le coffre-fort pour les sauvegardes continuera à être sur site en cas d'incident majeur au niveau du cloud privé. Ainsi, les laboratoires de proximité pourront utiliser une connexion de secours par VPN au laboratoire central pour continuer l'activité en attendant la reprise du cloud.

De même, les laboratoires de proximité seront équipés d'une base de données suffisante pour gérer l'activité quotidienne (voire sur 2 jours) en cas de problème de connexion avec le cloud et le laboratoire central. Une synchronisation sera effectuée chaque nuit avec le cloud pour assurer que les données sont à jour.

### 4.3.2 Plan de reprise d’activité (PRA)
Spécifie les mécanismes de redémarrage du SI après un sinistre (sites de secours, réplication, orchestration).

### 4.3.3 Niveaux de service
Présente les engagements de service (SLA) et les seuils cibles de disponibilité.

Le système doit garantir une haute disponibilité de 99,9% soit 8 heures d'indisponibilité maximum par an.

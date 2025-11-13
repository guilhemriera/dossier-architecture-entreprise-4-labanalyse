# 1. Introduction et contexte

## 1.1 Objectif du document
Ce document décrit la vision d’architecture du système d’information, son périmètre, ses objectifs et les choix structurants. Il constitue la référence commune entre équipes métiers, techniques et sécurité.

## 1.2 Contexte général
Le contexte présente l’environnement dans lequel le projet s’inscrit, les enjeux métiers, les contraintes de l’existant et les besoins de transformation du système d’information.

### 1.2.1 Contexte métier
**LabAnalyse** est un réseau de laboratoires d'analyses médicales spécialisé dans les analyses de routine et spécialisées, couvrant la biochimie, l'immunologie, la bactériologie et la biologie moléculaire. L'entreprise exploite actuellement 42 sites et prévoit d'étendre son réseau à 57 laboratoires dans les 24 prochains mois.

Le secteur de l'analyse médicale fait face à des enjeux majeurs :
- **Croissance** : extension géographique et montée en charge (3,4 millions d'analyses par an visées)
- **Efficacité** : réduction des délais de rendu des résultats
- **Conformité** : respect des exigences réglementaires (RGPD, certification HDS, accréditation des laboratoires)
- **Innovation** : dématérialisation des processus et intégration d'outils d'intelligence artificielle

### 1.2.2 Contexte SI existant
L'architecture technique actuelle repose sur 4 serveurs physiques vieillissants et non virtualisés situés dans le laboratoire central. Cette infrastructure présente plusieurs limites :

**Limites fonctionnelles :**
- Accès limité depuis les 57 sites distants

**Limites techniques :**
- Infrastructure non scalable
- Risque de défaillance élevé (équipements vieillissants)
- Performances dégradées avec la montée en charge
- Absence de redondance et de plan de continuité

**Raisons de la refonte :**
- Soutenir la croissance externe (15 nouveaux sites)
- Garantir une disponibilité de 99,8% 
- Moderniser les processus métier
- Réduire les risques opérationnels

### 1.2.3 Perspectives d'évolution
Les évolutions prises en compte dans la cible architecturale incluent :

**Évolutions réglementaires :**
- Renforcement des exigences de cybersécurité (directive NIS2)
- Application du RGPD aux données de santé
- Évolution des standards d'accréditation des laboratoires

**Obsolescence technique :**
- Migration vers le cloud pour remplacer l'infrastructure vieillissante
- Modernisation des interfaces avec les automates
- Mise en place d'un mode dégradé hors-ligne

**Nouveaux besoins métiers :**
- Prélèvements à domicile avec tablettes mobiles
- Portail médecin pour prescription et suivi
- Intégration d'outils d'intelligence artificielle pour l'analyse

## 1.3 Objectifs et contraintes
Ce chapitre regroupe les objectifs attendus du projet et les contraintes susceptibles d’influencer les choix d’architecture.

### 1.3.1 Objectifs fonctionnels
Les objectifs fonctionnels du projet visent à transformer les processus métier pour :

**Fonctionnement Déconnecté du centre :**
- Déployer un système de prelèvement à domicile avec tablettes mobiles
- Assurer un mode dégradé hors-ligne pour les laboratoires de proximité

**Conformité et sécurité :**
- Renforcer la conformité aux exigences réglementaires (RGPD, HDS, accréditation)
- Assurer la traçabilité des actions et la signature électronique des résultats
- Mettre en place des alertes automatiques pour les résultats critiques
- Garantir l'archivage réglementaire des données sur 20 ans

**Exploitation optimisée de la donnée :**
- Centraliser les données patients et analyses dans le cloud
- Faciliter le pilotage via des tableaux de bord opérationnels
- Préparer l'intégration d'outils d'intelligence artificielle pour l'aide au diagnostic

### 1.3.2 Objectifs techniques
Les ambitions techniques du projet incluent :


**Performance et scalabilité :**
- Support de 57 sites distants avec performances acceptables
- Gestion de 500 utilisateurs interne, 450 patients et 3,4 millions d'analyses par an
- Architecture cloud scalable automatiquement

**Résilience et disponibilité :**
- Haute disponibilité de 99,9% (< 8h d'arrêt par an)
- Mode dégradé hors-ligne avec synchronisation automatique sous 10 minutes
- Plan de continuité et de reprise d'activité

**Cybersécurité :**
- Chiffrement des communications (TLS 1.3) et données au repos (AES-256)
- Authentification forte multi-facteurs (MFA)
- Supervision de sécurité avec SIEM et corrélation d'alertes
- Hébergement HDS certifié pour les données de santé

**Intégration fluide :**
- Migration progressive depuis l'existant
- Coexistence cloud/sites locaux en mode hybride
- Conservation des interfaces utilisateur familières
- Formation minimale requise pour les équipes

### 1.3.3 Contraintes
Les contraintes identifiées qui influencent les choix d'architecture sont :

**Contraintes légales et réglementaires :**
- **RGPD** : protection des données personnelles de santé, durées de conservation, droits des personnes
- **Certification HDS** obligatoire pour l'hébergement cloud des données de santé
- **Réglementation biologie médicale** : obligations d'accréditation, conservation des comptes rendus, capacité d'audit
- **PCI-DSS** pour la gestion sécurisée des paiements
- **Directive NIS2** pour les opérateurs de services essentiels

**Contraintes budgétaires :**
- Maîtrise des coûts d'infrastructure cloud (optimisation des ressources)
- ROI attendu sur la réduction des coûts opérationnels
- Budget limité pour la formation des équipes

**Contraintes de délais :**
- Mise en service des 15 nouveaux sites dans les 24 mois
- Migration progressive pour éviter l'interruption de service
- Formation des équipes en parallèle du déploiement

**Contraintes de ressources humaines :**
- DSI limitée à 5 personnes (expertise technique restreinte)
- 380 utilisateurs métier à former sur les nouveaux outils
- Disponibilité limitée des biologistes pour la validation des règles métier

**Contraintes techniques et logicielles :**
- Interopérabilité avec les automates existants multi-constructeurs
- Conservation des données existantes (migration sans perte)
- Qualité de service réseau variable selon les sites distants
- Dépendance aux progiciels SIL existants (personnalisation limitée)

**Contraintes géographiques :**
- 57 sites répartis géographiquement (latence réseau)
- Hébergement cloud obligatoirement en France (souveraineté)
- Qualité de connexion variable selon les sites (nécessité du mode dégradé)





# 3. Vue applicative

## 3.1 Exigences non fonctionnelles
Regroupe les exigences applicatives en termes de performance, sécurité, disponibilité et observabilité.

### 3.1.1 Performance et scalabilité
Spécifie les objectifs de performance, de montée en charge et de temps de réponse par typologie de traitement.

### 3.1.2 Résilience et tolérance aux pannes
Décrit les mécanismes de reprise automatique, redondance et déploiement sans interruption.

## 3.2 Architecture fonctionnelle applicative
Décrit la structure logique des applications, leurs rôles et leurs interactions pour supporter les processus métier.

### 3.2.1 Cartographie applicative
Présente la cartographie des applications principales et satellites. Chaque application est positionnée selon son rôle : front-office, back-office, référentiel, orchestration, intégration.

### 3.2.2 Domaines fonctionnels
Regroupe les applications par domaines en référence avec la vue métier (ex. CRM, facturation, gestion des stocks). Explique leurs interactions et les principes de découplage.

### 3.2.3 Évolutions cibles
Expose la vision cible : consolidation, urbanisation, ajout de fonctionnalité, modernisation technologique ou migration cloud.

## 3.3 Flux et intégration
Décrit les échanges de données entre applications et les mécanismes utilisés pour garantir cohérence et performance.

>**Illuster au moins un diagramme de séquence pour un flux dans ce chapitre**

### 3.3.1 Typologie des flux
Classe les échanges selon leur nature : synchrone (API REST, SOAP), asynchrone (messagerie, événements), ou batch (ETL).

### 3.3.2 Bus d’entreprise et interfaçage
Présente le(s) rôle(s) du bus d'entreprise mise en oeuvre dans le système d'information et le(s) besoin(s) qu'il cherche à couvrir par rapport au context applicatif de l'entreprise.

### 3.3.3 Gestion de la donnée
Décrit les stratégies de partage, duplication et gouvernance de la donnée. Proproser un schema de modèle de données "simplifié". Pour les objets importants de la solution applicative, identifier les systèmes contenant ces données en référence.

## 3.4 Architecture applicative
Définit les principes d’organisation des applications : couches, composants, frameworks, et interactions.

>**Cette section doit contenir un schema d'architecture applicatif de la solution** 

### 3.4.1 Principes d’architecture
Expose les choix structurants : séparation des couches (présentation, métier, données), modularité, réutilisabilité et maintenabilité.

### 3.4.2 Patterns techniques
Précise les patterns utilisés : MVC, CQRS, Event Sourcing, API Gateway, façade de service, microservices...

### 3.4.3 Technologies et langages
Liste les technologies retenues (langages, frameworks, middlewares).

### 3.5 Observabilité et supervision
Présente les solutions de journalisation, de métriques et de traçabilité applicative.

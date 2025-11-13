# 3. Vue applicative

## 3.1 Exigences non fonctionnelles
*Regroupe les exigences applicatives en termes de performance, sécurité, disponibilité et observabilité.*

### 3.1.1 Performance et scalabilité
*Spécifie les objectifs de performance, de montée en charge et de temps de réponse par typologie de traitement.*

#### 3.1.1.1 Exigence fournie
1. Haute disponibilité : Le SIL étant critique pour l'activité quotidienne (enregistrement patients, accès aux dossiers, validation de résultats), le système doit garantir une disponibilité de 99,9% soit maximum 8 heures d'indisponibilité par an, avec capacité de bascule rapide en cas de défaillance. 



#### 3.1.1.2 Exigences supposées
1. Charge personnel : 500 utilisateur (380 membre du personnel actuel + augmentation lié à la création de 15 sites estimée à partir des 360 employés de laboratoire).
2. Charge sites : 57 sites distants
3. Charge patients : 20 000 (5% du nombre de patients totaux (450 000 patients)).
4. Charge client (potentielle future patient) : 90 000 (20% du nombre de patients totaux).
5. Charge analyses : 2.5 millions d'analyses par an. (comme pour les sites et le personnelle, on tablera sur une augmentation de 35%. Donc on visera 3.4 millions d'analyses par an).

### 3.1.2 Résilience et tolérance aux pannes
*Décrit les mécanismes de reprise automatique, redondance et déploiement sans interruption.*

#### 3.1.2.1 Exigence fournie
2. Protection et récupération des données : Les données médicales doivent être protégées contre toute perte avec des sauvegardes.


## 3.2 Architecture fonctionnelle applicative
*Décrit la structure logique des applications, leurs rôles et leurs interactions pour supporter les processus métier.*

### 3.2.1 Cartographie applicative
*Présente la cartographie des applications principales et satellites. Chaque application est positionnée selon son rôle : front-office, back-office, référentiel, orchestration, intégration.*

**SIL (Système d'Information de Laboratoire) :**

La majorité des application sont regroupé dans un progiciel de gestion de laboratoire avec les roles suivants :
- Back-office : Gestion des dossiers patients, enregistrement des precscriptions, traçabilité des échantillons, validation des résultats par les biologistes, édition des comptes rendus et facturation.
- Référentiel : Base de données patients, base de données analyses, base de données prescriptions
- Orchestration : interfaçages avec les automates d'analyse.
- Intégration : API REST avec le portail patient et les clients web des laboratoires de proximité.


**Clients web laboratoires de proximités :**

Les Laboratoires de proximité utilisent une application web pour s'interfacé avec le SIL. 
Rôle :
- Back-office : Enregistrement des patients, consultation des résultats, gestion des rendez-vous.
- Intégration : API REST avec le SIL


**Portail patient :**

Les patients utilisent un portail web pour consulter leurs résultats et prendre des rendez-vous. 
Rôle :
- Front-office : Portail patient
- Référentiel : Base de données patients, base de données analyses, base de données prescriptions
- Intégration : API REST avec le SIL


### 3.2.2 Domaines fonctionnels
*Regroupe les applications par domaines en référence avec la vue métier (ex. CRM, facturation, gestion des stocks). Explique leurs interactions et les principes de découplage.*


Ci-dessous les domaines fonctionnels en lien avec les processus métier identifiés dans la vue métier :
1. prise de RDV et accueil
2. prélèvements (sur site et à domicile, dont en mode dégradé)
3. acheminement et traçabilité des échantillons
4. analyses (avec interface pour automatisation)
5. contrôle des résultats (technique puis biologique) et compte rendu
6. diffusion des résultats (via portails patients et médecin)
7. facturation
8. gestion qualité et conformité 


En ce sens, il est adapté de faire le regroupement suivant des domaines fonctionnels :
prise de RDV et accueil : SIL, Application web laboratoires de proximité, Portail patient
prélèvements : SIL, Application web laboratoires de proximité
acheminement et traçabilité des échantillons : SIL
analyses : SIL
contrôle des résultats et compte rendu : SIL
diffusion des résultats : SIL, Portail patient
facturation : SIL
gestion qualité et conformité : SIL


### 3.2.3 Évolutions cibles
*Expose la vision cible : consolidation, urbanisation, ajout de fonctionnalité, modernisation technologique ou migration cloud.*
**Application tablette pour interventions à domicile :**

Un projet d'intervention à domicile est envisagé. Dans celui-ci, les infirmiers seront équipés de tablettes avec une application dédiée. L'application permettra d'avoir accès aux dossiers patients, d'enregistrer les prélèvements et d'éditér les étiquettes. Cela ce fera avec une connexion incertaine avec le SIL.
Rôle :
- Back-office : Enregistrement des patients, gestion des prélèvements, édition des étiquettes.
- Référentiel : Base de données patients, base de données analyses, base de données prescriptions (stockage local en mode dégradé)
- Intégration : API REST avec le SIL (synchronisation asynchrone en mode dégradé)


**Portail d'accès pour médecins prescripteurs :**
Un portail web dédié aux médecins prescripteurs est envisagé pour faciliter la prescription et le suivi des patients.
Rôle :
- Front-office : Portail médecin
- Référentiel : Base de données patients, base de données analyses, base de données prescriptions
- Intégration : API REST avec le SIL

**AI d'analyse de résultats :**
Un système d'intelligence artificielle pour aider à l'analyse des résultats est envisagé. Il analysera les résultats des analyses et proposera des interprétations aux biologistes.
Rôle :

- Back-office : Analyse des résultats, génération d'interprétations.
- Intégration : API REST avec le SIL


**Cloud hébergé :**
Pour répondre aux egixences de scalabilité et de disponibilité, le SIL sera migré vers une solution cloud hébergée. Cela permettra une meilleure gestion des pics de charge et une haute disponibilité.

## 3.3 Flux et intégration
*Décrit les échanges de données entre applications et les mécanismes utilisés pour garantir cohérence et performance.*

**Flux principaux :**
- **Patient <--> Portail patient** : requette d'authentification
- **Portail patient <--> SIL** : API REST pour la verfication des identifiants, la consultation des résultats et la prise de rendez-vous.
- **Clients web laboratoires de proximités <--> SIL** : API REST pour l'enregistrement des patients, la consultation des résultats et la gestion des rendez-vous.
- **Application tablette <--> SIL** : Synchronisation asynchrone en mode dégradé via API REST.
- **Medecins prescripteurs <--> Portail médecin** : Authentification
- **Portail médecin <--> SIL** : API REST pour la prescription et le suivi des patients.
- **AI d'analyse de résultats <--> SIL** : API REST pour l'envoi des résultats et la réception des interprétations.
- **Automates d'analyse <--> SIL** : Interface dédiée pour l'automatisation des analyses.
- **SIL <--> Base de données** : Accès direct pour la gestion des données patients, analyses, prescriptions.

>***Illuster au moins un diagramme de séquence pour un flux dans ce chapitre***

![diagramme de séquence pour le flux pour le flux correspondant à l'accèss des résultats d'analyse par un patient via le portail patient](diagrammes\finaux\utilisation_portail_patient_pour_acces_resultat.svg)




### 3.3.1 Typologie des flux
*Classe les échanges selon leur nature : synchrone (API REST, SOAP), asynchrone (messagerie, événements), ou batch (ETL).*

- **Patient <--> Portail patient** : Synchrone
- **Portail patient <--> SIL** : Synchrone
- **Clients web laboratoires de proximités <--> SIL** : Synchrone 
- **Application tablette <--> SIL** : Synchrone (mode connecté), Asynchrone (mode dégradé)
- **Medecins prescripteurs <--> Portail médecin** : Synchrone
- **Portail médecin <--> SIL** : Synchrone
- **AI d'analyse de résultats <--> SIL** : Synchrone
- **Automates d'analyse <--> SIL** : Asynchrone
- **SIL <--> Base de données** : Synchrone

### 3.3.2 Bus d’entreprise et interfaçage
*Présente le(s) rôle(s) du bus d'entreprise mise en oeuvre dans le système d'information et le(s) besoin(s) qu'il cherche à couvrir par rapport au context applicatif de l'entreprise.*

Dans ce cadre, l'ESB a pour rôle entre le SIL et les autres applications (portail patient, clients web laboratoires de proximités, application tablette, portail médecin, AI d'analyse de résultats, automates d'analyse) et de permetre un interfaçage standardisé et centralisé. Il est d'autant plus adapté au vu du nombre de site distants et de la sensibilité des données échangées.


### 3.3.3 Gestion de la donnée
*Décrit les stratégies de partage, duplication et gouvernance de la donnée. Proproser un schema de modèle de données "simplifié". Pour les objets importants de la solution applicative, identifier les systèmes contenant ces données en référence.*

La stragégie de partage repose sur une structure centralisée autour de la basse donnée princiale du SIL. A cette base de données s'ajoute une base de données de sauvegarde et d'archivage. 
Enfin, de manière plus temporaire, pour pouvoir fonctionné en mode dégradé, chaque laboratoire de proximité et chaque tablette d'intervention à domicile dispose d'une base de données locale qui est synchronisée 3 fois par jours avec la base de données principale du SIL. Celle-ci ne stocke que les rendez-vous et les dossiers patients sur 16h (de manière à suporté une indisponibilité avec le SIL de 8h) (à l'échel du site ou de la tourné de l'infermier).

## 3.4 Architecture applicative
*Définit les principes d’organisation des applications : couches, composants, frameworks, et interactions.*

>**Cette section doit contenir un schema d'architecture applicatif de la solution** 

### 3.4.1 Principes d’architecture
*Expose les choix structurants : séparation des couches (présentation, métier, données), modularité, réutilisabilité et maintenabilité.*

Les couches de l'architecture applicative sont les suivantes :
1. Couche de présentation : Portail patient, Portail médecin, Clients web laboratoires de proximités, Application tablette
2. Couche métier : IA d'analyse, SIL (gestion des dossiers patients, enregistrement des prescriptions, traçabilité des échantillons, validation des résultats par les biologistes, édition des comptes rendus, facturation, interfaçages avec les automates d'analyse)
3. Couche données : Base de données principale du SIL, base de données de sauvegarde et d'archivage, bases de données locales des laboratoires de proximité et des tablettes d'intervention à domicile.

Cette architecture est centralisé sur le SIL gérant la majorité des fonctionnalités métier et étant adapté à une équipe SI réduite. De plus, de part la capacité d'upscalling du cloud, le SIL pourra gérer les pics de charge lors des périodes d'activité intense et l'expention de **LabAnalyse** à l'avenir.

Cette architecture permet de ne pas trop souffrir d'un disfonctionnement du SIL grâce aux bases de données locales des laboratoires de proximité et des tablettes d'intervention à domicile. De ce fait, le SI sera robuste à une perte du SIL ou de la connexion avec celui-ci dans la limite de la robustèce du cloud.

### 3.4.2 Patterns techniques
*Précise les patterns utilisés : MVC, CQRS, Event Sourcing, API Gateway, façade de service, microservices...*

L'architecture applicative repose sur les patterns suivants :
- **MVC (Model-View-Controller)** : Utilisé dans les applications web (Portail patient, Portail médecin, Clients web laboratoires de proximités, Application tablette) pour séparer la logique de présentation, la logique métier et la gestion des données.
- **API Gateway** : Utilisé pour centraliser les appels aux différentes API REST entre le SIL et les autres applications, assurant ainsi une gestion cohérente des accès, de la sécurité et du routage des requêtes.

### 3.4.3 Technologies et langages
*Liste les technologies retenues (langages, frameworks, middlewares).*

Les technologies et langages retenus pour l'architecture applicative sont les suivants :
- **Langages** : Java (pour le SIL), JavaScript (pour les applications web)
- **Frameworks** : Spring Boot (pour le SIL), React (pour les applications web)
- **Middlewares** : API Gateway (pour la gestion des API REST entre le SIL et les autres applications)

### 3.5 Observabilité et supervision
*Présente les solutions de journalisation, de métriques et de traçabilité applicative.*

La supervision applicative repose sur les solutions suivantes :
- **Journalisation** : Utilisation de frameworks de logging (comme Log4j pour Java) pour enregistrer les événements applicatifs, les erreurs et les transactions dans des fichiers de log centralisés.
- **Métriques** : Mise en place de systèmes de monitoring (comme Prometheus et Grafana) pour collecter et visualiser les métriques de performance des applications, telles que les temps de réponse, les taux d'erreur et l'utilisation des ressources.
- **Traçabilité applicative** : Utilisation de solutions de traçabilité distribuée (comme Jaeger) pour suivre les requêtes à travers les différentes couches et services de l'architecture applicative, facilitant ainsi le diagnostic des problèmes et l'optimisation des performances.

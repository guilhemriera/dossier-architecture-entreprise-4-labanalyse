# 2. Vue métier

## 2.1 Contexte fonctionnel

*Présente le domaine métier concerné par le projet, les activités principales impactées et les enjeux opérationnels associés à la transformation du système d’information.*

### 2.1.1 Domaine d’activité

*Décrit les missions, produits ou services de l’entreprise dans le périmètre couvert, ainsi que les fonctions opérationnelles supportées par la solution.*

**LabAnalyse** est un réseau de laboratoires d'analyses médicales réalisant à la fois des analyses de routine et spécialisées, que ce soit en biochimie immunologie, bactériologie ou biologie moléculaire. 

La solution cible supporte l'accueil et la prise de RDV, la traçabilité, le pilotage et validation des analyses, et l'envoi sécurisé des résultats. 

### 2.1.2 Objectifs opérationnels

*Explique les gains attendus dans les processus métiers (simplification, automatisation, rapidité, traçabilité, satisfaction client, conformité réglementaire).*

- réduire les délais de rendu
- accroître la remise des résultats en dématérialisé
- renforcer conformité et traçabilité
- soutenir la montée en charge
- assurer 99.9% de disponibilité

## 2.2 Processus métier

*Expose les processus cibles que la solution doit supporter, sous forme de flux métier, d’activités et d’interactions entre acteurs.*



### 2.2.1 Cartographie des processus

*Présente la vision globale des processus métier concernés et leurs interconnexions. Met en évidence les dépendances avec d’autres domaines fonctionnels.*

Dans l'ordre chronologique du processus:

1. prise de RDV et accueil
2. prélèvements (sur site et à domicile, dont en mode dégradé)
3. acheminement et traçabilité des échantillons
4. analyses (avec interface pour automatisation)
5. contrôle des résultats (technique puis biologique) et compte rendu
6. diffusion des résultats (via portails patients et médecin)
7. facturation
8. gestion qualité et conformité 

Dépendances clés: 

- SI médecins / hôpitaux
- hébergeur (hébergement cloud)
- tiers payant, mutuelles, etc.
- routage numérique
- gestion sécurisée de l'identité (pour éviter les erreurs d'attribution)

### 2.2.2 Processus cibles

*Décrit le fonctionnement futur (To-Be) à l’aide d'ajout des composants nouveau si il en existe sur la cartographie des processus de l'existant. Met en avant les évolutions majeures par rapport à l’existant.*

Évolutions:

- prélèvements: support d'un mode dégradé en offline
- résultats: accès via un portail en ligne
- analyses: automatisation via middleware et automates; auto-validation
- hébergement de données sur le cloud (remplace le serveur central)

### 2.2.3 Processus support

*Inclut les processus de support nécessaires (référentiels, contrôle qualité, supervision métier, audit, reporting).*

- Gestion des référentiels métier
- Pilotage qualité et conformité
- Supervision des flux (enregistrement, transmission des échantillons, interfaces SIL <--> middleware <--> automates)
- Reporting et aide au pilotage : tableaux de bord des opérations (volume par site, volume par examen, etc.)
- Support utilisateurs : assistance et formation pour biologistes, techniciens, accueil, préleveurs
- Archivage : archivage des comptes rendus et journaux selon les durées requises


> ⚠️ **Exigence : Dans la suite du dossier d'architecture il est demandé de se concentrer surtout sur les processus en lien avec les produits de l'entreprise**

  

## 2.3 Exigences fonctionnelles

*Regroupe l’ensemble des besoins fonctionnels et contraintes métier à satisfaire par la solution.*

### 2.3.1 Exigences principales

*Détaille les fonctions clés que le système doit offrir et les conditions de réussite associées.*

- Accès distribué et résilient : accès au SIL depuis 57 sites avec performances acceptables, même en cas de latence ou charge importante. 
- Mode dégradé : mode hors-ligne pour les applications de prélèvements avec stockage local et synchronisation automatique.
- Interfaçage équipements médicaux : intégration bidirectionnelle avec automates multi-constructeurs, traçabilité complète et gestion des erreurs.

### 2.3.2 Exigences de qualité de service

*Spécifie les objectifs de performance, disponibilité, et réactivité du système vis-à-vis des processus métiers.*

- Haute disponibilité: 99.9% (< 8h de coupure par an), bascule rapide
- Protection et récupération des données: données médicales protégées contre toute perte via des sauvegardes  

### 2.3.3 Contraintes légales et réglementaires

*Liste les exigences liées à la conformité, à la protection des données (RGPD) et aux normes sectorielles.*

- Cloud : hébergeur certifié HDS (Hébergeur de Données de Santé) pour le cloud
- Protection des données personnelles (RGPD) : durées de conservation des données limitée, droits des personnes (accès, rectification, limitation), information et consentement lorsque nécessaire
- Exigences biologie médicale : support des obligations d’accréditation de laboratoire, conservation des comptes rendus et données analytiques sur les durées applicables et capacité d’extraction pour les audits

## 2.4 Cas d’usage et scénarios

*Présente les interactions typiques entre utilisateurs et système, sous forme de cas d’usage illustrant les principales fonctionnalités.*

  
### 2.4.1 Parties prenantes

*Ce chapitre identifie les acteurs impliqués dans la conception, la validation et la maintenance de la solution, ainsi que la structure de gouvernance associée.*


#### 2.4.1.1 Acteurs internes

*Liste les entités internes à l’organisation : DSI, métiers, exploitation, sécurité, qualité, data. Décrit leurs responsabilités dans le cycle de vie de la solution.*

- Direction & Métiers : biologistes, techniciens, accueil-facturation, qualité, finances
- DSI : responsable applicatif SIL, intégrations, data, infrastructure

#### 2.4.1.2 Acteurs externes

*Identifie les fournisseurs, éditeurs, intégrateurs et hébergeurs. Précise leurs rôles et leurs interactions avec les équipes internes.*

- Éditeur SIL et middlewares automates : intégration bi-directionnelle, règles d'autovalidation des résultats 
- Hébergeur certifié HDS : stockage cloud
- Fournisseur d'automates
- Fournisseur réseau
- Prestataire gestion d'identité sécurisée

### 2.4.2 Cas d’usage majeurs

*Décrit les scénarios clés avec leurs étapes, conditions de déclenchement, flux de données et résultats attendus.*

CU1 : Prélèvement à domicile
- Déclencheur : tournée planifiée
- Étapes : 
	- Prélèvement
	- Saisie sur l'application mobile et contrôle
	- Synchronisation avec le SIL du site
- Flux : app mobile <--> SIL du site <--> cloud
- Résultat : dossier mis à jour, prélèvement tracés
- Variante mode dégradé : stockage en local + synchronisation automatique au retour de la connexion

CU2 : Prélèvement au laboratoire
- Déclencheur : arrivée du patient à l'accueil
- Étapes : 
	- Accueil
	- Prélèvement sur place
	- Saisie et contrôle dans le SIL directement depuis le poste de prélèvement 
- Flux : poste de prélèvement du site <--> SIL du site <--> cloud
- Résultat : dossier mis à jour, prélèvement disponibles pour l'analyse
- Variante mode dégradé : stockage en local puis synchronisation au retour de la connexion; procédures sur papier (puis rattrapage) si les postes de prélèvements ou le SIL sont indisponibles

CU3 : Ordonnancement et exécution sur automate
- Déclencheur : prélèvement enregistré
- Étapes : 
	- Génération des analyses à effectuer
	- Envoi des ordres
	- Exécution
	- Retour des résultas et erreurs éventuelles
- Flux : SIL <--> Middleware <--> Automate
- Résultat : résultats bruts exploitables, traçabilité

CU4 : Validation biologique et résultats critiques
- Déclencheur : résultats disponibles
- Étapes:
	- application des règles d'auto-validation
	- vérification par un biologiste
	- commentaires
	- signature électronique
	- alerte au médecin si résultat critique
	- mise à disposition des résultats
- Flux : SIL -> Portail patient et médecin
- Résultat : résultats finaux disponibles, alertes tracées

CU5: Facturation
- Déclencheur : compte rendu disponible
- Étapes : 
	- vérification des droits du patient
	- Télétransmission & tiers payant
- Flux : SIL <--> Organismes payeurs
- Résultat : Facture émise, recouvrement tracé

### 2.4.3 Exceptions et règles métier

*Liste les cas particuliers, exceptions ou règles spécifiques à appliquer pour garantir la cohérence et la conformité métier.*

- Mode dégradé:
	- entrée dans le mode : déclenchée automatiquement si perte de réseau de plus de 30s
	- sortie du mode : au retour du réseau; synchronisation sous 10min 
- Diffusion des résultats: publication sur les portails médecin/patient seulement après signature
- Résultats critiques : seuils définis par spécialité ; appel au médecin sous 15min 
- Autovalidation : règles d'autovalidation par examen, validation manuelle obligatoire si anomalie soulevée

## 2.5 Modèle d’information métier

*Formalise les objets manipulés par les processus métiers (clients, produits, commandes...) et leurs relations.*

### 2.5.1 Relations

*Présente les liens entre objets (cardinalités, dépendances, héritages) sous forme de diagramme conceptuel.*

cf modele-info-metier.svg
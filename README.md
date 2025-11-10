[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/t-iXNFKi)
## Rappel des consignes pour le projet d'architecture

### Attendus du projet
Rédigez un Dossier d'Architecture (DA) pour l'entreprise décrite dans le scénario ci-dessous. Un modèle de DA est fourni via un dépôt GitHub Classroom, mis à disposition par l'enseignant et attribué aux élèves du groupe travaillant sur le scénario. Les activités suivantes doivent être réalisées :

- Élaborer le Dossier d'Architecture en incluant au moins les éléments du modèle fourni.
- Documenter toutes les décisions structurantes du DA dans des ADR (Architecture Decision Record) dans le dépôt du projet. Il est notamment requis de consigner les décisions concernant les produits sélectionnés dans l'architecture de la solution applicative.
- Créer au moins un diagramme de séquence (à intégrer dans la vue « Architecture Applicative ») avec un niveau de détail technique élevé pour au moins un flux fonctionnel de la solution. Le choix du flux doit être pertinent pour qu'il soit intéressant à étudier et doit inclure au moins trois acteurs ou composants. Ce diagramme doit contenir des informations sur les protocoles, les messages échangés, les URL utilisées (si API REST par exemple), les topics, etc. La représentation « C4 Model – Dynamic Diagram » ou le format UML peut être utilisée.
- Préparer une présentation au format PowerPoint (ou équivalent) pour exposer les informations clés du DA lors de la session de l'ARB (Architecture Review Board).

Toutes les informations ne sont pas fournies ; il est attendu que les étudiants effectuent des recherches sur les technologies, réfléchissent aux options possibles et fassent des choix (toujours avec une justification). Il est tout à fait possible de proposer des ajouts d'exigences dans le scénario pour définir des solutions d'architecture plus satisfaisantes, en expliquant cela à travers le mécanisme des ADR. Le modèle de DA peut également être complété si cela est pertinent (en ajoutant la mention `NEW` devant le titre du chapitre ou du fichier ajouté dans le dépôt).

### Exigences
- Le dossier doit être finalisé et transmis à l'enseignant une semaine avant la session de l'ARB (le planning est à voir avec l'enseignant).
- Le travail est réalisé en groupe et la répartition des tâches est laissée libre, mais tous les élèves du groupe doivent présenter lors de l'ARB. Dans la mesure du possible, chaque modification du DA dans GitHub doit être effectuée directement par l'élève ayant travaillé sur le sujet.
- Réaliser au moins l'architecture d'une vue du dossier d'architecture en utilisant le modèle C4.

## Principes du modèle
Nous avons découpé l'architecture du projet en cinq vues (métier, applicative, infrastructure, cybersécurité et exploitation), **chaque vue étant auto-porteuse**. 

Le principe de base est de proposer un **ensemble de vues d'architecture alignées sur les rôles que l'on trouve le plus fréquemment dans les organisations et sur leurs préoccupations respectives**. Par exemple, un architecte d'infrastructure ou un ingénieur DevOps a rarement besoin de connaître le détail de l'architecture logicielle (le détail des frameworks utilisés ou la façon de gérer les erreurs). De même, un PO ou un architecte d'entreprise va s'intéresser à la vision macroscopique des modules applicatifs et de leurs interactions principales ("le batch B appelle le service S") mais rarement du détail de l'infrastructure sous-jacente (choix de la base de données du service, dimensionnement des machines, …).

Un dossier suivant ce modèle sera ainsi constitué :

* d'une [vue metier](02_vue_metier.md) présentant le contexte métier, les processus, les acteurs, les règles de gestion, etc. ;
* d'une [vue applicative](03_vue_applicative.md) présentant le découpage en modules applicatifs et l'architeture technique de la solution (composants, interactions, technologies, etc.) ;
* d'une [vue infrastructure](04_vue_infrastructure.md) présentant les zones d'hébergement, les typologie de serveurs, les middlewares, etc. ;
* d'une [vue cybersécurité](05_vue_cybersecurite.md) présentant les aspects liés à la sécurité, aux accès, à la gestion des secrets, etc. ;
* d'une [vue exploitation](06_vue_exploitation.md) présentant les aspects liés à la supervision, à la journalisation, aux sauvegardes, etc. ;

Dans chaque vue, on retrouvera le triptyque :

* **Contraintes** : les contraintes juridiques, budgétaires, technologiques et normatives applicables au projet ;
* **Exigences** non fonctionnelles (ENF) : les exigences non fonctionnelles exprimées par les porteurs du projet, dans la limite des contraintes mentionnées précédemment;
* **Solution** : la description de l'architecture retenue, répondant aux exigences non fonctionnelles.


### Conseils sur la rédaction de votre dossier d'architecture 
* **Rester bref**, chaque mot doit avoir son utilité. Pas d'explication bateau type 'ceci est l'introduction', pas de redites d'autres documents, d'historique de l'entreprise ou de concepts vagues ;
* Un lecteur doit comprendre le fonctionnement et les contraintes de l'application sans être noyé de détails.
* Si un chapitre n'est pas applicable, ne pas le laisser vide mais simplement mentionner `N/A` pour que le lecteur sache que le sujet a été traité ou `TODO` s'il reste à compléter ;
* Ce modèle se veut **suffisamment complet pour couvrir la plupart des applications**. Il est donc normal que de nombreux chapitres ne soient pas applicables dans votre contexte. Il est également possible d'ajouter des chapitres spécifiques si nécessaire en ajoutant la mention `NEW` dans le titre du chapitre ; 

Les [diagrammes C4](https://c4model.com/) utilisent la personnalisation [C4 de plantuml](https://github.com/plantuml-stdlib/C4-PlantUML). Il est possible d'utiliser l'éditeur en ligne [https://www.planttext.com/](https://www.planttext.com/) pour créer et modifier les diagrammes C4.

## Terminologie  

> 💡 Les documentations d'architecture utilisent souvent plusieurs termes synonymes pour le même concept, de façon interchangeable et possiblement ambiguë. Afin d'éviter toute confusion, nous avons choisi de définir précisément les termes utilisés dans ce modèle.

- **Module** : Unité de code qui regroupe des fonctionnalités ou des services liés. Nous utilisons ce terme pour désigner les API (qui contiennent elles-mêmes des **endpoints**), les traitements par lots ou **batchs** (qui contiennent des **jobs**), et les **IHM/GUI** (interfaces graphiques) qui contiennent des pages.

- **Application** : En architecture monolithique, une application complète d'un seul tenant. En architecture microservices, un ensemble logique de modules.

- **Composant d'infrastructure** : Exécutable tiers ou équipement proposant des services d'infrastructure tels que la persistance pour une base de données, le messaging pour les queues, la répartition de charge pour un load-balancer, la détection de malwares pour une API antivirus, etc. Ne doit pas être confondu avec un 'composant', qui décrit une sous-partie logicielle d'un module ou d'une application monolithique (et qui est rarement documentée dans un DA car trop proche de l'implémentation).

- **Unité déployable** : Paquet/artefact autonome (zip, war, jar, gem, .deb, image OCI/Docker, binaire, etc.) en général construit et publié par un système de CI (Intégration Continue) et qui contient les exécutables d'un module (ex : 'jar' d'une application Spring Boot, archive d'une application PHP ou JS) ou d'un composant d'infrastructure (ex : 'deb' d'installation d'une base de données PostgreSQL).## Rappel des consignes pour le projet d'architecture

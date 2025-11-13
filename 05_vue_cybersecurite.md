# 5. Vue cybersécurité

Le système d’information du laboratoire manipule des données de santé à caractère personnel, des données administratives ainsi que des données financières. La cybersécurité doit donc assurer la confidentialité, l’intégrité, la disponibilité et la traçabilité du SI.

L’architecture peut s’appuyer sur un cloud privé certifié HDS, éventuellement SecNumCloud pour renforcer l’approche souveraine au risque d'un surcoût de 15%. Le cloud privé réduit l’exposition Internet mais nécessite une gouvernance stricte pour éviter les accès non maîtrisés par le fournisseur.
## 5.1 Principes de sécurité

- Durcissement des OS présents dans les laboratoires
	- Réduction de la surface d'attaque
	- Isolation des VM et des processus
	- Application des correctifs de sécurité
- Gestion des droits et renforcement des contrôles d'accès
- Principe du moindre privilège et Zero Trust
- Journalisation et surveillance
### 5.1.1 Politique de sécurité

- ISO 27001 avec des audits organisationnels pour vérifier la conformité tous les 3 ans
- Directive NIS2 destinée aux opérateurs de services essentiels OSE
- PGSSIS (Politique Générale de Sécurité des Systèmes d’Information de Santé)
- Guide d'hygiène informatique de l'ANSSI
- Les mesures prioritaires de sécurité des systèmes d'information, Référentiel à destination des établissements de santé (ANSSI)
- PSSI de l'entreprise déclinée en procédures

### 5.1.2 Gouvernance sécurité

Equipe DSI de 5 personnes
- 1 RSSI
- Deux techniciens infrastructure et support
- Deux techniciens applicatifs

Le RSSI peut assumer le rôle de DPO même si cela présente un risque de conflit d'intérêt.

Les biologistes référents sont à consulter pour les aspects réglementaires et qualité.

Les datacenters doivent être situés en France pour la souveraineté.

### 5.1.3 Conformité et réglementation

- RGPD pour les données en général
- Certification HDS (Hébergeur de Données de Santé) obligatoire pour les données de santé
- SecNumCloud recommandé mais pas obligatoire
- Certification pour la qualité des soins HAS, critère 3.06-02 : "les risques
numériques sont maîtrisés" 
- PCI-DSS pour la facturation des rendez-vous et des analyses

Audits de test d'intrusion (tous les ans), d'architecture et de configuration (tous les 2-3 ans) par une entreprise qualifiée PASSI

## 5.2 Sécurité des accès et identités

### 5.2.1 Authentification et fédération

Authentification forte avec Multi-Factor Authentication (MFA) pour toutes les identités
- identités métiers
- identités clients (et médecins)
- identités privilégiées (possibilité de rajouter le modèle Zero)

Utilisation de SAML 2.0 pour la fédération des identités pour une compatibilité avec les progiciels utilisés

### 5.2.2 Autorisation et rôles

La gestion des droits d'accès se fera sur un modèle RBAC hierarchisé. Les équipes métiers et techniques devront collaborer pour définir les différents rôles de l'entreprise (biologiste, infirmière, préleveur, technicien d'infrastructure, administrateur) ainsi que les droits d'accès associés. 

Le système de contrôle des droits d'accès va ainsi vérifier automatiquement les rôles de chaque utilisateur qui accède à une ressource dans le but de la consulter ou de la modifier.

### 5.2.3 Gestion des comptes et traces

Donner les *birth rights* adéquats lors de la création du compte afin de ne pas ralentir les processus métiers. De même, faire en sorte que la demande de droits supplémentaires soit efficace permet d'éviter le développement de mauvaises pratiques qui nuisent à la sécurité.

La gestion des comptes doit respecter le cycle Join-Move-Leave. Lorsqu'un employé quitte l'entreprise, son compte et ses accès doivent être révoqués. De manière similaire, les droits d'un employé effectuant une mobilité doivent être examinés. Par exemple, un employé qui quitte un laboratoire de proximité pour un autre ne doit plus avoir les accès pour l'ancien laboratoire et obtenir les nouveaux accès.

Pas de rotations des mots de passe car ce système conduit à une alternance entre deux mots de passe. Privilégier de la sensibilisation pour la création d'un mot de passe fort et la non-divulgation de celui-ci (posts-it).

Journalisation des tentatives de connexion infructueuses ou réussies ainsi que l'accès à toutes les ressources. Les actions critiques effectuées dans l'application métier et la modification des résultats doivent être surveillées avec encore plus de rigueur.

## 5.3 Sécurité des données

### 5.3.1 Chiffrement et anonymisation

- Les communications internes et externes sont chiffrées en utilisant TLS 1.3
- Chiffrement au repos des bases de données et des sauvegardes en AES-256
- Protocole IPSEC
- Pseudonymisation pour les traitements analytiques

### 5.3.2 Sauvegarde et rétention

- Chiffrement des sauvegardes
- Test pour vérifier l'efficacité de la restauration
- Suivre les obligations légales de conservation des données médicales (20 ans)

### 5.3.3 Protection contre les fuites de données

- Solutions DLP
	- Surveillance des exports de données lourds
	- Contrôle des impressions
	- Blocage des clés USB

## 5.4 Sécurité opérationnelle

### 5.4.1 Supervision de sécurité (SOC)

- Corrélation des logs via le SIEM
- Alertes automatiques en cas d'activités suspectes et d'anomalie réseau
- Dashboard simplifiés pour accéder aux logs et aux alertes

### 5.4.2 Gestion des vulnérabilités

- Cycles de patching
	- Mensuel pour les serveurs et les postes des laboratoires
	- Hebdomadaire pour les équipements réseau
- Test d'intrusion annuel par un prestataire PASSI
- Gestion des alertes CVE
	- Veille sur les nouvelles CVE ou usage récent d'une ancienne CVE
	- Vérification de la vulnérabilité de l'entreprise
	- Correctif immédiat si le score dépasse 7 (entre 48h et 72h)
	- Correctif à appliquer plus tard sinon
### 5.4.3 Réponse aux incidents

- Souscription à un CERT externe en cas d'incident car la DSI n'a pas les moyens de répondre rapidemment et efficacement
- Chaîne d'escalade RSSI -> Direction -> CERT externe
- Communication avec l'ARS pour prévenir la violation des données de santé
- Sensibilisation ou formation régulière des équipes (phishing, mots de passe faibles)

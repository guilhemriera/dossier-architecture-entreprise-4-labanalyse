# 7. Annexes

## 7.1 Glossaire
Fournit les définitions des termes, acronymes et abréviations utilisés dans le dossier d’architecture.

### 7.1.1 Termes métier et organisationnels


| Terme   |                           Signification                            |                                                         Commentaire                                                         |
| :------ | :----------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------: |
| CA      |                            Cour d’appel                            |  "Alors que les juridictions de première instance rendent un « jugement », une cour d’appel rend un « arrêt »" [Wikipedia]  |
| PSSI    |          Politique de Sécurité des Systèmes d'Information          |                          Plan d'action défini pour maintenir un bon niveau de sécurité [Wikipedia]                          |
| PGSSI-S | Politique Générale de Sécurité des Systèmes d’Information de Santé |                                  Politique encadrant les règles de sécurité pour l'e-santé                                  |
| HDS     |                   Hébergeur de Données de Santé                    |             Certification dont le but est de renforcer la protection des données de santé à caractère personnel             |
| DPO     |                Délégué à la Protection des Données                 | Personne chargée de vérifier que les lois de protection des données personnelles sont bien appliquées dans une organisation |
| ARS     |                     Agence Régionale de Santé                      |        Etablissement public adminstratif chargé de mettre en oeuvre la politique de santé dans sa région [Wikipedia]        |


### 7.1.2 Termes applicatifs

| Terme | Signification | Commentaire |
|:-------- |:--------:|:--------:|
|EIDAS|Electronic IDentification Authentication and trust Services | Règlement européen sur la signature électronique
|SPA| Single Page Application | Application Web dont les pages sont générées en javascript dans le navigateur


### 7.1.3 Termes techniques 


| Terme  |               Signification               |                                                                               Commentaire                                                                                |
| :----- | :---------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| RP     |               Reverse Proxy               | Mantataire inverse effectuant des appels HTTP pour le compte d'un client (en général sur Internet).Permet entre autres d'augmenter la sécurité par rupture protocolaire. |
| SIEM   | Security Information and Event Management |                                                      Système de collection des logs et des évènements informatiques                                                      |
| CERT   |     Computer Emergency Response Team      |                                            Centre d'alerte et de réaction aux attaques informatiques destiné aux entreprises                                             |
| DMZ    |            DeMilitarized Zone             |                                         Sous-réseau qui fait office d'intermédiaire entre un réseau interne et un réseau externe                                         |
| VPC    |           Virtual Private Cloud           |                                                             Cloud privé virtuel hébergé dans un cloud public                                                             |
| ACL    |            Access Control List            |                                                         Liste des permissions associées à une ressource système                                                          |
| SD-WAN |    Software-Defined Wide Area Network     |                        Technologie réseau qui utilise les principes réseau défini par logiciel pour améliorer les performances du WAN [Fortinet]                         |
| DAS    |          Direct-Attached Storage          |                                                           Stockage directement attaché au serveur sans réseau                                                            |
| SAN    |           Storage Area Network            |                                                           Réseau dédié haut-débit qui émule des disques locaux                                                           |


### 7.1.4 Sources

* https://sante.gouv.fr/systeme-de-sante/numerique-en-sante/sih/dossier-cybersecurite/article/la-cybersecurite-un-enjeu-majeur-pour-les-etablissements-de-sante
* https://www.cnil.fr/fr/passer-laction/le-delegue-la-protection-des-donnees-dpo
* https://www.hpe.com/fr/fr/what-is/data-center-networking.html
* https://www.sentinelone.com/fr/cybersecurity-101/cloud-security/cloud-security-in-healthcare/
* https://evernex.com/fr/blog/le-role-du-stockage-sur-bandes-2/
* https://esante.gouv.fr/produits-services/pgssi-s
* https://sante.gouv.fr/ministere/defense-et-securite-hfds/article/cyber-securite
* https://www.fortinet.com/fr/resources/cyberglossary/sd-wan-explained

## 7.2 Références documentaires
Liste les documents de référence majeurs utilisés : normes, politiques internes, guides techniques, cahiers des charges, lien internet.

- Cours Architecture des Systèmes d'Information
- ISO 27001
- Les mesures prioritaires de sécurité des systèmes d'information, Référentiel à destination des établissements de santé (ANSSI)

## 7.4 Liste des décisions d’architecture
Documente les décisions structurantes (ADR) avec leurs justifications et impacts attendus. Faire ici le lien vers les ADR du dépôt

| Identifiant                                                                  |              Titre               |
| :--------------------------------------------------------------------------- | :------------------------------: |
| [ADR-SOLUTION-01](/decisions/solution/adr-solution-01.md)                    |  Choix du modèle d'architecture  |
| [ADR-INFRASTRUCTURE-01](./decisions/Infrastructure/datacenter-adr)           | Modèle d'hébergement Datacenter  |
| [ADR-INFRASTRUCTURE-02](./decisions/Infrastructure/stockage-principal-adr)   | Stockage des données principales |
| [ADR-INFRASTRUCTURE-03](./decisions/Infrastructure/stockage-sauvegardes-adr) |     Stockage des sauvegardes     |
| [ADR-INFRASTRUCTURE-04](./decisions/Infrastructure/stockage-principal-adr)]  |      Stockage des archives       |

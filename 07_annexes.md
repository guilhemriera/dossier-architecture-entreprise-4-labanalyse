# 7. Annexes

## 7.1 Glossaire
Fournit les définitions des termes, acronymes et abréviations utilisés dans le dossier d’architecture.

### 7.1.1 Termes métier et organisationnels


| Terme   |                           Signification                            |                                                        Commentaire                                                        |
| :------ | :----------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| CA      |                            Cour d’appel                            | "Alors que les juridictions de première instance rendent un « jugement », une cour d’appel rend un « arrêt »" [Wikipedia] |
| PSSI    |          Politique de Sécurité des Systèmes d'Information          |                                                                                                                           |
| PGSSI-S | Politique Générale de Sécurité des Systèmes d’Information de Santé |                                                                                                                           |
| HDS     |                   Hébergeur de Données de Santé                    |                                                                                                                           |
| DPO     |                Délégué à la Protection des Données                 |                                                                                                                           |
| ARS     |                     Agence Régionale de Santé                      |                                                                                                                           |


### 7.1.2 Termes applicatifs

| Terme | Signification | Commentaire |
|:-------- |:--------:|:--------:|
|EIDAS|Electronic IDentification Authentication and trust Services | Règlement européen sur la signature électronique
|SPA| Single Page Application | Application Web dont les pages sont générées en javascript dans le navigateur


### 7.1.3 Termes techniques 


| Terme  |               Signification               |                                                                               Commentaire                                                                                |
| :----- | :---------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| RP     |               Reverse Proxy               | Mantataire inverse effectuant des appels HTTP pour le compte d'un client (en général sur Internet).Permet entre autres d'augmenter la sécurité par rupture protocolaire. |
| SIEM   | Security Information and Event Management |                                                                                                                                                                          |
| CERT   |     Computer Emergency Response Team      |                                                                                                                                                                          |
| DMZ    |            DeMilitarized Zone             |                                                                                                                                                                          |
| VPC    |           Virtual Private Cloud           |                                                                                                                                                                          |
| ACL    |            Access Control List            |                                                                                                                                                                          |
| SD-WAN |    Software-Defined Wide Area Network     |                                                                                                                                                                          |
| DAS    |          Direct-Attached Storage          |                                                                                                                                                                          |

### 7.1.4 Sources

* https://sante.gouv.fr/systeme-de-sante/numerique-en-sante/sih/dossier-cybersecurite/article/la-cybersecurite-un-enjeu-majeur-pour-les-etablissements-de-sante
* https://www.cnil.fr/fr/passer-laction/le-delegue-la-protection-des-donnees-dpo
* https://www.hpe.com/fr/fr/what-is/data-center-networking.html
* https://www.sentinelone.com/fr/cybersecurity-101/cloud-security/cloud-security-in-healthcare/
* https://evernex.com/fr/blog/le-role-du-stockage-sur-bandes-2/
* https://esante.gouv.fr/produits-services/pgssi-s
* https://sante.gouv.fr/ministere/defense-et-securite-hfds/article/cyber-securite

## 7.2 Références documentaires
Liste les documents de référence majeurs utilisés : normes, politiques internes, guides techniques, cahiers des charges, lien internet.

- Cours Architecture des Systèmes d'Information
- ISO 27001
- Les mesures prioritaires de sécurité des systèmes d'information, Référentiel à destination des établissements de santé (ANSSI)

## 7.4 Liste des décisions d’architecture
Documente les décisions structurantes (ADR) avec leurs justifications et impacts attendus. Faire ici le lien vers les ADR du dépôt

| Identifiant | Titre |
|:-------- |:--------:|
| [ADR-SOLUTION-01](/decisions/solution/adr-solution-01.md)    | Choix du modèle d'architecture  |
| [ADR-INFRASTRUCTURE-01](/decisions/context/adr-infrastructure-01.md)    | Modèle d'hébergement Datacenter  |
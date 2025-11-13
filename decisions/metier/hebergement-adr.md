# Hébergement HDS & modèle de déploiement

## Statut

Acceptée

## Contexte

Le SI de LabAnalyse doit desservir 57 sites avec une disponibilité de 99,9 %, tout en respectant RGPD et HDS. L’existant « serveur central » limite la scalabilité, les mises à jour et la reprise après incident. Les usages clés (portails patient/médecin, interfaçage automates, montée en charge) exigent une plateforme résiliente.

## Options Envisagées

- On-premise modernisé (datacenter interne) : Maîtrise physique, latences réseau locales; Invest CAPEX élevé, délais de provisioning, difficile à faire certifier HDS bout-en-bout
- Cloud HDS : Déploiement rapide, services managés, coûts OPEX
- Hybride (on-prem + cloud HDS) : Garde-fous locaux (caches/relays), migration progressive; Complexité d’exploitation, doubles compétences/outils

## Décision

Adopter un déploiement Cloud HDS (France) pour le noyau SI (SIL, middleware d’intégration, portails), avec services managés (base de données, sauvegardes, monitoring).
Justification : meilleur compromis scalabilité/coûts d’exploitation, accélère les mises en production, simplifie la conformité HDS/RGPD et soutient la croissance multi-sites.


## Conséquences
- Positives
    - Disponibilité accrue, sauvegardes managées
    - Scalabilité pour pics (campagnes, épidémies)
    - Observabilité unifiée (logs/metrics/traces), patching simplifié
- Négatives / Risques
    - Coûts récurrents OPEX
    - Verrous fournisseurs : exiger des clauses de réversibilité

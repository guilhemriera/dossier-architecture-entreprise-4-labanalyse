# Mode dégradé et  synchronisation offline pour les prélèvements

## Statut

Acceptée

## Contexte

Les prélèvements à domicile et certains sites subissent des coupures réseau. Le métier impose une continuité d’activité (saisie, étiquetage, contrôles) avec traçabilité et zéro perte. À la reconnexion, les dossiers doivent se synchroniser sans conflits, en respectant les règles (ex. pas d’écrasement d’un résultat signé).

## Options Envisagées
- Pas de vrai offline (cache minimal) : simple mais rupture d’activité dès perte de réseau, non conforme aux exigences
- Offline simple ("last-writer-wins") : Implémentation rapide mais risque d’écrasement silencieux, non conforme traçabilité/audit
- Offline robuste par journal d’événements + identifiants uniques : Traçabilité fine, reprise déterministe, gestion explicite des conflits mais plus complexe

## Décision

Mettre en place un mode dégradé robuste basé sur :
- Identifiants générés offline (préfixe site/terminal) pour échantillons & opérations
- Journal d’événements local (création prélèvement, étiquetage, contrôle, etc.)
- Stockage local chiffré + signature des opérations sensibles
- Synchronisation à la reconnexion avec replay et règles de résolution (ex. pas d'overwrite d’un résultat validé/signé ; fusion des métadonnées non conflictuelles)
- Purge locale après accusé de réception serveur + conservation des journaux selon les durées requises.

Justification : garantit la continuité métier, la traçabilité et la sécurité des données sans compromettre l’intégrité des résultats.

## Conséquences

- Positives
    - Continuité de service en mobilité, zéro perte (journal/replay), audit complet
    - Réduction des retards de rendu liés aux aléas réseau
- Négatives / Risques
    - Complexité de dev/test (cas de conflits, replays partiels)
- Impacts techniques & organisationnels
    - Stratégie de conflits documentée (priorités, règles par type d’objet)
    - Tests terrain (coupures simulées), procédures papier de secours encadrées
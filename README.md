## Rapport de Projet : Automatisation du Rapprochement de Factures Fournisseurs (POC)

### 1. Contexte et Problématique Opérationnelle
Actuellement, le département approvisionnement valide manuellement l'intégralité des factures fournisseurs. Ce processus soulève plusieurs défis majeurs :

*   **Volume critique :** Plusieurs centaines de factures sont réceptionnées mensuellement pour chaque environnement.
*   **Goulot d'étranglement :** Une seule ressource est allouée à cette tâche.
*   **Coût temporel élevé :** Le traitement manuel d'une facture prend en moyenne 4 minutes.
*   **Flux tendu :** L'impossibilité d'anticiper le volume oblige les équipes à traiter les factures en urgence, uniquement à l'approche de leur date d'échéance.
*   **Fiabilité de la donnée :** La monotonie de cette tâche sans valeur ajoutée augmente statistiquement le risque d'erreurs de saisie humaine.

### 2. Objectif du Proof of Concept (POC)
Le but de ce projet pilote est de démontrer, sur un environnement spécifique (Luxcos), qu'il est possible de réduire drastiquement la charge de travail manuel grâce à l'Intelligence Artificielle. L'objectif n'est pas de remplacer la validation, mais de générer une **shortlist de factures 100% fiables** destinées à être validées en masse par le département IT.

### 3. Fonctionnement et Sécurité du Processus
L'automatisation repose sur une logique de sécurité stricte :
1.  **Extraction OCR (Azure AI) :** Numérisation et lecture intelligente des données de la facture (sans erreur de frappe).
2.  **Rapprochement Base de Données :** L'algorithme croise les données lues avec les commandes enregistrées dans l'ERP.
3.  **Filtre de Sécurité Stricte :** Une facture n'est classée "Éligible à l'automatisation" que si la correspondance est parfaite (Référence exacte, Quantité identique, Prix unitaire validé). Toute exception bloque l'automatisation et renvoie la facture vers un traitement manuel.

### 4. Résultats de l'Analyse
L'algorithme a été exécuté sur un jeu de test représentatif composé de plusieurs centaines de factures réelles.

**[INSÉRER GRAPHIQUE 1 : Répartition des statuts de validation (Automatique vs Manuel)]**

*   **60% de Validation Automatique :** Ces factures correspondent parfaitement aux données de l'ERP et sont intégrées à la shortlist pour validation IT en masse.
*   **40% de Traitement Manuel :** Ces factures présentent des anomalies légitimes (changement de tarification fournisseur, exceptions métier, surcoût de transport) justifiant l'intervention humaine.

### 5. Impact et Gain d'Efficacité

| Indicateur | Processus Manuel (Avant) | Processus Automatisé (Après) |
| :--- | :--- | :--- |
| **Charge de travail** | 100% des factures vérifiées à la main | Seules les factures problématiques (40%) sont traitées |
| **Temps alloué** | ~4 min par facture (Toutes factures) | ~4 min par facture (Uniquement sur les cas complexes) |
| **Fiabilité** | Risque d'erreur de saisie humaine | Comparaison mathématique stricte par l'algorithme |
| **Gestion des flux** | Traitement en retard / Flux tendu | Dégagement de temps pour anticiper les échéances |

### 6. Prochaines Étapes
1.  Transmission de la "shortlist" générée au département IT pour implémentation d'une routine de validation en masse dans l'ERP.
2.  Adaptation et extension du script aux autres bases de données et environnements de production.
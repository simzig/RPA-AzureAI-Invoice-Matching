## Rapport de Projet : Automatisation du Rapprochement de Factures Fournisseurs (POC)

### 1. Contexte et Problématique Opérationnelle
Actuellement, le département approvisionnement valide manuellement l'intégralité des factures fournisseurs. Ce processus soulève plusieurs défis majeurs :

*   **Volume critique :** Plusieurs centaines de factures sont réceptionnées mensuellement pour chaque environnement.
*   **Goulot d'étranglement :** Une seule ressource est allouée à cette tâche.
*   **Coût temporel élevé :** Le traitement manuel d'une facture prend en moyenne 4 minutes.
*   **Flux tendu :** L'impossibilité d'anticiper le volume oblige les équipes à traiter les factures en urgence, uniquement à l'approche de leur date d'échéance.
*   **Fiabilité de la donnée :** La monotonie de cette tâche sans valeur ajoutée augmente statistiquement le risque d'erreurs de saisie humaine.

### 2. Objectif du Proof of Concept (POC)
Le but de ce projet pilote est de démontrer, sur un environnement spécifique (Luxcos), qu'il est possible de réduire drastiquement la charge de travail manuel grâce à l'Intelligence Artificielle. L'objectif n'est pas de remplacer la validation, mais de générer une **shortlist de factures fiables** destinées à être validées en masse.

### 3. Fonctionnement et Sécurité du Processus
L'automatisation repose sur une logique métier stricte intégrant les règles de gestion de la comptabilité :
1.  **Extraction OCR (Azure AI) :** Numérisation et lecture intelligente des données de la facture (sans erreur de frappe).
2.  **Rapprochement Base de Données :** L'algorithme croise les données lues avec les commandes enregistrées dans l'ERP.
3.  **Validation Paramétrée :** Une facture est classée "Éligible à l'automatisation" sous des conditions précises :
    *   Correspondance absolue de la référence de commande.
    *   Correspondance absolue des quantités facturées par rapport à l'ERP.
    *   **Tolérance tarifaire :** Les factures présentant un écart de prix mineur sont acceptées et intégrées à la validation automatique (le prix de l'ERP sera écrasé par le nouveau prix, conformément aux règles opérationnelles).
    *   Toute autre exception (écart majeur, frais de port anormaux, référence inconnue) bloque l'automatisation et renvoie la facture vers un traitement manuel.

### 4. Résultats de l'Analyse
L'algorithme a été exécuté sur un jeu de test représentatif composé de plusieurs centaines de factures réelles.

*   **60% de Validation Automatique :** Ces factures remplissent les critères (match parfait ou écart de prix mineur toléré) et sont intégrées à la shortlist pour une validation en masse.
*   **40% de Traitement Manuel :** Ces factures présentent des anomalies majeures ou non tolérées (changement de tarification fournisseur important, exceptions métier, surcoût de transport) justifiant l'intervention humaine.

### 5. Analyse des Coûts et Impact Opérationnel
Le modèle économique de cette solution repose sur un retour sur investissement (ROI) quasi immédiat en comparant le coût d'exécution machine au coût du travail humain.

*   **Coût technologique (Azure AI) :** La tarification de l'API Document Intelligence est facturée à l'usage, représentant un coût opérationnel marginal (de l'ordre de quelques dizaines d'euros pour plusieurs milliers de factures).
*   **Économie de temps humain :** Le traitement manuel de 1000 factures requiert approximativement 66 heures de travail (à raison de 4 min/facture). L'automatisation de 60% de ce volume permet de réallouer environ 40 heures par mois et par environnement vers des tâches à plus haute valeur ajoutée.
*   **Gain de fiabilité :** Application systématique et stricte des règles de gestion, éliminant le risque d'erreur de saisie humaine.

### 6. Prérequis à la Mise en Production
La mise en production effective nécessite de résoudre deux goulots d'étranglement architecturaux actuels :

1.  **Automatisation de la validation sur Adfinity :** Actuellement, la validation s'opère en deux temps : sur notre ERP interne (qui supporte la validation en masse) et sur le logiciel de comptabilité Adfinity. Adfinity ne permettant aujourd'hui qu'une validation unitaire manuelle, une adaptation de leur solution (via import ou API) est requise pour traiter la shortlist de manière groupée.
2.  **Sourcing automatisé des documents :** Pour les tests, les PDF ont été téléchargés manuellement. Pour un processus "End-to-End", le script devra pouvoir récupérer ces fichiers automatiquement, soit via l'accès à un dossier réseau d'Adfinity, soit en interceptant directement les pièces jointes à leur réception dans la boîte mail générique.

### 7. Prochaines Étapes et Vision à Long Terme
Une fois la fiabilité d'Azure AI démontrée et validée sur le processus d'approvisionnement, l'outil a vocation à être déployé plus largement au sein du département comptabilité. 

Les capacités de l'intelligence artificielle permettent de cibler d'autres tâches manuelles redondantes, telles que :
*   Le tri et la classification automatique des documents comptables dès leur réception par email.
*   L'extraction de métadonnées pour l'imputation analytique sans saisie manuelle.
*   La systématisation d'autres flux de validation inter-services.
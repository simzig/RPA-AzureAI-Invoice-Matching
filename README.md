# RPA-AzureAI-Invoice-Matching

## 🎯 Project Overview
Ce projet est un Proof of Concept (POC) d'automatisation (RPA) conçu pour le rapprochement de factures fournisseurs. Il utilise l'intelligence artificielle pour extraire les données de PDF et les compare de manière automatisée avec les bases de données d'un ERP.

## ⚙️ Tech Stack
* **Langage :** Python 3
* **IA & OCR :** Azure AI Document Intelligence
* **Data Processing :** Pandas, Numpy
* **Reporting :** OpenPyXL

## 🚀 Fonctionnalités Clés
* **Extraction OCR :** Analyse de documents PDF pour en extraire les métadonnées (Fournisseur, Lignes de facturation, Quantités, Prix unitaire).
* **Rapprochement ERP :** Matching par références (CLX, CIL, CIP), vérification des quantités et des prix unitaires.
* **Calcul automatique :** Déduction des frais de port unitaires et alertes basées sur une tolérance métier (>20%).
* **Export Excel :** Génération de rapports d'audit avec mise en forme conditionnelle (Code couleur de validation).

## 🛣️ Roadmap de mise en production (Handover)
Ce projet est un POC fonctionnel. Les optimisations architecturales suivantes sont prévues pour le passage en production par les futures équipes :
* **Sécurité :** Migration de la clé API Azure codée en dur vers un gestionnaire de variables d'environnement (`.env` via `python-dotenv`).
* **Traçabilité :** Remplacement des sorties console (`print`) par le module standard `logging` pour le suivi des exécutions serveur.
* **Maintenabilité :** Implémentation du typage statique (Type Hinting) pour documenter le code et fiabiliser la reprise.

## 🛠️ Utilisation
1. Cloner le dépôt : `git clone https://github.com/VOTRE_NOM/RPA-AzureAI-Invoice-Matching.git`
2. Installer les dépendances : `pip install pandas openpyxl azure-ai-formrecognizer`
3. Renseigner vos propres identifiants Azure (`ENDPOINT` et `KEY`) dans le script principal.
4. Placer les factures PDF dans un dossier `/facture_test` et lancer l'analyse.
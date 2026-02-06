# ArgSpanMatcher-NLP

## Description

Ce projet implémente des méthodes pour l'extraction d'arguments dans des textes en utilisant le format BIO (Begin, Inside, Outside). Il compare une approche naïve basée sur la fréquence lexicale avec une approche avancée utilisant des modèles de langage (LLM) comme RoBERTa. Le projet évalue également le transfert de domaine entre des essais étudiants (AAE) et des résumés médicaux (abstraits).

## Installation

1. Clonez le dépôt :

   ```bash
   git clone <repository-url>
   cd ArgSpanMatcher-NLP
   ```

2. Installez les dépendances :
   ```bash
   pip install -r requirements.txt
   ```

## Dépendances

- torch
- transformers
- datasets
- seqeval
- pandas
- numpy
- accelerate
- scikit-learn
- huggingface_hub

## Données

Le projet utilise des données annotées en format BIO pour l'extraction d'arguments :

- **AAE (Argument Annotated Essays)** : Essais étudiants annotés.
  - `aae_train.json` : Ensemble d'entraînement
  - `aae_dev.json` : Ensemble de développement
  - `aae_test.json` : Ensemble de test

- **Abstracts Médicaux** : Résumés médicaux annotés.
  - `abstrct_neoplasm_train.json`, `abstrct_neoplasm_dev.json`, `abstrct_neoplasm_test.json` : Néoplasmes
  - `abstrct_glaucoma_test.json` : Glaucome
  - `abstrct_mixed_test.json` : Mixte

## Utilisation

### Approche Naïve (Baseline Lexicale)

Exécutez le notebook `arg_matcher_naive.ipynb` pour :

- Charger les données
- Construire un modèle basé sur la fréquence des mots
- Faire des prédictions sur les ensembles de test
- Évaluer les performances

### Approche LLM

Exécutez le notebook `arg_match_llm.ipynb` pour :

- Fine-tuner un modèle RoBERTa pour l'extraction d'arguments
- Évaluer sur les domaines source et cible

### Scripts Utilitaires

- `scripts/evaluate.py` : Évalue les prédictions par rapport aux vérités terrain.

  ```bash
  python scripts/evaluate.py data/aae_test.json predictions/naive/naive_essays_final.json
  ```

- `scripts/view_data.py` : Visualise les tokens et statistiques des données.

## Structure du Projet

```
.
├── data/                    # Fichiers JSON originaux
├── predictions/             # Résultats générés (fichiers JSON)
│   ├── llm/                 # Prédictions du modèle LLM
│   └── naive/               # Prédictions de l'approche naïve
├── scripts/                 # Scripts utilitaires
│   ├── evaluate.py
│   └── view_data.py
├── arg_matcher_naive.ipynb
├── arg_match_llm.ipynb
├── README.md
└── requirements.txt
```

## Évaluation

Les performances sont mesurées en précision, rappel et F1-score par label BIO. Utilisez `seqeval` pour des rapports détaillés.

Exemples de résultats :

- Approche naïve : Baseline pour mesurer l'impact du domaine
- LLM : Amélioration attendue grâce à la compréhension sémantique

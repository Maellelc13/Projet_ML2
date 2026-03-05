## Projet ML2 – Détection de fraude

Ce projet s’articule autour de **trois notebooks principaux**, à exécuter dans l’ordre suivant :

1. `EDA/EDA_final.ipynb`  
   - Analyse exploratoire des données brutes (`kaggle_b2_fraud_train_v4.csv` / `kaggle_b2_fraud_test_v4.csv`).
   - Vérifie la structure du jeu de données, la distribution de la cible, les valeurs manquantes et quelques relations simples avec la fraude.

2. `Preprocess/Preprocessing_final.ipynb`  
   - Met en œuvre le **prétraitement complet** :
     - suppression des colonnes de fuite d’information et des identifiants,
     - harmonisation des catégories texte (`payment_method`, `occupation`, `region`, …),
     - séparation numériques / catégorielles / texte,
     - imputation, standardisation, One‑Hot Encoding, filtrage de corrélation,
     - création du mapping `feature_i → nom de feature d’origine`.
   - Exporte les jeux **prétraités** utilisés pour la modélisation :
     - `data/train_preprocessed_v2_V4.csv`
     - `data/test_preprocessed_v2_V4.csv`
     - `data/feature_mapping_v2_V4.csv`

3. `Modélisation/Modélisation_final.ipynb`  
   - Charge les CSV prétraités et sépare train / validation / test.
   - Entraîne et compare plusieurs modèles :
     - Régression logistique, KNN, Arbre de décision, Random Forest,
       AdaBoost, Gradient Boosting, XGBoost (avec optimisation de seuil),
       et un ensemble simple basé sur XGBoost / RF / GB.
   - Calcule les métriques (F1, rappel, précision) et un **coût métier**
     \(130×FN + 15×FP\) pour chaque modèle.
   - Sauvegarde les meilleurs modèles en pickle dans `Models/` et génère des
     soumissions Kaggle dans `Prédiction/`.
   - **Note** : le dossier `Models/` est dans le `.gitignore` (il n’est pas versionné). Il est créé automatiquement à la première exécution du notebook. Pour que les cellules « comparaison » et « SHAP » fonctionnent, il faut avoir exécuté auparavant les cellules d’entraînement de chaque modèle (Régression logistique, KNN, Arbre, Random Forest, AdaBoost, Gradient Boosting, XGBoost).
   - Fournit les sections d’**interprétation** :
     - coefficients et odds ratios de la régression logistique,
     - graphes SHAP pour XGBoost,
     - synthèse business et choix du modèle final.

### Pré‑requis

- **Accès au projet** : cloner le dépôt GitHub suffit pour avoir l’ensemble du code et des notebooks.
- **Environnement** : Python 3.10+ avec les librairies usuelles (`pandas`, `numpy`, `scikit-learn`, `xgboost`, `matplotlib`, `seaborn`, `shap`, …). Les notebooks peuvent être exécutés avec Jupyter, VS Code ou tout autre environnement supportant les notebooks.
- **Données** : placer les fichiers `kaggle_b2_fraud_train_v4.csv` et `kaggle_b2_fraud_test_v4.csv` dans le dossier `data/` (chemins relatifs utilisés dans les notebooks).
- Exécuter les **trois notebooks dans l’ordre** (1 → 2 → 3) pour reproduire les résultats.
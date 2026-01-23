# Adult Income Classification Project

Ce projet vise à prédire si le revenu annuel d'un individu dépasse 50 000 $ en se basant sur les données de recensement (dataset "Adult Income"). Il s'agit d'un problème de **classification binaire**.

## 📋 Structure du Projet

L'analyse est divisée en trois étapes majeures, documentées dans le notebook `projet.ipynb` :
1. **Exploration des données (EDA) et analyses non supervisées**
2. **Préprocessing et ingénierie des données**
3. **Modélisation supervisée et évaluation**

---

## 🛠️ Choix Techniques et Étapes

### 1. Analyse Exploratoire et Gestion des Données
- **Stratification au Split** : Nous avons utilisé `stratify=y` lors de la séparation train/test (80/20) pour préserver le déséquilibre des classes (75% <=50K / 25% >50K).
- **Traitement des Valeurs Manquantes** : Les données manquantes (identifiées par des `?`) concernaient environ 7% des lignes. Plutôt que de les supprimer, nous avons opté pour une **imputation par le mode** (valeur la plus fréquente) pour les variables catégorielles afin de conserver la richesse statistique du dataset.

### 2. Modélisation
Plusieurs modèles ont été testés (Random Forest, Régression Logistique, etc.), mais le **Gradient Boosting** a été retenu pour sa capacité à capturer des relations non-linéaires complexes. Un **tuning d'hyperparamètres** a été effectué pour optimiser le score F1.

---

## 📊 Analyse des Résultats (Gradient Boosting Tuné)

### Matrice de Confusion
Le modèle affiche une précision globale d'environ **87%**. Cependant, l'analyse détaillée révèle un profil **"Prudent"** :
- **Faux Négatifs (805)** : Le modèle "rate" une partie des hauts revenus.
- **Faux Positifs (380)** : Les erreurs de surestimation sont limitées.
- **Interprétation** : Le modèle privilégie la certitude avant de classer un profil en ">50K". C'est un comportement conservateur face au déséquilibre des classes.

### Importance des Features (Hypothèses vs Réalité)
Initialement, nous supposions que l'éducation et l'âge seraient les facteurs clés. Les résultats montrent une réalité plus nuancée :
- **Le statut marital (Marié)** est le prédicteur n°1 (35% d'importance). Dans ce dataset, c'est un indicateur social extrêmement fort de stabilité financière.
- **Capital Gain/Loss** : Les indicateurs financiers directs suivent logiquement en importance.
- **Variables Sociologiques** : Le sexe et la race apparaissent en fin de classement. Le modèle s'appuie davantage sur des variables de parcours de vie (éducation, situation familiale) que sur des critères biologiques.

---

## 🚀 Conclusion
Le projet démontre qu'un modèle de Gradient Boosting peut prédire le revenu avec une forte fiabilité, mais qu'il reste sensible à la distribution des données historiques. La prédominance du statut marital souligne l'importance du contexte socio-temporel des données (recensement de 1994). 

Pour améliorer le rappel sur la classe minoritaire, des techniques comme le SMOTE ou l'ajustement du seuil de décision pourraient être envisagées.

---
## 💻 Installation
1. Clonez le dépôt.
2. Installez les dépendances : `pip install -r requirements.txt`.
3. Lancez le notebook `projet.ipynb`.

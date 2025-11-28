# Cours de science de données 
# EL KHAOULANI WISSALE
# Ecole national de commerce et de gestion
<img src="WISSALE.jpeg" style="height:264px;margin-right:232px"/> 

- ## Nom du fichier : SEA Building Energy Benchmarking
## Sommaire

- Introduction
- Présentation du Dataset
- Méthodologie
- Nettoyage des Données
- Analyse Exploratoire
- Matrice de Corrélation
- Modélisation : Régression Linéaire
- Modélisation : Régression Logistique
- Résultats et Interprétations
- Conclusions et Recommandations
- Annexes
  ## 1. INTRODUCTION
- 1.1 Contexte
Le programme de benchmarking énergétique de Seattle a été établi pour suivre et améliorer l'efficacité énergétique des bâtiments de la ville. Les bâtiments représentent environ 33% des émissions totales de carbone de Seattle, ce qui en fait un secteur crucial dans la lutte contre le changement climatique.
- 1.2 Objectifs de l'Analyse
Cette analyse vise à :

- Comprendre les facteurs influençant la consommation énergétique des bâtiments
- Identifier les relations entre différentes variables énergétiques
- Prédire la consommation énergétique à partir de caractéristiques du bâtiment
- Classifier les bâtiments selon leur efficacité énergétique
- Fournir des insights exploitables pour les décideurs politiques

- 1.3 Réglementation
Le programme exige que les propriétaires de bâtiments non résidentiels et multifamiliaux de plus de 20 000 pieds carrés suivent leurs performances énergétiques et rapportent annuellement à la Ville de Seattle.
## 2. PRÉSENTATION DU DATASET
## 2.1 Source et Collection des Données

Source : City of Seattle, Department of Planning and Development
Année : 2016
Plateforme : Kaggle Open Dataset
Type : Données publiques de benchmarking énergétique

## 2.2 Caractéristiques du Dataset

- Nombre de bâtiments : Variable selon le nettoyage
- Période couverte : Année fiscale 2016
- Secteurs inclus : Bureaux, commerces, résidences multifamiliales, hôtels, etc.
  ## 3. MÉTHODOLOGIE
  Données Brutes
    ↓
Exploration Initiale
    ↓
Nettoyage & Prétraitement
    ↓
Analyse Exploratoire (EDA)
    ↓
Analyse de Corrélation
    ↓
Modélisation (Régression Linéaire & Logistique)
    ↓
Évaluation & Interprétation
    ↓
Conclusions & Recommandations
Outils et Technologies

- Langage : Python 3.x
- Bibliothèques principales :

pandas : manipulation de données
numpy : calculs numériques
matplotlib & seaborn : visualisations
scikit-learn : modélisation machine learning
kagglehub : accès aux données Kaggle



- 3.3 Approche Statistique

- Méthode de détection d'outliers : IQR (Interquartile Range)
- Imputation : Médiane pour les valeurs manquantes
- Normalisation : StandardScaler pour les modèles de régression
- Validation : Split train/test (80/20)
  ## 4. NETTOYAGE DES DONNÉES
## 4.1 Problèmes Identifiés
- Valeurs Manquantes
Les données présentent des valeurs manquantes dans plusieurs colonnes clés :

Certains bâtiments n'ont pas de score ENERGY STAR
Données de consommation énergétique incomplètes
Informations sur les émissions GES parfois absentes

- Valeurs Aberrantes (Outliers)

Bâtiments avec des consommations énergétiques extrêmes
Erreurs de saisie possibles
Cas particuliers (bâtiments industriels, événementiels)

## 4.2 Stratégies de Nettoyage
- Étape 1 : Sélection des Variables

Focus sur les variables numériques pertinentes
Exclusion des colonnes avec plus de 50% de données manquantes

- Étape 2 : Suppression des Outliers
Utilisation de la méthode IQR :
Q1 = 25ème percentile
Q3 = 75ème percentile
IQR = Q3 - Q1
Limite inférieure = Q1 - 1.5 × IQR
Limite supérieure = Q3 + 1.5 × IQR
- Étape 3 : Imputation

Méthode : Médiane (robuste aux valeurs extrêmes)
Justification : Préserve la distribution centrale des données

## 4.3 Impact du Nettoyage
- Avant nettoyage :

Nombre de lignes : N (variable)
Données manquantes : X%

- Après nettoyage :

Nombre de lignes : M (après suppression outliers)
Données manquantes : 0%
Pourcentage de données conservées : ~XX%


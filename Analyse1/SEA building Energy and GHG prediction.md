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
## 5. ANALYSE EXPLORATOIRE
## 5.1 Distribution des Variables
- Consommation Énergétique (SiteEnergyUse)

Distribution : Asymétrique positive (skewed right)
Caractéristiques : Majorité des bâtiments consomment modérément, quelques gros consommateurs
Médiane vs Moyenne : La médiane est inférieure à la moyenne, confirmant l'asymétrie

- Intensité Énergétique (SiteEUI)

Utilité : Normalise la consommation par la surface
Interprétation : Mesure l'efficacité énergétique indépendamment de la taille
Variabilité : Grande variation entre bâtiments de types différents

- Score ENERGY STAR

Échelle : 0 à 100 (100 = meilleure performance)
Distribution : Relativement équilibrée avec pics autour de certaines valeurs
Signification : Compare la performance du bâtiment à des bâtiments similaires au niveau national

## 5.2 Statistiques Descriptives
Les statistiques montrent :

- Écarts-types élevés : Grande variabilité entre bâtiments
- Valeurs minimales/maximales : Confirment la diversité du parc immobilier
- Quartiles : Permettent d'identifier les bâtiments performants vs moins performants
## 6. MATRICE DE CORRÉLATION
## 6.1 Analyse des Corrélations
Corrélations Fortes Attendues
Surface et Consommation Totale (r ≈ 0.8 - 0.9)

- Interprétation : Les grands bâtiments consomment plus d'énergie
- Logique : Corrélation naturelle et attendue
- Utilité : Confirme la nécessité de normaliser par la surface

Consommation Énergétique et Émissions GES (r ≈ 0.9 - 0.95)

- Interprétation : Plus un bâtiment consomme, plus il émet de GES
- Importance : Lien direct entre efficacité énergétique et impact climatique
- Politique publique : Justifie les programmes d'amélioration énergétique

Corrélations Intéressantes
Électricité vs Gaz Naturel (r ≈ 0.3 - 0.5)

- Interprétation : Corrélation modérée, suggère des profils énergétiques variés
- Exemples :
Bâtiments avec chauffage électrique vs gaz
Data centers (forte électricité, peu de gaz)
Hôtels (équilibre électricité/gaz)

- Score ENERGY STAR et Intensité Énergétique (r ≈ -0.6 à -0.8)

- Interprétation : Corrélation négative attendue
- Signification : Les bâtiments avec haute intensité énergétique ont des scores plus bas
- Validation : Confirme la pertinence du score ENERGY STAR

## 6.2 Implications pour la Modélisation
- Multicolinéarité

- Variables hautement corrélées peuvent causer des problèmes dans les modèles
Nécessité de sélectionner soigneusement les features
Considération pour des techniques de réduction de dimensionnalité si nécessaire

Sélection de Features
Les corrélations guident le choix des variables explicatives :

Éviter d'utiliser ensemble des variables trop corrélées
Privilégier les variables avec corrélation significative avec la cible
Considérer les aspects pratiques (disponibilité des données)
'''
'print("\n\n5. MATRICE DE CORRÉLATION")
print("-"*80)

# Calculer la matrice de corrélation
correlation_matrix = df_clean.corr()

print("\nMatrice de corrélation:")
print(correlation_matrix)

# Visualisation de la matrice de corrélation
plt.figure(figsize=(12, 10))
sns.heatmap(correlation_matrix, 
            annot=True, 
            fmt='.2f', 
            cmap='coolwarm', 
            center=0,
            square=True,
            linewidths=1,
            cbar_kws={"shrink": 0.8})
plt.title('Matrice de Corrélation - Variables Énergétiques', 
          fontsize=16, fontweight='bold', pad=20)
plt.tight_layout()
plt.savefig('02_matrice_correlation.png', dpi=300, bbox_inches='tight')
print("\n✓ Graphique sauvegardé: 02_matrice_correlation.png")

# Identifier les corrélations les plus fortes
print("\nTop 10 des corrélations les plus fortes:")
corr_pairs = correlation_matrix.unstack()
corr_pairs = corr_pairs[corr_pairs < 1]  # Exclure les auto-corrélations
corr_pairs = corr_pairs.sort_values(ascending=False).drop_duplicates()
print(corr_pairs.head(10))
'''


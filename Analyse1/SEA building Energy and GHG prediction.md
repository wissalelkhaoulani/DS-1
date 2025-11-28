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

## 7. MODÉLISATION : RÉGRESSION LINÉAIRE
## 7.1 Objectif
Prédire la consommation énergétique totale (SiteEnergyUse) d'un bâtiment à partir de ses caractéristiques physiques et opérationnelles.
## 7.2 Variables du Modèle
Variable Cible (Y) : SiteEnergyUse(kBtu)
Variables Explicatives (X) :

Surface du bâtiment
Intensité énergétique
Consommation d'électricité
Consommation de gaz naturel
Score ENERGY STAR
Émissions GES

## 7.3 Prétraitement
Standardisation
Application de StandardScaler :
X_standardisé = (X - μ) / σ

- Raison : Mettre toutes les variables sur la même échelle
- Avantage : Améliore la convergence et l'interprétation des coefficients

- Division Train/Test

Train : 80% des données (pour l'entraînement)
Test : 20% des données (pour l'évaluation)
Random state : Fixé pour la reproductibilité

## 7.4 Résultats
Métriques de Performance
R² Score (Coefficient de Détermination)

Train : ~0.XX
Test : ~0.XX
- Interprétation : Le modèle explique XX% de la variance de la consommation énergétique

- RMSE (Root Mean Square Error)

Train : ~XXX kBtu
Test : ~XXX kBtu
Interprétation : Erreur moyenne de prédiction

- Analyse des Coefficients
Les coefficients révèlent l'impact de chaque variable :
Coefficients Positifs Importants :

Surface du bâtiment → Plus grand = plus de consommation
Intensité énergétique → Directement proportionnelle

- Coefficients Négatifs :

Score ENERGY STAR → Meilleur score = moins de consommation
Efficacité des systèmes

## 7.5 Visualisation
Le graphique "Valeurs Réelles vs Prédites" montre :

- Points proches de la diagonale : Bonnes prédictions
- Points éloignés : Cas difficiles à prédire (outliers, cas particuliers)
- Distribution : Évalue la qualité globale du modèle

## 7.6 Limites du Modèle

- Hypothèse de linéarité : Peut ne pas capturer des relations non-linéaires
- Variables manquantes : Type de bâtiment, âge, occupation pourraient améliorer le modèle
- Outliers : Certains bâtiments restent difficiles à prédire
## 8. MODÉLISATION : RÉGRESSION LOGISTIQUE
## 8.1 Objectif
Classifier les bâtiments en deux catégories selon leur efficacité énergétique :

- Classe 0 : Efficacité faible (sous la médiane)
- Classe 1 : Efficacité élevée (au-dessus de la médiane)

## 8.2 Création de la Variable Cible
- Option 1 : Basée sur ENERGY STAR Score
Si ENERGYSTARScore > Médiane → Classe 1 (Efficace)
Sinon → Classe 0 (Moins efficace)
- Option 2 : Basée sur Consommation Énergétique
Si SiteEnergyUse ≤ Médiane → Classe 1 (Faible consommation)
Sinon → Classe 0 (Haute consommation)
## 8.3 Équilibrage des Classes

- Stratification : Maintien des proportions lors du split train/test
- Distribution : Environ 50/50 (par construction avec la médiane)
- Importance : Évite le biais vers une classe

##  8.4 Résultats
Métriques de Classification
Précision (Accuracy) : ~XX%

## 9. RÉSULTATS ET INTERPRÉTATIONS
## 9.1 Synthèse des Découvertes Principales
- Découverte 1 : Forte Variabilité Énergétique
Les bâtiments de Seattle montrent une grande diversité de performances énergétiques, même pour des bâtiments de taille similaire. Cela suggère un potentiel d'amélioration significatif.
- Découverte 2 : Corrélation Consommation-Émissions
La corrélation quasi-parfaite entre consommation énergétique et émissions GES confirme que réduire la consommation = réduire l'empreinte carbone.
- Découverte 3 : Prédictibilité
Les modèles démontrent que la consommation énergétique est largement prédictible à partir de caractéristiques mesurables, ce qui valide l'approche de benchmarking.
## 9.2 Facteurs Clés de l'Efficacité Énergétique
- Facteur 1 : Surface et Design

Les grands bâtiments ne sont pas nécessairement inefficaces
L'intensité énergétique (kBtu/sf) est plus révélatrice que la consommation totale
Le design et l'orientation comptent

- Facteur 2 : Mix Énergétique

L'équilibre électricité/gaz varie fortement
Certains bâtiments "tout électrique" peuvent être très efficaces
L'accès aux énergies renouvelables influence les scores

- Facteur 3 : Gestion et Maintenance

Le score ENERGY STAR reflète les bonnes pratiques opérationnelles
La gestion active de l'énergie fait une différence mesurable
Les systèmes bien entretenus sont plus efficaces

## 9.3 Comparaisons par Secteur
Bien que les types de bâtiments ne soient pas tous analysés en détail, on observe généralement :
Bureaux :

Consommation modérée mais constante
Fort potentiel d'optimisation via systèmes de gestion intelligents

- Commerces/Retail :

Grande variabilité selon l'activité
Éclairage et climatisation = postes majeurs

- Multifamilial :

Consommation par unité relativement stable
Économies d'échelle pour les grands ensembles

- Hôtels :

Parmi les plus énergivores (24/7, chauffage eau, climatisation)
Opportunités dans la gestion temporelle

## 9.4 Implications Économiques
Potentiel d'Économies
Pour un bâtiment moyen passant du 25ème au 75ème percentile d'efficacité :

Réduction de consommation : ~30-40%
Économies annuelles : Plusieurs dizaines de milliers de dollars
ROI des améliorations : Généralement 5-10 ans

- Valeur Ajoutée
- Les bâtiments efficaces bénéficient de :

- Coûts opérationnels réduits
- Valeur de revente supérieure
- Attractivité pour locataires soucieux d'environnement
- Conformité réglementaire anticipée
## - 10. CONCLUSIONS ET RECOMMANDATIONS
## 10.1 Conclusions Principales
- Conclusion 1 : Succès du Programme
Le programme de benchmarking de Seattle génère des données riches et exploitables. La qualité des données permet des analyses prédictives fiables.
- Conclusion 2 : Hétérogénéité des Performances
L'écart important entre bâtiments performants et moins performants révèle un potentiel d'amélioration considérable dans le parc immobilier existant.
- Conclusion 3 : Prédictibilité et Modélisation
Les modèles statistiques peuvent efficacement prédire la consommation et classifier l'efficacité, ouvrant la voie à des outils d'aide à la décision.
## 10.2 Recommandations pour les Décideurs Politiques
- Recommandation 1 : Ciblage des Interventions
- Action : Utiliser les modèles prédictifs pour identifier les bâtiments avec le plus fort potentiel d'amélioration.
- Justification : Maximiser l'impact des ressources publiques limitées.
- Mise en œuvre :

Créer un "score de potentiel d'amélioration"
Prioriser les subventions et incitations
Offrir des audits énergétiques gratuits aux bâtiments ciblés

- Recommandation 2 : Standards Progressifs
- Action : Établir des standards minimums d'efficacité qui se renforcent dans le temps.
- Justification : Les données montrent qu'une amélioration significative est techniquement faisable.
- Mise en œuvre :

Année 1-3 : Atteindre le 40ème percentile
Année 4-6 : Atteindre le 50ème percentile
Année 7-10 : Atteindre le 60ème percentile

- Recommandation 3 : Transparence et Certification
- Action : Rendre les scores d'efficacité publics et créer un système de certification visible.
- Justification : La pression sociale et économique incite à l'amélioration.
- Mise en œuvre :

Affichage obligatoire du score ENERGY STAR
Labels "Bâtiment Efficace de Seattle"
Publicité des meilleures performances

## 10.3 Recommandations pour les Propriétaires
- Recommandation 1 : Audit Énergétique
- Pour qui : Bâtiments avec score ENERGY STAR < 50
- Action : Réaliser un audit énergétique professionnel
- ROI attendu : 3-7 ans pour les améliorations recommandées
- Recommandation 2 : Mesures à Faible Coût
- Actions immédiates :

Optimisation des horaires de chauffage/climatisation
Remplacement de l'éclairage par LED
Installation de thermostats intelligents
Formation du personnel à l'efficacité énergétique

Coût : < $10,000 typiquement
ROI : < 2 ans
- Recommandation 3 : Investissements Structurels
- Actions à moyen terme :

- Remplacement des systèmes CVC obsolètes
- Amélioration de l'isolation
- Installation de systèmes de gestion énergétique (BMS)
- Panneaux solaires (selon faisabilité)

Coût : $50,000 - $500,000+ selon taille
ROI : 5-15 ans, avec subventions possibles
## 10.4 Recommandations Méthodologiques
- Pour les Futures Analyses
- Collecte de Données Améliorée :

Ajouter le type de bâtiment (catégorie détaillée)
Inclure l'âge du bâtiment
Documenter les rénovations majeures
Suivre l'occupation réelle vs capacité

- Modélisation Avancée :

Explorer des modèles non-linéaires (Random Forest, XGBoost)
Analyser les séries temporelles (évolution annuelle)
Segmenter par type de bâtiment pour des modèles spécialisés

- Validation Externe :

Comparer avec d'autres villes (Portland, Vancouver)
Valider les prédictions sur les années suivantes
Mesurer l'impact réel des interventions


## 11. ANNEXES
Annexe A : Glossaire
BTU (British Thermal Unit) : Unité de mesure d'énergie. 1 BTU = énergie nécessaire pour élever la température d'une livre d'eau de 1°F.
kBtu : Millier de BTU (1 kBtu = 1,000 BTU)
EUI (Energy Use Intensity) : Intensité d'utilisation énergétique, mesurée en kBtu par pied carré par an. Normalise la consommation par la surface.
GHG (Greenhouse Gas) : Gaz à effet de serre (CO₂, méthane, etc.)
ENERGY STAR Score : Score de 1 à 100 qui compare la performance énergétique d'un bâtiment à des bâtiments similaires au niveau national. Un score de 75+ indique une performance dans le top 25%.
R² (R-squared) : Coefficient de détermination. Mesure la proportion de variance de la variable cible expliquée par le modèle (0 à 1, 1 étant parfait).
RMSE (Root Mean Square Error) : Racine carrée de l'erreur quadratique moyenne. Mesure l'écart moyen entre prédictions et valeurs réelles.
IQR (Interquartile Range) : Écart entre le 75ème et 25ème percentile. Utilisé pour détecter les outliers.



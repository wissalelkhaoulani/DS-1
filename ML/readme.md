# Cours de science de données 
# EL KHAOULANI WISSALE
# Ecole national de commerce et de gestion
<img src="WISSALE.jpeg" style="height:264px;margin-right:232px"/> 
**Nom du fichier** : Wine Quality
- **Dataset information** : Two datasets are included, related to red and white vinho verde wine samples, from the north of Portugal. The goal is to model wine quality based on physicochemical tests (see [Cortez et al., 2009], http://www3.dsi.uminho.pt/pcortez/wine/) The two datasets are related to red and white variants of the Portuguese "Vinho Verde" wine. For more details, consult: http://www.vinhoverde.pt/en/ or the reference [Cortez et al., 2009].  Due to privacy and logistic issues, only physicochemical (inputs) and sensory (the output) variables are available (e.g. there is no data about grape types, wine brand, wine selling price, etc.).

These datasets can be viewed as classification or regression tasks.  The classes are ordered and not balanced (e.g. there are many more normal wines than excellent or poor ones). Outlier detection algorithms could be used to detect the few excellent or poor wines. Also, we are not sure if all input variables are relevant. So it could be interesting to test feature selection methods..

- ## CODE
```from ucimlrepo import fetch_ucirepo 
  
# fetch dataset 
wine_quality = fetch_ucirepo(id=186) 
  
# data (as pandas dataframes) 
X = wine_quality.data.features 
y = wine_quality.data.targets 
  
# metadata 
print(wine_quality.metadata) 
  
# variable information 
print(wine_quality.variables) 
```
0          fixed_acidity  Feature   Continuous        None   
1       volatile_acidity  Feature   Continuous        None   
2            citric_acid  Feature   Continuous        None   
3         residual_sugar  Feature   Continuous        None   
4              chlorides  Feature   Continuous        None   
5    free_sulfur_dioxide  Feature   Continuous        None   
6   total_sulfur_dioxide  Feature   Continuous        None   
7                density  Feature   Continuous        None   
8                     pH  Feature   Continuous        None   
9              sulphates  Feature   Continuous        None   
10               alcohol  Feature   Continuous        None   
11               quality   Target      Integer        None   
12                 color    Other  Categorical        None   

               description units missing_values  
0                     None  None             no  
1                     None  None             no  
2                     None  None             no  
3                     None  None             no  
4                     None  None             no  
5                     None  None             no  
6                     None  None             no  
7                     None  None             no  
8                     None  None             no  
9                     None  None             no  
10                    None  None             no  
11  score between 0 and 10  None             no  
12            red or white  None             no  
# his code snippet is used to fetch and inspect a dataset from the UCI Machine Learning Repository using the ucimlrepo library. Here's a breakdown of what each part does:

from ucimlrepo import fetch_ucirepo: This line imports the fetch_ucirepo function from the ucimlrepo library. This function is designed to easily download datasets from the UCI Machine Learning Repository.

wine_quality = fetch_ucirepo(id=186): This line calls the fetch_ucirepo function, passing id=186 to specify that you want to retrieve the 'Wine Quality' dataset (which has UCI ID 186). The fetched dataset, including its features, targets, and metadata, is stored in the wine_quality object.

X = wine_quality.data.features: This line extracts the feature data from the wine_quality object. Typically, these are the input variables used to make predictions. X will be a Pandas DataFrame containing these features.

y = wine_quality.data.targets: This line extracts the target data (also known as labels or output variables) from the wine_quality object. This is what you are trying to predict. y will be a Pandas DataFrame (or Series) containing these targets.

print(wine_quality.metadata): This line prints the metadata associated with the dataset. Metadata includes information like the dataset's name, description, number of instances, number of features, tasks it's suitable for (e.g., Classification, Regression), creators, and more.

print(wine_quality.variables): This line prints detailed information about each variable (feature and target) in the dataset. This typically includes the variable's name, role (e.g., Feature, Target), type (e.g., Continuous, Categorical), description, and whether it has missing values.

In summary, this code is a standard way to load a dataset from UCI into Python and get an initial understanding of its structure and content before proceeding with data analysis or model building.

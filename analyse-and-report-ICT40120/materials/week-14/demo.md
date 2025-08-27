# Week 14 Clustering Lab; Unsupervised Models and Data Challenges

## Learning Objectives

- Understand unsupervised clustering methods and their importance in real-world AI projects
- Apply k-means clustering to real data using pandas and scikit-learn
- Identify and address data challenges such as missing values and imbalance
- Interpret and discuss findings for practical industry applications

---

## 1. Lab Setup and Introduction

- Import necessary Python libraries; pandas, numpy, matplotlib, seaborn, scikit-learn
- Explain that the class will use a classic UCI dataset (the 'Iris' dataset) for an unsupervised clustering exercise

```python
import pandas as pd
import numpy as np
from sklearn.datasets import load_iris
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt
import seaborn as sns

# Load the Iris dataset
data = load_iris()
df = pd.DataFrame(data.data, columns=data.feature_names)
df['species'] = pd.Categorical.from_codes(data.target, data.target_names)
df.head()
```

---

## 2. Exploration and Preparation

- Introduce the concept of 'dirty' or imbalanced real-world data; Not all AI data is clean or well-balanced
- Simulate a real-world issue by injecting some missing values into the dataset

```python
# Inject missing values randomly
np.random.seed(42)
missing_rate = 0.1  # 10 percent of values set to NaN
mask = np.random.rand(*df[data.feature_names].shape) < missing_rate
df.loc[:, data.feature_names] = df[data.feature_names].mask(mask)
df.isnull().sum()
```

- Discussion question; Why does missing data occur in practice? How does it affect ML workflows?

---

## 3. Data Cleaning and Imputation

- Demonstrate a common industry approach; fill missing values using the average (mean) for each feature

```python
# Fill missing values with column means
df_filled = df.copy()
for col in data.feature_names:
    df_filled[col] = df_filled[col].fillna(df_filled[col].mean())
df_filled.isnull().sum()
```

---

## 4. Clustering with K-Means

- Explain the principle behind k-means clustering and industry relevance in LLM data, anomaly detection, or customer segmentation
- Run a k-means clustering experiment with k = 3 (since there are three species in the real dataset)

```python
# Run k-means clustering
features = data.feature_names
kmeans = KMeans(n_clusters=3, random_state=42)
df_filled['cluster'] = kmeans.fit_predict(df_filled[features])

# Visualize clusters
plt.figure(figsize=(8, 6))
sns.scatterplot(
    x='sepal length (cm)', y='sepal width (cm)',
    hue='cluster', palette='Set2', data=df_filled)
plt.title('K-Means Clusters (k=3) on Iris Dataset')
plt.show()
```

---

## 5. Analysis and Discussion of Results

- Compare clusters to true species labels (noting clustering is unsupervised, so labels are not used in training)
- Calculate the contingency table to see how clusters align with true species

```python
pd.crosstab(df_filled['cluster'], df_filled['species'])
```

- Reflection question; Why might the clusters not correspond perfectly to the species? What real-world implications does this have for AI dataset engineering?

---

## 6. Real-World Data Challenges; Imbalance and Scaling

- Briefly create imbalance by downsampling one class; explain the challenge for unsupervised models

```python
# Make dataset imbalanced by reducing one species
df_imbalanced = pd.concat([
    df[df.species == 'setosa'],
    df[df.species == 'versicolor'].sample(frac=0.5, random_state=42),
    df[df.species == 'virginica']
])
print(df_imbalanced['species'].value_counts())
```

- Rerun the k-means analysis on the imbalanced dataset; discuss effects

```python
# Impute again
for col in data.feature_names:
    df_imbalanced[col] = df_imbalanced[col].fillna(df_imbalanced[col].mean())
kmeans_imbalanced = KMeans(n_clusters=3, random_state=42)
df_imbalanced['cluster'] = kmeans_imbalanced.fit_predict(df_imbalanced[features])
pd.crosstab(df_imbalanced['cluster'], df_imbalanced['species'])
```

- Discussion; In industry, how would you mitigate or flag issues from imbalanced or incomplete data when clustering?

---

## 7. Wrap-Up; Best Practices and Industry Takeaways

- Summarize key lessons; Clean, complete data is rare in industry; Clustering can reveal insights but requires careful interpretation
- Highlight links to prior learning (data preprocessing, reporting) and future weeks (scaling to large datasets)
- Practical takeaway; Always document data challenges and cleaning steps for reproducibility and auditability

---

## 8. Reflection and Assessment Preparation

- List three real-world scenarios where clustering is used in industry (e.g. customer segmentation, anomaly detection, topic discovery in large text corpora)
- Briefly write about one obstacle faced in this lab and suggest a possible industry solution
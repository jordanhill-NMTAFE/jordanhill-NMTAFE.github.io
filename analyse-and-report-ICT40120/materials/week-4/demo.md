# Week 4 Demo. First Data Lab. Exploring and Visualizing Data with Python

## Learning Objectives

- Understand how to load and explore a public open dataset in Python.
- Gain practical experience using Jupyter Notebooks for data science workflows.
- Learn foundational tools. pandas, numpy, matplotlib, seaborn.
- Create basic data visuals and interpret their meaning.
- Apply industry-relevant best practices for initial data analysis.

---

## 1. Introduction and Setup

This week we begin hands-on work with real data. You will use practical skills valued by modern AI labs and data-driven companies; loading, exploring, and visualizing open datasets. These tools and workflows are used to analyze, clean, and document the large datasets that drive AI progress.

**Setup steps;**

- Ensure Anaconda or Miniconda is installed.
- Open Anaconda Navigator or use terminal; run `jupyter notebook`.
- Start a new notebook; select Python 3.

---

## 2. Loading an Open Dataset

We will use the "Iris" dataset from the UCI Machine Learning Repository. This dataset is widely used in AI education and allows us to focus on core data analysis skills.

```python
import pandas as pd

# Load the Iris dataset directly from UCI
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data"
col_names = ["sepal_length", "sepal_width", "petal_length", "petal_width", "species"]
df = pd.read_csv(url, header=None, names=col_names)

df.head()
```

---

## 3. Exploring Data with Pandas

Explore the main properties of the dataset.

```python
# Display the shape; number of rows and columns
df.shape
```

```python
# Show column data types
df.dtypes
```

```python
# Show summary statistics for numerical columns
df.describe()
```

```python
# Preview the first 10 rows
df.head(10)
```

---

## 4. Basic Numpy Operations

Understand arrays; perform simple computations.

```python
import numpy as np

# Convert a series to numpy array and calculate mean
sepal_lengths = df["sepal_length"].values
np.mean(sepal_lengths)
```

---

## 5. Visualizing Data with Matplotlib

Start with a simple histogram and scatter plot.

```python
import matplotlib.pyplot as plt

# Histogram of sepal lengths
plt.hist(df['sepal_length'], bins=20, color='skyblue')
plt.title("Distribution of Sepal Lengths")
plt.xlabel("Sepal Length (cm)")
plt.ylabel("Frequency")
plt.show()
```

```python
# Scatter plot of sepal vs. petal length
plt.scatter(df['sepal_length'], df['petal_length'], c='green')
plt.title("Sepal vs. Petal Length")
plt.xlabel("Sepal Length")
plt.ylabel("Petal Length")
plt.show()
```

---

## 6. Enhanced Visuals with Seaborn

Use seaborn for advanced statistical plots.

```python
import seaborn as sns

# Pairplot for all features, colored by species
sns.pairplot(df, hue='species')
plt.suptitle("Pairwise Feature Relationships", y=1.02)
plt.show()
```

```python
# Boxplot example: Sepal length by species
sns.boxplot(x="species", y="sepal_length", data=df)
plt.title("Sepal Length Distribution by Species")
plt.show()
```

---

## 7. Practical Exercise

**Try these tasks on your own;**

- Calculate and print the average petal width for each iris species.
- Create a bar chart comparing the mean sepal width of each species.
- Find and print how many missing values (if any) are in each column.

---

## 8. Troubleshooting and Best Practices

- If a dataset link fails, check your internet or use a local CSV copy.
- Watch for missing values (`NaN`). Use `df.isnull().sum()` to count missing items.
- Always check data types before analysis. Use `df.dtypes`.
- Reset the notebook kernel if plots don’t show; save work first.

---

## 9. Industry Insight

These exploratory skills are essential in AI research, data engineering, and at tech companies handling real-world datasets. Data visualization helps communicate findings and spot data issues early, supporting reproducible workflows and responsible AI practice.

---

## 10. Reflection and Assessment Prep

- What insights did you learn about the Iris dataset today?
- Where in a real company or AI project would you use these tools?
- What problems might occur if you skip data exploration?

---

## 11. Summary and Next Steps

Today you got hands-on with Python's core data tools; pandas, numpy, matplotlib, and seaborn. You learned to load, inspect, and visualize open data using industry-standard environments. Next week we will focus on dataset documentation and reporting standards, building on today’s skills to ensure your work is clear, organized, and reusable.
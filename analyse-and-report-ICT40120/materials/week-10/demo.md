# Week 10 Lab Walkthrough  
## Exploratory Data Analysis (EDA) on a UCI ML Dataset  
**Learning Objectives**
- Gain hands-on experience with EDA, using Jupyter and industry-standard Python tools  
- Learn to load, explore, and visualize a public dataset; identify trends, outliers, and key findings  
- Prepare and present EDA results in a structured, industry-relevant format  

---

## 1. Introduction and Setup  

- Brief overview of EDA and its relevance in AI/data engineering roles;  
- Outline connections between EDA and workplace tools/standards (e.g. Python, pandas, reproducibility);  
- Highlight assessment links and importance for industry compliance and project workflow.

```python
# Cell: Lab Environment Setup
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set up basic plotting style
sns.set(style='whitegrid')
```

---

## 2. Load Dataset  

- Select a real-world dataset from the UCI Machine Learning Repository;  
- Demonstrate data import, preview, and documentation review;  
- Discuss open data best practices and versioning (from previous weeks).

```python
# Cell: Dataset Loading
# Example: UCI's 'Wine Quality' dataset (red wine), commonly used in EDA demos
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/wine-quality/winequality-red.csv"
df = pd.read_csv(url, sep=';')

# Preview rows and structure
df.head()
```

---

## 3. Initial Data Exploration  

- Summarize key dataset features; use head, info, describe;  
- Discuss data types, non-null counts, look for initial anomalies.

```python
# Cell: Dataset Summary
df.info()
df.describe()
df.isnull().sum()  # Check for missing values
```

---

## 4. Visualising Distributions and Key Features  

- Plot distributions of selected variables;  
- Use boxplots, histograms to identify outliers or unusual trends;  
- Reference workplace reasons for visualization (communication, QA, analysis, reproducibility).

```python
# Cell: Distribution Visualization
fig, axs = plt.subplots(1, 2, figsize=(12, 4))
sns.histplot(df['alcohol'], bins=20, kde=True, ax=axs[0])
axs[0].set_title('Alcohol Content Distribution')
sns.boxplot(x=df['quality'], y=df['alcohol'], ax=axs[1])
axs[1].set_title('Alcohol by Wine Quality')
plt.tight_layout()
plt.show()
```

---

## 5. Identifying Trends, Outliers, and Correlations  

- Use scatterplots/correlation matrices to examine feature relationships;  
- Document findings with markdown commentary, relating to responsible data analysis in AI.

```python
# Cell: Correlation Analysis
corr_matrix = df.corr()
plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix, annot=True, fmt=".2f", cmap='coolwarm', square=True)
plt.title('Correlation Matrix')
plt.show()

# Cell: Scatterplot of Two Features
sns.scatterplot(data=df, x='alcohol', y='quality')
plt.title('Alcohol vs. Quality')
plt.show()
```

---

## 6. Presenting EDA Findings (Industry Practice)  

- Summarize main trends, anomalies, and potential data quality issues;  
- Structure findings as you would for a research report or industry documentation.

**Example Markdown Cell:**  
- Alcohol content is positively correlated with wine quality;  
- Outliers detected in sulphates and residual sugar (see boxplots);  
- Dataset is clean, with no missing values, but some variables are skewed;  
- Further exploration could involve feature engineering or ML modeling steps.

---

## 7. Practical Exercises  

- Students select another feature or pair of features to explore;  
- Create their own visualizations (histogram, boxplot, scatterplot);  
- Reflect on implications for AI projects (e.g. model bias, interpretability).

**Prompt:**  
- Choose two features, visualize their relationship, and describe any patterns or outliers you observe;  
- Consider and note: How might this finding influence a machine learning workflow?

---

## 8. Troubleshooting and Best Practices  

- Discuss common issues (missing data, poor labels, unbalanced classes);  
- Point out best practices for EDA in industry: clear documentation, data versioning, reproducibility with Jupyter;  
- Encourage students to write clear markdown explanations alongside each code block.

---

## 9. Reflection and Prep for Assessment  

- Remind students this lab forms the process/method for the Week 14 EDA assessment on another UCI dataset;  
- Suggest further reading on dataset documentation standards and open data ethics, as per course/industry standards;  
- Reflection prompt: What was most surprising about this dataset, and how would you communicate key findings to a non-technical audience?

---

## 10. Summary and Next Steps  

- Recap: Industry focus on reproducible, well-documented, and ethically evaluated data analysis;  
- Next week: Turning EDA insights into structured reports and data science deliverables;  
- Highlight importance of industry tools (pandas, numpy, matplotlib, seaborn), open data practices, and communication skills.
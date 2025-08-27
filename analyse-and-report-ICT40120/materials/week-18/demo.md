# Week 18 Demo: Course Synthesis and Knowledge Test Preparation

## 1. Setup and Introduction

Welcome to Week 18. This session focuses on consolidating your learning and preparing you for the upcoming knowledge-based assessment. By the end of this workshop, you will;
- Review foundational and advanced concepts covered throughout the course.
- Practice with a mock knowledge test to identify gaps and reinforce critical knowledge areas.
- Engage in hands-on coding exercises reflecting workplace tasks in data science and AI dataset engineering.
- Participate in a Q&A and receive targeted coaching to maximize assessment readiness.

---

## 2. Mock Knowledge Test

Answer each of the following questions. Check the explanation after each answer to self-assess and identify gaps.

### Q1. What is an open dataset and how does its structure benefit AI model development?

*Write your answer below; then check the model answer.*

**Model Answer**;  
An open dataset is a collection of data available publicly, usually with minimal restrictions. Its standardized, well-documented structure ensures transparency and reproducibility, allowing AI models to be trained and evaluated consistently.

---

### Q2. Name two common tools for large-scale data analysis in Python. What are their primary uses?

*Write your answer below; then check the model answer.*

**Model Answer**;  
pandas is used for data manipulation and analysis with structured data (tables, CSV, DataFrames); numpy is used for efficient numerical computations on large arrays and matrices.

---

### Q3. Explain the importance of dataset documentation and version control in industry projects.

*Write your answer below; then check the model answer.*

**Model Answer**;  
Thorough dataset documentation enables others to understand and use the dataset correctly; version control tracks changes, ensuring reproducibility and accountability across teams when working on evolving datasets.

---

### Q4. Describe a real-world example where data ethics or privacy could directly impact an AI project.

*Write your answer below; then check the model answer.*

**Model Answer**;  
Developing a facial recognition model using unconsented, scraped images from the web raises privacy violations; failing to address this could lead to legal issues and loss of public trust.

---

### Q5. Using the code snippet below, what does the function accomplish?

```python
import pandas as pd
df = pd.read_csv("open_data.csv")
df_clean = df.dropna().drop_duplicates()
print(df_clean.shape)
```

**Model Answer**;  
The function reads a CSV into a DataFrame, then removes any rows with missing values and duplicates, finally printing the shape (rows, columns) of the cleaned dataset.

---

*Continue to use this self-test format for additional knowledge areas as needed before proceeding to coding review/demos.*

---

## 3. Industry Case Review and Mini-Demos

### Review: Loading and Documenting a Dataset

**Task**;  
Load a public dataset (such as one from HuggingFace or UCI ML Repository); Generate a basic data dictionary describing column meanings and data types.

```python
import pandas as pd

# Example: UCI Wine Quality Dataset
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/wine-quality/winequality-red.csv"
df = pd.read_csv(url, sep=';')
data_dictionary = pd.DataFrame({
    "Column": df.columns,
    "Type": [df[col].dtype for col in df.columns],
    "Example_Value": [df[col].iloc[0] for col in df.columns]
})
display(data_dictionary)
```

**Description**;  
This code demonstrates fetching a real-world dataset, checking structure, and documenting key features, reflecting industry best practices for dataset onboarding.

---

### Demo: Handling Missing Data

**Task**;  
Identify and report missing values, then impute missing data for numeric columns.

```python
missing_summary = df.isnull().sum()
print("Missing values per column;", missing_summary)

# Impute missing values (if any) using column mean
df_imputed = df.fillna(df.mean(numeric_only=True))
```

**Description**;  
Reporting and imputing missing values reduces data quality issues and ensures sound machine learning outcomes.

---

### Demo: Quick Exploratory Data Analysis (EDA)

**Task**;  
Visualize feature distributions using industry-standard tools.

```python
import matplotlib.pyplot as plt

df.hist(bins=20, figsize=(12, 8))
plt.suptitle('Feature Distributions in Wine Quality Data')
plt.show()
```

**Description**;  
This EDA step provides quick insights into feature ranges and potential outliers, supporting informed preprocessing for AI workflows.

---

### Demo: Simple ML Application (Classification)

**Task**;  
Apply logistic regression to predict wine quality category.

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Binary classification; quality >= 7 is 'good'
df['good_quality'] = (df['quality'] >= 7).astype(int)

X = df.drop(['quality', 'good_quality'], axis=1)
y = df['good_quality']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
print("Test set accuracy;", accuracy_score(y_test, y_pred))
```

**Description**;  
This classification pipeline mirrors real world workplace tasks, from data preparation to model evaluation.

---

## 4. Practical Exercises

1. From a provided open dataset, document five potential sources of bias and propose one mitigation strategy for each.
2. Implement a data versioning workflow using a tool such as DVC or Git-LFS; track changes to raw vs. cleaned data files and reflect on traceability in team settings.
3. Formulate three key questions that a compliance officer would need answered to verify your project's adherence to data privacy legislation.
4. Re-analyze a failed ML experiment from your previous project; identify the data or modelling issue, document it, and explain how you resolved it.

---

## 5. Reflection and Self-Assessment Prompts

- List three ways that your Python and ML skills developed over the course connect to typical AI team workflows in industry.
- Reflect on one ethical dilemma you encountered or discussed during the course, and describe how you would address it in a professional setting.
- Identify an aspect of your data documentation that you would improve for an industry audience, explaining your reasoning.
- What feedback on your project work so far has helped you most in developing your dataset analysis or reporting skills?

---

## 6. Q&A and Final Assessment Checklist

Open Q&A;  
- Bring unresolved conceptual, technical, or project challenges for discussion.
- Share practical workplace scenarios for instructor or peer feedback.

Assessment Preparation Checklist;  
- Ensure all competency requirements for units BSBDAT501, ICTDAT401, and BSBCRT404 are addressed in your submissions.
- Review and complete all project documentation (including data dictionaries, version history, and ethical considerations).
- Practice with additional knowledge review/test questions before formal assessment in Week 18.

---

## Summary and Next Steps

This session is your opportunity to consolidate learning, clarify assessment expectations, and resolve outstanding challenges. Effective preparation draws on course content, practical skills, and industry standards for AI dataset engineering. Next steps; complete final assessments, seek feedback proactively, and prepare for workplace-based application of your learning. Week 19 will focus on reassessment opportunities and final project support if required.
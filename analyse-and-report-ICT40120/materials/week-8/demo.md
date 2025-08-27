# Week 8 Demo. Creating Reproducible Data Pipelines

## Learning Objectives
- Build simple reproducible data pipelines using open data.
- Practice data and code versioning with tools used in industry.
- Document all steps clearly in markdown following best practice.
- Understand workplace expectations for storing and securing data workflows.

---

## Prerequisites
- Basic use of pandas, numpy, and Jupyter from Weeks 4 and 7.
- Awareness of open dataset sources and documentation (Weeks 2, 5).
- Data cleaning skills from Week 7.

---

## 1. Introduction to Data Versioning and Reproducibility

A reproducible data pipeline means anyone (including you, in the future) can run your steps and get the same result.  
Versioning helps track changes to your code and data. This is essential in AI and data science teams to avoid data leaks, loss of work, and ensure trust in results.

---

## 2. Creating a Simple Data Pipeline (Hands-On)

We will use the Iris dataset (UCI ML Repository) for this demonstration.

### Step 1. Load and Inspect the Data

```python
import pandas as pd

url = "https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data"
cols = ["sepal_length", "sepal_width", "petal_length", "petal_width", "class"]
df = pd.read_csv(url, names=cols)

df.head()
```

---

### Step 2. Basic Data Cleaning

- Remove duplicate rows.
- Handle any missing values.

```python
df = df.drop_duplicates()
df = df.dropna()
df.info()
```

---

### Step 3. Save the Cleaned Data

We should save each new dataset version with a clear name and date.

```python
import datetime

today = datetime.date.today().strftime('%Y%m%d')
filename = f"iris_cleaned_{today}.csv"
df.to_csv(filename, index=False)
```

---

## 3. Versioning Your Code and Data

In industry, we use tools to track changes and enable collaboration.

- **Option 1. Git**; For versioning code and small datasets.
- **Option 2. DVC (Data Version Control)**; For larger datasets and pipelines.

For this demo, we will use Git for basic versioning.

---

### Step 4. Initialize a Git Repository (Terminal Example)

- Go to your project folder and run:
```bash
git init
git add demo_notebook.ipynb iris_cleaned_YYYYMMDD.csv
git commit -m "Initial cleaned dataset and pipeline notebook"
```
- Each change should have a short, clear message.

*(Replace YYYYMMDD with today's date.)*

---

#### Discussion

- What is the purpose of commit messages?
- How would a team use branches for different experiments?

---

### Step 5. Document Your Process in Markdown

Best practices in industry include:

- Write clear markdown for each code and analysis step.
- List inputs, outputs, versions, and data sources.
- Always describe problems or decisions (e.g., why certain rows were removed).

#### Example:

```markdown
## Data Cleaning
- Source: UCI ML Iris dataset (link above)
- Removed duplicates (none found), dropped missing values (none found).
- Saved versioned file: iris_cleaned_YYYYMMDD.csv
- Code and outputs in this notebook, versioned with Git.
```

---

### Step 6. Store Your Work Securely

Workplaces require data to be stored in approved locations.

- Use institutional storage or secure cloud; never store confidential or large datasets in personal accounts.
- Understand and follow your organization’s data policies.

#### Exercise

Write a markdown section explaining where and how your files would be stored and who has access in a real company.

---

## 4. Reflection and Best Practices

- How does versioning code and data help teams work together?
- What could go wrong if files are not versioned or well documented?
- Why does the industry require secure, reproducible pipelines especially for AI data?

---

## 5. Next Steps

- Practice using DVC on a larger dataset in the next session.
- Review this notebook; make sure each code step is matched with a markdown description.
- Commit any changes as you go.

---

## Summary

- You created a basic reproducible data pipeline.
- You learned data and code versioning using Git.
- You documented your work as required in modern AI and data engineering teams.
- You discussed secure data storage and compliance.

---
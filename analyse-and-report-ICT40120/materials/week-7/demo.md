# Week 7 Demo; Data Cleaning Lab; Preprocessing with Pandas

---

## Learning Objectives

- Understand common data cleaning tasks for AI and large datasets;  
- Learn to handle missing values, identify and manage outliers, and apply essential data transformations using pandas;  
- Prepare data for later analysis and machine learning applications;  
- Build confidence in interpreting, assessing, and cleaning real-world data.

---

## Lab Agenda

1. Setup and Introduction
2. Theoretical Overview; Why Data Cleaning Matters in Large Scale AI Datasets
3. Demo; Identifying and Handling Missing Values
4. Demo; Detecting and Addressing Outliers
5. Demo; Data Type Conversion and Feature Transformation
6. Practical Mini-Exercise; Clean a Realistic Sample Dataset
7. Industry Case Study; Cleaning a Public AI Dataset Sample
8. Troubleshooting Common Issues; Best Practices in Data Cleaning Workflows
9. Reflection; Self-Assessment and Next Steps

---

## 1. Setup and Introduction

Welcome to Week 7.  
This session will focus on essential data cleaning tasks using pandas in Python; skills needed for all modern AI and data engineering roles.  
You will load, inspect, and prepare data using industry-standard workflows used by tech companies, research teams, and open data consortia.

```python
# Standard setup
import pandas as pd
import numpy as np

# Display options for easier exploration
pd.set_option("display.max_columns", 10)
pd.set_option("display.width", 80)
```

---

## 2. Why Data Cleaning is Critical for AI

- Raw or collected data is rarely perfect;  
- Issues such as missing data, inconsistent types, and outliers can skew AI models;  
- Large scale datasets (like LAION-5B, COCO) are documented with known imperfections;
- Cleaning ensures reliable, transparent analysis and reproducible results;
- Complies with industry standards for responsible AI and data use.

---

## 3. Demo; Identifying and Handling Missing Values

Let us start by loading a small sample dataset with common problems;  
This simulates the kinds of issues found in open datasets used for AI:

```python
# Sample data with missing values
data = {
    "image_id": [1, 2, 3, 4, 5],
    "caption": ["A dog runs", np.nan, "Two cats sleep", "A bird flies", ""],
    "score": [0.98, 0.76, None, 1.0, 0.89]
}
df = pd.DataFrame(data)
df
```

### Detecting missing values

```python
# Find missing values
df.isnull()
```

```python
# Summary count of all missing values
df.isnull().sum()
```

### Cleaning options

- Remove rows with any missing values;  
- Fill missing values with a placeholder or estimate.

```python
# Drop missing rows
df_cleaned = df.dropna()
df_cleaned

# Fill missing captions
df["caption"] = df["caption"].replace("", np.nan)
df["caption"] = df["caption"].fillna("No caption provided")
df
```

---

## 4. Demo; Detecting and Addressing Outliers

Outliers can distort analysis and model training;  
Industry often uses simple quantile or z-score methods;

```python
# Add example outlier to the dataset
df.loc[5] = [6, "A noise example", 500] # Clearly unrealistic score

# Detect outliers using interquartile range
q1 = df["score"].quantile(0.25)
q3 = df["score"].quantile(0.75)
iqr = q3 - q1
lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

outliers = df[(df["score"] < lower_bound) | (df["score"] > upper_bound)]
outliers

# Optionally remove outliers
df_no_outliers = df[~((df["score"] < lower_bound) | (df["score"] > upper_bound))]
df_no_outliers
```

---

## 5. Demo; Data Type Conversion and Feature Transformation

Correct data types improve efficiency and analytical accuracy;  
String categories, numeric conversions, and normalization are standard steps;

```python
# Check data types
df.dtypes

# Convert columns as needed
df["image_id"] = df["image_id"].astype(str)
df["score"] = pd.to_numeric(df["score"], errors="coerce")

# Min-Max normalization for score column
score_min = df["score"].min()
score_max = df["score"].max()
df["score_normalized"] = (df["score"] - score_min) / (score_max - score_min)

df.head()
```

---

## 6. Practical Mini-Exercise; Clean a Realistic Sample Dataset

Download the supplied sample data ('sample_open_data.csv') from the course resources.  
Perform the following tasks;  
- Identify any missing values and handle appropriately  
- Find and deal with at least one outlier  
- Convert columns to correct data types  
- Create a new normalized feature column ('score_scaled')  
- Summarize your cleaning steps; explain your choices

Use a new notebook cell for your solution.

---

## 7. Industry Case Study; Cleaning a Public AI Dataset Sample

Many open datasets for AI (such as LAION-5B or COCO) require substantial cleaning before use;
For example, in LAION image-caption data, missing captions or extreme scores are common issues;  
- Review the short LAION sample data provided in the resources  
- Apply your cleaning and transformation steps  
- Discuss how these realistically impact downstream ML or AI work

---

## 8. Troubleshooting Common Issues and Best Practices

- Always check data types after cleaning;  
- Document each cleaning step for reproducibility;  
- Use assert statements to validate cleaning if applicable;  
- Where possible, automate cleaning scripts for large datasets;  
- Never delete or change original data; always work on a copy.

---

## 9. Reflection and Self-Assessment

- What challenges did you encounter in the cleaning process?  
- How do your cleaning decisions affect the reliability of later ML analysis?  
- How might you automate these steps for much larger datasets?  
- List two industry standards or best practices you followed.

---

## Next Steps

Next week, you will learn about documenting, versioning, and storing data workflows;  
These skills will ensure your cleaned datasets remain useful, reproducible, and ready for collaboration in real-world AI or data science teams.
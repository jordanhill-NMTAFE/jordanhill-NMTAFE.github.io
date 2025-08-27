# Week 6 Workshop; Data Bias and Quality Group Investigation

## Learning Objectives
- Identify and explain the main dimensions of data quality; timeliness, authority, relevance, completeness, and accuracy  
- Detect common types of bias in datasets; selection bias, labeling bias, and sampling bias  
- Assess how quality issues and biases impact real AI applications and outcomes  
- Practise critical evaluation skills by investigating an authentic open dataset using Python  

---

## Agenda
1. Setup; review goals and expectations for the session  
2. Introduction to data quality and typical data biases  
3. Guided group activity; investigate an open dataset, identify issues, and discuss impacts  
4. Debrief and class discussion; share findings  
5. Instructor summary, Q and A, and reflections  

---

## 1. Setup and Introduction

Explain the industry importance of evaluating data quality and bias; 
- AI systems depend on high-quality, unbiased data  
- Bias and quality issues can lead to unfair, inaccurate, or invalid AI decisions  
- Real industry roles require these evaluation skills to ensure responsible AI development  
Refer to standards from Week 5 (datasheets for datasets, documentation) and ethics from Week 3  

---

## 2. Concepts; Data Quality and Data Bias

### Data Quality Dimensions
- Timeliness; is the data up to date?  
- Authority; does the source have expertise?  
- Relevance; is the data suitable for your application?  
- Completeness; are data records and fields filled?  
- Accuracy; are data values correct and reliable?  

### Types of Data Bias
- Selection bias; how data is chosen may exclude key groups  
- Sampling bias; how samples are collected can skew results  
- Label bias; human or systemic errors in assigning data labels  
- Confirmation bias; keeping records that support an assumption  

---

## 3. Guided Practical Example (Instructor-led)

Select a small, real open dataset (for example; UCI Adult Income dataset, or a small subset of LAION-5B metadata).

### Overview of Dataset
- Display and explain basic dataset info  
- Describe intended AI applications  

```python
import pandas as pd

# Example using Adult Income dataset (replace with a chunk of an open image or text AI dataset if preferred)
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.data"
cols = ["age", "workclass", "fnlwgt", "education", "education_num", "marital_status", 
        "occupation", "relationship", "race", "sex", "capital_gain", "capital_loss", 
        "hours_per_week", "native_country", "income"]

df = pd.read_csv(url, header=None, names=cols, na_values=" ?", skipinitialspace=True)
df.head(5)
```

---

### Demonstrate investigation of a few quality and bias issues

```python
# Check for missing values (completeness)
df.isnull().sum()
```

```python
# Check for class imbalance in target variable (bias, relevance)
df["income"].value_counts(normalize=True)
```

```python
# Check for demographic imbalance (potential bias)
df["sex"].value_counts(normalize=True)
df["race"].value_counts(normalize=True)
```

```python
# Optional; visualize bias
import matplotlib.pyplot as plt
df["sex"].value_counts().plot(kind="bar", title="Gender distribution in dataset")
plt.show()
```

Explain;
- What imbalances were found  
- How missing or skewed data can affect AI models trained using this dataset  

---

## 4. Group Investigation Task

Split into small groups (2-4 people); each group gets a dataset sample (same or different, e.g., Adult Income, subset of COCO metadata).

**Each group will**;
- Review dataset documentation and features  
- Use Python (pandas) to check for missing data, imbalance, or other quality issues  
- Identify at least one potential source of bias  
- Discuss how these issues might impact an AI system built using this data  

**Suggested steps**;
1. Load your data sample and inspect the first few rows  
2. Check for missing or obviously inaccurate values  
3. Check target/class distributions (imbalances)  
4. Check demographic or feature breakdowns  
5. Write a short note; what quality/bias issues did you find? How could these affect an AI application?  

---

### Practical Coding Example (to guide student groups)
```python
# Replace with dataset sample given to your group
df = pd.read_csv("group_dataset_sample.csv")
print(df.info())
print(df.head())
print(df.isnull().sum())

# Example: Explore a protected attribute (like 'sex', 'race', 'category')
print(df["sex"].value_counts())
print(df["income"].value_counts())
```

---

## 5. Class Debrief and Reflection

Each group;
- Shares the most significant data quality or bias issue they found  
- Suggests at least one way to address or mitigate the issue (e.g., resampling, imputation, documentation improvement)  

Class discussion prompts;
- How could these issues affect a real-world AI system, such as a credit scoring or image recognition tool?  
- What steps should an AI professional take to document and manage these risks?  

---

## 6. Instructor Summary and Wrap-up

- Data quality and bias assessment is essential for reliable, fair AI outcomes  
- These skills are required in all major AI and data industry roles  
- Next week will focus on cleaning and preprocessing data to directly address some of the issues you found today  
- Review your group's notes and write down; What is one question you still have about bias or data quality?

---

## Reflection/Assessment Questions

1. List two key dimensions of data quality and explain why they matter in AI  
2. Describe at least one type of data bias found in your group investigation  
3. Give an example of how a bias or quality issue might impact an AI application  
4. Suggest one step to remediate a data quality or bias issue in the dataset you explored  

---
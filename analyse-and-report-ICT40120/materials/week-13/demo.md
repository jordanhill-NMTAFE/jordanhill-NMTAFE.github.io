# Week 13 Demo — Training a Simple Classifier on Open Data (Hands-On Guide)

## Session Overview

- Learn how to apply supervised machine learning basics using an open dataset with scikit-learn.
- Gain practical experience in preparing data, splitting into train and test sets, training a simple model, and interpreting results.
- Build skills directly relevant to industry datasets and upcoming assessments.
- Emphasize reproducible, transparent, and ethical data workflows as required in modern AI roles.

---

## Learning Outcomes

- Know how to load and inspect open datasets using Python and standard ML libraries.
- Prepare data for classification tasks, including cleaning and visualization.
- Split data for training and testing to prevent overfitting.
- Train a simple classification model and evaluate its performance.
- Interpret model outputs using industry-standard metrics.
- Understand best practices for transparent, reproducible machine learning.

---

## 1. Setup and Preparation

- Ensure you have Python 3.x, Jupyter Notebook, scikit-learn, pandas, matplotlib, and seaborn installed.
- You can use Anaconda or pip; ask your lecturer if you need help with your environment.

```python
# Install necessary packages if not already available
!pip install scikit-learn pandas matplotlib seaborn
```

---

## 2. Load and Inspect an Open Dataset

- For reproducibility in this demo, we use the famous "Iris" dataset, available directly from scikit-learn.
- In industry, similar steps apply to larger or more complex datasets (e.g., CSVs, open repositories, HuggingFace).

```python
from sklearn.datasets import load_iris
import pandas as pd

# Load data
iris = load_iris(as_frame=True)
df = iris.frame

# Inspect the first few rows
df.head()
```

---

## 3. Basic Data Exploration

- Review dataset features and target (label).
- Visualize class (species) distribution to check for class balance.

```python
print(df.info())
print(df.describe())

# Quick class distribution
print(df['target'].value_counts())
df['target'].plot(kind='hist', title='Class Distribution')
```

---

## 4. Prepare and Split the Data

- We split the data into features (X) and target labels (y).
- Use train_test_split to create separate training and test sets (recommended industry practice).

```python
from sklearn.model_selection import train_test_split

X = df.drop('target', axis=1)
y = df['target']

# Create 70/30 split for training and testing
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

print("Training samples:", X_train.shape[0])
print("Test samples:", X_test.shape[0])
```

---

## 5. Train a Simple Classifier

- Use DecisionTreeClassifier for interpretability and ease of use (industry-standard starting point).
- Fit the classifier on the training data.

```python
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)
```

---

## 6. Evaluate Classifier Performance

- Predict labels for the test set and evaluate performance using accuracy, confusion matrix, and classification report.
- Discuss what these metrics mean and how they are used in industry.

```python
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

y_pred = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
print("Classification Report:\n", classification_report(y_test, y_pred, target_names=iris.target_names))
```

---

## 7. Interpret Results and Identify Pitfalls

- Review metrics and discuss possible sources of error (overfitting, class imbalance, insufficient features).
- Encourage students to consider ethical and transparent reporting (avoid overclaiming accuracy, document data prep and decisions).

---

## 8. Practical Exercise

- Adjust the max_depth hyperparameter of the DecisionTreeClassifier and observe any changes in accuracy.
- Try using another model (e.g., LogisticRegression) and compare results.

```python
# Change tree depth
model2 = DecisionTreeClassifier(max_depth=2, random_state=42)
model2.fit(X_train, y_train)
print("Accuracy with max_depth=2:", accuracy_score(y_test, model2.predict(X_test)))
```

---

## 9. Reflection and Industry Application

- Discuss how similar steps are used in real AI projects for classifying large-scale data (images, text, etc.).
- Highlight importance of transparent, well-documented processes for professional roles.
- Prompt: What issues might occur with larger, messier real-world datasets? How could you address them?

---

## 10. Troubleshooting and Best Practices

- Always check for missing data and proper class balance before training.
- Random seeds (random_state) ensure reproducibility.
- Use comments and clear variable names; document all steps and decisions.
- Save your notebook regularly and annotate key outputs.

---

## 11. Summary and Next Steps

- Today, you built a complete (if simple) supervised ML pipeline from data exploration to model evaluation.
- Next week, you will work with more complex datasets and advanced model selection.
- Review your notebook and practice repeating the workflow with another open dataset from scikit-learn (e.g., wine, breast cancer).
- Prepare questions and challenges for discussion.

---

## 12. Assessment Link

- The skills practiced today will be part of your Week 14 applied ML assessment using a UCI Machine Learning dataset.
- Ensure you save your notebook and notes for future reference and possible reassessment.
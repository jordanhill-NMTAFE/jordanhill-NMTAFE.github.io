# Week 1 Demo; How Data Drives AI; Demonstrating Large Dataset Impact

## Learning Objectives
- Understand how dataset size and quality affect AI model performance.
- Identify what open datasets are and how they are used in real AI projects.
- Observe and discuss hands-on examples using real data.

---

## 1. Welcome and Setup

- Introduce course focus; real-world, large-scale AI datasets and practical skills.
- Outline session activities; live demo, discussion, mini-coding lab.
- Ensure every student can access Jupyter Notebooks and basic Python tools.

---

## 2. Why Data Matters in AI

- AI learns patterns by analyzing data; larger, cleaner datasets = better results.
- Modern systems need millions of examples (e.g., for language translation or image recognition).
- Industry examples; OpenAI uses huge datasets to train chat models; image recognition in self-driving cars uses millions of pictures.
- Start a quick group brainstorm; list AI you use every day that relies on large datasets.

---

## 3. What Are Open Datasets?

- Open datasets are freely accessible data collections; used by both companies and researchers.
- Key examples include LAION-5B (images and text used for AI vision/language) and COCO (image labeling for ML).
- Open datasets support transparency, reproducibility, and responsible AI.
- Students review dataset websites briefly; note scale (billions of images/texts).

---

## 4. Demo; Small vs Large Dataset in Practice

### Activity Overview

- Use a simple, well-known dataset (MNIST digits or UCI Iris dataset).
- Show what happens when you train a machine learning model on a small subset versus a larger subset of the same data.
- Discuss real-world implications; self-driving car trained on 100 vs 1,000,000 images.
- Allow students to predict what will happen; which model will perform better and why.

### Code Example (Python, Jupyter)

```python
import numpy as np
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Load dataset
digits = load_digits()

# Create small and large training sets
X_small, _, y_small, _ = train_test_split(digits.data, digits.target, train_size=0.1, stratify=digits.target, random_state=42)
X_large, _, y_large, _ = train_test_split(digits.data, digits.target, train_size=0.8, stratify=digits.target, random_state=42)

# Define and train models
model_small = LogisticRegression(max_iter=1000)
model_large = LogisticRegression(max_iter=1000)

model_small.fit(X_small, y_small)
model_large.fit(X_large, y_large)

# Evaluate on test data
_, X_test, _, y_test = train_test_split(digits.data, digits.target, test_size=0.2, stratify=digits.target, random_state=42)

y_pred_small = model_small.predict(X_test)
y_pred_large = model_large.predict(X_test)

print("Accuracy with small dataset:", accuracy_score(y_test, y_pred_small))
print("Accuracy with large dataset:", accuracy_score(y_test, y_pred_large))
```
- Students compare results; discuss why larger dataset improves results.
- Visualize a few predictions with images to drive the point home.
  
---

## 5. Industry Case Study; LAION-5B and COCO

- Very large datasets like LAION-5B enable advanced AI (e.g., image search, text-to-image models like DALL-E).
- Real projects; Google Photos and OpenAI models leverage millions/billions examples.
- Discuss issues of bias, quality, and ethics (set up for future weeks).
- Show a short video or slide of a modern AI system referencing open datasets.

---

## 6. Mini Challenge

- Students form pairs; brainstorm three examples in their daily life influenced by training data scale.
- Volunteers share thoughts; facilitator highlights dataset role in each AI example.

---

## 7. Reflection and Next Steps

- Discuss what surprised students most about demo results.
- Ask; why might some data not improve a model? Introduce concept of data quality for Week 6.
- Preview next week; where to find open data and how to judge its reliability.
- Quick quiz; 3 questions testing understanding of why dataset scale matters.

---

## 8. Summary

- Reinforce big idea; high-quality, large-scale data is the foundation of modern AI.
- Highlight main tools and datasets to be explored through the course.
- Invite students to explore dataset websites and bring one interesting dataset idea for discussion in Week 2.
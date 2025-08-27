# Week 3 Demo: From Pseudocode to Working Script - Data Automation Example

---

## Introduction

In this workshop, you will learn to transform machine learning workflow requirements into actionable pseudocode, and then implement both Python and Bash scripts for real-world data automation tasks. The goal is to build confidence in designing and automating repeatable ML processes—a core skill for roles in AI development and engineering.

---

## Learning Objectives

- Understand how to break down ML data workflows into logical pseudocode steps.
- Practice translating pseudocode into working Python and Bash scripts.
- Collaborate to develop, test, and troubleshoot simple automation pipelines.
- Prepare for future assessments by creating reusable templates and code patterns.

---

## Agenda

1. What is pseudocode and why do data engineers use it?
2. Guided example; data pipeline in pseudocode, then script.
3. Collaborative hands-on lab; convert, code, and test.
4. Practical troubleshooting and best practices.
5. Reflection and summary; how this skill connects to future topics.

---

## 1. Pseudocode for Data Pipelines

Pseudocode is a human-friendly way to express logic before jumping into coding. It makes decomposing problems easier and helps verify your approach before scripting.

**Why use pseudocode in ML workflows?**
- Clarifies data movement and processing steps.
- Simple to share and review with team members.
- Eases translation across platforms or languages.

**Example: Data Ingestion and Preprocessing Script (Pseudocode)**

```markdown
1. Specify source location for dataset
2. Check if dataset exists locally
    - If not, download dataset from given URL
3. Unzip or extract files if needed
4. Preprocess data
    - Remove missing or corrupted entries
    - Normalize or scale relevant features
5. Save cleaned data to output directory
```

---

## 2. Translating Pseudocode to Python Script

Let us turn the above pseudocode into a basic Python script for automating part of the ML workflow

```python
import os
import urllib.request
import zipfile
import pandas as pd

# 1. Specify the source URL for dataset
dataset_url = "https://example.com/data/sample_dataset.zip"
local_zip_path = "sample_dataset.zip"
extract_dir = "data"

# 2. Check if dataset exists locally
if not os.path.exists(local_zip_path):
    print("Downloading dataset.")
    urllib.request.urlretrieve(dataset_url, local_zip_path)

# 3. Unzip or extract
if not os.path.exists(extract_dir):
    print("Extracting dataset.")
    with zipfile.ZipFile(local_zip_path, 'r') as zip_ref:
        zip_ref.extractall(extract_dir)

# 4. Preprocess data
csv_path = os.path.join(extract_dir, "sample_data.csv")
df = pd.read_csv(csv_path)
df = df.dropna()  # Remove missing entries
df = (df - df.mean()) / df.std()  # Example normalization

# 5. Save cleaned data
df.to_csv(os.path.join(extract_dir, "cleaned_data.csv"), index=False)
print("Preprocessing complete.")
```

---

## 3. Translating Pseudocode to Bash Script

Bash scripting can automate data operations in cloud and local environments

```bash
# 1. Specify source and destination
DATASET_URL="https://example.com/data/sample_dataset.zip"
ZIP_FILE="sample_dataset.zip"
EXTRACT_DIR="data"

# 2. Check and download
if [ ! -f "$ZIP_FILE" ]; then
  echo "Downloading dataset."
  wget $DATASET_URL -O $ZIP_FILE
fi

# 3. Extract dataset
if [ ! -d "$EXTRACT_DIR" ]; then
  echo "Extracting files."
  unzip $ZIP_FILE -d $EXTRACT_DIR
fi

# 4. Preprocess (using csvkit for demo)
csvcut -c 1,2,3 $EXTRACT_DIR/sample_data.csv > $EXTRACT_DIR/cleaned_data.csv

echo "Automation complete."
```

---

## 4. Collaborative Coding and Review

- Pair up and take turns; one writes pseudocode for a new automation task (e.g., fetch latest weather data), the other translates to Python or Bash.
- Use shared online notebook or cloud shell for real-time feedback.
- Discuss which steps are best suited for Bash vs Python, and why.
- Experiment with adding error handling or logging.

---

## 5. Troubleshooting and Best Practices

- Always check for file existence before downloads or writes.
- Use descriptive variable names and inline comments.
- Break large scripts into functions (Python) or well-named sections (Bash).
- Document scripts for future users.

---

## Reflection Questions

- How does writing pseudocode improve your scripting workflow?
- When would a Bash script be preferable to Python, and vice versa?
- What would you do differently if running this pipeline in a cloud VM or HPC environment?

---

## Preparing for Assessment

- Save your scripts; these can serve as templates for your Week 10 portfolio.
- Practice translating between pseudocode, Python, and Bash to reinforce learning.
- Reflect on how you could adapt these automation patterns to handle ML project data in Azure or HPC systems.

---

## Summary and Next Steps

- Today’s session introduced industry-style automation for ML using both Python and Bash, starting from clear logic in pseudocode.
- Practice decomposing larger ML tasks into modular steps.
- Next week, you will explore coding standards and version control for team-based development.
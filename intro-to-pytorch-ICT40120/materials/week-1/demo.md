# Week 1 Demo: Python Scripting for ML - A Simple Workflow

## Learning Objectives
- Understand the course structure and expectations for Machine Learning Engineering and AI workflows.
- Review fundamental Python scripting concepts for use in ML applications.
- Demonstrate a complete mini ML workflow using Python, including data loading, model creation (stub), and output of results.
- Recognise the relevance of scripting in practical AI/ML industry contexts.

---

## Agenda

1. Course introduction and orientation; discuss industry context and learning goals.
2. Refresher on Python scripting essentials for ML.
3. Guided demo; build and run a simple end-to-end ML script in Python.
4. Discuss industry applications and real-world relevance.
5. Summary, key takeaways, and next steps.

---

## 1. Course Orientation and Industry Context

- This course develops your skills in PyTorch, cloud computing, and ML workflows using Python.
- Applied focus prepares you for roles such as AI Developer or ML Engineer in modern tech environments.
- Industry tools featured include Python, PyTorch, Azure, Bash, and High Performance Computing (HPC) best practices.
- Scripting is essential in automating, deploying, and scaling ML projects in real workplaces, where Python remains the core language used by professionals.

---

## 2. Python Scripting Essentials for ML

- Scripts are reusable, shareable, and essential for automating ML processes; every ML engineer must fluently create and modify Python scripts.
- Core Python skills needed; working with data types, lists, dictionaries, control flow, functions, and basic file I/O.
- Review: Define a function, load data, perform a calculation, and print results.

```python
# Example
def greet(name):
    print(f"Hello, {name}! Welcome to the ML course.")

greet("Student")
```

---

## 3. Guided Demo: End-to-End Mini ML Workflow

This practical exercise walks you through:
- Loading a simple dataset using Python and a common ML library
- Creating a model placeholder ("stub") to illustrate the pipeline
- Outputting basic results to show workflow completion

### Step 1: Data Loading

- Simulate loading a CSV (e.g. exam scores data); Use pandas for simplicity

```python
import pandas as pd

# Sample data creation (would normally be loaded from a file)
data = {'student': ['Alice','Bob','Charlie'], 'score': [85, 90, 78]}
df = pd.DataFrame(data)

print("Sample Data:")
print(df)
```

### Step 2: Model Creation (Stub)

- For now, create a simple function as a stand-in for a real ML model
- In industry, this might be a PyTorch or scikit-learn model class

```python
def model_stub(input_scores):
    # Pretend model simply classifies as 'pass' or 'fail' based on score
    return ['pass' if score >= 80 else 'fail' for score in input_scores]

results = model_stub(df['score'])
df['result'] = results

print("With Results:")
print(df)
```

### Step 3: Output Results

- Save results to a new CSV file; Output a summary to the console

```python
df.to_csv('results.csv', index=False)
print("Results saved to results.csv")
print("Summary:")
print(df['result'].value_counts())
```

---

## 4. Industry Application and Best Practices

- Scripting automates repetitive tasks in model development and deployment workflows; saves time and reduces errors.
- In real projects, you would extend scripts for data validation, pre-processing, experiment tracking, and cloud automation.
- Example scenario; A government department builds scripts to automate student performance analytics on scalable cloud VMs.
- As best practice, always document your scripts with comments and README files for team use.

---

## 5. Practice Activity

Try modifying the workflow:
- Add an extra column for 'grade' based on score bands (e.g. A, B, C)
- Change the model_stub to assign grades instead of just pass/fail
- Print out students who achieved the highest and lowest grades

```python
def assign_grade(score):
    if score >= 90:
        return 'A'
    elif score >= 80:
        return 'B'
    elif score >= 70:
        return 'C'
    else:
        return 'D'

df['grade'] = df['score'].apply(assign_grade)
print(df)

print("Top performer:")
print(df[df['score'] == df['score'].max()])

print("Lowest performer:")
print(df[df['score'] == df['score'].min()])
```

---

## 6. Reflection and Discussion

- Why is scripting seen as foundational to ML engineering in top tech firms?
- How might automating a workflow like this improve team productivity or reduce human mistakes?
- What challenges might arise in real-world scripts versus this simple example?

---

## Summary and Next Steps

- Today you built a complete mini ML workflow script in Python; practiced data loading, model logic, and output.
- Next week, you will apply scripting skills to cloud environments using Bash.
- Homework: Review Python basics if needed; Try adapting today's script for a new dataset (weather, sales, etc.) and share your code in class.
- Remember; In industry, strong scripting habits form the backbone of all advanced AI and ML systems.
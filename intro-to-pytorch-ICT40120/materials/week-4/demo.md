# Week 4 Demo: Setting Up Your First ML Git Repository

---

## Learning Objectives

- Understand the role and advantages of version control in ML/AI projects and HPC environments.
- Initialize a new Git repository; make your first commits; push to a remote repo.
- Apply standard organisational coding standards including documentation, code structure, and policies.
- Practice real-world collaboration scenarios and resolve basic merge/branch issues.
- Prepare for industry workflows with best practices and troubleshooting tips.

---

## 1. Why Version Control Matters in Machine Learning

- Ensures your code is trackable and reproducible; critical for ML model integrity and compliance.
- Facilitates team collaboration by managing changes and tracking experiments.
- Required for most industry MLOps pipelines, model versioning, and audits.

**Discussion**  
- What happens when code or model files change and you don’t know what/why?  
- How could this affect a government or industry AI deployment?

---

## 2. Step-by-Step: Initialize Your Git Repository

**Activity**  
Follow these steps to create your own ML project repository.

### 2.1. Prepare Your Workspace

- Open a terminal and navigate to your ML project directory or create one

```bash
mkdir my_ml_project
cd my_ml_project
```

### 2.2. Initialize a Git Repository

- Start local version control

```bash
git init
```

### 2.3. Add Your Scripts

- Create a basic script file; use clear naming and initial docstring to match standards

```python
# example script: basic_data_loader.py
"""
Purpose. Load sample data and print summary stats for project initial test.
Author. Your Name (your.email@example.com)
Date. YYYY-MM-DD
"""

import pandas as pd

def main():
    print('This script loads data and prints stats.')

if __name__ == "__main__":
    main()
```

- Stage and commit your script

```bash
git add basic_data_loader.py
git commit -m "Initial commit. Added basic data loader script."
```

### 2.4. Connect to a Remote Repository (e.g., GitHub/Azure DevOps)

- On your platform, create a new repository with the same name.
- Connect with:

```bash
git remote add origin https://github.com/your-username/my_ml_project.git
git push -u origin master
```

---

## 3. Organisational Coding Standards and Repository Structure

- Every repo must have a clear structure; include at minimum
  - README.md; explains project, dependencies, and usage
  - src/ or scripts/; stores code scripts, one task per file
  - data/; placeholder or note (never push large data!)
  - .gitignore; excludes sensitive or clutter files (e.g. data/, .env, *.pyc files)

### 3.1. Example .gitignore

```bash
# Ignore data and environment files
data/
*.csv
*.env
__pycache__/
```

### 3.2. Example README.md Structure

```
# Project Name

Summary; Short project description and goal

Project Structure; Briefly describe folder and file structure

How to Run; Commands or steps to execute scripts

Author and Contact; Your name and contact email
```

---

## 4. Working as a Team: Branches, Pull, and Merge

**Scenario Exercise**  
- You and a classmate edit the same script. Use branches to manage changes.

### 4.1. Create a Branch and Edit

```bash
git checkout -b feature-add-stats
# Make changes to basic_data_loader.py
git add basic_data_loader.py
git commit -m "Added basic stats function"
git push -u origin feature-add-stats
```

- Open a Pull Request (PR) on your platform; review and merge.

**Common Pitfalls**
- Merge conflicts happen when two changes overlap; Git will alert and ask you to edit before merging.
- Always pull latest (`git pull`) before making big changes.

---

## 5. Industry Practices and Assessment Preparation

- Professionals must follow agreed code style, documentation, and commit message policies.
- All scripts should have clear docstrings, purpose, and author details.
- Ensure all group work demonstrates standards and can be reviewed or audited.

---

## 6. Hands-on Challenges and Reflection

**Practical Challenges**
- Clone a provided template repo; set up your own branch; add a script and push changes.
- Update the README to reflect your changes.
- Review a classmate’s Pull Request or branch.

**Discussion**
- Share an experience you’ve had with code or file loss. How would version control have helped?
- How does this workflow directly connect to industry MLOps, model tracking, and responsible AI?

---

## 7. Troubleshooting and Best Practices

- If you accidentally committed sensitive data, remove with `git rm` and amend history with care.
- Use `git status` and `git log` often to check your work.
- Always document your changes and reasons in commit messages.

---

## 8. Summary and Next Steps

- By following coding standards and version control, you set the foundation for scalable and professional AI/ML projects.
- Practice these skills for all scripts and assignments going forward.
- Review key links; GitHub guides, internal standards, and TAFE assessment rubrics.

---

**Preparation for Next Week**
- Set up new repos for PyTorch workshops.
- Practice pushing updates and collaborating via Pull Requests.
# Week 2 Workshop; Bash Scripting and Shell Environments for Cloud ML Tasks

## Learning Objectives

- Understand the role of Bash scripting in Linux and cloud ML environments
- Practice writing scripts for file and directory management
- Implement documentation and best practices in Bash scripts
- Execute scripts in Ubuntu or cloud shell environments
- Prepare foundational skills for cloud-based ML workflows

---

## Workshop Agenda

1. Introduction to Bash and Shell Environments
2. Basic Bash Commands for File and Directory Management
3. Scripting Fundamentals; Writing and Running Bash Scripts
4. Best Practices; Script Documentation and Readability
5. Hands-On Practice; Practical Tasks
6. Troubleshooting; Common Errors and How to Solve Them
7. Reflection and Next Steps

---

## 1. Introduction to Bash and Shell Environments

- Bash is a common command-line shell used to interact with Unix/Linux systems
- Shell scripting automates repetitive tasks, essential in cloud and ML workflows
- Industry practice; Bash is used for setup, file management, job scheduling, and ML orchestration on platforms like Ubuntu and Azure

---

## 2. Basic Bash Commands for File and Directory Management

- `ls` lists files and directories
- `cd` changes directories
- `pwd` shows the current working directory
- `mkdir` makes directories
- `touch` creates empty files
- `cp`, `mv` copy or move files and directories
- `rm` removes files

### Practical Example

```bash
# List files and directories
ls

# Create a directory called 'demo_folder' and move into it
mkdir demo_folder
cd demo_folder

# Create an empty file called 'script.txt'
touch script.txt

# Move back and remove the directory
cd ..
rm -r demo_folder
```

---

## 3. Scripting Fundamentals; Writing and Running Bash Scripts

- Bash scripts are plain text files with a series of commands
- All scripts start with a 'shebang' line; this tells the system which interpreter to use

### Script Example

```bash
#!/bin/bash
# This script creates a set of directories for a machine learning project

echo 'Creating base project directories.';

mkdir -p ML_project/{data,models,logs,notebooks,src};
echo 'Project structure created successfully.';
```

#### How to Save and Run

- Save script as 'setup_ml_project.sh'
- Make executable with `chmod +x setup_ml_project.sh`
- Run with `./setup_ml_project.sh`

---

## 4. Best Practices; Script Documentation and Readability

- Use comments to explain sections and key lines in scripts
- Follow consistent naming conventions
- Include a usage note at the start

### Example

```bash
#!/bin/bash
# setup_environment.sh
# Usage; ./setup_environment.sh
# Description; Sets up standard folders for an ML project

echo 'Setting up directories for ML workflow.';

mkdir -p data raw processed models logs src;

echo 'Setup complete. Check your directory structure!';
```

---

## 5. Hands-On Practice; Practical Tasks

- Write a script to back up a dataset directory to a timestamped folder
- Include comments and clear variable names

### Example Scaffold

```bash
#!/bin/bash
# backup_dataset.sh
# Usage; ./backup_dataset.sh source_directory

SOURCE=$1
DATE=$(date +%Y-%m-%d_%H-%M-%S)
BACKUP_DIR="${SOURCE}_backup_${DATE}"

echo "Backing up $SOURCE to $BACKUP_DIR";
cp -r $SOURCE $BACKUP_DIR;
echo "Backup completed.";
```

#### Exercises

- Modify the script to check if the source directory exists; print an error if not
- Add code to remove backups older than 7 days (hint; use `find` and `rm`)

---

## 6. Troubleshooting; Common Errors and Solutions

- 'Permission denied' means script may need 'chmod +x'
- Missing variables or typos can break scripts; debug with `set -x`
- Always check directory paths before running destructive commands like `rm`

---

## 7. Reflection and Next Steps

- Reflect; How could these scripting skills streamline ML project setup or data management?
- How might these scripts adapt if deploying on Azure or different ML cloud platforms?
- Next week; Learn how to structure larger scripts, write pseudocode, and automate more complex ML workflows

---

## Assessment Preparation

- Script writing and documentation will be assessed in upcoming projects
- Practicing script automation now builds confidence for managing cloud-based ML environments in later weeks

---

## Summary

- Bash scripting is a critical foundational skill for ML workflow automation in industry environments
- Mastering these basics prepares you for deeper cloud and ML automation tasks throughout the course
# Week 14 Workshop: Cloud Infrastructure Assessment Readiness

## Learning Objectives

- Understand the assessment process for cloud infrastructure and GPU VM setup.
- Demonstrate Azure VM creation, network configuration, and Bash scripting for job automation.
- Practice collecting evidence and documenting workflows for assessment.
- Troubleshoot common issues and build on previous cloud and PyTorch exercises.

---

## 1. Workshop Introduction

**Purpose and Value**
- This session prepares you for the practical assessment by simulating real-world industry scenarios.
- You will practice VM and cloud configuration, use Bash for automation, and document your progress for workplace and assessment requirements.
- Industry alignment; these skills are directly relevant to ML engineering and cloud computing roles.

---

## 2. Overview of Assessment Tasks

- Create an Azure GPU VM suitable for ML workloads.
- Configure secure network settings and attach required storage.
- Use Bash scripting to automate basic environment setup and monitoring.
- Run a simple test script on the GPU VM to verify setup.
- Capture and organize screenshots; build an evidence portfolio for submission.

---

## 3. Step-by-Step Walkthrough

### 3.1. Create and Configure an Azure GPU VM

**Steps**
- Log into Azure Portal and navigate to Virtual Machines.
- Select 'Create Virtual Machine' and choose a GPU-enabled image.
- Configure resources; set CPU, memory, and storage to recommended levels for ML tasks.
- Open inbound ports as required for SSH and Jupyter access; set secure credentials.
- Deploy the VM and record the public IP address.

### 3.2. Network and Storage Configuration

**Steps**
- Attach a persistent storage disk for datasets and models.
- Verify network security group (NSG) rules; allow only necessary ports.
- Use the Azure portal or CLI to confirm configuration.

```bash
# Example: Checking attached disks (run on your VM)
lsblk
```

---

### 3.3. Connect to the VM and Basic Environment Setup

**Steps**
- Use SSH to connect to the VM from your local system.

```bash
# SSH example
ssh username@your-public-ip
```

- Update the system, install Python, pip, and required dependencies.

```bash
# Example Bash for environment setup
sudo apt update
sudo apt install python3-pip
pip3 install torch
```

---

### 3.4. Bash Script for Job Automation

**Activity**
- Write a simple Bash script to automate common tasks; e.g., environment setup, checking GPU status.

```bash
#!/bin/bash
# bash script: setup_and_check_gpu.sh
echo "Updating packages."
sudo apt update
echo "Installing NVIDIA drivers (simulation)."
# sudo apt install nvidia-driver-XXX  # Uncomment with correct driver
echo "Checking GPU status."
nvidia-smi
```

- Make your script executable and run it.

```bash
chmod +x setup_and_check_gpu.sh
./setup_and_check_gpu.sh
```

---

### 3.5. Run a Test PyTorch Script on the GPU

**Activity**
- Validate GPU availability in Python; this confirms correct setup.

```python
import torch
print("CUDA Available:", torch.cuda.is_available())
print("GPU Device Name:", torch.cuda.get_device_name(0))
```

- Save script output and take a screenshot for your assessment evidence.

---

### 3.6. Evidence Collection and Documentation

**Best Practice Tips**
- Document each key step using screenshots or terminal outputs.
- Organize evidence in a logical order; use filenames with timestamps and descriptions.
- Example screenshot list; VM creation, network settings, CLI output (nvidia-smi, torch.cuda), Bash script execution.

---

### 3.7. Troubleshooting Guidance

- Common issues; no GPU detected, failed pip installs, network SSH failure.
- Check VM size and image; verify drivers, check Python environment paths.
- Use `dmesg`, `systemctl status`, or Azure logs for deeper diagnostics.
- Ask peers/instructor for help—collaboration is a workplace skill!

---

## 4. Practical Exercises

- Complete each step with your own Azure Student account or classroom subscription.
- Submit a folder with all screenshots and brief notes as trial evidence.

---

## 5. Review and Assessment Preparation Checklist

- Did you create and configure a GPU-enabled Azure VM?
- Have you attached storage and secured your network setup?
- Did your Bash script successfully run and automate environment checks?
- Can you confirm GPU availability in PyTorch using your own script?
- Is your documentation clear, organized, and complete?

---

## 6. Next Steps and Portfolio Submission Guidelines

- Finalize your evidence and notes.
- Assemble your assessment portfolio as per submission instructions.
- Ask questions, review your work, and use week 15 for any follow-up issues.

---

## Reflection Questions

- What steps were easiest or most challenging? Why?
- How does this workflow reflect real-world ML engineering jobs?
- What improvements could you make to your Bash scripts or documentation?

---

## Summary

- By completing this workshop, you have prepared for a key industry-aligned assessment and gained practical skills in cloud ML deployments.
- These skills are directly transferable to Machine Learning Engineering and HPC industry roles.
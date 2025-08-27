# Week 7 Demo. Provision Your First Azure GPU VM

## Learning Objectives

- Identify and choose suitable Azure cloud computing resources for ML workloads
- Provision and configure an Azure GPU-enabled VM for use with PyTorch and AI workloads
- Establish secure SSH access to your VM from your development workstation
- Explain the practical purpose of different cloud resources and access controls in AI/ML production workflows

---

## 1. Introduction to Azure Cloud for Machine Learning

**Industry and Practical Context**
- Cloud computing is essential for scalable AI projects. GPU-powered VMs are industry-standard for training and inference in ML workflows.
- Azure offers a variety of services. Understanding which one to select is key for cost, performance, and compliance.

**Key Concepts**
- Cloud deployment models; public cloud; hybrid; private; which one fits regulated AI workloads.
- Virtual Machines (VMs); virtualized computers in the cloud; pay-as-you-go usage.
- GPUs on Azure; enable high-performance computation for training deep learning models.

> *Reflection*. Describe a scenario in industry where using a cloud-based GPU VM would provide a significant benefit.

---

## 2. Azure Resource Groups, Users, and Access

**Resource Groups**
- Resource groups help organize and manage related Azure resources together.
- Typical structure; one resource group per project, helps with budgeting and access control.

**User Access and Permissions**
- Use least privilege principles; never grant unnecessary admin rights.
- Azure Role-Based Access Control (RBAC); assign only what students need for assessment tasks.

---

## 3. Hands-on. Create and Configure Your Azure GPU VM

### *Step-by-Step Lab*

#### Part A. Prepare Your Azure Account

- Make sure your Azure student or institutional account is active.
- Check credit balance if on free tier to avoid accidental charges.
- If you don’t already have one, set up your Azure account at [https://azure.microsoft.com/free](https://azure.microsoft.com/free).

#### Part B. Create a Resource Group

```python
# Bash cell. Run in your local terminal where Azure CLI is installed.
!az group create --name ai-ml-demo-rg --location australiacentral
```
- Name your group for your project; e.g. ai-ml-demo-rg.
- Use an Australian region for lower latency and compliance.

#### Part C. VM Selection – Compare Compute Options

- For ML, select a VM with a GPU; e.g. NC, ND, or NV series on Azure.
- Start with Standard_NC6 (single NVIDIA K80 GPU; cost-effective for first project).

> *Exercise*. Visit the Azure VM families page and compare at least two GPU VM types; note their typical uses in an ML context.

#### Part D. Provision the Azure VM

```python
# Run in shell with Azure CLI; update '--admin-username' and '--ssh-key-values' with your details.
!az vm create 
  --resource-group ai-ml-demo-rg 
  --name mygpudemo-vm 
  --image UbuntuLTS 
  --size Standard_NC6 
  --admin-username azurestudent 
  --ssh-key-values ~/.ssh/id_rsa.pub
```
- Always use SSH keys for secure access; never password logins in production.
- Choose Ubuntu LTS for widest compatibility with ML tooling.

> *Tip*. If you do not have an SSH keypair, generate one with `ssh-keygen -t rsa -b 4096`.

#### Part E. Configure Network and Secure Access

```python
# To open port 22 only for SSH, run
!az vm open-port --port 22 --resource-group ai-ml-demo-rg --name mygpudemo-vm
```
- Never open unnecessary ports. Limit SSH to your IP where possible.

#### Part F. SSH into Your VM

```python
# Bash command to connect
!ssh azurestudent@<vm-public-ip>
```
- Replace `<vm-public-ip>` with the IP from the `az vm create` output.

> *Troubleshooting*. If connection fails, check security groups/firewall and ensure the VM is running.

---

## 4. Practical Config – First Steps After Login

- Update and upgrade packages
```python
!sudo apt update && sudo apt upgrade -y
```
- Install Python and essential ML libraries
```python
!sudo apt install python3-pip
!pip3 install torch torchvision torchaudio
```
- Check GPU availability in Python
```python
import torch
print(torch.cuda.is_available()) # True means GPU is ready
```

---

## 5. Reflection and Troubleshooting

- List three ways to secure your cloud-based VM against unauthorized access.
- How would you automate VM provisioning for multiple students in a class setting?

---

## 6. Industry Case Study

**Case Study**
- A local data science consultancy regularly prototypes NLP models on short-lived Azure GPU VMs.
- Engineers use resource groups for cost tracking and RBAC for safe team access.
- On completion, all resources are deleted to prevent budget overruns and security risks.

---

## 7. Summary and Next Steps

- You can now provision, secure, and access a GPU VM in Azure – a foundational industry skill.
- Preparation for next week; networking and storage configuration for scalable ML workloads.
- Suggested practice; repeat this process, try provisioning other VM types, and document each step as screenshots for your assessment portfolio.

---
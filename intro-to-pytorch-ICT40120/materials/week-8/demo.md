# Week 8 Practical Lab: Azure Networking and Storage for Scalable AI Workflows

## Learning Objectives

- Understand the purpose and structure of virtual networks and storage in Azure for ML workloads.
- Design and deploy a simple virtual network to support AI resources and data movement.
- Configure cloud storage, mount persistent datasets, and validate access from compute resources.
- Test connectivity between VMs, storage, and (optionally) a database component in Azure.
- Apply troubleshooting skills and interpret diagnostic commands/logs relevant to cloud networking and storage.

---

## 1. Introduction and Industry Context

As ML Engineers and Cloud AI Developers, building robust, secure, and scalable networked environments is critical. This week we'll simulate the setup of a cloud infrastructure that supports high-performance machine learning workflows on Azure, focusing on networking and storage—key areas that underpin modern ML production. You'll gain practical experience setting up the environment exactly as you might in a tech company or government data science team.

---

## 2. Lab Scenario

You have been tasked to support an ML development team by provisioning:
- A secure, isolated virtual network for compute resources;
- A cloud storage account for datasets and outputs;
- Configuration to allow virtual machines (VMs) to read/write to storage with minimal latency and the correct access controls.

---

## 3. Step-by-Step Lab Instructions

### 3.1. Lab Setup; Prerequisites

- Ensure you have access to an Azure account and permissions to create/manage resources.
- Install **Azure CLI** locally or use Azure Cloud Shell.
- Make sure your resource group and region are chosen (substitute your values in command examples).

---

### 3.2. Create a Resource Group

```bash
# Replace with your unique resource group name and preferred region
az group create --name ml-lab-rg --location australiaeast
```
- Creates a container for all resources deployed in this lab.

---

### 3.3. Design and Deploy a Virtual Network with a Subnet

- A virtual network (VNet) allows secure, private communication between Azure resources.

```bash
az network vnet create \
  --resource-group ml-lab-rg \
  --name ml-vnet \
  --address-prefix 10.1.0.0/16 \
  --subnet-name compute-subnet \
  --subnet-prefix 10.1.1.0/24
```
- VNet design allows you to control IP ranges, isolation, and security. Subnets can be created for compute, storage, and database workloads.

---

### 3.4. Deploy a Storage Account

- Used to persist ML datasets, model artifacts, checkpoints, and logs.

```bash
az storage account create \
  --name mllabstorage$RANDOM \
  --resource-group ml-lab-rg \
  --location australiaeast \
  --sku Standard_LRS \
  --kind StorageV2
```
- StorageV2 supports blobs, files, tables, and queues; Standard_LRS ensures redundancy within the region.

---

### 3.5. Create a File Share in the Storage Account

- File shares support persistent, POSIX-compatible datasets that VMs can access.

```bash
az storage share-rm create \
  --storage-account mllabstorage1234 \
  --resource-group ml-lab-rg \
  --name datasets
```

---

### 3.6. Deploy a Virtual Machine into the Network

- Example uses Ubuntu for compatibility with ML tooling.

```bash
az vm create \
  --resource-group ml-lab-rg \
  --name mlcompute01 \
  --image Ubuntu2204 \
  --vnet-name ml-vnet \
  --subnet compute-subnet \
  --public-ip-address '' \
  --size Standard_DS2_v2 \
  --admin-username azureuser \
  --generate-ssh-keys
```
- No public IP is assigned for improved security (simulate enterprise best practice).

---

### 3.7. Mount the Azure File Share on the VM

- After VM deployment, connect via SSH from the Cloud Shell or a jump box within the VNet.

**On the VM, install required utilities:**
```bash
sudo apt-get update
sudo apt-get install cifs-utils -y
```

**Mount the file share:**
- Retrieve the storage account key (replace `<your-storage-account>`):

```bash
STORAGE_KEY=$(az storage account keys list --resource-group ml-lab-rg --account-name mllabstorage1234 --query [0].value -o tsv)
sudo mkdir /mnt/datasets
sudo mount -t cifs //mllabstorage1234.file.core.windows.net/datasets /mnt/datasets \
  -o vers=3.0,username=mllabstorage1234,password=$STORAGE_KEY,dir_mode=0777,file_mode=0777,serverino
```

- **Test read/write to mounted directory:**
```bash
echo "hello from ml VM" | sudo tee /mnt/datasets/testfile.txt
cat /mnt/datasets/testfile.txt
```

---

### 3.8. (Optional) Test Network Access Between Compute, Storage, and a Database

- Deploy an Azure Database (e.g., PostgreSQL) in the same VNet and test connectivity. Review firewall rules and required VNet integration steps.

---

## 4. Troubleshooting Tips

- Use `az network vnet list` and `az vm list-ip-addresses` to verify network configuration.
- For storage issues, check keys/permissions, and review mount options for syntax errors.
- Use `ping`, `telnet`, and `nslookup` inside VMs to diagnose network routing or DNS issues.
- Consult Azure Activity Log for audit and diagnostic messages.

---

## 5. Real-World Case Study

*Scenario*: A data science team needs to share large training datasets between compute VMs running PyTorch scripts and wants high availability, security, and compliance. By using VNets, Azure Files, and controlling access via private endpoints, your solution mirrors enterprise practices in finance, healthcare, and government AI applications.

---

## 6. Reflective Questions

- What are the main security advantages of placing all resources inside a VNet?
- Why is mounting storage using Azure Files preferred for ML workloads over downloading datasets locally?
- How would you modify the design for higher resilience or scale (e.g., using multiple subnets, network security groups, or geo-redundancy)?
- Can you see parallels between this workflow and automation/script development covered in weeks 2-4?

---

## 7. Summary and Next Steps

* You have designed and deployed practical Azure networking and storage components.
* These skills underpin building and scaling AI/ML workflows in a cloud environment.
* Next week: secure database integration and secret management for ML workflows.

---

## 8. Challenge Exercise

- Modify the above workflow to create a second subnet for database resources. Deploy a managed database and allow only the compute subnet to access it.
- Write a Bash script to automate the file share mounting process for multiple compute VMs.
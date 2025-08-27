# Week 12 Demo / Workshop: Autoscaling and Automated Resource Management in Azure

## Learning Objectives

- Understand the concepts and benefits of autoscaling for machine learning workloads in the cloud.
- Configure, trigger, and test automatic scaling for Azure GPU resources.
- Write and adapt Bash scripts to automate deployment and resource management tasks using Azure CLI.
- Monitor and analyze resource usage with Azure monitoring tools and interpret output for optimization.
- Relate cloud automation practices to workplace standards in ML engineering and AI operations.

---

## Agenda

1. Introduction to Autoscaling and Automation in Cloud ML
2. Demo; Setting up Autoscale on Azure GPU VMs
3. Hands-On; Bash Scripting for Cloud Resource Automation
4. Monitoring and Analyzing Resource Usage in Azure
5. Troubleshooting and Best Practices
6. Reflection and Application to Assessments

---

## 1. Introduction to Autoscaling and Automation in Cloud ML

Autoscaling is a cloud computing feature that allows resources such as virtual machines to scale up or down automatically based on demand; this ensures both cost efficiency and performance in ML workflows that have variable workloads. Automation with scripting increases consistency, reproducibility, and reduces manual intervention, which is required in professional environments.

---

## 2. Demo; Setting up Autoscale on Azure GPU VMs

### Activity; What is Autoscale?

- Autoscale automatically adjusts the number of VM instances depending on workload. In ML, this is critical when demand spikes during model training or inference.
    - Benefits include reduced operational cost, improved resource utilization, and increased reliability.

### Activity; Enable Autoscale on an Azure VM Scale Set

1. Use Azure CLI to create a VM scale set with GPU support.
2. Configure autoscale rules; for example, scale out when CPU or GPU utilization exceeds 70%, and scale in below 30%.

```bash
# Create a resource group
az group create --name ml-autoscale-demo --location australiaeast

# Create a GPU VM scale set
az vmss create \
  --resource-group ml-autoscale-demo \
  --name gpu-vmss-demo \
  --image microsoft-ads:linux-data-science-vm-ubuntu:linuxdsvmubuntu:latest \
  --vm-sku Standard_NC6 \
  --instance-count 1 \
  --upgrade-policy-mode automatic \
  --authentication-type ssh \
  --admin-username azureuser \
  --generate-ssh-keys

# Set up autoscale rules (scale up when CPU > 70% for 10 min, scale down when < 30%)
az monitor autoscale create \
  --resource-group ml-autoscale-demo \
  --resource gpu-vmss-demo \
  --resource-type Microsoft.Compute/virtualMachineScaleSets \
  --min-count 1 \
  --max-count 4 \
  --count 1

az monitor autoscale rule create \
  --resource-group ml-autoscale-demo \
  --autoscale-name gpu-vmss-demo \
  --condition "Percentage CPU > 70 avg 10m" \
  --scale out 1

az monitor autoscale rule create \
  --resource-group ml-autoscale-demo \
  --autoscale-name gpu-vmss-demo \
  --condition "Percentage CPU < 30 avg 10m" \
  --scale in 1
```

- *Exercise;* Try modifying the trigger conditions (e.g. for GPU utilization if supported in your subscription).

---

## 3. Hands-On; Bash Scripting for Cloud Resource Automation

### Activity; Automate Resource Provisioning and Cleanup

- Use Bash scripts to repeatedly deploy, manage, or tear down resources as per real team practices.

```bash
# Example script to automate VMSS teardown
#!/bin/bash
RESOURCE_GROUP="ml-autoscale-demo"
VMSS_NAME="gpu-vmss-demo"

echo "Deallocating VM scale set..."
az vmss deallocate --resource-group $RESOURCE_GROUP --name $VMSS_NAME

echo "Deleting resource group and all resources..."
az group delete --name $RESOURCE_GROUP --yes --no-wait
```

- *Exercise;* Write a Bash script that checks VM instance count and sends an alert if it exceeds a threshold.

---

## 4. Monitoring and Analyzing Resource Usage in Azure

### Activity; Monitor and Interpret Azure Metrics

- Use Azure Portal or CLI to view performance metrics such as CPU usage, memory, or GPU utilization.

```bash
# List available metrics for the scale set
az monitor metrics list-definitions \
  --resource "/subscriptions/<subscription-id>/resourceGroups/ml-autoscale-demo/providers/Microsoft.Compute/virtualMachineScaleSets/gpu-vmss-demo"

# Example: Get average CPU percentage in the past hour
az monitor metrics list \
  --resource "/subscriptions/<subscription-id>/resourceGroups/ml-autoscale-demo/providers/Microsoft.Compute/virtualMachineScaleSets/gpu-vmss-demo" \
  --metric "Percentage CPU" \
  --aggregation Average \
  --interval PT1H
```

- *Exercise;* Analyze a monitoring log and identify when autoscaling events occurred. What was the trigger?

---

## 5. Troubleshooting and Best Practices

- Common issues;
    - Scale set does not add instances; check quotas, permissions, trigger thresholds.
    - Automation script errors; validate Azure CLI versions and API compatibility.
    - Misconfigured scaling rules; always review settings in Azure Portal for real-time feedback.
- *Tip;* Test autoscaling by using CPU/GPU stress tests and monitor how scaling events are logged.

---

## 6. Reflection and Application to Assessments

- *Assessment Prep;* How does scripting automation and autoscale relate to the test on infrastructure and Bash scripting?
- *Discussion;* Why is automation of resource management critical in a production ML context? How does this reduce operational risk?
- *Case Study;* Imagine a model training run peaks overnight; autoscale ensures enough GPU instances are online with no manual watch needed.

---

## Reflection Questions

- List three reasons why autoscaling is beneficial for machine learning workloads.
- Write a short Bash snippet for sending a notification if more than 3 VM instances are detected.
- Summarize the difference between manual and automated resource management in the cloud workplace.
- Describe one real-world scenario (from your studies or imagination) where autoscaling would directly prevent service interruption.

---

## Summary and Next Steps

- Autoscaling and automation skills enable scalable, reliable ML/cloud deployments; they directly support industry needs and your upcoming assessments.
- For next week; prepare example scripts to manage GPU training jobs on single VMs before advancing to distributed workloads.
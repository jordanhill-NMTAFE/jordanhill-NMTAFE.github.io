# Week 13 Workshop; Speeding Up PyTorch on a GPU VM

## Learning Objectives

- Understand the benefits and engineering challenges of running PyTorch on GPUs for ML inference and training
- Move existing PyTorch projects from CPU to GPU, using best practices for device management
- Optimise data loading, batching, and throughput for GPU utilisation in HPC or cloud VMs
- Debug, monitor, and resolve common hardware/software resource issues in GPU-accelerated environments
- Prepare for individual assessments involving Azure GPU VMs and production-ready model development

## Introduction

This hands-on lab will deepen your skills in GPU-accelerated machine learning using PyTorch. You will use industry tools and workflows relevant to cloud environments such as Azure, with a focus on practical application and troubleshooting. This experience prepares you for both immediate assessment tasks and industry-standard ML engineering roles.

---

## 1. Setup; Confirming GPU Availability

Use these commands to check and validate whether your cloud VM or local environment has a supported GPU.

```python
import torch

# Print device type; Expect 'cuda' if a supported GPU is available
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
print('Selected device;', device)

# Print detected GPUs
if torch.cuda.is_available():
    print('CUDA device count;', torch.cuda.device_count())
    print('Current CUDA device;', torch.cuda.current_device())
    print('CUDA device name;', torch.cuda.get_device_name(0))
else:
    print('No CUDA-capable GPU detected. Check VM/driver setup.')
```

**Exercise**
- Run the code above. Record your device type and GPU details in your lab journal.
- Troubleshoot if 'cuda' is not available; Check VM specs, driver state, and ask for support if needed.

---

## 2. Moving Your Model and Data to GPU

Learn how to move models and data between CPU and GPU for optimal performance; this is a key PyTorch workflow in both development and production environments.

```python
import torch
import torch.nn as nn

# Dummy model and tensor
model = nn.Linear(512, 10)
sample_data = torch.randn(16, 512)

# Move both model and tensor to GPU (if available)
model = model.to(device)
sample_data = sample_data.to(device)

# Forward pass
output = model(sample_data)
print('Output shape;', output.shape)
print('Model and data on device;', output.device)
```

**Exercise**
- Update any existing CPU-only scripts to use .to(device).
- Reflect; What could go wrong if you forget to move data or model correctly?

---

## 3. Comparing CPU vs GPU Performance

Explore the impact of GPU acceleration by comparing CPU and GPU training times on a simple neural network.

```python
import time

device_cpu = torch.device('cpu')
device_gpu = torch.device('cuda' if torch.cuda.is_available() else 'cpu')

# Simple model definition
class SimpleNet(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(512, 256)
        self.relu = nn.ReLU()
        self.fc2 = nn.Linear(256, 10)
    def forward(self, x):
        return self.fc2(self.relu(self.fc1(x)))

# Random input and target
input_data = torch.randn(1024, 512)
target = torch.randint(0, 10, (1024,))

# Define loss and optimizer
def train_epoch(model, device):
    model = model.to(device)
    inputs = input_data.to(device)
    targets = target.to(device)
    optimizer = torch.optim.Adam(model.parameters())
    criterion = nn.CrossEntropyLoss()
    for epoch in range(5):
        optimizer.zero_grad()
        outputs = model(inputs)
        loss = criterion(outputs, targets)
        loss.backward()
        optimizer.step()

# Time on CPU
cpu_model = SimpleNet()
start = time.time()
train_epoch(cpu_model, device_cpu)
print('CPU time;', time.time() - start, 'seconds')

# Time on GPU if available
if torch.cuda.is_available():
    gpu_model = SimpleNet()
    start = time.time()
    train_epoch(gpu_model, device_gpu)
    print('GPU time;', time.time() - start, 'seconds')
else:
    print('Skip GPU timing. No GPU available.')
```

**Discussion**
- How much faster is GPU training in your environment?
- What factors might affect speedup (model size, data copy speeds, batch size)?

---

## 4. Optimising Data Loading and Batching

Efficient data loading is critical for GPU throughput. Use DataLoader, batching, and pin_memory to optimise processing.

```python
from torch.utils.data import DataLoader, TensorDataset

# Simulate large dataset
data = torch.randn(10000, 512)
labels = torch.randint(0, 10, (10000,))
dataset = TensorDataset(data, labels)

dataloader = DataLoader(dataset, batch_size=128, shuffle=True, pin_memory=True)

# Iterate and transfer batches to GPU
for batch_data, batch_labels in dataloader:
    batch_data = batch_data.to(device, non_blocking=True)
    batch_labels = batch_labels.to(device, non_blocking=True)
    # Simulate training step...
```

**Tips**
- Use suitable batch sizes to balance efficiency and memory constraints.
- Enable pin_memory and non_blocking=True for faster data transfer from host to GPU.

**Exercise**
- Experiment with different batch sizes; Observe memory usage and training speed.
- Document findings and best batch size for your model.

---

## 5. Monitoring and Debugging Resource Usage

Use built-in and industry tools to track GPU memory, utilisation, and temperature.

**Shell Command Example (run in terminal)**
```
!nvidia-smi
```

**In PyTorch**
```python
if torch.cuda.is_available():
    print('Allocated CUDA memory (MB);', torch.cuda.memory_allocated() // (1024*1024))
    print('Max allocated CUDA memory (MB);', torch.cuda.max_memory_allocated() // (1024*1024))
```

**Exercise**
- Check GPU usage while running different batch sizes or models.
- If you encounter OOM (Out of Memory) errors; Try reducing batch size, clearing cache (torch.cuda.empty_cache()), or simplifying the model.

---

## 6. Troubleshooting Checklist; Common Issues

- CUDA device not detected; Restart VM, check driver install, validate instance type.
- Data/model mismatch; Move ALL tensors/models to same device.
- Out-of-memory errors; Lower batch size, monitor memory usage, clear GPU cache.
- Kernel crash; Ensure only supported operations are run on GPU.
- Performance plateau; Check data pipeline bottlenecks, experiment with pinned memory, and adjust dataloader workers.

**Reflection**
- Document a troubleshooting issue you encountered. Describe your steps to resolve it.

---

## 7. Industry Case Study; Real-World GPU Optimisation

In AI product teams, moving workloads to GPU is a key step in scaling from prototype to production. For example, rapid model training on Azure GPU VMs allows data scientists to iterate faster and deploy models with higher accuracy.

**Scenario**
- A local software company used Azure NC-series VMs to cut their model training times from 12 hours to 40 minutes, resulting in rapid deployment and major cost savings. They used batch size tuning and resource monitoring best practices similar to those in this workshop.

---

## 8. Reflection and Assessment Questions

- In 2-3 sentences, explain why it's important to optimise both data pipelines and compute pipelines when working with GPU VMs.
- List two GPU troubleshooting techniques you might use before a major assessment or in an industry setting.
- What are the ethical or cost considerations when scaling up GPU resources in commercial AI workflows?

---

## 9. Summary and Next Steps

- You have practiced key skills to move and optimise PyTorch workloads on GPUs, troubleshoot resource issues, and prepare for industry or assessment settings.
- Next week, you will review these skills in the context of cloud infrastructure assessment and production model deployment.
- Make sure your project scripts use robust device management techniques and document any performance bottlenecks discovered in this lab.
- Review Azure GPU VM documentation before attempting your assessment project.

---
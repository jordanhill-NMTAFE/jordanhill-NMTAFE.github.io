# Week 15; Distributed Training Fundamentals; Multi-GPU PyTorch Jobs

## Learning Objectives

- Understand how distributed training enables scalable, efficient machine learning for real-world AI and data science projects
- Learn to set up, launch, and monitor distributed jobs using torchrun and accelerate on multi-GPU systems
- Gain hands-on experience adapting existing PyTorch scripts for multi-GPU use
- Monitor distributed training jobs with industry-standard experiment tracking tools
- Prepare for final projects and industry requirements in ML engineering and cloud-based AI deployment

---

## 1. Agenda

1. Introduction to distributed training and data parallelism in industry workflows
2. Multi-GPU setup and environment checks
3. Running distributed jobs with torchrun; PyTorch DataParallel and DistributedDataParallel
4. Accelerate for simplified multi-GPU workflows
5. Experiment tracking and monitoring
6. Hands-on challenges and troubleshooting
7. Reflection and preparation for assessment

---

## 2. Industry Context and Relevance

- Modern AI projects and ML engineering roles require the ability to efficiently train models at scale
- Distributed training is standard practice in cloud, HPC, and enterprise AI environments
- Employers expect basic competency with tools like torchrun, accelerate, and experiment trackers

---

## 3. Introduction to Distributed Training

Distributed training allows heavy workloads (e.g. deep learning, large datasets) to be split across multiple GPUs or nodes; this is called data parallelism.

Key components;
- Each GPU processes a subset of the data
- Gradients are synchronized between devices every step
- Two common methods; DataParallel (easy, single machine), DistributedDataParallel (recommended for performance and scalability)

---

## 4. Environment Setup and Prerequisites

Before running distributed jobs, ensure that your environment supports multiple GPUs and has the required packages.

### Checking available GPUs

```python
import torch

print("GPUs detected: ", torch.cuda.device_count())
for i in range(torch.cuda.device_count()):
    print(f"GPU {i}:", torch.cuda.get_device_name(i))
```

- You should see at least two GPUs listed to proceed with multi-GPU demos

### Install required libraries (if missing)

```python
# Install accelerate package if not already present
!pip install accelerate
```

---

## 5. Running Distributed Jobs with torchrun

PyTorch's torchrun utility is recommended for launching distributed jobs.

### Example: Training a simple model using DistributedDataParallel

Modify a basic training script to support DDP

```python
import torch
import torch.nn as nn
import torch.optim as optim
import torch.multiprocessing as mp
import torch.distributed as dist
from torch.nn.parallel import DistributedDataParallel as DDP

def setup(rank, world_size):
    dist.init_process_group("nccl", rank=rank, world_size=world_size)
    torch.cuda.set_device(rank)

def cleanup():
    dist.destroy_process_group()

def train(rank, world_size):
    setup(rank, world_size)
    model = nn.Linear(10, 2).to(rank)
    ddp_model = DDP(model, device_ids=[rank])

    loss_fn = nn.MSELoss().to(rank)
    optimizer = optim.Adam(ddp_model.parameters(), lr=0.001)

    # Dummy input and target
    inputs = torch.randn(32, 10).to(rank)
    targets = torch.randn(32, 2).to(rank)

    for epoch in range(5):
        outputs = ddp_model(inputs)
        loss = loss_fn(outputs, targets)
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
        print(f"Rank {rank}, Epoch {epoch}, Loss: {loss.item()}")

    cleanup()

if __name__ == "__main__":
    world_size = torch.cuda.device_count()
    mp.spawn(train, args=(world_size,), nprocs=world_size, join=True)
```

- Save this script as `distributed_train.py` then launch with

```bash
torchrun --nproc_per_node=2 distributed_train.py
```
- Replace `2` with the number of available GPUs

---

## 6. (Optional) Using accelerate for Simplified Multi-GPU Training

Huggingface accelerate abstracts away some complexities of distributed PyTorch.

```python
from accelerate import Accelerator
import torch
import torch.nn as nn
import torch.optim as optim

accelerator = Accelerator()
device = accelerator.device

model = nn.Linear(10, 2)
optimizer = optim.Adam(model.parameters())

model, optimizer = accelerator.prepare(model, optimizer)

inputs = torch.randn(32, 10)
targets = torch.randn(32, 2)

for epoch in range(5):
    optimizer.zero_grad()
    outputs = model(inputs)
    loss = nn.MSELoss()(outputs, targets)
    accelerator.backward(loss)
    optimizer.step()
    print(f"Epoch {epoch}, Loss: {loss.item()}")
```

- To launch with accelerate:

```bash
accelerate config
accelerate launch your_script.py
```

- Follow prompts for device and distributed options

---

## 7. Monitoring Distributed Jobs; Experiment Tracking

Experiment tracking is a standard part of MLOps and industry AI workflows.

Here is an example using TensorBoard for basic scalar logging:

```python
from torch.utils.tensorboard import SummaryWriter

writer = SummaryWriter(log_dir="./runs/experiment1")

for epoch in range(10):
    # Training code...
    train_loss = 0.2 * epoch  # Dummy loss value
    writer.add_scalar("Loss/train", train_loss, epoch)

writer.close()
```

- After running your training script, launch TensorBoard:
```bash
tensorboard --logdir=./runs
```
- View metrics in your browser

---

## 8. Hands-on Challenge

- Modify a simple model to use `DistributedDataParallel` or `accelerate` for multi-GPU training (see above examples)
- Track training loss and another metric of your choice using TensorBoard or MLflow
- Try running your script with at least 2 GPUs; take a screenshot of the TensorBoard dashboard with your results

---

## 9. Troubleshooting Common Issues

- Ensure all dependencies support CUDA and are version matched (PyTorch, CUDA, torchrun, accelerate)
- NCCL backend is required for GPU; ensure driver compatibility and proper CUDA_VISIBLE_DEVICES settings
- Use unique output directories for logs and checkpoints to avoid conflicts
- Monitor GPU usage with `nvidia-smi` during training for resource bottlenecks

---

## 10. Reflection and Assessment Preparation

- What are the main benefits of distributed training in production AI?
- Describe the steps required to prepare and launch a distributed PyTorch job
- How does experiment tracking support MLOps standards in industry?
- List two issues that might arise in multi-GPU training and their solutions

---

## 11. Summary and Next Steps

- Distributed training is essential for scaling ML workloads in cloud and HPC
- torchrun and accelerate are industry tools for efficiently managing distributed jobs
- Experiment tracking is a baseline industry requirement; practice integrating it into all projects
- Next week; begin your final projects implementing these concepts, with support for both single and multi-GPU workflows
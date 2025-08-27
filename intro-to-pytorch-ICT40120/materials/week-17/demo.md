# Week 17 Demo; Multi-GPU Distributed Training, Experiment Tracking, and Performance Analysis

## Learning Objectives

- Understand principles and benefits of multi-GPU distributed training in PyTorch.
- Set up and run distributed jobs using torchrun or accelerate.
- Integrate experiment tracking tools to monitor training and analyse results.
- Interpret, compare, and present distributed training performance metrics.
- Prepare project results for technical and non-technical audiences.

---

## 1. Introduction; Real-World Industry Context

- High-performance ML teams routinely use distributed training to accelerate AI workloads; mastering this is key for production roles.
- Experiment tracking ensures reproducibility and comparison of different models or runs, forming the basis for MLOps best practices.
- Industry workflows demand code that is clear, well-tracked, and demonstrably scalable; this lab models those requirements.

---

## 2. Review; From Single-GPU to Multi-GPU Workflows

- In previous labs you implemented and ran PyTorch scripts on a single GPU; you learned to test, document, and report results.
- This week you will expand your workflow; scaling the same model to run in parallel over multiple GPUs using data parallelism.

---

## 3. Setup; Environment and Data Preparation

- Ensure your environment has access to at least two GPUs; this may be Azure VM or local workstation.
- Activate your Python virtual environment and install the required packages if needed.
- Required packages; torch, torchvision, accelerate or torchrun, tensorboard or wandb for experiment tracking.

```python
# Code Cell: Check and List Available GPUs
import torch

print("Torch version;", torch.__version__)
print("CUDA available;", torch.cuda.is_available())
print("Number of GPUs;", torch.cuda.device_count())
print("GPU Names;", [torch.cuda.get_device_name(i) for i in range(torch.cuda.device_count())])
```

> **Troubleshooting:** If no GPUs are listed, review your Azure VM or local CUDA setup. Consult the Week 14 troubleshooting handout.

---

## 4. Task; Refactor Single-GPU Model for Multi-GPU Training

- Update your training script; wrap your model with `torch.nn.DataParallel` or migrate components to use `torchrun` or `accelerate`.
- DataParallel example is simplest but less flexible; accelerate or torchrun is preferred for real-world use.

```python
# Code Cell: Sample Model Wrapping with DataParallel
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 128),
    nn.ReLU(),
    nn.Linear(128, 10)
)

if torch.cuda.device_count() > 1:
    print("Using", torch.cuda.device_count(), "GPUs!")
    model = nn.DataParallel(model)

model.cuda()
```

---

## 5. Distributed Training with torchrun; Step-by-Step Guide

- torchrun enables launching processes across multiple GPUs and nodes; part of PyTorch's distributed training toolkit.
- Example launch command for 2 GPUs:
  ```
  torchrun --nproc_per_node=2 your_script.py
  ```
- Your training script must initialize the distributed environment and set the right device per process.

```python
# Code Cell: Example Main Block for Distributed Setup
import torch
import torch.distributed as dist
import os

def main():
    dist.init_process_group("nccl")
    local_rank = int(os.environ["LOCAL_RANK"])
    torch.cuda.set_device(local_rank)
    print(f"Running on GPU {local_rank}")

    # Your model, dataloader, optimizer, etc.
    # model = ...
    # model.cuda(local_rank)
    # ...

if __name__ == "__main__":
    main()
```

---

## 6. Integrating Experiment Tracking; Logging Key Metrics

- Integrate tracking tools; use TensorBoard or Weights&Biases (wandb) for logging loss, accuracy, and runtime metrics.
- Set up dashboard or log file for easy comparison between single-GPU and multi-GPU results.

```python
# Code Cell: Simple TensorBoard Logging Example
from torch.utils.tensorboard import SummaryWriter

writer = SummaryWriter(log_dir='runs/distributed_demo')

for epoch in range(epochs):
    train_loss = ...
    val_accuracy = ...
    writer.add_scalar('Loss/train', train_loss, epoch)
    writer.add_scalar('Accuracy/val', val_accuracy, epoch)

writer.close()
```

> **Exercise:** Extend the logging code to record additional metrics such as GPU memory usage, throughput (images/sec), or gradient norm.

---

## 7. Exercise; Experiment Tracking with Weights&Biases (Optional Industry Tool)

- Log in or create a wandb account.
- Add wandb tracking lines to your script, logging all hyperparameters and metrics.

```python
# Code Cell: wandb Integration Example
import wandb

wandb.init(project="multi_gpu_demo")
wandb.config.update({"epochs": epochs, "batch_size": batch_size})

for epoch in range(epochs):
    train_loss = ...
    wandb.log({"train_loss": train_loss, "epoch": epoch})
# When training finishes
wandb.finish()
```

---

## 8. Interpreting Results; Comparing Performance

- Collect run-time, memory utilization, accuracy, and other metrics from both single-GPU and multi-GPU jobs.
- Use experiment tracking dashboards to visualize differences.
- Typical outcomes; multi-GPU speeds up training, but may have startup overhead or reduced scaling efficiency depending on model and batch size.

> **Discussion:** Why might distributed training not yield a perfect linear speedup? How can batch size and I/O become bottlenecks?

---

## 9. Prepare and Present Results; Assessment Expectations

- Create a summary table or graph comparing single-GPU and multi-GPU performance for your model.
- Document experiment parameters; number of GPUs, model hyperparameters, major differences in setup.
- Use screenshots from TensorBoard/wandb dashboards to support your analysis.
- Write a brief reflection; What worked well? What were the main bottlenecks? How might these be addressed in a production environment?

> **Submission checklist;**
> - Code with correct multi-GPU setup.
> - Experiment tracking (TensorBoard/wandb) screenshots.
> - Table or graph with performance comparison.
> - Short reflection (100-200 words).

---

## 10. Industry Best Practices; Troubleshooting and Quality Assurance

- Test your code by running short jobs before scaling up; check logs for silent failures.
- Reproducibility; make random seeds and environment settings explicit.
- Document any problems and how you solved them.
- Share your findings as you would with a team; clear code, tracked results, concise summary.

---

## 11. Reflection and Next Steps

- Project presentation in Week 18; practice explaining your workflow and interpreting results for both technical and non-technical audiences.
- Review industry checklists for model monitoring, scaling, and reporting before final submission.
- Prepare 1-2 questions about distributed training or experiment tracking for class discussion.

---

# Summary

- Distributed training enables scalable deep learning on modern hardware; critical for applied ML roles.
- Experiment tracking is fundamental for reliable, reproducible, and industry-standard workflows.
- Your Week 17 project is an integrated demonstration of these advanced, workplace-ready skills.
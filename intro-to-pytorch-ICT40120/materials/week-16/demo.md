# Week 16 Demo; Complete Single-GPU Training Workflow in PyTorch

## Introduction and Learning Objectives

- Understand and implement the complete end-to-end deep learning pipeline using PyTorch on a single GPU.
- Demonstrate clear evidence of competency for assessment, aligning with industry standards for documentation and reproducibility.
- Reflect on the importance of code clarity, workflow structure, and best practices in ML engineering.


## Agenda

1. Setup; hardware and software preparation
2. Data preparation; loading and pre-processing
3. Model definition; PyTorch neural network modules
4. Training loop; GPU device utilisation
5. Model evaluation; metric calculation and result interpretation
6. Checkpointing and saving artefacts
7. Evidence gathering for assessment
8. Industry alignment and reflection activities
9. Troubleshooting and reproducibility best practices
10. Wrap-up and next steps

---

## 1. Setup; Hardware and Software Preparation

- Ensure access to a GPU-enabled environment; e.g. Azure GPU VM, Kaggle notebook, or local hardware with CUDA.
- Required software; Python 3.8+, PyTorch, Jupyter or Jupytext-compatible code editor.
- Confirm PyTorch detects the GPU and set device before proceeding.

```python
import torch

# Check if CUDA GPU is available
if torch.cuda.is_available():
    device = torch.device('cuda')
    print('GPU is available and PyTorch is using:', torch.cuda.get_device_name(0))
else:
    device = torch.device('cpu')
    print('No GPU detected; defaulting to CPU')
```

---

## 2. Data Preparation; Loading and Pre-processing

- Use a standard dataset; e.g. MNIST or CIFAR-10 for demo clarity.
- Apply typical transformations; normalization, conversion to tensors.
- Demonstrate loading data with proper batching for GPU acceleration.

```python
from torchvision import datasets, transforms
from torch.utils.data import DataLoader

# Data pre-processing pipeline
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))
])

# Load dataset; here using MNIST as an example
train_dataset = datasets.MNIST(root='./data', train=True, download=True, transform=transform)
test_dataset = datasets.MNIST(root='./data', train=False, download=True, transform=transform)

# DataLoaders for batching
batch_size = 64
train_loader = DataLoader(train_dataset, batch_size=batch_size, shuffle=True)
test_loader = DataLoader(test_dataset, batch_size=batch_size, shuffle=False)
```

---

## 3. Model Definition; PyTorch Neural Network Construction

- Define a simple neural network using PyTorch nn.Module.
- Demonstrate moving model to GPU device.

```python
import torch.nn as nn
import torch.nn.functional as F

class SimpleMLP(nn.Module):
    def __init__(self):
        super(SimpleMLP, self).__init__()
        self.fc1 = nn.Linear(28*28, 128)
        self.fc2 = nn.Linear(128, 64)
        self.fc3 = nn.Linear(64, 10)
    
    def forward(self, x):
        x = x.view(-1, 28*28)  # flatten
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x

# Instantiate and move to device
model = SimpleMLP().to(device)
print(model)
```

---

## 4. Training Loop; GPU Device Utilisation

- Set up an optimizer (e.g. Adam), loss criterion, and training loop.
- Ensure all data and model computations are on the GPU.
- Monitor and print training progress.

```python
import torch.optim as optim

criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

# Training process
num_epochs = 5
for epoch in range(num_epochs):
    model.train()
    running_loss = 0.0
    for images, labels in train_loader:
        images, labels = images.to(device), labels.to(device)  # move to GPU
        
        optimizer.zero_grad()
        outputs = model(images)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()
        
        running_loss += loss.item()
    print(f'Epoch {epoch+1}; Loss; {running_loss/len(train_loader):.4f}')
```

---

## 5. Model Evaluation; Metric Calculation and Result Interpretation

- Evaluate accuracy on test set, explain metrics.
- Move model to evaluation mode, disable gradient computation.

```python
model.eval()
correct = 0
total = 0
with torch.no_grad():
    for images, labels in test_loader:
        images, labels = images.to(device), labels.to(device)
        outputs = model(images)
        _, predicted = torch.max(outputs.data, 1)
        total += labels.size(0)
        correct += (predicted == labels).sum().item()

print(f'Accuracy on test dataset; {100 * correct / total:.2f}%')
```

---

## 6. Checkpointing and Saving Artefacts

- Save trained model parameters for reproducibility and future use.
- Demo the save and load process.

```python
model_path = 'simplemlp_mnist.pth'
torch.save(model.state_dict(), model_path)
print('Model checkpoint saved at', model_path)

# To load the model elsewhere:
# model.load_state_dict(torch.load(model_path))
```

---

## 7. Evidence Gathering for Assessment

- Document analytics output; loss curves, accuracy scores.
- Take screenshots or download results for submission (per assessment guidance).
- Ensure all code is well-commented and every stage includes markdown explanation.

---

## 8. Industry Alignment and Reflection Activities

- Discuss typical industry workflows; why GPUs are essential for rapid experimentation.
- Invite students to relate each demo step to a real-world deployment; e.g. 'How would you automate this pipeline on Azure or within an MLOps workflow?'
- Example reflection question; What steps would you add to meet Responsible AI principles or model versioning standards?

---

## 9. Troubleshooting and Reproducibility Best Practices

- Common errors; CUDA out of memory, device mismatch, data loader bottlenecks.
- Tips for avoiding workflow errors; always specify device, validate CUDA availability before batch jobs, log environment and library versions.
- Encourage using script headers to auto-select device and warn on fallback.

---

## 10. Summary and Next Steps

- Reviewed full cycle from data loading to evaluation on GPU using PyTorch.
- Clear evidence required for assessment; annotated code, metric output, model artefacts.
- Prepare for next week; multi-GPU workflows, distributed training, and scaling experiments.
- Encourage saving your notebook and results for reassessment week if needed.

---

# Practical Exercise

- Complete the MNIST end-to-end workflow as per the demo.
- Experiment with model structure or optimizer; record and comment on the effect.
- Generate an evidence report using screenshots, markdown summaries, and saved models for your assessment submission.

---

# Reflection and Assessment Preparation

- How did single-GPU acceleration improve your training process?
- What documentation or artifacts will you prepare for your assessment evidence?
- Which best practices would you share with a new team member joining this workflow?
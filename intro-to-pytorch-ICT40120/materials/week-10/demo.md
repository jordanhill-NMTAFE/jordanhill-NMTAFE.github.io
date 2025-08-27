# Week 10 Portfolio Project Workshop: PyTorch Fundamentals and Portfolio Readiness

## Learning Objectives
- Apply foundational PyTorch skills to develop a mini-project suitable for your portfolio.
- Integrate Bash and Python scripting for automation and reproducibility.
- Use documentation and industry coding standards in code review and portfolio assembly.
- Develop skills in code testing, reflection, and best practice documentation.

---

## Agenda

- Quick Recap; PyTorch Fundamentals from Weeks 5-6
- Hands-on: Tensor Operations and Autograd in PyTorch
- Practice: Bash & Python integration for ML workflows
- Code Documentation and Review Activity
- Portfolio Preparation; Testing and Reflection
- Summary and Next Steps

---

## [1] Environment Setup (Python & PyTorch)

```python
import torch
print("PyTorch version:", torch.__version__)

# Check if GPU is available.
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
print("Device selected:", device)
```

*Instructions; Run this cell to ensure your environment is ready for PyTorch development.*

---

## [2] PyTorch Tensors: Foundations

- Tensors are the primary data structure in PyTorch.
- Real-world example; images, time series, tabular data.

```python
# Create tensors and perform basic operations.
a = torch.tensor([2.0, 4.0, 6.0])
b = torch.ones(3)
sum_ab = a + b

print("Tensor a:", a)
print("Tensor b:", b)
print("Sum:", sum_ab)
print("Multiplication:", a * b)
```

*Practical exercise; Create a tensor for a mini batch of 3 images, each 2x2.*

---

## [3] Autograd Basics; Automatic Differentiation

- Autograd supports gradient calculation critical for ML.
- Industry link; All neural network training leverages this feature.

```python
x = torch.tensor(2.0, requires_grad=True)
y = x**3 + x**2
y.backward()  # Computes gradient

print("Gradient at x=2:", x.grad)
```

*Question; Why is setting requires_grad=True important in your ML projects? Document your answer below.*

---

## [4] Neural Network Module Practice

- Define a simple linear model using nn.Module.
- Review the class structure for portfolio quality.

```python
import torch.nn as nn

class SimpleModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc = nn.Linear(2, 1)
    def forward(self, x):
        return self.fc(x)

# Instantiate and inspect model
model = SimpleModel()
print(model)
```

*Industry tip; Always document your model class using docstrings and comments.*

---

## [5] Bash & Python Integration for Workflow Automation

- Real-world scenario; Downloading a dataset and launching a training script.

```bash
# Bash: Download the iris dataset (Linux/Mac command)
wget https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data -O iris.csv
```

```python
# Python: Load and inspect the dataset
import pandas as pd
df = pd.read_csv('iris.csv', header=None)
print(df.head())
```

*Exercise; Write a Bash script to create a backup of your Jupyter notebook using cp.*

---

## [6] Best Practice Coding, Documentation, and Review

- Use clear comments and docstrings for every function/module.
- Example function with documentation:

```python
def normalize_tensor(tensor):
    """
    Normalize a PyTorch tensor to range [0,1].
    Args:
        tensor (torch.Tensor): Input tensor.
    Returns:
        torch.Tensor: Normalized tensor.
    """
    return (tensor - tensor.min()) / (tensor.max() - tensor.min())
```

*Portfolio activity; Refactor one of your previous notebooks to include clear docstrings, comments, and versioning notes.*

---

## [7] Testing & Reflection; Industry-aligned Standards

- Validate your code using assertions or test scripts.

```python
test_tensor = torch.tensor([5.0, 10.0])
output = normalize_tensor(test_tensor)
assert torch.allclose(output, torch.tensor([0.0, 1.0]))
```

*Reflection; Write 2-3 sentences about the value of testing and documentation in AI/ML model deployment. How does this align with industry expectations?*

---

## [8] Troubleshooting Guidance

- Common errors; Shape mismatches, missing gradients, device errors.
    - *Tip; Always check tensor shapes and device assignments in early debug steps.*
    - For CUDA errors; confirm GPU availability and move tensors to device with tensor.to(device).

---

## [9] Peer Review and Portfolio Enhancement

- Exchange your notebook with a peer.
- Use a checklist; comments, docstrings, logical structure, test coverage.
- Provide at least one constructive suggestion.

---

## [10] Summary and Next Steps

- This workshop has reinforced critical PyTorch and workflow skills needed for your portfolio project.
- Your updated notebook will form the basis for your first assessment submission.
- Next week; deeper focus on documentation, experiment tracking, and workflow automation.

---

## Reflection Questions

- What aspect of PyTorch did you find most challenging, and how did you overcome it?
- How would you explain the role of Bash scripting in cloud-based ML workflows to a colleague?
- List two ways to ensure your code meets industry documentation standards.
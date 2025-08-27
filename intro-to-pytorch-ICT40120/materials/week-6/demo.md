# Week 6 Demo: Building a Simple Neural Network in PyTorch

## Learning Objectives
- Understand PyTorch's autograd system for automatic differentiation
- Define and construct a basic neural network using PyTorch modules and layers
- Perform and visualize forward and backward passes
- Diagnose common autograd and tensor errors and apply debugging best practices
- Connect model components and workflows to real-world industry scenarios

---

## 1. Introduction and Motivation

Deep neural networks are the backbone of modern AI applications. This workshop shows how to define, train, and debug a simple neural network in PyTorch—covering essentials for building production-ready models and preparing for scalable GPU/cloud training.

---

## 2. Setup and Requirements

```python
# Ensure these libraries are installed in your environment
import torch
import torch.nn as nn
import torch.optim as optim

# Check PyTorch and GPU availability
print("PyTorch version:", torch.__version__)
print("CUDA available:", torch.cuda.is_available())
```

---

## 3. PyTorch Autograd Basics

Autograd is PyTorch's automatic differentiation system. It tracks operations on tensors with requires_grad=True, enabling flexible computation of gradients for model training.

```python
# Create tensors with autograd tracking enabled
x = torch.tensor([2.0, 3.0], requires_grad=True)
y = x * 3 + 2
z = y.sum()
print('Value of z:', z.item())
z.backward()  # Perform backpropagation
print('Gradient of x:', x.grad)
```

### Key Takeaways
- Autograd tracks tensor operations to build a computation graph.
- Calling .backward() computes all gradients needed for optimization.

---

## 4. Building a Simple Neural Network

PyTorch neural networks are defined as subclasses of nn.Module. Layers are assembled in the constructor, and the forward method implements computation from input to output.

### Industry Context
In the workplace, modular, reusable PyTorch models accelerate experimentation and deployment in AI workflows—essential for production ML pipelines.

```python
class SimpleNet(nn.Module):
    def __init__(self, input_dim, hidden_dim, output_dim):
        super(SimpleNet, self).__init__()
        self.fc1 = nn.Linear(input_dim, hidden_dim)       # Input to hidden
        self.relu = nn.ReLU()                             # Activation
        self.fc2 = nn.Linear(hidden_dim, output_dim)      # Hidden to output
        
    def forward(self, x):
        out = self.fc1(x)
        out = self.relu(out)
        out = self.fc2(out)
        return out

# Initialize the network
net = SimpleNet(input_dim=2, hidden_dim=4, output_dim=1)
print(net)
```

---

## 5. Manual Forward and Backward Pass

Trace the flow of a sample input through the network and understand how errors are propagated backward for learning.

```python
# Example input and target
input = torch.tensor([[1.0, -1.0]], requires_grad=True)
target = torch.tensor([[0.5]])

# Forward pass (prediction)
output = net(input)
print('Output:', output.item())

# Calculate loss
loss_fn = nn.MSELoss()
loss = loss_fn(output, target)
print('Loss:', loss.item())

# Backward pass (compute gradients)
loss.backward()
for name, param in net.named_parameters():
    if param.requires_grad:
        print(f'Gradient for {name}: {param.grad}')
```

---

## 6. Common Debugging: Autograd and Shape Errors

### Frequent Pitfalls
- Mismatch in input/output shapes.
- Forgetting requires_grad=True.
- In-place operations that break the computation graph.

### Example 1: Shape Mismatch Error

```python
try:
    input_bad = torch.tensor([1.0, 2.0, 3.0])  # Wrong shape for input_dim=2
    net(input_bad)
except Exception as e:
    print('Shape error:', str(e))
```

### Example 2: In-place Operation Error

```python
bad_tensor = torch.tensor([1.0, 2.0], requires_grad=True)
try:
    bad_tensor += 1  # In-place; can break autograd
    bad_tensor.backward(torch.ones_like(bad_tensor))
except Exception as e:
    print('In-place op error:', str(e))
```

**Best Practice**; Always check tensor shapes and use out-of-place operations when working with autograd.

---

## 7. Hands-On Exercise

- Define your own neural network class with different layer sizes
- Pass a batch of random inputs through the network
- Identify and fix any shape or type errors
- Calculate loss and perform backward propagation

```python
# TODO: Fill in dimensions and try different architectures, e.g., more layers
class StudentNet(nn.Module):
    def __init__(self):
        super(StudentNet, self).__init__()
        # Your layers here
        pass
    
    def forward(self, x):
        # Your computation here
        pass

# Create input and test your network
```

---

## 8. Industry Case Study

*Scenario*: You are tasked with building a network to predict equipment failure in a manufacturing plant using sensor data. The sensors provide multivariate numerical data daily.

**Discussion**;
- How would you structure your input layer?
- What shapes and datatypes would you expect from your data pipeline?
- What production issues could shape/autograd errors cause in a factory setting?

---

## 9. Troubleshooting Checklist

- Check input and output tensor shapes at each step
- Verify requires_grad status for tensors that need gradients
- Watch for unintended in-place operations (avoid .add_(), .relu_(), etc.)
- Use loss.backward() only once per computational graph unless retain_graph=True

---

## 10. Reflection and Assessment Prep

- How does PyTorch’s autograd system simplify model training compared to manual differentiation?
- What steps are needed to transition from a working script to a scalable, production-grade ML pipeline?
- What are the key differences in debugging code locally, on cloud VMs, and on distributed GPUs?
- Try writing unit tests for your SimpleNet to check input shapes and gradient flow

---

## 11. Summary and Next Steps

- You can now define, train, and debug basic neural networks with PyTorch
- These foundations will power future work in GPU computing, distributed training, and production ML
- Prepare by reviewing the official PyTorch tutorials on [Neural Networks](https://pytorch.org/tutorials/beginner/blitz/neural_networks_tutorial.html) and [Autograd](https://pytorch.org/tutorials/beginner/blitz/autograd_tutorial.html)
- Next week; You’ll apply these skills to real cloud GPU environments and manage scalable AI workflows in Azure

---

### End of Demo
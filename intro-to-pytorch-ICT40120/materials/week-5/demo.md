# Week 5: Practical Tensor Manipulation with PyTorch

## Learning Objectives
- Understand the role of PyTorch and tensors in modern machine learning workflows
- Create, index, reshape, and batch tensors in PyTorch
- Connect tensor operations to real-world, industry workflows
- Develop skills foundational for rapid prototyping, model development, and scalable ML on cloud/HPC

---

## 1. Introduction; The Role of PyTorch in Industry

PyTorch is widely used for developing, training, and deploying machine learning and AI models. Its tensor library enables fast mathematical operations on CPU and GPU, making it especially powerful for high-performance and cloud-based ML workflows.

- PyTorch is fundamental for machine learning engineers working on scalable, production-ready systems
- Tensor manipulation forms the backbone of all training, inference, and data transformation tasks

---

## 2. Environment Setup

Before starting, ensure you have access to JupyterLab or VSCode and PyTorch installed (CPU or GPU). For cloud delivery, this may be on Azure or local Ubuntu VMs. Check installation with:

```python
import torch
print(torch.__version__)
print("CUDA Available?" , torch.cuda.is_available())
```

---

## 3. Creating Tensors

Tensors are multi-dimensional arrays, similar to NumPy arrays, but with GPU acceleration. Industry AI models use tensors to store data, parameters, gradients, and more.

### Create various types of tensors

```python
import torch

# Create a tensor from a list
tensor_example = torch.tensor([[1, 2], [3, 4]])
print("2x2 Tensor;")
print(tensor_example)

# Random tensor for initialising neural network weights
weights = torch.rand(3, 3)
print("3x3 Random Weight Matrix;")
print(weights)

# Zero and one tensors, useful for data/batch initialization
zeros_tensor = torch.zeros(2, 4)
ones_tensor = torch.ones(4)
print(zeros_tensor)
print(ones_tensor)
```

---

## 4. Indexing and Slicing Tensors

Practical machine learning workflows require extracting and updating tensor values with high performance; for example, selecting batches or updating model parameters.

```python
data = torch.arange(16).reshape(4, 4)
print("Original Data;")
print(data)

# Index single value
print("Value at row 1, col 2;", data[1, 2])

# Slice a batch (rows 1 and 2)
print("Rows 1 and 2;")
print(data[1:3])

# Update a section (simulate gradient update step)
data[0:2, 0:2] = 99
print("After update;")
print(data)
```

**Practical tip:** Efficient slicing supports scalable data loading in production training.

---

## 5. Reshaping and Transposing Tensors

Real-world ML tasks (e.g., computer vision, NLP) often require reshaping data for batch processing or neural network input.

```python
batch = torch.arange(24).reshape(2, 3, 4)  # Example: 2 batches, 3 instances, 4 features
print("Original Shape;", batch.shape)

# Flatten all but batch for feeding into linear layer
flattened = batch.view(2, -1)
print("Flattened for NN input;", flattened.shape)

# Transpose dimensions (common in sequence models)
transposed = batch.permute(1, 0, 2)
print("Transposed Shape;", transposed.shape)
```

---

## 6. Batch Operations and Broadcasting

Industry standard ML operations involve automatic expansion (broadcasting) to efficiently handle data of varying shapes – crucial for cloud scale ML.

```python
a = torch.ones(2, 3)
b = torch.arange(3)
# Broadcasting b to shape (2, 3)
sum_result = a + b
print("Broadcast Addition Result;")
print(sum_result)
```

---

## 7. Hands-On Challenges

### Exercise 1; Create a 3D tensor of shape (4, 3, 2) filled with random numbers
### Exercise 2; Extract the second “row” from each “batch” of your tensor
### Exercise 3; Reshape a (16,) tensor into a (4, 4) matrix, then transpose it
### Exercise 4; Simulate a batch update by multiplying all elements in the first batch by 0.9
### Exercise 5; Document one practical scenario in your own words where tensor reshaping is necessary in machine learning

---

## 8. Industry Case Study; Why Tensor Manipulation Matters

In a production AI pipeline, model training requires loading massive volumes of image data, batching into tensors, reshaping for GPU memory efficiency, and slicing for augmentations; these workflows enable companies to scale up deep learning pipelines on cloud VMs and HPC clusters.

- “How does this relate to your work or future role?” Reflect on how precise tensor control enables scalable, reliable ML deployments

---

## 9. Troubleshooting and Best Practices

- If you get shape mismatch errors, print tensor shapes at each step
- Use .clone() when making modified copies of tensors to avoid in-place changes affecting original data
- Apply .to(device) to move tensors to GPU for large-scale acceleration

---

## 10. Reflection and Assessment Preparation

- Complete all code examples and exercises; compare your answers with peers for review
- Document at least two “gotchas” or issues you encountered and how you solved them; this aligns with industry documentation standards
- Prepare a 1-2 sentence summary; why is practical tensor manipulation essential for AI engineers working in industry?

---

## 11. Summary and Next Steps

- This session has established key skills for working with PyTorch tensors, a foundation for cloud ML, GPU acceleration, and distributed training
- Review and annotate your code examples; this will form a portfolio component for Week 10 assessment
- Next week we build on these foundations to start using PyTorch autograd and neural network modules
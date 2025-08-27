# Week 11 Demo; Production ML Workflows and Experiment Tracking

## Learning Objectives
- Understand the purpose of experiment tracking in machine learning workflows
- Set up and run MLflow or Weights & Biases to track PyTorch experiments
- Document and interpret experiment results with tracking dashboards
- Apply reproducibility, transparency, and responsible AI principles in real-world projects

---

## 1. Introduction; Why Track ML Experiments?

- Machine learning development often involves running multiple experiments; without tracking, results can become disorganised or lost
- Experiment tracking enables reproducibility, transparency, and compliance; critical for production environments and workplace standards
- Industry requires clear model documentation, versioning, and clear audit trails for model behaviour and evaluation metrics

---

## 2. Overview of Experiment Tracking Tools

- MLflow and Weights & Biases (W&B) are popular open-source tools for tracking ML experiments; both integrate with PyTorch and support cloud-based workflows
- Tracking tools record configuration parameters, code versions, training metrics, results, and artefacts (such as model weights)
- Allows comparison of different experiment runs and supports model versioning for deployment readiness

---

## 3. Hands-On Demo; Setting Up Tracking for PyTorch Experiments

### Step 1; Environment Setup

- Ensure Python, pip, and PyTorch are installed; install MLflow or W&B as shown

```python
# Uncomment the following line to install MLflow
# !pip install mlflow

# Uncomment the following line to install Weights & Biases
# !pip install wandb
```

---

### Step 2; Quickstart; Logging with MLflow

- Import MLflow and set up a simple experiment tracking context

```python
import mlflow
import torch
import torch.nn as nn

# Dummy experiment; simple linear model
with mlflow.start_run(run_name="linear_regression_demo"):
    model = nn.Linear(10, 1)
    mlflow.log_param("input_dim", 10)
    mlflow.log_param("output_dim", 1)
    mlflow.log_param("learning_rate", 0.01)
    
    # Simulate a metric (loss)
    train_loss = 0.123
    mlflow.log_metric("train_loss", train_loss)
    # Log a model file
    torch.save(model.state_dict(), "model_weights.pth")
    mlflow.log_artifact("model_weights.pth")
```

- Run the above cell; MLflow will save parameters, metrics, and the model to its default directory

---

### Step 3; View and Interpret Results

- To start the local MLflow UI and explore your results, run in the terminal:

```
mlflow ui
```

- Open the URL provided and observe experiment runs, parameters, metrics, and artefacts

---

### Alternative; Quickstart with Weights & Biases

- Login to W&B (requires free account) and initialise a run

```python
import wandb
wandb.login()  # Single-time login in notebook

run = wandb.init(project="pytorch_experiment_demo")
config = wandb.config
config.learning_rate = 0.01

# Simulate loss logging
wandb.log({"train_loss": 0.123})

wandb.finish()
```

- View your run at https://wandb.ai/; compare metrics, parameters, and visualizations in the W&B dashboard

---

## 4. Documenting and Interpreting Results

- Use tracking dashboards to visualise and compare multiple experiment runs; look for changes in loss, accuracy, or other metrics across different configurations
- Document key findings and model configuration in your experiment report; note which run produced the best performance and why
- Industry standard is to include: model version, data version, training parameters, results, and hyperparameter configurations in all model documentation

---

## 5. Industry Example; Reproducibility and Compliance

- Many organisations require all model training to be tracked and reproducible; this supports responsible AI and compliance with data governance regulations
- Example; A government AI project must audit all model decisions; experiment tracking is essential for demonstrating transparency and repeatability

---

## 6. Practical Exercise

- Task; Modify the provided PyTorch script to track an additional hyperparameter (e.g. batch size or optimizer type) and log validation accuracy after each epoch
- Compare at least two runs with different parameters; use MLflow or W&B dashboard to interpret which setup performed best

---

## 7. Troubleshooting and Best Practices

- If the tracking dashboard does not show new runs, confirm your script is calling log_param, log_metric, or wandb.log correctly
- Ensure unique run names or identifiers for each experiment
- Always document code version and data source for reproducibility; this supports MLOps and industry deployment pipelines

---

## 8. Reflection and Assessment Preparation

- Questions for review; Why is experiment tracking critical in production ML pipelines? What information should be included in experiment logs for workplace compliance? How does structured experiment tracking prepare you for deployment and MLOps workflows?
- Apply tracking workflows to upcoming assessments and projects; use experiment tracking to evidence and justify model development decisions

---

## 9. Summary and Next Steps

- This week; you set up, ran, and interpreted experiment tracking with MLflow/W&B; gained experience with documentation and reproducibility best practices
- Next week; Focus on Cloud Automation and Autoscaling for ML workloads using Azure and Bash scripting; Experiment tracking will be integrated into cloud pipelines
---
layout: default
title: "intro-to-pytorch-ICT40120"
permalink: /intro-to-pytorch-ICT40120/
---

## Course Materials

### Slides
View the course slides in the [slides directory](slides/).

### Notebooks
Access the course notebooks in the [notebooks directory](notebooks/).

### Guides and Handouts
Find course guides and handouts in the [materials directory](materials/).



# intro-to-pytorch-ICT40120

## Course Overview
**Course Overview: PyTorch and Cloud-Based Machine Learning Workflows**

> Assessment policy update: All assessments are deferred until next term and will be assessed via one Final Portfolio. This term is formative-only: students practice PyTorch and cloud skills without graded submissions. Guidance remains in `2 KAD/5 Assess Tool/`, but due dates are moved to next term.

This hands-on TAFE course is designed for aspiring machine learning practitioners and cloud engineers seeking to bridge the gap between foundational programming and real-world AI development. Delivered over 20 weeks in a face-to-face format at NMTAFE East Perth, this course takes a project-driven approach—helping students gain both the technical depth and practical experience needed to thrive in the rapidly evolving field of machine learning (ML) and artificial intelligence (AI).

**What you will learn:**

- **PyTorch Fundamentals:** Build a solid foundation by mastering PyTorch tensor operations, automatic differentiation (autograd), and the construction of neural network modules. Develop and test production-quality scripts and applications suitable for real-world AI tasks.
- **GPU-Accelerated and Distributed Computing:** Gain hands-on experience in utilizing GPU resources for ML training and inference. Learn how to scale workloads effectively, moving from single-GPU experiments to distributed training using torchrun and accelerate.
- **Cloud Infrastructure for AI:** Configure and manage Microsoft Azure GPU virtual machines—deploy, monitor, and optimize cloud-based compute, storage, and networking resources for scalable, high-performance ML workloads.
- **Automation and Scripting:** Use Bash scripting to automate cloud environment management, support concurrent workflows, and enforce best practices in efficiency and reproducibility.
- **End-to-End Machine Learning Projects:** Develop, document, and present two full-scale PyTorch applications—including both solo and team-based components—that demonstrate your mastery from fundamentals to deployment and monitoring.

**Key skills and knowledge areas:**

- Script writing (Python, Bash) with focus on ML automation and integration (unit: ICTPRG435)
- Cloud service configuration (Azure VMs, autoscaling, managed databases, storage) (unit: ICTCLD401)
- High Performance Computing (HPC) concepts relevant to ML/AI
- Model versioning, documentation, and model monitoring (MLOps basics)
- Responsible AI, testing frameworks, and workplace-ready standards

**Practical applications:**

Throughout the course, you’ll work on realistic projects and simulated workflows modeled after those used by local software companies and government departments. Assessments will include developing and debugging scripts, configuring and scaling cloud environments, and running distributed ML training with Azure and PyTorch.

By course completion, you’ll have a portfolio that demonstrates your ability to:
- Develop, test, and document interactive scripts for ML workflows
- Configure, automate, and scale GPU cloud infrastructure to meet business and technical needs
- Apply best practices in AI model management, monitoring, and responsible deployment

**Who is this for?**

This course is tailored for Cert IV data science and AI students with foundational Python and ML knowledge. It's ideal if you’re preparing for a career as an AI developer, ML engineer, or cloud computing specialist—and want real-world, job-ready skills in ML engineering and cloud-based AI.

**Industry relevance and workplace preparation:**

Every topic and task is contextualized to current industry needs—including model deployment, versioning, and parallel processing for AI using cutting-edge tools like PyTorch, accelerate, and Hugging Face. You'll develop technical skills mapped directly to the requirements of leading employers and workplace projects, positioning you for success in the fast-moving AI industry.

**Expectations and commitment:**

This is an intensive, project-based course. Students should expect approximately 3 hours of class time and 2 hours of out-of-class study per week, totaling 100 hours of structured learning and hands-on practice. All assessments must be completed at a competent level to achieve certification. You’ll regularly engage in practical labs, real-world problem-solving, and portfolio-building activities—developing both your technical expertise and your readiness for the workforce.

## Course Structure
- **1 Learning Materials**: Weekly learning materials and resources
- **2 KAD**: Knowledge and Assessment Development
  - **1 LAP**: Learning and Assessment Plan
  - **2 Preassess Validation**: Pre-assessment validation documents
  - **3 Postassess Validation**: Post-assessment validation documents
  - **4 Assess Sub and FB Form**: Assessment submission and feedback forms
  - **5 Assess Tool**: Assessment tools and instruments
  - **6 Marking Guide**: Assessment marking guides
  - **7 Assess Mapping Matrix**: Assessment mapping matrices
- **Unit of Competencies**: Unit of competency documents
- **docs**: Additional documentation
- **Mock Policies**: Mock organizational policies for assessment

## Getting Started
1. Review the Learning and Assessment Plan in `2 KAD/1 LAP/`
2. Update course-specific information in `2 KAD/1 LAP/fields.md`
3. Customize assessment tools in `2 KAD/5 Assess Tool/`
4. Add learning materials to `1 Learning Materials/`

## Development Setup
This course uses `uv` for dependency management. To set up the development environment:

```bash
# Install uv if not already installed
curl -LsSf https://astral.sh/uv/install.sh | sh

# Create virtual environment and install dependencies
uv venv
uv pip install -e .

# For development dependencies
uv pip install -e ".[dev]"
```

## Content Generation
Use the content generator to create Word documents from the markdown files:
```bash
python -m src.main generate --target /path/to/course
```

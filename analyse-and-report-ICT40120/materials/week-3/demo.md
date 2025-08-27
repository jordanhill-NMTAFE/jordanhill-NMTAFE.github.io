# Week 3 Demo; Ethical Dilemmas; Case Study Exercises

## Setup and Introduction

- Welcome and outline today’s focus; Building ethical awareness in handling open datasets used in AI.
- Review key concepts from last week; Importance of reliable data sources in AI; Connect to the need for ethical/legal compliance.

## Learning Objectives

- Understand basic data ethics principles and relevant legal frameworks for AI and data science.
- Identify legal risks and ethical dilemmas common in large open datasets.
- Develop practical skills for group analysis and decision-making on real-world scenarios in data ethics.

---

## Part 1; Foundations of Data Ethics and Legal Compliance

### Markdown Cell  
- Data ethics includes principles like privacy, fairness, accountability, and transparency; These guide responsible AI development.
- Legal obligations for data handling often include laws such as GDPR, Australian Privacy Act, and codes of practice for data use.
- Organisations must comply with regulations and also self-regulate using best-practice guidelines.

### Group Discussion Prompt  
- What are examples of laws or codes you may have heard of that impact how data is collected and used?  
- Why is it important to think about ethics as well as compliance in AI?

---

## Part 2; Industry Case Study Introduction

### Markdown Cell  
- In industry, teams often work with massive open datasets (e.g. LAION-5B, COCO) where ethical and legal issues can arise; For example, collecting images from the internet without explicit consent, or data containing personal information.
- Real-world datasets sometimes have hidden risks; e.g., inclusion of sensitive data, copyright concerns, or potential biases that may harm particular groups.
- Today you will work in small groups on case studies to identify risks and propose solutions.

---

## Part 3; Case Study Activities

### Case Study 1; Consent and Privacy in Open Image Datasets

#### Markdown Cell  
- Scenario; A team is using a large, web-scraped dataset (like LAION-5B) to train an image recognition model; Some images appear to contain private individuals in public and private spaces; The dataset does not have explicit user consent.
- Discuss in groups;  
  - What are the major ethical and legal risks?  
  - What steps could the team take to reduce harm and ensure compliance?
- Each group shares their key points with the class.

---

### Case Study 2; Bias and Fairness in Dataset Collection

#### Markdown Cell  
- Scenario; A dataset from Kaggle is being repurposed to build an AI model for job application screening; Analysis reveals an over-representation of data from one gender and one geographic region.
- Discuss in groups;  
  - What are the potential impacts of bias in this dataset?  
  - What ethical principles are being challenged?
  - Propose steps for improving dataset fairness.

---

### Hands-On Practical; Identifying Sensitive Attributes

#### Markdown Cell  
- In many datasets, identifying and documenting “sensitive attributes” is part of ethical data handling.
- Try this sample code to explore a small sample dataset and flag potential sensitive fields.

```python
import pandas as pd

# Example data (adapted from a UCI dataset)
data = {
    'user_id': [1, 2, 3, 4],
    'age': [25, 37, 29, 41],
    'gender': ['M', 'F', 'F', 'M'],
    'country': ['AU', 'US', 'AU', 'IN'],
    'image_url': [
        'img1.jpg', 'img2.jpg', 'img3.jpg', 'img4.jpg'
    ]
}
df = pd.DataFrame(data)

# Identify potential sensitive fields
sensitive_fields = ['age', 'gender', 'country', 'image_url']
df[sensitive_fields]
```

#### Reflection Prompt  
- Which of these fields might present privacy, bias, or fairness challenges if used incorrectly?
- How could metadata and documentation help reduce ethical risks in real projects?

---

## Part 4; Class Discussion and Industry Relevance

### Markdown Cell  
- Ask each group to summarize their case and main recommendations.
- Discuss;  
  - How do these scenarios reflect real roles in AI research labs or data engineering teams?
  - What skills are required to recognize and address ethical dilemmas in practice?
  - How are workplace responsibilities shaped by industry codes, not just laws?

---

## Part 5; Summary and Next Steps

### Markdown Cell  
- Recap main points; Data ethics and legal compliance are critical skills for all AI and data science roles.
- Open datasets have real risks; Teams must be proactive in identifying and addressing issues.
- Next week; We will start working hands-on with Python and open source tools that help manage data workflows responsibly.

### Reflection Questions

- What is the difference between legal compliance and ethical responsibility?
- Why do organisations need both policies and active decision-making to handle open datasets safely?
- Share one example from today’s cases that surprised you or challenged your assumptions.
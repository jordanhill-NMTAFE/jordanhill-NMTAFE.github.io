# Week 11 Workshop: Drafting Clear, Stakeholder-Focused EDA Reports

## Learning Objectives
- Identify the key components of a clear, concise EDA report for industry stakeholders.
- Practice synthesising data insights for actionable recommendations.
- Develop technical communication skills and apply peer review feedback to improve report quality.

---

## Setup and Introduction

This week, you will work in teams to draft, review, and refine sample EDA report sections using open datasets. We will use Jupyter notebooks and Python tools from industry, focusing on how technical analysis is presented clearly for stakeholders.

---

## What Stakeholders Need from EDA Reports

- Focus on business or project outcomes; avoid unnecessary technical jargon.
- Use clear visualizations to illustrate key findings.
- Summarise actionable insights and recommendations.
- Ensure documentation is reproducible and follows industry standards.

**Task;**
- List two reasons why clear communication in data reports is important for AI or data science teams.

---

## EDA Report Structure Overview

A strong EDA report for stakeholders usually includes;

- Title and executive summary; State dataset, purpose, and headline findings.
- Data overview; Describe the data source, size, structure, and any limitations.
- Methodology; Briefly explain the EDA approach (tools, cleaning steps, sampling).
- Key findings with visuals; Use concise graphs or tables, highlight trends and anomalies.
- Actionable recommendations; Suggest next steps or business actions based on findings.
- Appendix; Include relevant code, data dictionaries, or technical details for reproducibility.

---

## Demonstration; Building an EDA Report Section

We will use a sample dataset ('penguins' from the seaborn library). Let's walk through preparing a simple visualization and summary for a non-technical stakeholder.

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

# Load sample dataset
df = sns.load_dataset('penguins')

# Basic summary
summary = df.describe(include='all')
print(summary)

# Simple plot: distribution of species
sns.countplot(data=df, x='species')
plt.title('Penguin Species Distribution')
plt.show()
```

**Discussion;**
- How does the plot help a stakeholder understand the dataset?
- What additional information might they need?

---

## Guided Group Activity; Drafting a Report Section

Form small teams. Each will write the 'Key Findings' section for the penguins EDA, targeting a manager at a wildlife research organisation. Use the data and visual from the demo, and:
- Explain what the most important trends or patterns are.
- Use bullet points for recommendations.
- Keep language simple and direct.

---

## Peer Review; Giving and Receiving Constructive Feedback

Swap your draft sections with another team. Review using the checklist below:

- Is the main finding clear and supported by the data?
- Are visuals easy to understand?
- Are recommendations actionable and relevant?
- Is technical jargon avoided or explained?
- Is the writing concise?

**Task;**
- Give specific feedback on what worked and what could be improved.

---

## Best Practices for Stakeholder-Focused Writing

- Lead with findings; explain why they matter for business or project goals.
- Use visuals and summaries, not raw code or complex stats outputs.
- Document sources and methods for reproducibility.
- Respect privacy and ethics when discussing data insights.

---

## Reflection

- What difficulties did you face when trying to clarify results for non-technical audiences?
- How could industry data teams improve report quality and communication?

---

## Next Steps

- Apply these skills to your upcoming EDA assessment.
- Review examples of industry EDA reports for inspiration.
- Practice giving and responding to peer feedback on technical documents.

---
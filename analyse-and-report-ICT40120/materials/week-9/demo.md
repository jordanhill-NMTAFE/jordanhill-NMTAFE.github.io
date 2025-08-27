# Week 9 Demo; Practical Policy Review; Analyse and Assess Data Procedures

---

## Learning Objectives

- Understand the structure and purpose of organisational data policies.
- Identify key compliance requirements for data ethics and privacy.
- Critically review a sample data policy; spot risks and propose improvements.
- Connect industry standards to practical policy assessment tasks.

---

## 1. Introduction; Data Policies in Real-World AI/IT Contexts

Organisations working with large datasets must have data policies that outline how data is collected, processed, stored, and shared. These policies ensure compliance with laws, industry standards, and ethical guidelines, particularly important in AI and data science workplaces where sensitive or large-scale data is used.

**Key Points:**
- Data policies support responsible data management and ethical AI.
- Failure to comply can result in legal risks, reputational damage, or project failures.
- Policies should align with industry best practices and relevant data protection regulations.

---

## 2. Activity; Reading and Understanding a Sample Data Policy

**Setup:**
Read the simplified data policy extract below. Annotate key elements related to;
- Data collection practices
- Ethical use of data
- Privacy and security measures
- Data documentation and versioning

**Sample Data Policy Extract**
> The organisation collects only data required for project objectives. All sensitive or personal data must be anonymised prior to analysis. The Data Science Team uses version control for datasets. Data access is restricted and logged. Any sharing of data requires manager approval and must follow documented procedures. All team members must complete annual ethics and privacy training.

**Questions:**
- What strengths do you see in this policy?
- Can you spot any missing or unclear areas relevant to AI/data projects?

---

## 3. Practical Exercise; Identify Policy Gaps and Risks

- List any potential risks or compliance gaps based on the sample policy.
    - Consider organisational AI use cases; sensitive data; external data sources; data documentation.
- Document your findings in bullet points.

```python
# Example Python exercise; use for text analysis or checklists if applicable
policy_points = [
    "Collect data required for project.",
    "Anonymise sensitive data.",
    "Use version control.",
    "Restrict data access.",
    "Require approval for data sharing.",
    "Annual ethics training."
]

risks = []

# Check for missing items
if not any("data retention" in point for point in policy_points):
    risks.append("No clear guidance on how long data is kept.")

if not any("incident response" in point for point in policy_points):
    risks.append("Missing procedures for data breaches or incidents.")

if not any("data lineage" in point for point in policy_points):
    risks.append("Lack of documentation for data sources and transformations.")

print("Identified gaps or risks;", risks)
```

---

## 4. Workshop; Propose Policy Improvements

Based on your risk analysis or the code output above;
- Propose at least two specific improvements or additional provisions to strengthen the sample policy.
- Explain your reasoning using industry standards (e.g., open dataset documentation, reproducible pipelines, privacy by design).

**Example;**
- Add section on data retention and secure deletion practices.
- Specify requirements for incident response plans and regular audits.

---

## 5. Industry Connection; Case Study Discussion

Discuss in pairs or small groups;
- How do leading AI companies (e.g., those contributing to LAION, HuggingFace datasets) document and enforce data policies?
- What lessons can be applied from open data consortia or regulatory frameworks (e.g., GDPR, Australian Privacy Principles)?

---

## 6. Hands-on Activity; Visual Checklist for Policy Review

Create a checklist to guide organisational data policy reviews using Python and pandas.

```python
import pandas as pd

# Example checklist data
checklist_items = [
    "Clear purpose for data collection.",
    "Anonymisation of personal data.",
    "Version control for datasets.",
    "Access controls and logging.",
    "Approval process for data sharing.",
    "Data retention policy.",
    "Incident response plan.",
    "Regular ethics training."
]

review_status = ["Yes", "Yes", "Yes", "Yes", "Yes", "No", "No", "Yes"]
df = pd.DataFrame({"Policy Provision": checklist_items, "Included in Policy": review_status})
df
```

---

## 7. Reflection and Assessment Practice

- Reflect; How confident do you feel reviewing and critiquing a data policy?
- Practice for assessment; Review another anonymised policy sample or bring your own; use your checklist to evaluate and propose improvements.
- Share findings with the class or submit via Jupyter notebook.

---

## 8. Summary and Next Steps

**Key Takeaways;**
- Organisational data policies must balance regulatory, ethical, and practical requirements.
- Practical policy reviews help ensure data practices are robust, ethical, and industry aligned.
- Policy critique skills are essential for workplace readiness in AI/data roles.

**Next Week;**
- Hands-on exploratory data analysis with real datasets; apply your policy review skills to data usage scenarios.
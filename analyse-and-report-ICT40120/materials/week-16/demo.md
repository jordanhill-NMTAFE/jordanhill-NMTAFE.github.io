# Week 16 Demo. Ethics Debate; Solving Complex Dilemmas in AI Data

## Learning Objectives

- Identify and critically evaluate advanced ethical dilemmas in AI datasets.
- Develop and present reasoned arguments to address real-world data ethics challenges.
- Apply technical and procedural methods to mitigate privacy and bias risks in modern AI data workflows.
- Enhance communication and debate skills relevant to industry and workplace settings.

---

## 1. Introduction; Advanced Data Ethics Challenges in AI

The use of very large and open datasets for machine learning raises unique and complex ethical questions not fully addressed by traditional data compliance frameworks. Key challenge areas include:
- Dataset bias and fair representation of minority groups.
- Informed consent and secondary data use.
- Privacy risks in generative AI and LLM training.
- Policy and compliance in global datasets.
- Balancing data utility and ethical harm.

---

## 2. Case Scenarios; Real-World AI Data Dilemmas

### Scenario 1; Dataset Bias in Face Recognition

A public face recognition dataset is found to have low representation of certain ethnic groups. ML models trained on this data perform poorly for minorities, leading to unfair outcomes in real-world systems.

- What bias mitigation strategies could you implement?
- What are the risks if these biases are unaddressed?

### Scenario 2; Informed Consent and Web-Scraped Data

A large language model is trained on open web data, including social media posts and online forums. Many data subjects did not provide explicit permission for their content to be used in AI training.

- Is this use ethical, even if technically legal?
- What privacy-preserving solutions could address these concerns?

### Scenario 3; Regulatory Change and Data Policy

A national privacy law changes, making certain previously open datasets non-compliant. Your organization has an existing workflow relying on these datasets.

- How do you respond to sudden policy changes?
- What steps ensure ongoing compliance and responsible data management?

---

## 3. Hands-On Activity; Implementing Privacy-Preserving Demo

You will now explore technical approaches to reduce privacy risks in dataset sharing and analysis.

### Example; Data Anonymization with pandas

```python
import pandas as pd

# Example dataset containing personally identifiable information
df = pd.DataFrame({
    "user_id": [101, 102, 103],
    "email": ["user1@email.com", "user2@email.com", "user3@email.com"],
    "age": [23, 34, 28],
    "gender": ["female", "male", "nonbinary"]
})

# Remove direct identifiers for anonymization
anonymized_df = df.drop(columns=["user_id", "email"])
print(anonymized_df)
```

**Exercise.** Modify the above to implement k-anonymity by generalizing the 'age' feature (use ranges instead of exact ages).

---

## 4. Debate Setup; Roles, Rules, and Structure

### Teams

- Split class into teams. Each team will be assigned one ethical case scenario (see above).
- Roles; Each team selects Lead Speaker, Researcher, and Challenger.

### Preparation

- Research real examples and industry standards relevant to your scenario. Explore how big tech, non-profits, or research labs responded to similar dilemmas.
- Use course resources and last week's project tools to analyze your scenario, referencing data ethics frameworks (e.g., ACM, IEEE, GDPR).

### Debate Structure

1. Each team presents a summary of the case and their recommended ethical solution (up to 5 minutes).
2. Opposing team delivers a rebuttal, identifying possible risks, unintended consequences, or weaknesses (3 minutes).
3. Open Q&A; Other students ask clarifying questions.
4. Final reflection; Teams summarize how their views evolved or solidified (2 minutes each).

---

## 5. Technical Exploration; Fairness Metrics with sklearn and Fairlearn

Evaluate model fairness using open-source tools available in industry.

```python
from sklearn.datasets import fetch_openml
from fairlearn.metrics import demographic_parity_difference
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

# Load sample dataset
data = fetch_openml(data_id=1590, as_frame=True) # 'adult' dataset
X = data.data
y = (data.target == '>50K').astype(int)

# Use 'sex' as sensitive feature
A = X["sex"]

# Simple pre-processing
X = X.select_dtypes(include='number').fillna(0)
X_train, X_test, y_train, y_test, A_train, A_test = train_test_split(
    X, y, A, test_size=0.33, random_state=42
)

# Train a basic classifier
clf = LogisticRegression(max_iter=500)
clf.fit(X_train, y_train)
y_pred = clf.predict(X_test)

# Check demographic parity difference
dpd = demographic_parity_difference(y_test, y_pred, sensitive_features=A_test)
print("Demographic Parity Difference:", dpd)
```

**Exercise.** What could you do if your model shows a high demographic parity difference (>0.1)? List two mitigation strategies.

---

## 6. Reflection and Assessment Preparation

### Self-Check Questions

- What are the main ethical risks when collecting and processing open datasets in AI?
- How do policy and regulation changes affect ongoing AI projects?
- When is it appropriate to use, anonymize, or avoid certain data in AI model training?
- Prepare a short paragraph; Summarize one strategy to improve ethical outcomes in your course projects.

---

## 7. Summary and Next Steps

- Ethical analysis is a critical skill for modern data science and AI professionals.
- Practical technical tools and robust debate skills both contribute to responsible AI development.
- Next week; Integrating your learning; Finalizing open dataset and ML projects.
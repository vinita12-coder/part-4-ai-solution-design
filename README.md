# Part 4: AI Solution Design — Loan Default Prediction

## Task 1: Business Domain
**Finance**

---

## Task 2: Business Problem Definition

**What problem is being solved?**
Banks and financial institutions struggle to accurately identify customers who
are likely to default on loans. Current manual review processes are slow,
inconsistent, and unable to handle large volumes of applications.

**Who are the users and stakeholders?**
- Loan officers and credit analysts
- Bank risk management teams
- Customers applying for loans

**What is the current manual or traditional process?**
Credit officers manually review applicant documents, check CIBIL scores, and
apply rule-based thresholds. This process takes 2-5 days per application and
misses complex patterns in customer behavior.

**Limitations of the current process:**
- Slow turnaround time
- Human bias in decisions
- Cannot detect complex multi-variable risk patterns
- High cost of manual review at scale

---

## Task 3: AI Task Type

**Classification** — specifically Binary Classification

**Why?**
The output is one of two categories: Default (1) or No Default (0).
A feed-forward neural network can learn complex non-linear relationships
between features like income, credit history, debt ratio, and loan amount
to predict this binary outcome.

---

## Task 4: Data Requirement Plan

**Type of data needed:** Structured / Tabular data

**Input Features:**
| Feature | Type |
|---|---|
| Age | Numerical |
| Annual Income (INR) | Numerical |
| Loan Amount | Numerical |
| Loan Tenure (months) | Numerical |
| CIBIL / Credit Score | Numerical |
| Debt-to-Income Ratio | Numerical |
| Employment Type | Categorical |
| Number of Previous Loans | Numerical |
| Payment Delay History | Numerical |
| Collateral Available | Categorical (Yes/No) |

**Target Variable:** `loan_default` (0 = No Default, 1 = Default)

**Data Collection Method:**
- Internal bank transaction and loan records
- Credit bureau data (CIBIL, Experian)
- Customer application forms

**Data Quality Risks:**
- Missing income or credit score values
- Class imbalance (fewer defaulters than non-defaulters)
- Outdated credit history records
- Privacy restrictions on sharing customer financial data

---

## Task 5: Model Recommendation

**Recommended Model: Feed-Forward Neural Network (Multilayer Perceptron)**

**Architecture:**
- Input Layer: 10 features
- Hidden Layer 1: 128 neurons, ReLU activation
- Dropout: 0.3
- Hidden Layer 2: 64 neurons, ReLU activation
- Output Layer: 1 neuron, Sigmoid activation

**Why this model?**
- Tabular structured data with mixed feature types
- Can learn complex non-linear relationships between features
- Scales well with large datasets
- Supports batch training and early stopping to avoid overfitting

**Alternative considered:** Logistic Regression (simpler, interpretable baseline)

---

## Task 6: Evaluation Plan

**Technical Metrics:**
| Metric | Why |
|---|---|
| Accuracy | Overall correctness |
| Precision | Avoid false approvals |
| Recall | Catch actual defaulters |
| F1-Score | Balance precision and recall |
| AUC-ROC | Overall model discrimination ability |

**Business Metrics:**
- Reduction in loan default rate (%)
- Time saved per loan application (hours)
- Cost saved per avoided default (INR)

**Possible Failure Cases:**
- Model approves a high-risk customer (false negative)
- Model rejects a creditworthy customer (false positive — customer loss)

**Human Review / Validation Process:**
- Borderline predictions (probability 0.4–0.6) reviewed by loan officers
- Monthly model performance audit
- Quarterly retraining with new data

---

## Task 7: Responsible AI Considerations

**Bias in Data:**
- Historical loan data may reflect past discrimination against certain regions
  or income groups — model can inherit and amplify this bias

**Incorrect Predictions:**
- A false rejection harms a genuine customer's financial access
- A false approval causes financial loss to the bank

**Privacy Concerns:**
- Customer financial data is highly sensitive
- Must comply with RBI data protection guidelines and IT Act provisions

**Over-reliance on AI:**
- Loan officers may blindly trust model predictions without using judgment
- Need mandatory human review for edge cases

**Impact on Users:**
- Low-income or first-time borrowers with thin credit histories may be
  unfairly rejected due to lack of historical data

**Need for Human Oversight:**
- AI should assist decisions, not replace them entirely
- All rejected applications must have a human-reviewable explanation

---

## Task 8: Final One-Page Solution Summary

| Field | Details |
|---|---|
| **Problem** | Predict which loan applicants are likely to default |
| **Domain** | Finance / Banking |
| **AI Task Type** | Binary Classification |
| **Proposed AI Solution** | Feed-Forward Neural Network (MLP) |
| **Required Data** | Customer financial records, credit scores, loan history |
| **Model Recommendation** | 2-layer Neural Network with Sigmoid output |
| **Key Evaluation Metrics** | F1-Score, AUC-ROC, Recall |
| **Expected Business Impact** | 30–40% reduction in default rate, 70% faster approvals |
| **Top Risk** | Bias against underserved customers, data privacy |
| **Mitigation Plan** | Regular bias audits, human review for edge cases, explainability layer |

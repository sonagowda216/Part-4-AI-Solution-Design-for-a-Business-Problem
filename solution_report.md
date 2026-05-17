# AI Solution Design Report
## Insurance Claim Fraud Detection System

### 1. Business Domain
**Insurance**

### 2. Business Problem
Insurance companies process thousands of claims daily. A significant portion are fraudulent. Manual review is slow, expensive, and inconsistent. The goal is to build an AI system that automatically scores each claim for fraud risk so investigators can focus on high-risk cases.

### 3. AI Task Type
**Binary Classification** — Fraud (1) vs Not Fraud (0)
- Input: Structured claim records (amount, type, claimant history, timing, location)
- Output: Fraud probability score (0–1) + binary flag
- Learning: Supervised (labeled historical data required)

### 4. Data Requirements
| Data Type | Source | Format |
|---|---|---|
| Claim records | Internal CRM/Policy DB | Structured CSV |
| Claimant history | Internal | Structured |
| Agent notes | Internal ticketing | Unstructured text |
| Fraud labels | Fraud investigation team | Binary (0/1) |
| External data | Third-party APIs | JSON |

**Challenges:** Class imbalance (~2-5% fraud), missing values, data freshness, privacy (GDPR)

### 5. Model Recommendation
- **Primary:** XGBoost — high accuracy on tabular data, handles imbalance with class weights
- **Alternative:** Feed-Forward Neural Network (Dense 128 → 64 → 1, Sigmoid)
- **Baseline:** Logistic Regression for comparison

### 6. Evaluation Plan
**Technical:** Recall (primary), Precision, F1-Score, AUC-ROC, Confusion Matrix
**Business:** Fraud catch rate (target: 70%+), manual hours saved (~40%), resolution time, customer satisfaction

### 7. Responsible AI
| Risk | Mitigation |
|---|---|
| False fraud flags | Human-in-the-loop review for all flagged claims |
| Bias in data | Quarterly fairness audits |
| Privacy | Data anonymization, GDPR compliance |
| Model drift | Monthly monitoring, quarterly retraining |
| Explainability | SHAP values per claim |

### 8. Expected Business Impact
- ~35% reduction in undetected fraud losses
- ~40% reduction in manual review hours
- Faster resolution for legitimate claimants → higher customer satisfaction

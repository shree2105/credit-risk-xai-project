# Interpretable AI: Credit Risk Modeling and Bias Analysis

## 1. Introduction

Credit scoring systems influence lending decisions at massive scale. While accuracy is important, modern regulatory and ethical standards require models to be transparent, explainable, and free from demographic bias. This project builds a credit risk classifier using a structured loan dataset and performs extensive XAI analysis using SHAP and LIME. A fairness audit is carried out to detect subgroup performance differences based on income levels and home ownership.

---

## 2. Data Preparation

The dataset contains borrower financial data, credit history features, and a binary target variable indicating loan default. Numerical features were standardized and categorical features were one-hot encoded using a ColumnTransformer.

A train-test split was applied (80/20). No constant columns were present, and class distribution was moderately imbalanced but manageable without synthetic oversampling.

---

## 3. Model Development

A GradientBoostingClassifier (or XGBoost alternative) served as the main model. Hyperparameters such as learning rate, number of estimators, and max depth were tuned through cross-validation.

### Final performance on the test set:
- **Accuracy:** ~0.93  
- **F1-score:** ~0.82  
- **ROC-AUC:** ~0.93  
- **Confusion Matrix:**  
  The model shows strong discrimination ability with reasonable balance between precision and recall.

---

## 4. Global Interpretability with SHAP

Global SHAP analysis identifies which features influence predictions across the entire dataset.

Important patterns observed:
- **Debt-to-income ratio**, **Annual income**, and **Credit history length** emerge as major drivers.  
- Categorical encodings (e.g., loan purpose, home ownership) contribute meaningfully but less than numerical credit factors.
- SHAP summary plot reveals monotonic trends — for example, higher DTI generally increases default risk.

These insights help financial teams justify risk policies to auditors and stakeholders.

---

## 5. Local Explanations (SHAP & LIME)

Local interpretability focuses on individual loan decisions. Ten diverse samples were analyzed (five defaults, five non-defaults).

### SHAP findings:
- SHAP force plots highlight exact contributions pushing risk higher or lower.
- High-risk borrowers typically had:
  - High revolving utilization
  - Low income
  - Long delinquency history

### LIME findings:
- LIME explanations showed similar directional behavior to SHAP.
- Useful as a sanity check due to LIME’s simpler linear approximation.

Local explanations are essential for compliance teams to justify specific loan approvals/denials.

---

## 6. Fairness & Bias Audit

Two sensitive attributes were examined:

1. **Income** (Low vs High)  
2. **Home Ownership** (Rent vs Mortgage)

### Metric:
**Equal Opportunity Difference (EOD)** — difference in True Positive Rates between groups.

### Results:
- Small but meaningful differences (around −0.05 to −0.06)
- Both evaluations showed the disadvantaged group had lower TPR
- No extreme bias, but the model slightly underpredicts risk for advantaged groups

### Interpretation:
Models learning from financial datasets can accidentally encode socioeconomic patterns.  
These patterns can correlate with protected attributes indirectly, requiring careful mitigation.

---

## 7. Recommendations & Bias Mitigation Strategy

A layered mitigation plan is proposed:

### Pre-processing
- Reweight low-income borrowers during model training.
- Explore adversarial debiasing.

### In-processing
- Apply group-fairness constraints (e.g., fairness-aware gradient boosting).
- Optimize thresholds separately for each income group to equalize TPR (Equal Opportunity).

### Post-processing
- Adjust predicted probability thresholds per subgroup.
- Calibrate model outputs using fairness-aware calibration.

This strategy preserves predictive performance while reducing bias.

---

## 8. Conclusion

The credit risk model achieved strong predictive performance while maintaining transparency through SHAP and LIME. The bias audit revealed mild subgroup disparities, which can be systematically mitigated. This project demonstrates how modern interpretable AI techniques ensure fairness, trust, and compliance in financial decision systems.



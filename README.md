#  Credit Risk Modeling with SHAP, LIME & Bias Auditing

This project develops a transparent and fair credit risk prediction model using a real-world style loan dataset (similar to Lending Club). Beyond predictive accuracy, the main goal is to interpret model behavior and evaluate potential demographic bias.

The project includes:

### ✔ Data Preprocessing & Feature Engineering
- Handling missing values  
- Numeric + categorical preprocessing  
- OneHotEncoding  
- Train-test split  
- Class rebalancing check  

### ✔ Model Training
- Gradient Boosting Classifier (or XGBoost alternative)
- Hyperparameter tuning
- Metrics: Accuracy, F1-score, ROC-AUC, Confusion Matrix

### ✔ Explainability Components
#### Global Interpretability
- SHAP summary plot (bar + beeswarm)
- Feature importance ranking

#### Local Interpretability
- SHAP explanations for 10 specific loans  
- LIME explanations for selected samples

### ✔ Bias & Fairness Audit
- Sensitive features tested:
  - Income level (Low vs High)
  - Home ownership categories
- Metrics:
  - Equal Opportunity Difference  
  - TPR, FPR comparison  
- Bias interpretation + mitigation plan

### ✔ Final Report
- Full text-based analysis in `report.md`
- Bias audit in `bias_audit_results.txt`
- Global and local SHAP visualizations saved as images

---

## Repository Structure


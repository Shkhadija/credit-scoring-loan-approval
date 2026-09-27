
# Credit Scoring Model for Loan Approval Decisions

A credit scoring model built the way a bank would: predicts an applicant's default probability from application-time data, then converts it into an approve/decline decision using a cost-optimal threshold (not the default 0.5) — since misclassifying a bad applicant as good is 5x more costly than the reverse.

Built on the German Credit (Statlog) dataset (1,000 applicants, 700 good / 300 bad). Compares Logistic Regression vs XGBoost, handles class imbalance, and uses SHAP to explain individual decisions.



## Results

| Model | ROC-AUC | Threshold | Min Cost |
|---|---|---|---|
| Logistic Regression (selected) | 0.80 | 0.46 | 93 |
| XGBoost | 0.78 | 0.14–0.34 | 106–114 |

At threshold 0.46: 53.5% approval rate, 83% of bad applicants correctly flagged.

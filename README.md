# Credit Scoring Model for Loan Approval Decisions

An application credit scoring model built the way a bank would build one: given an applicant's profile at application time, the model outputs a default probability, which is then converted into an approve/decline decision using a cost-optimal threshold rather than a default 0.5 cutoff. The threshold reflects the real, asymmetric cost of lending mistakes — misclassifying a bad applicant as good is treated as 5x more costly than the reverse.

Built on the German Credit (Statlog) dataset (1,000 applicants, 700 good / 300 bad), the project compares a Logistic Regression baseline against XGBoost, handles class imbalance explicitly, and uses SHAP to explain individual credit decisions in a way that could be defended to a customer or regulator.

**Key result:** Logistic Regression (threshold = 0.46) was selected as the final model — it achieved both a lower expected cost and more stable, reproducible results than XGBoost. The project also includes bonus components: a points-based credit scorecard, probability calibration analysis, and a fairness audit across age and gender groups.

## Repository structure

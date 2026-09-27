
# Note: Imbalance, Cost & Threshold Justification

## Class Imbalance & Cost Handling

Dataset is imbalanced 70/30 (good/bad). Two layers of handling were used:
1. Model-level: class_weight="balanced" (Logistic Regression) and scale_pos_weight (XGBoost) upweight the minority "bad" class during training.
2. Decision-level: instead of the default 0.5 cutoff, the threshold was chosen by minimizing total expected cost using the official cost matrix (FN=5, FP=1) — since a bad applicant classified as good is 5x more costly than the reverse.

## Threshold Justification

Cost was computed across thresholds 0.01-0.95 for each model. Logistic Regression's minimum cost (93) occurred at threshold 0.46 — close to 0.5, a sane and stable result. XGBoost's mathematical minimum occurred at a much lower threshold (0.06-0.34, varying by run), but checking the confusion matrix at that point showed 60-70% of good applicants being declined — not a workable lending policy despite the lower "cost" number. This is why Logistic Regression, threshold=0.46, was selected as the final model.

XGBoost's results were also not reproducible across runs/environments despite fixed random_state, while Logistic Regression's were identical every time — an additional reason to prefer the simpler model here.

## What Drives Risk (SHAP)

Top risk-increasing factors: high credit_amount, long duration_months, high installment_rate_pct, negative checking account balance. Interestingly, having no checking account at all reduces predicted risk — a known quirk of this dataset (no-account applicants are often a different demographic, not inherently riskier).

Individual example: applicant with 11,816 DM requested over 45 months, negative checking balance, and an unproven credit history (no credits taken, or none recorded at this bank) scored 0.97 default probability — correctly declined (actual outcome was indeed "bad").

## Fairness Note (Limitation)

Approval rate varies by age group (41% for 18-25 vs 66% for 36-50) — likely driven by credit history length correlating with age, not age itself. This should be reviewed before production use. Gender comparison is also limited by a known dataset issue: the personal_status_sex attribute conflates sex and marital status inconsistently.


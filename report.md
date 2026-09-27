# Credit Scoring Decision Report
## How the Score Maps to a Decision

Every applicant receives a default probability score between 0 and 1 (0 = certain to repay, 1 = certain to default). This score is compared against a decision threshold of 0.46:

- Score below 0.46 → APPROVE
- Score 0.46 or above → DECLINE

This threshold is not the default 0.5 midpoint — it was chosen deliberately based on the cost trade-off below.

## The Cost Trade-off

Not all mistakes cost the same. Approving a loan that later defaults is far more expensive than declining a loan that would have been repaid. Our cost matrix treats a missed bad applicant as 5x more costly than a wrongly declined good applicant.

Because of this asymmetry, the model is intentionally more cautious than a coin-flip threshold would suggest. At threshold 0.46:

- 53.5% of applicants are approved
- 83% of actual bad-credit applicants are correctly declined
- Total expected cost on our test set: 93 (vs. 106+ for a less careful threshold)

## Bottom Line

The model trades a lower approval rate for a much lower rate of costly bad loans slipping through. This reflects standard lending practice: it is better to decline several creditworthy applicants than to approve one who defaults.

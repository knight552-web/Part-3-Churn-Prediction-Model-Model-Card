# Model Card

## Model Overview

**Model Type:** Logistic Regression

**Business Objective:** Predict whether a customer will churn within the next 60 days.

## Training Data

- Train: 1,728 customers
- Validation: 336 customers
- Test: 336 customers

## Final Threshold

**0.45**

## Final Test Performance

| Metric | Score |
|----------|----------:|
| Accuracy | 80.95% |
| Precision | 79.55% |
| Recall | 83.33% |
| F1 Score | 81.40% |
| ROC-AUC | 88.58% |

## Key Drivers of Churn

Positive churn indicators:
- Return rate
- Negative support ticket rate
- Discount dependency

Retention indicators:
- Platinum loyalty membership
- Organic acquisition
- Marketing engagement

## Monitoring Recommendations

Monitor prediction distribution, feature drift, churn-rate changes, and campaign effectiveness.

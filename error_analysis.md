# Error Analysis Report

## Overview

The final Logistic Regression model was evaluated using a classification threshold of 0.45.

While overall performance was strong, some prediction errors remain. Understanding these errors helps identify opportunities for future model improvement.

## False Negatives

False negatives are customers who churned but were predicted as retained.

| Customer ID | Probability | Recency | Frequency | Monetary |
|------------|------------:|---------:|----------:|----------:|
| CUST00093 | 0.267 | 85 | 1 | 759.64 |
| CUST00145 | 0.410 | 30 | 1 | 502.35 |
| CUST00157 | 0.214 | 0 | 1 | 376.83 |
| CUST00188 | 0.112 | 29 | 2 | 1880.31 |
| CUST00267 | 0.108 | 29 | 1 | 441.97 |

### Interpretation

These customers appeared healthy based on observable behavior but still churned, suggesting some churn drivers are not captured in the current feature set.

## False Positives

False positives are customers predicted to churn who ultimately remained active.

| Customer ID | Probability | Recency | Frequency | Monetary |
|------------|------------:|---------:|----------:|----------:|
| CUST00027 | 0.486 | 70 | 1 | 2128.34 |
| CUST00100 | 0.669 | 70 | 1 | 372.37 |
| CUST00144 | 0.593 | 86 | 2 | 928.58 |
| CUST00165 | 0.510 | 103 | 3 | 1825.77 |
| CUST00177 | 0.738 | 82 | 1 | 255.04 |

## Key Insight

The model performs well overall, but customers with moderate activity levels remain challenging to classify accurately.

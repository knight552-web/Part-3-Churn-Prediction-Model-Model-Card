# Customer Churn Prediction – Part 3

## Overview

This repository contains the machine learning component of the D2C Customer Churn Capstone Project.

The objective is to predict whether a customer will churn within the next 60 days using historical customer behavior, transaction history, support interactions, and engagement signals.

The model is intended to support customer retention initiatives by identifying customers at high risk of churn before they become inactive.

---

## Business Problem

Customer acquisition is significantly more expensive than customer retention.

The goal of this project is to proactively identify customers likely to churn so that targeted retention campaigns can be launched before customer disengagement becomes permanent.

---

## Dataset

The project uses the leakage-safe modeling dataset:

`rfm_modeling_snapshot.csv`

This dataset contains engineered customer-level features generated from data available on or before the snapshot date.

### Target Variable

`churn_next_60d`

* 1 = Customer churns within the next 60 days
* 0 = Customer remains active

### Dataset Size

| Split      | Records |
| ---------- | ------: |
| Train      |   1,728 |
| Validation |     336 |
| Test       |     336 |
| Total      |   2,400 |

---

## Modeling Approach

### Models Evaluated

1. Logistic Regression
2. Random Forest

### Model Selection

Logistic Regression was selected as the final model because it:

* Outperformed Random Forest on validation data
* Provided stronger interpretability
* Is easier to explain to business stakeholders
* Is simpler to deploy and monitor

---

## Threshold Optimization

Instead of using the default classification threshold of 0.50, threshold tuning was performed on the validation dataset.

### Selected Threshold

**0.45**

### Reasoning

A threshold of 0.45 produced:

* Highest F1 Score
* Strong Recall
* Balanced Precision and Recall

This threshold supports business objectives by maximizing churn detection while controlling retention costs.

---

## Final Test Performance

| Metric    |  Score |
| --------- | -----: |
| Accuracy  | 80.95% |
| Precision | 79.55% |
| Recall    | 83.33% |
| F1 Score  | 81.40% |
| ROC-AUC   | 88.58% |

### Confusion Matrix

|              | Predicted Stay | Predicted Churn |
| ------------ | -------------: | --------------: |
| Actual Stay  |            132 |              36 |
| Actual Churn |             28 |             140 |

---

## Key Churn Drivers

The strongest positive indicators of churn were:

* High return rates
* Negative support interactions
* Heavy discount dependency

The strongest indicators of retention were:

* Platinum loyalty membership
* Organic acquisition channel
* Marketing engagement

---

## Loading the Saved Model

The trained model was saved using Joblib and includes the complete preprocessing pipeline and Logistic Regression model.

### Load the Model

```python
import joblib

model = joblib.load("models/model.pkl")
```

---

## Making Predictions

The loaded model expects input data with the same feature structure used during training.

Example:

```python
import pandas as pd

sample_customer = pd.DataFrame({
    "recency_days": [45],
    "frequency_180d": [3],
    "monetary_180d": [2500],
    "return_rate_180d": [0.10],
    "avg_discount_pct_180d": [0.25],
    "avg_rating_180d": [4.2],
    "category_diversity_180d": [2],
    "ticket_count_90d": [1],
    "negative_ticket_rate_90d": [0.0],
    "avg_resolution_hours_90d": [12],
    "days_since_signup": [300],
    "sessions_30d": [8],
    "product_views_30d": [20],
    "cart_adds_30d": [5],
    "wishlist_adds_30d": [1],
    "abandoned_carts_30d": [2],
    "email_opens_30d": [3],
    "campaign_clicks_30d": [1],
    "last_visit_days_ago": [7],
    "city_tier": ["Tier 1"],
    "age_group": ["25-34"],
    "acquisition_channel": ["Organic"],
    "loyalty_tier": ["Gold"],
    "preferred_category": ["Skin Care"],
    "marketing_consent": ["Yes"]
})
```

### Generate Churn Probability

```python
churn_probability = model.predict_proba(sample_customer)[0][1]

print(churn_probability)
```

### Generate Churn Prediction

The final model uses an optimized threshold of **0.45**.

```python
threshold = 0.45

prediction = int(churn_probability >= threshold)

print(prediction)
```

Output:

```text
0 = Customer Expected to Stay
1 = Customer Likely to Churn
```

---

## Generated Artifacts

### Model Artifact

`model.pkl`

Contains:

* preprocessing pipeline
* missing-value handling
* categorical encoding
* trained Logistic Regression model

### Metrics Artifact

`metrics.json`

Contains:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC
* Selected threshold

### Documentation

* `model_card.md`
* `error_analysis.md`

---

## Business Recommendations

Based on the model findings:

1. Prioritize customers with high churn probabilities.
2. Investigate customers with high return rates.
3. Improve support experiences for customers with negative ticket histories.
4. Reduce reliance on discount-heavy retention strategies.
5. Expand loyalty-program participation.

---

## Future Improvements

Potential enhancements include:

* Gradient Boosting or XGBoost models
* Campaign response features
* Customer lifetime value features
* Automated model retraining
* Drift monitoring

---

## Author

Adrian Dsouza

D2C Customer Churn Intelligence Capstone Project

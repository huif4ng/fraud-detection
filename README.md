# fraud-detection
Production-grade fraud detection system that ingests financial transaction data, engineers features at scale using PySpark, trains a machine learning classifier, serves predictions via a REST API, and monitors model performance over time — all containerised with Docker and tracked with MLflow.

> STATUS: In progress

---

# Overview

This project is designed to simulate a real-world anti-fraud machine learning system.

The focus is not just model performance, but end-to-end ML system ownership:
- scalable feature engineering
- imbalanced classification
- model serving
- monitoring and drift detection
- reproducible deployment

---

# Dataset
## IEEE-CIS Fraud Detection Dataset
Source: kaggle.com/c/ieee-fraud-detection
- ~590,000 transactions, 433 features
- Transaction and identity tables
- Highly imbalanced fraud labels (3.5% fraud)
- Realistic financial transaction patterns

## Completed
- Exploratory Data Analysis (`01_eda.ipynb`)
- Missing value analysis
- Transaction behaviour exploration
- Initial fraud pattern investigation

## In Progress
- PySpark feature engineering pipeline
- XGBoost model training
- FastAPI inference API
- Docker containerisation
- MLflow experiment tracking
- Drift monitoring with Evidently AI

--- 

# Key Findings from EDA 
1. Fraud Rate: 3.499%
- Dataset is heavily imbalanced
- This changes the modelling strategy:
  - Accuracy is not a useful metric
  - Precision and recall become more important

2. Missing Values Are Extensive — and Potentially Informative
- Several feature groups contain substantial missingness:
  - id_* features
  - dist2
  - Many D_* features
  - Many V_* engineered features
  - R_emaildomain
  - Some M_* variables
- Data collection might be inconsistent across users.
- Missingness may carry some fraud signal. Handling missing data carefully will be an important part of the modelling pipeline.

3. Transaction Amounts Are Highly Skewed
- Data transformation and scalinh will likely improve model stability

4. Temporal Behaviour Appears Important
- Initial exploration of TransactionDT suggests transaction timing contains useful behavioural information.

5. Several feature groups appear potentially valuable for profiling:
- Distance features
- Count features
- Days from previous transaction
- Vesta engineered Features
- Feature engineering is critical

6. Device and Identity Signals May Be Useful
- May help detect anomalies, synthetic identities or suspicious behavioral clusters

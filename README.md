# fraud-detection
Production-grade fraud detection system that ingests financial transaction data, engineers features at scale using PySpark, trains a machine learning classifier, serves predictions via a REST API, and monitors model performance over time — all containerised with Docker and tracked with MLflow.

STATUS: In progress

# Dataset
## IEEE-CIS Fraud Detection Dataset
- Source: kaggle.com/c/ieee-fraud-detection
- ~590,000 transactions, 433 features
- Transaction and identity tables
- Highly imbalanced fraud labels (3.5% fraud)
- Realistic financial transaction patterns

# Key Findings from EDA 
The exploratory analysis focused on understanding fraud behaviour, feature quality, and modelling challenges before any model training.

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
- Missingness may carry some fraud signal. Handling of missing data must be careful

3. Transaction Amounts Are Highly Skewed
- Log transformation will likely improve model stability

4. Temporal Behaviour Appears Important
- Initial exploration of TransactionDT suggests transaction timing contains useful behavioural information.

5. Several feature groups appear potentially valuable for profiling:
- Distance features
- Count features
- Days from previous transaction
- Vesta engineered Features
- Feature engineering is critical

6. Device and Identity Signals May Be Useful

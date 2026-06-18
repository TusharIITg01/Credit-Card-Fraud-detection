# Credit Card Fraud Detection & Risk Intelligence System

##  Project Overview

Credit card fraud is a critical challenge in the financial industry due to the highly imbalanced nature of transaction data. Traditional classification models often achieve high accuracy while failing to detect fraudulent transactions.

This project develops an end-to-end fraud detection system using Machine Learning, Imbalanced Learning techniques, Explainable AI, and Business Intelligence reporting.

The objective is not only to detect fraudulent transactions but also to generate interpretable fraud risk scores that can support fraud investigation and monitoring.

##  Business Problem

Financial institutions process millions of transactions daily, while fraudulent transactions represent only a tiny fraction of the total volume.

Challenges:

* Extremely imbalanced dataset
* High cost of missing fraud cases
* Need to minimize false alarms
* Requirement for model explainability

The goal is to maximize fraud detection while maintaining an acceptable false positive rate.


##  Dataset Information

### Source

Kaggle Credit Card Fraud Detection Dataset

### Dataset Characteristics

| Metric                  | Value   |
| ----------------------- | ------- |
| Total Transactions      | 284,807 |
| Fraudulent Transactions | 492     |
| Valid Transactions      | 284,315 |
| Features                | 30      |
| Target Variable         | Class   |

Target:

* 0 → Legitimate Transaction
* 1 → Fraudulent Transaction

Most features are anonymized PCA-transformed variables (V1–V28).

---

##  Exploratory Data Analysis

Performed:

### Class Imbalance Analysis

Fraud Rate:

0.173%

This confirms the severe class imbalance problem.

### Transaction Amount Analysis

Compared transaction amounts between:

* Fraudulent Transactions
* Legitimate Transactions

### Correlation Analysis

Strong fraud-related features identified:

* V14
* V17
* V12
* V10
* V16

##  Model Development

### 1. Logistic Regression (Baseline)

Used as the benchmark model.

Results:

* Precision: 0.85
* Recall: 0.58
* ROC-AUC: 0.95

### 2. Threshold Optimization

Instead of using the default threshold (0.5), multiple thresholds were evaluated.

Best Threshold:

0.1

Results:

* Precision: 0.85
* Recall: 0.75

Key Finding:

Threshold tuning significantly improved fraud detection capability without sacrificing precision.

### 3. SMOTE

Synthetic Minority Oversampling Technique (SMOTE) was applied to address class imbalance.

Results:

* Precision: 0.05
* Recall: 0.87

Observation:

Although recall increased substantially, the model generated a very large number of false positives.

### 4. ADASYN

Adaptive Synthetic Sampling (ADASYN) was evaluated.

Results:

* Precision: 0.02
* Recall: 0.89

Observation:

ADASYN achieved high recall but produced excessive false alarms, making it unsuitable for deployment.

### 5. XGBoost (Final Model)

XGBoost was selected as the final production model.

Reasons:

* Handles non-linear relationships effectively
* Performs well on imbalanced datasets
* Robust classification performance

Results:

| Metric    | Value |
| --------- | ----- |
| Precision | 0.61  |
| Recall    | 0.80  |
| ROC-AUC   | 0.978 |

Confusion Matrix:

TN = 56,602

FP = 49

FN = 19

TP = 76

Key Finding:

XGBoost achieved the best balance between fraud detection and false positive reduction.

##  Explainable AI (SHAP)

SHAP (SHapley Additive exPlanations) was used to interpret model predictions.

Top Fraud Drivers:

1. V14
2. V4
3. V12
4. V11
5. V10
6. V3
7. V8

Key Insights:

* Low V14 values strongly increase fraud probability.
* Low V12 values are associated with fraudulent behavior.
* Transaction amount is not a primary fraud indicator.
* Fraud detection is driven by transaction behavior patterns rather than transaction size.


##  Fraud Risk Scoring Engine

The XGBoost model was converted into a risk scoring system.

Risk Score:

0 – 100

Risk Categories:

* Low Risk
* Medium Risk
* High Risk

Alert Levels:

* Low
* Medium
* High

This allows fraud analysts to prioritize suspicious transactions efficiently.

## 🛠️ Tech Stack

Python
Pandas
NumPy
Matplotlib
Seaborn
Scikit-Learn
Imbalanced-Learn
XGBoost
SHAP
Power BI
Google Colab

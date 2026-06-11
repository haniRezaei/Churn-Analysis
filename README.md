# Churn-Analysis

# Telecom Customer Churn Prediction

### End-to-End Data Analytics & Machine Learning Project

**Python • SQL Server • Power BI • Scikit-learn • XGBoost**

---

## Project Overview

This project develops a complete end-to-end analytics pipeline to identify customers at risk of leaving a telecom company. The workflow covers data cleaning, exploratory data analysis, SQL integration, machine learning model development, prediction on new customers, and business intelligence reporting through an interactive Power BI dashboard.

### Business Objective

* Predict which customers are likely to churn.
* Understand the factors driving customer attrition.
* Provide actionable recommendations to improve customer retention.
* Deliver insights through a business-ready dashboard.

---

# Project Architecture

```text
Raw Customer Data
        │
        ▼
Data Cleaning & Feature Engineering
        │
        ▼
Exploratory Data Analysis (EDA)
        │
        ▼
SQL Server Data Warehouse
        │
        ▼
Machine Learning Models
        │
        ▼
Churn Prediction for New Customers
        │
        ▼
Power BI Dashboard & Business Insights
```

---

# Key Results

| Metric                         | Result                             |
| ------------------------------ | ---------------------------------- |
| Total Customers                | 6,418                              |
| Features                       | 32                                 |
| Best Model                     | Random Forest (GridSearchCV Tuned) |
| Test AUC                       | 0.892                              |
| Accuracy                       | 84%                                |
| Churn Recall                   | 77%                                |
| New Customers Evaluated        | 411                                |
| Customers Flagged as High Risk | 386                                |
| High-Risk Percentage           | 93.9%                              |
| Top Churn Driver               | Contract Type                      |

---

# Repository Structure

```text
telecom-churn-prediction/

├── data/
│   ├── Customer_Data.csv
│   ├── churn_data.csv
│   ├── join_data.csv
│   ├── prod_services.csv
│   └── Predictions.csv
│
├── notebooks/
│   ├── 1_Churn_data_cleaning.ipynb
│   ├── 2_Churn_Visualization.ipynb
│   └── 3_machine_learning_Churn.ipynb
│
├── sql/
│   └── Solution1.ssmssln
│
├── dashboard/
│   └── churn_dashboard.pbix
│
└── README.md
```

---

# Data Preparation

## Missing Value Treatment

Several columns contained missing values that required domain-specific handling:

| Column           | Treatment            |
| ---------------- | -------------------- |
| Value_Deal       | Filled with "None"   |
| Multiple_Lines   | Filled with "No"     |
| Internet_Type    | Filled with "None"   |
| Service Features | Filled with "No"     |
| Churn_Category   | Filled with "Others" |
| Churn_Reason     | Filled with "Others" |

---

## Feature Engineering

Additional business-focused features were created to improve interpretability and model performance.

### Customer Segmentation Features

* Monthly_Charge_Range
* Age_Group
* Tenure_Group

### Power BI Sorting Features

* AgeGrp_Sorting
* TenureGrp_Sorting

These engineered features enabled more meaningful customer segmentation and clearer dashboard visualizations.

---

# Exploratory Data Analysis

Key findings from the analysis include:

### Contract Type Strongly Influences Churn

| Contract Type  | Churn Rate |
| -------------- | ---------- |
| Month-to-Month | 52.4%      |
| One Year       | 11.2%      |
| Two Year       | 2.8%       |

Customers with month-to-month contracts are substantially more likely to leave.

---

### Customer Tenure Matters

Customers with short tenure exhibit significantly higher churn rates than long-term customers.

---

### Service Adoption Reduces Churn

Customers without:

* Online Security
* Premium Support
* Backup Services

show noticeably higher churn tendencies.


# Machine Learning Pipeline

## Data Leakage Prevention

To ensure realistic model evaluation, train-test splitting was performed before fitting encoders.

```python
Split Data
      ↓
Fit Encoders on Training Data
      ↓
Transform Training Data
      ↓
Transform Test Data
```

This prevents information leakage from the test set into the training process.

---

## Models Evaluated

| Model         | Train AUC | Test AUC | Accuracy | Recall |
| ------------- | --------- | -------- | -------- | ------ |
| Random Forest | 0.970     | 0.892    | 84%      | 77%    |
| XGBoost       | 0.934     | 0.897    | 82%      | 81%    |

Although XGBoost achieved a slightly higher AUC, Random Forest was selected due to its stronger balance between recall, precision, stability, and interpretability.

---

## Handling Class Imbalance

Class distribution:

| Class   | Count |
| ------- | ----- |
| Stayed  | 4,275 |
| Churned | 1,732 |

Techniques used:

### Random Forest

```python
class_weight='balanced'
```

### XGBoost

```python
scale_pos_weight = 2.47
```

---

# Feature Importance

Top predictors of churn identified by the Random Forest model:

| Rank | Feature                     | Importance |
| ---- | --------------------------- | ---------- |
| 1    | Contract Type               | 24.95%     |
| 2    | Total Revenue               | 11.58%     |
| 3    | Total Charges               | 10.92%     |
| 4    | Total Long Distance Charges | 7.93%      |
| 5    | Monthly Charge              | 7.51%      |

Contract type emerged as the strongest driver of customer churn.

---

# Predicting Churn for New Customers

The final model was applied to newly joined customers.

| Prediction         | Count | Percentage |
| ------------------ | ----- | ---------- |
| High Risk of Churn | 386   | 93.9%      |
| Likely to Stay     | 25    | 6.1%       |

---

## Why Are New Customers High Risk?

Compared to existing customers, new customers exhibit several risk factors:

| Risk Factor              | New Customers | Existing Customers |
| ------------------------ | ------------- | ------------------ |
| Month-to-Month Contracts | 89%           | 49%                |
| No Online Security       | 90%           | 70%                |
| No Premium Support       | 90%           | 70%                |
| Average Monthly Charge   | $43           | $65                |

The dominance of month-to-month contracts explains much of the elevated churn risk.

---

# Business Recommendations

Based on the findings, the following retention strategies are recommended:

### 1. Promote Long-Term Contracts

Offer discounts and incentives for annual contracts that the expected impact: Reduce churn from 52% to approximately 11%.

### 2. Free Online Security Trial

Provide free online security for the first three months to increase engagement and service dependency.

### 3. Free Premium Support

Offer onboarding support for new customers during the critical early stages of the customer lifecycle.

### 4. Proactive Retention Campaigns

Target customers with churn probabilities above 80% using:

* Personalized outreach
* Retention offers
* Loyalty rewards

---

# Power BI Dashboard

The Power BI dashboard provides:

* Customer overview KPIs
* Churn analysis by demographics
* Churn analysis by services
* Revenue impact analysis
* High-risk customer monitoring
* Machine learning prediction insights
* Executive-level business recommendations



# Technology Stack

| Layer                   | Technologies               |
| ----------------------- | -------------------------- |
| Programming             | Python                     |
| Data Processing         | Pandas, NumPy              |
| Visualization           | Matplotlib, Seaborn        |
| Database                | SQL Server                 |
| Machine Learning        | Scikit-learn, XGBoost      |
| Dashboarding            | Power BI                   |
| Development Environment | Jupyter Notebook, Anaconda |

# Final Business Insight – New Customer Risk Prediction

The model was applied to a group of 411 newly joined customers to evaluate their churn risk based on patterns learned from historical data. The results show that 386 customers (approximately 93.9%) are predicted to be at high risk of churn, while only 25 customers are likely to remain active.

This outcome is strongly explained by the underlying behavior of the new customer segment. A significant majority of these customers (around 89%) are on Month-to-Month contracts, which the model has identified as the most important predictor of churn risk in the historical dataset. In comparison, long-term contracts such as One-Year and Two-Year agreements show significantly lower churn rates, indicating that contractual commitment plays a critical role in customer retention.

Importantly, this is not a model error but a meaningful business insight. The model has learned a real and consistent pattern: customers with short-term contracts are substantially more likely to churn. Since new customers have not yet transitioned into long-term contracts or developed strong service loyalty, they naturally fall into a higher-risk category.

From a business perspective, this finding highlights a clear strategic opportunity. The company should focus on converting Month-to-Month customers into long-term contracts through targeted incentives, onboarding offers, and loyalty programs. Additionally, proactive retention campaigns should be launched for the 386 high-risk customers to prevent early-stage churn and improve overall customer lifetime value.


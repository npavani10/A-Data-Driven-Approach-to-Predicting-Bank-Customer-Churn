# 📊 Bank Customer Churn Prediction

**Authors**: Angel Molekunnel & Pavani Narla  
**Course**: MIST 6060 – Project  
**Tool Used**: [Weka](https://www.cs.waikato.ac.nz/ml/weka/)

## 🧠 Project Objective
Customer churn is a major challenge for banks, impacting revenue and long-term customer relationships.  
This project builds a **machine learning model** to predict **bank customer churn** using **Weka**, allowing for early identification of at-risk customers and enabling targeted retention strategies.

---

## 🗂️ Dataset Overview

- **Source**: [Kaggle – Bank Customer Churn Dataset](https://www.kaggle.com/datasets/pentakrishnakishore/bank-customer-churn-data)
- **Records**: 10,000+  
- **Attributes**: Customer demographics, financial behavior, account transactions, and churn labels.

### 🔑 Key Variables
- `customer_id`, `age`, `gender`, `occupation`, `dependents`, `vintage`, `city`
- `current_balance`, `monthly_credits`, `monthly_debits`, `net worth category`, `branch_code`
- `churn` → **Target variable** (1 = churned, 0 = retained)

---

## 🧼 Data Preprocessing

### 1. Cleaning Missing Values
- **Gender**: Filled with mode → `Male`
- **Dependents**: Filled with median → `0`
- **City**: Filled with mode → `1020`
- **Occupation**: Filled with mode → `student`

### 2. Target Attribute Reordering
- Moved `churn` column to the last position for Weka recognition as the class label.

### 3. Attribute Selection
- Used **CorrelationAttributeEval** to remove attributes with low/negative correlation:
  - Removed: `customer_id`, `last_transaction`, `current_balance`, `vintage`, `age`, `net worth category`, `city`, `current_month_balance`

### 4. Normalization
- Normalized numerical fields to [0, 1] range:
  - Includes: `previous_month_balance`, `monthly_credits`, `monthly_debits`, `average balances`, etc.

---

## 🔍 Modeling Techniques & Results

### 🔸 1. Linear Regression (Baseline)
- **MAE**: 0.2579  
- **RMSE**: 0.3864  
- Not suitable for classification but provided useful feature insights.

### 🔸 2. J48 Decision Tree
- **Accuracy**: 81.47%  
- **Precision/Recall (Class 1)**: 0.0  
- Failed to detect churners due to **class imbalance**.

### 🔸 3. Naive Bayes (Before Resampling)
- **Precision (Class 1)**: 0.326  
- **Recall (Class 1)**: 0.261  
- **F1 Score**: 0.290  
- Low performance due to underrepresentation of churners.

---

## 🔄 Resampling to Fix Class Imbalance

- Used **Weka Resample Filter** with `BiasToUniformClass = 1.0`  
- Ensured balanced distribution between churners and non-churners.

### 📊 Naive Bayes (After Resampling)
- **Accuracy**: 82.20%  
- **Precision (Class 1)**: 0.840  
- **Recall (Class 1)**: 0.795  
- **F1 Score (Class 1)**: 0.817  
- **Kappa Statistic**: 0.6441 (substantial agreement)

---

## 📈 Key Churn Predictors Identified

| Feature                        | Insight                                         |
|-------------------------------|--------------------------------------------------|
| `current_month_debit`         | High debit activity linked to churn              |
| `previous_month_balance`      | Fluctuations suggested customer dissatisfaction  |
| `average_monthly_balance_prevQ2` | Decline signaled early disengagement         |
| Other Influencers             | `current_month_credit`, `gender`, `dependents`, `occupation`, `branch_code`

---

## ✅ Conclusion

The **resampled Naive Bayes model** offered the best performance, with significant gains in churner prediction.  
The project highlights the impact of **predictive analytics** in banking, enabling actionable, data-driven customer retention strategies.

---


## 💡 Tools & Libraries
- [Weka](https://www.cs.waikato.ac.nz/ml/weka/) – Data preprocessing, modeling, and evaluation  
- Filters used: `ReplaceMissingValues`, `Reorder`, `Normalize`, `Resample`, `CorrelationAttributeEval`, `NumericToNominal`

---

## 📬 Contact
For questions or feedback, feel free to reach out via email:
- Pavani Narla – pavani_narla@student.uml.edu

# A Data Driven Approach to Predicting Bank Customer Churn
This project aims to build a machine learning-based predictive model using Weka to identify bank customers likely to churn. Churn prediction enables banks to proactively retain high-risk customers by understanding the behavioral and financial indicators that signal potential attrition.
🗂️ Dataset Overview:
Source: Kaggle – Bank Customer Churn Dataset
Size: Over 10,000 records
Attributes: Include demographics, financial behaviors, account transactions, and churn labels.

Key Variables:
customer_id, age, gender, occupation, dependents, vintage, city
current_balance, monthly_credits, monthly_debits, net worth category, branch_code
churn (target variable: 1 = churned, 0 = retained)

🧼 Data Preprocessing:
1. Cleaning Missing Values
Gender: Filled with mode = “Male”
Dependents: Filled with median = 0
City: Filled with mode = “1020”
Occupation: Filled with mode = “student”

2. Target Attribute Reordering
The churn column was moved to the last position to ensure Weka recognizes it as the class label.

3. Attribute Selection
Used CorrelationAttributeEval in Weka to remove low or negatively correlated attributes, including 
customer_id, last_transaction, current_balance, vintage, age, net worth category, city, current_month_balance

4. Normalization
Applied normalization to scale numerical attributes between [0, 1] for consistent model input.
Included variables like previous_month_balance, monthly_credits/debits, average balances, etc.

🔍 Modeling Techniques & Results:
🔸 1. Linear Regression (Used for baseline analysis)
MAE: 0.2579, RMSE: 0.3864
Provided useful insights into important features but not suitable for classification.

🔸 2. J48 Decision Tree
Accuracy: 81.47%
Precision/Recall (Class 1): 0.0
Model failed to detect churners due to class imbalance.

🔸 3. Naive Bayes (Before Resampling)
Precision (Class 1): 0.326
Recall (Class 1): 0.261
F1 Score: 0.290
Performance was low due to churners being underrepresented.

🔄 Resampling to Fix Class Imbalance
Used Weka’s Resample filter with BiasToUniformClass = 1.0 to rebalance the dataset.
📊 Naive Bayes (After Resampling)
Accuracy: 82.20%
Precision (Class 1): 0.840
Recall (Class 1): 0.795
F1 Score (Class 1): 0.817
Kappa Statistic: 0.6441 (indicates substantial agreement)

📈 Key Churn Predictors Identified
current_month_debit – High debit activity correlated with churn
previous_month_balance – Fluctuations suggested dissatisfaction
average_monthly_balance_prevQ2 – Declines showed early disengagement
Other Influencers: current_month_credit, gender, dependents, occupation, branch_code

🧠 Conclusion
The resampled Naive Bayes model proved to be the most effective. It overcame class imbalance and improved precision, recall, and F-measure for predicting churners. The project demonstrates how predictive analytics can help banks reduce churn by identifying and acting on early warning signs of customer attrition.



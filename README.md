# 📊 Customer Churn Analysis & Prediction System

## 🚀 Project Overview

This project presents an end-to-end **Customer Churn Analysis and Prediction System** built using:

- **SQL Server (ETL & Data Processing)**
- **Power BI (Business Intelligence Dashboard)**
- **Python + Random Forest (Machine Learning Prediction)**

The objective of this project is to analyze historical churn behavior and predict future churners to enable proactive customer retention strategies.

---

# 📌 What is Churn?

Churn refers to customers who stop doing business with a company.

In a telecom context, churn may occur when:
- A customer cancels their subscription
- A contract is not renewed
- A customer switches to a competitor

Customer retention is critical because acquiring new customers costs significantly more than retaining existing ones.

---

# 🎯 Project Objectives

### 1️⃣ Analyze Historical Customer Data Across:
- Demographic factors
- Geographic distribution
- Payment & Account Information
- Services used

### 2️⃣ Identify:
- Churn patterns
- Customer risk segments
- Key churn drivers

### 3️⃣ Build:
- Interactive Executive Dashboard (Power BI)
- Machine Learning Model to Predict Future Churners

---

# 🏗️ Project Architecture

```
CSV Data → SQL Server (ETL) → Power BI Dashboard
                             → Python ML Model → Predictions → Power BI
```

---

# 🛠️ STEP 1 — ETL Process (SQL Server)

## Database Creation
Created database:
```sql
CREATE DATABASE db_Churn
```

## Data Loading
- Imported CSV into staging table (`stg_Churn`)
- Cleaned NULL values
- Standardized categorical fields
- Converted data types
- Inserted cleaned data into production table (`prod_Churn`)

## Created Views for BI & ML
```sql
CREATE VIEW vw_ChurnData AS
SELECT * FROM prod_Churn WHERE Customer_Status IN ('Churned', 'Stayed');

CREATE VIEW vw_JoinData AS
SELECT * FROM prod_Churn WHERE Customer_Status = 'Joined';
```

---

# 🔄 STEP 2 — Power BI Data Transformation

## Created Calculated Columns

### Churn Status
```DAX
Churn Status = IF([Customer_Status] = "Churned", 1, 0)
```

### Monthly Charge Range
```DAX
IF [Monthly_Charge] < 20 THEN "<20"
ELSE IF < 50 THEN "20-50"
ELSE IF < 100 THEN "50-100"
ELSE ">100"
```

### Age Group
- < 20
- 20–35
- 36–50
- > 50

### Tenure Group
- < 6 Months
- 6–12 Months
- 12–18 Months
- 18–24 Months
- ≥ 24 Months

## Created Measures

```DAX
Total Customers = COUNT(prod_Churn[Customer_ID])
New Joiners = CALCULATE(COUNT(prod_Churn[Customer_ID]), prod_Churn[Customer_Status] = "Joined")
Total Churn = SUM(prod_Churn[Churn Status])
Churn Rate = [Total Churn] / [Total Customers]
```

---

# 📊 STEP 3 — Executive Dashboard Insights

## Key Metrics
- Total Customers: 6,418
- Total Churn: 1,732
- Churn Rate: 27%
- New Joiners: 411

## Key Findings

### 📌 Contract Type
- Month-to-month customers have highest churn
- Long-term contracts significantly reduce churn

### 📌 Services
- Fiber optic users show higher churn
- Premium Support reduces churn
- Paperless billing users show higher churn risk

### 📌 Geography
- Certain states show higher churn rates

### 📌 Payment Method
- Credit card autopay users historically churn less

---

# 🤖 STEP 4 — Machine Learning Model

## Algorithm Used: Random Forest

### Why Random Forest?
- Handles categorical + numerical features
- Reduces overfitting
- Provides feature importance
- Robust classification performance

## Data Preparation
- Removed irrelevant columns
- Label encoded categorical variables
- Mapped target variable:
  - Stayed → 0
  - Churned → 1

## Train-Test Split
```python
train_test_split(test_size=0.2, random_state=42)
```

## Model Training
```python
RandomForestClassifier(n_estimators=100, random_state=42)
```

## Evaluation
- Confusion Matrix
- Classification Report
- Feature Importance Visualization

---

# 🔮 STEP 5 — Predicting Future Churners

- Applied trained model to `vw_JoinData`
- Predicted churn probability for active customers
- Filtered customers predicted as churned
- Exported results to CSV
- Loaded predictions into Power BI

## Predicted High-Risk Customers: 374

---

# 📈 Prediction Dashboard

Displays:
- Customer ID
- Monthly Charge
- Revenue
- Refunds
- Referrals
- Contract Type
- Payment Method
- State
- Demographic Segments

This allows business teams to target high-risk customers before they churn.

---

# 🧠 Business Value

This system enables:

✅ Early identification of high-risk customers  
✅ Targeted retention campaigns  
✅ Contract upgrade strategies  
✅ Service improvement decisions  
✅ Revenue protection  

---

# 🏁 Conclusion

This project successfully demonstrates:

- End-to-end ETL pipeline using SQL Server
- Interactive BI dashboard using Power BI
- Predictive Machine Learning using Random Forest
- Deployment of predicted churners for business use

It combines:
Data Engineering + Data Analytics + Machine Learning

---

# 🔮 Future Improvements

- Hyperparameter tuning
- SMOTE for imbalance handling
- Model deployment via API
- Automated retraining pipeline
- Real-time churn prediction system

---

# 📚 Tools & Technologies Used

- Microsoft SQL Server
- SQL Server Management Studio (SSMS)
- Power BI Desktop
- Python (Pandas, NumPy, Scikit-Learn)
- Jupyter Notebook
- Random Forest Algorithm

---

# 👨‍💻 Author

Customer Churn Analysis & Prediction Project  
End-to-End Business Intelligence & Machine Learning Solution

---

⭐ If you found this project useful, feel free to connect and collaborate!

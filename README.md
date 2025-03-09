# 🚀 Credit Risk Model for Lauki Finance  

## 📌 Project Overview  
Lauki Finance, an NBFC in India, partnered with **AtliQ AI** to develop a **Credit Risk Model** that categorizes loan applicants into **Poor, Average, Good, and Excellent** credit risk groups. This project aims to help financial institutions assess risk, minimize defaults, and improve loan approvals using machine learning.  

🔗 **Live App:** [Credit Risk Model on Streamlit](https://rohesen-ml-project-credit-risk-modelling-using-regression.streamlit.app/)  



[Credit Risk Model on Streamlit](https://github.com/Rohesen/ml-project-credit-risk-modelling-using-regression/blob/main/credit-risk-model-vid.gif) 


🔗 **GitHub Repository:** [View on GitHub](https://github.com/Rohesen/ml-project-credit-risk-modelling-using-regression)  

---

## 📂 Dataset Details  
We received three datasets with the following structure:  

| Dataset | Rows | Columns |
|---------|------|---------|
| **Customers** | 50,000 | 12 |
| **Loans** | 50,000 | 15 |
| **Bureau** | 50,000 | 8 |

After merging datasets using `cust_id`, we obtained a combined dataset with **33 columns** containing key demographic, financial, and credit-related details.

---

## 🔧 Data Preprocessing  
### ✅ Data Cleaning  
- Converted `default` column from `bool` to `int` for consistency.  
- Checked for **missing values** and **duplicates** and handled them accordingly.  
- Identified and **fixed errors** in the `loan_purpose` column.  
- Removed outliers in `processing_fee` where **processing_fee / loan_amount < 0.03**.  

### 📊 Exploratory Data Analysis (EDA)  
- **Age Distribution**: Younger customers (< 37 years) showed a higher likelihood of default.  
- **Loan Tenure & Delinquency**: Higher values in `loan_tenure_months`, `delinquent_months`, `total_dpd`, and `credit_utilization_ratio` indicate higher default risk.  
- **Loan to Income Ratio (LTI)**: Higher LTI correlates strongly with default cases.  
- **Delinquency Ratio**: A strong predictor for credit risk assessment.  

---

## 🏗 Feature Engineering & Feature Selection  
- Created **new features** such as `loan_to_income` for better risk assessment.  
- Dropped non-informative columns (`disbursal_date`, `installment_start_dt`, etc.).  
- Calculated **Variance Inflation Factor (VIF)** to remove multicollinear features.  
- Applied **categorical encoding** for non-numeric variables.  

---

## 🤖 Model Training  
Tried multiple approaches to get the **best performing model**:  

| Attempt | Model | Class Imbalance Handling | Tuning Method | AUC Score |
|---------|-------|-------------------------|---------------|-----------|
| 1️⃣ | Logistic Regression, RandomForest, XGBoost | None | Default | ~0.85 |
| 2️⃣ | Logistic Regression, XGBoost | Under Sampling | Default | ~0.87 |
| 3️⃣ | Logistic Regression | SMOTE-Tomek | Optuna | ~0.94 |
| 4️⃣ | **XGBoost (Final Model)** | SMOTE-Tomek | Optuna | **0.98** ✅ |

---

## 📈 Model Evaluation  
- **ROC-AUC Score**: **0.98** → Excellent discriminatory power.  
- **KS Statistic**: **85.98%** at Decile 8 → Strong model performance.  
- **Gini Coefficient**: **0.96** → High predictive capability.  
- **Rank Ordering Check**: Model successfully ranks customers based on credit risk.  

---

## 🚀 Model Deployment  
The final **XGBoost model** was deployed using **Streamlit**.  

🔹 **Model Artifacts Saved Using `joblib`**  
```python
from joblib import dump

model_data = {
    'model': final_model,
    'features': X_train_encoded.columns,
    'scaler': scaler,
    'cols_to_scale': cols_to_scale
}
dump(model_data, 'artifacts/model_data.joblib')
```  

🔹 **Deployed on Streamlit Cloud**  
Check out the live model:  
🔗 **[Credit Risk Model on Streamlit](https://rohesen-ml-project-credit-risk-modelling-using-regression.streamlit.app/)**  

---

## 📜 Key Takeaways  
✅ Built a high-accuracy credit risk model (**98% AUC**)  
✅ Successfully categorized applicants into risk groups (**Poor, Average, Good, Excellent**)  
✅ Identified strong predictors like `credit_utilization_ratio` and `delinquent_months`  
✅ Deployed a fully functional **real-time prediction app** using **Streamlit**  

---

## 📢 Future Improvements  
🔹 Integrate **real-time data streaming** for continuous learning.  
🔹 Improve model explainability using **SHAP values**.  
🔹 Implement **ML Ops pipeline** for automated monitoring.  

---

## 📬 Contact  
If you have any questions or suggestions, feel free to connect! 🚀  

🔗 **GitHub:** [@Rohesen](https://github.com/Rohesen)  
🔗 **Live App:** [Streamlit Credit Risk Model](https://rohesen-ml-project-credit-risk-modelling-using-regression.streamlit.app/)  

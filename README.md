Here's your complete, self-contained README.md file with all the project information and image references:

#  Telco Customer Churn Prediction & Analysis

![Python](https://img.shields.io/badge/Python-3.12-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-green)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-Boosting-red)

## 📋 Executive Summary

Developed a machine learning model to predict telecom customer churn, achieving a **77% recall rate** with XGBoost to effectively identify at-risk customers before they leave. Feature importance analysis revealed that **month-to-month contracts, Fiber Optic internet service, and low customer tenure** are the primary drivers of churn. These actionable insights enable targeted retention strategies—such as offering discounted annual upgrades to new Fiber Optic subscribers—directly supporting revenue protection and maximizing Customer Lifetime Value (CLV).

## 💼 Business Problem

In the telecommunications industry, acquiring a new customer is significantly more expensive than retaining an existing one. With a baseline churn rate of **~26.5%**, this telecom company needs a proactive way to identify customers who are likely to cancel their subscriptions. The goal of this project is to build a predictive model that flags high-risk customers and provides the business with actionable insights on *why* they are leaving.

## 📊 Dataset Overview

**Source:** IBM Telco Customer Churn Dataset  
**Size:** 7,043 customer records  
**Features:** 21 columns including demographics, services, account information, and billing details

### Key Features:
- **Customer Demographics:** gender, SeniorCitizen, Partner, Dependents
- **Services:** PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies
- **Account Information:** tenure, Contract, PaperlessBilling, PaymentMethod
- **Financial:** MonthlyCharges, TotalCharges
- **Target Variable:** Churn (Yes/No)

## 🔍 Exploratory Data Analysis

### Churn Distribution

![Churn Distribution](images/churn_distribution.png)

The dataset shows a class imbalance with **73.5% of customers staying** and **26.5% churning**. This imbalance is common in churn prediction scenarios and requires careful handling during model training.

### Top 10 Features Driving Customer Churn

![Feature Importance](images/feature_importance.png)

The most influential factors in predicting customer churn are:
1. **Contract Type** (Two year & One year) - Customers on month-to-month contracts are most likely to churn
2. **Internet Service** (Fiber optic) - Fiber optic customers show higher churn rates
3. **Streaming Movies** - Customers with streaming services
4. **Payment Method** (Electronic check)
5. **Tenure** - Newer customers are more likely to leave

## 🤖 Modeling Approach

### Models Compared:
1. **Logistic Regression** (Baseline)
2. **XGBoost** (Advanced - Champion Model)

### Key Metrics:

| Model | Recall (Churn) | ROC-AUC | Business Value |
| :--- | :---: | :---: | :--- |
| **Logistic Regression** | 52% | 0.843 | Missed nearly half of the churners |
| **XGBoost** | **77%** | **0.840** | **Caught 3/4 of all at-risk customers** |

### Confusion Matrices

#### XGBoost Model (Champion)

![XGBoost Confusion Matrix](images/xgboost_confusion_matrix.png)

- **True Positives (Churners correctly identified):** 289
- **False Negatives (Churners missed):** 85
- **Recall:** 77% - Successfully identified 77% of customers who actually churned

#### Logistic Regression (Baseline)

![Logistic Regression Confusion Matrix](images/logistic_regression_confusion_matrix.png)

- **True Positives (Churners correctly identified):** 193
- **False Negatives (Churners missed):** 181
- **Recall:** 52% - Only identified about half of the churners

##  Key Business Insights

### 1. Contract Type is King
Customers on **month-to-month contracts** are vastly more likely to churn than those on 1-year or 2-year contracts.

**Recommendation:** Incentivize month-to-month users to switch to annual contracts with a 10-15% discount.

### 2. Fiber Optic Friction
Customers with **Fiber Optic internet service** churn at a higher rate than DSL users, likely due to higher monthly costs or unmet service expectations.

**Recommendation:** Investigate Fiber Optic pricing tiers and proactively offer tech-support check-ins for new Fiber users.

### 3. The Critical First Year
**Tenure** is a major predictor. New customers (0-12 months) are the most vulnerable.

**Recommendation:** Implement a robust "First 90 Days" onboarding and check-in process.

### 4. Payment Method Matters
Customers using **Electronic Check** show higher churn rates, possibly due to manual payment friction.

**Recommendation:** Offer incentives for customers to switch to automatic payment methods.

## 🛠️ Methodology

### 1. Data Preprocessing
- Handled missing values in `TotalCharges` (11 blank spaces converted to numeric)
- Dropped irrelevant `customerID` column
- Created `TenureGroup` feature to capture customer lifecycle stages
- Encoded binary categorical variables (Yes/No → 1/0)
- One-hot encoded multi-class categorical variables

### 2. Feature Engineering
- **TenureGroup:** Binned tenure into lifecycle stages (0-12 months, 13-24 months, etc.)
- **TotalCharges:** Converted from string to numeric, filled missing values with 0

### 3. Model Training
- **Train/Test Split:** 80/20 with stratification to maintain class balance
- **XGBoost Parameters:** 
  - `scale_pos_weight` to handle class imbalance
  - 100 estimators, learning rate 0.1, max depth 5

### 4. Evaluation Metrics
- **Primary Metric:** Recall (catching churners)
- **Secondary Metrics:** Precision, F1-Score, ROC-AUC
- **Visualization:** Confusion matrices, feature importance plots

## 💡 Business Recommendations

Based on the model's predictions and feature importance analysis:

1. **Target Month-to-Month Customers:** Launch a campaign offering 15% discount for customers who switch to annual contracts
2. **Fiber Optic Onboarding:** Create a dedicated support program for new Fiber Optic customers in their first 90 days
3. **Payment Method Incentives:** Offer $5/month credit for customers who switch from electronic check to automatic payments
4. **Early Warning System:** Use the model to flag high-risk customers and trigger retention offers before they churn
5. **Streaming Bundle Deals:** Customers with streaming services show higher churn - consider bundling discounts

## 📁 Project Structure


```
02-Churn-Prediction/
│
├── data/
│   └── Telco-Customer-Churn.csv      # Raw dataset
│
├── notebooks/
│   └── 01_EDA_and_Preprocessing.ipynb # Main analysis notebook
│
├── images/
│   ├── churn_distribution.png         # Churn distribution charts
│   ├── feature_importance.png         # Top 10 features chart
│   ├── xgboost_confusion_matrix.png   # XGBoost confusion matrix
│   └── logistic_regression_confusion_matrix.png  # LR confusion matrix
│
├── README.md                          # You are here!
│
└── requirements.txt                   # Dependencies
```

## 🚀 How to Run

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/02-Churn-Prediction.git
cd 02-Churn-Prediction
```

### 2. Create and Activate Conda Environment
```bash
conda create -n datascience python=3.12 -y
conda activate datascience
```

### 3. Install Dependencies
```bash
pip install pandas numpy scipy scikit-learn xgboost matplotlib seaborn jupyterlab
```

### 4. Launch Jupyter Lab
```bash
jupyter lab
```

### 5. Open the Notebook
Navigate to `notebooks/01_EDA_and_Preprocessing.ipynb` and run all cells.

##  Requirements

- Python 3.12+
- pandas
- numpy
- scikit-learn
- xgboost
- matplotlib
- seaborn
- jupyterlab

## 🎓 Learning Outcomes

This project demonstrates:
- **Data Science Workflow:** From raw data to business insights
- **Handling Imbalanced Data:** Using `scale_pos_weight` in XGBoost
- **Model Interpretability:** Feature importance analysis for stakeholder communication
- **Business Translation:** Converting technical metrics to actionable recommendations
- **End-to-End ML Pipeline:** Data cleaning → EDA → Feature engineering → Modeling → Evaluation → Insights

## 📈 Model Performance Summary

| Metric | Logistic Regression | XGBoost | Improvement |
|--------|---------------------|---------|-------------|
| **Recall (Churn)** | 52% | **77%** | +25% |
| **Precision (Churn)** | 66% | 52% | -14% |
| **F1-Score (Churn)** | 58% | 62% | +4% |
| **ROC-AUC** | 0.843 | 0.840 | -0.3% |

**Trade-off Analysis:** While XGBoost has slightly lower precision (more false positives), the 25% improvement in recall means we catch significantly more at-risk customers. In business terms, it's better to offer a retention discount to a happy customer (false positive) than to lose a customer entirely (false negative).

## 🔮 Future Enhancements

1. **Hyperparameter Tuning:** Use GridSearchCV or Optuna to optimize XGBoost parameters
2. **SHAP Values:** Add SHAP analysis for individual prediction explainability
3. **Deployment:** Build a Streamlit dashboard for real-time churn prediction
4. **A/B Testing:** Test retention strategies on high-risk customer segments
5. **Time Series Analysis:** Incorporate temporal patterns in customer behavior

## 📝 License

This project is for educational and portfolio purposes.

##  Author

**[Your Name]**  
Data Scientist | Machine Learning Engineer

---

*Built with ❤️ using Python, Scikit-Learn, and XGBoost*
```

---

##  Image Files You Need to Create

Save your generated images in an `images/` folder with these exact names:

1. **`churn_distribution.png`** - Your pie chart and bar chart showing 26.5% churn rate
2. **`feature_importance.png`** - The bar chart showing Top 10 Features (Contract_Two year, Contract_One year, InternetService_Fiber optic, etc.)
3. **`xgboost_confusion_matrix.png`** - The confusion matrix showing 770, 265, 85, 289
4. **`logistic_regression_confusion_matrix.png`** - The confusion matrix showing 934, 101, 181, 193

---

## ✅ Final Checklist

Before pushing to GitHub:

- [ ] Create `images/` folder and add all 4 images
- [ ] Update the GitHub URL in the "How to Run" section
- [ ] Replace `[Your Name]` with your actual name
- [ ] Create a `requirements.txt` file with:
  ```
  pandas
  numpy
  scikit-learn
  xgboost
  matplotlib
  seaborn
  jupyterlab
  ```
- [ ] Test that all image paths work correctly
- [ ] Push to GitHub and verify the README renders properly

This README is now completely self-contained with all the information, results, and insights from your project! 🎉

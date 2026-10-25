# Personal Loan Purchase Prediction (AllLife Bank)

[![Python 3.10](https://img.shields.io/badge/python-3.10-blue.svg)](https://www.python.org/downloads/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.6.1-orange.svg)](https://scikit-learn.org/stable/)

## 📌 Project Overview
AllLife Bank is a mid-sized US retail bank aiming to expand its asset customer base (borrowers) by converting existing depositors (liability customers) into personal loan customers. Last year's pilot campaign achieved a 9% conversion rate. This project builds and compares predictive machine learning models to identify high-potential customers, minimize marketing overhead, and maximize conversion rates.

## 🎯 Business Objective
* **Primary Goal**: Maximize **Recall** (minimize False Negatives) to capture as many potential loan customers as possible while keeping a healthy balance with Precision to prevent excessive marketing waste.
* **Secondary Goal**: Uncover demographic and behavioral factors (such as income, family size, education, and spending patterns) driving personal loan conversion.

## 📊 Dataset Dictionary
* `Age` / `Experience`: Demographic characteristics of the customer (perfectly correlated, handled in preprocessing).
* `Income` (in $k): Annual customer income.
* `ZIPCode`: Regional location zones (mapped into 7 distinct zones).
* `Family`: Size of the customer's family.
* `CCAvg` (in $k): Average monthly credit card spending.
* `Education`: 1: Undergraduate, 2: Graduate, 3: Professional.
* `Mortgage` (in $k): House mortgage value.
* `CD_Account` / `Securities_Account` / `Online` / `CreditCard`: Behavioral banking indicators.
* `Personal_Loan` (**Target**): Accepted personal loan in the pilot campaign (1: Yes, 0: No).

## 🛠️ Key Pipeline Stages
1. **Data Cleaning & Engineering**: Corrected erroneous negative `Experience` values, grouped `ZIPCode` into broader regions based on prefix zones, and mapped `Education` into human-readable categories.
2. **Exploratory Data Analysis (EDA)**: Identified strong correlation between `Age` and `Experience`. Discovered that high-income, highly-educated customers with larger family sizes and Certificate of Deposit (CD) accounts are significantly more likely to purchase a loan.
3. **Model Selection & Tuning**:
   * **Decision Trees**: Evaluated Default (overfitted), Pre-Pruning (optimized for max Recall), and Post-Pruning (Cost Complexity Pruning via `ccp_alpha`).
   * **Alternative Classifiers**: Scale-dependent classifiers (Logistic Regression, SVM, Gaussian Naive Bayes) were trained on scaled datasets, while ensembles (Random Forest, Gradient Boosting) were trained on unscaled data.

## 📈 Performance Comparison Summary

| Model | Test Accuracy | Test Recall | Test Precision | Test F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| **Decision Tree (Pre-Pruning)** | 95.7% | **96.0%** | 70.8% | 81.5% |
| **Decision Tree (Post-Pruning)**| 98.4% | 90.6% | 93.1% | **91.8%** |
| **Gradient Boosting** | 98.4% | 87.9% | 95.6% | 91.6% |
| **Random Forest** | 98.0% | 83.2% | **96.1%** | 89.2% |
| **Support Vector Machine** | 95.9% | 83.9% | 76.7% | 80.1% |
| **Logistic Regression** | 90.5% | 85.9% | 51.4% | 64.3% |

## 💡 Key Actionable Insights & Recommendations
* **High-Value Targeting**: Prioritize customers with an **Income above $116k**, a **family size of 3+**, and an **education level beyond Undergraduate**.
* **Cross-Selling Opportunities**: Customers holding a **Certificate of Deposit (CD) account** have a nearly **50% conversion rate**; these should be targeted with automated cross-selling campaigns.
* **Model Deployment**: 
  * Deploy **Decision Tree (Pre-Pruning)** if the absolute highest coverage (96.0% Recall) is desired and marketing budget is flexible.
  * Deploy **Decision Tree (Post-Pruning)** or **Gradient Boosting** for a highly balanced setup with low waste (Precision > 93%) and strong recall (~90.6%).

## 💻 How to Use
1. Install dependencies: `pip install -r requirements.txt` (or copy the notebook libraries command).
2. Place `Loan_Modelling.csv` under your runtime path.
3. Run the cells sequentially to reproduce the comparisons.

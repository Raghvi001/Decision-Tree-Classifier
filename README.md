
# Decision Tree Classifier

## About
This project implements a Decision Tree using sklearn.

## Features
- Data preprocessing
- Model training
- Accuracy evaluation

## Tech Used
- Python
- scikit-learn
- pandas
- matplotlib

## How to Run
1. Open notebook in Jupyter/Colab
2. Run all cells

# Restaurant Tip Prediction — Binary Classification

## Overview
Built a complete machine learning pipeline to predict whether a 
restaurant customer will give a high tip (≥$3) or low tip (<$3).
Compared three algorithms — Logistic Regression, Decision Tree 
and Random Forest — through systematic visual analysis and 
feature engineering.

**Best Result → Decision Tree (depth=1) — 76.2% CV Accuracy**

---

## Dataset
- Source: Seaborn tips dataset (built-in)
- Size: 244 rows, 7 original features
- Target: high_tip (1 = tip ≥ $3, 0 = tip < $3)
- Class balance: perfectly balanced 50/50 (123 vs 121 samples)

---
---

## Features Used
| Feature | Type | Description |
|---------|------|-------------|
| total_bill | Numerical | Total bill in dollars |
| size | Numerical | Number of people at table |
| bill_per_person | Engineered | total_bill divided by size |
| time_Dinner | Binary | 1 if dinner, 0 if lunch |
| day_Sun | Binary | 1 if Sunday |
| day_Sat | Binary | 1 if Saturday |
| smoker_No | Binary | 1 if non smoker |

---

## Complete Approach

### 1. Data Preparation
- Created binary target variable at $3 threshold
- Removed tip column to prevent data leakage
- Applied one hot encoding to all categorical variables
- Split into 80% training and 20% test sets

### 2. Logistic Regression
- Trained baseline logistic regression model
- Analyzed coefficients for feature importance
- Applied L2 regularization with C=0.01
- Best result: 71.3% CV accuracy, 0.825 ROC AUC

### 3. Model Evaluation
- Confusion matrix analysis (TP, TN, FP, FN)
- Precision, Recall and F1 Score per class
- ROC curve and AUC score
- Precision Recall curve and average precision
- Threshold tuning analysis

### 4. Visualization Analysis
- Class distribution → confirmed perfect 50/50 balance
- Total bill distribution → $9 median gap between classes
- Categorical features → time and day strongest predictors
- Correlation heatmap → total_bill strongest at ~0.5 correlation
- Feature importance → sex and Friday visits weakest features

### 5. Feature Engineering
- Removed weak features: sex_Female and day_Fri
- Created bill_per_person = total_bill / size
- Improved accuracy from 67.2% to 71.3% (+4.1%)
- Improved AUC from 0.767 to 0.825 (+0.058)

### 6. Decision Trees
- Trained unlimited tree → severe overfitting (99.5% train, 65.3% test)
- Tested depths 1 through 10 using cross validation
- Found optimal depth = 1 using only total_bill
- Depth 1 achieved best CV accuracy of 76.2%

### 7. Random Forest
- Trained 100 tree forest with bagging and feature randomness
- Tested 1 to 200 trees → stabilizes at 100 trees
- Feature importance averaged across all trees
- bill_per_person confirmed at 33.1% importance
- Limited by small dataset size (244 rows)

---

## Final Results

| Model | CV Accuracy | CV Std | ROC AUC |
|-------|------------|--------|---------|
| Logistic Reg (original) | 67.2% | 0.056 | 0.767 |
| Logistic Reg (engineered) | 71.3% | 0.063 | 0.825 |
| Decision Tree (depth=1) | **76.2%** | **0.043** | — |
| Decision Tree (depth=3) | 66.0% | 0.073 | — |
| Random Forest (100 trees) | 65.2% | 0.062 | 0.689 |

**Winner: Decision Tree depth=1 with 76.2% CV accuracy and 
lowest variance of 0.043**

---

## Key Findings

- total_bill was the single strongest predictor throughout all models
- Dinner customers were nearly twice as likely to give high tips vs lunch
- Sunday customers tipped most generously across the week
- Gender had almost zero impact on tipping behavior
- bill_per_person (engineered feature) contributed 33% of Random Forest importance
- Non smokers surprisingly tipped less than smokers in this dataset
- Decision Tree depth=1 outperformed Random Forest on this small dataset
- Simpler models generalize better when data is limited (244 rows)

---

## Technologies Used
- Python 3
- pandas — data manipulation and analysis
- numpy — numerical operations
- scikit-learn — model building and evaluation
- matplotlib — data visualization
- seaborn — statistical visualization

---

## How to Run

1. Clone this repository


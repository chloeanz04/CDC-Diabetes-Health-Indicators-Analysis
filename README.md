# [R] CDC Diabetes Health Indicators Analysis - Predictive Modeling

## Introduction

This project focuses on analyzing and building robust classification models to predict the risk of diabetes based on the Centers for Disease Control and Prevention (CDC) Health Indicators dataset.

## Key Tasks & Project Features

* **Exploratory Data Analysis (EDA):** Performed extensive data exploration to extract insights and confirm the statistical relationship between health features and the diabetes outcome.
* **Data Preprocessing & Imbalance Handling:** Applied advanced sampling techniques to address the severe class imbalance, a critical step for developing reliable predictive models.
* **Multi-class Classification Model:** Developed a model to predict three diabetes risk states: Non-diabetic, Pre-diabetic, and Diabetic.
* **Binary Classification Model:** Simplified the problem to classify individuals into 'Non-diabetic' vs. 'Diabetic or Pre-diabetic' for broader risk assessment.

## Methodology & Techniques

| Phase | Method/Technique Used | Description |
| :--- | :--- | :--- |
| **Analysis** | EDA & Independence Testing | Conducted rigorous analysis, confirming all selected variables exhibited a strong correlation ($\text{p-value} < 2.2e-16$) with the target variable. |
| **Pre-processing** | Combined Sampling | Successfully mitigated imbalance in the multi-class problem by combining **Undersampling** (for the majority class) and **SMOTE** (for the minority classes). |
| **Multi-class Model** | Random Forest | Optimized and selected **Random Forest** as the best model for 3-state prediction, trained exclusively on Health Indicator variables. |
| **Binary Model** | Logistic Regression | Transformed the problem to binary and utilized **Undersampling** to train a highly effective **Logistic Regression** model. |

## Key Results

| Model Type | Best Model Selected | Evaluation Metric | Result |
| :--- | :--- | :--- | :--- |
| **Multi-class (3 states)** | Random Forest | Accuracy | **77.6%** |
| | | Kappa | **0.66** |
| **Binary (2 states)** | Logistic Regression | AUC | **0.8113** |
| | | Accuracy | **72.56%** |

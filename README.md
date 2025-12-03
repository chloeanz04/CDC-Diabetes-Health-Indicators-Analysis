# [R] CDC Diabetes Health Indicators Analysis - Predictive Modeling

## Overview

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
<p align="center">
  <strong>Multi-class classification problem with a highly correlated dataset</strong>
</p>

<div align="center">

| Model                         | Accuracy | Kappa   | Macro-F1 |
|-------------------------------|---------|---------|----------|
| Multinomial Logistic Regression | 0.5148  | 0.2721  | 0.1344   |
| Random Forest                  | 0.7739  | 0.6609  | 0.4669   |
| Naive Bayes                    | 0.5007  | 0.2511  | 0.1217   |

</div>

**Observations:**  
- Both **Multinomial Logistic Regression** and **Naive Bayes** performed poorly, with similar evaluation metrics at quite low levels, especially **Macro-F1**, which was below 0.15.  
- **Random Forest**, however, showed much better performance:  
  - **Accuracy (0.7739):** With nearly 77.4% correct predictions, the model achieves relatively high accuracy.  
  - **Kappa (0.6609):** Indicates that model predictions depend on the true classes, but due to label imbalance, this value cannot be very high.  
  - **Macro-F1 (0.4669):** Still somewhat low, indicating the model does not perfectly balance predictions across all classes.

**Conclusion:**  
The **Random Forest** model is the most suitable for accurately predicting diabetes status based on input features. This allows for early detection of the disease and provides patients with appropriate treatment options tailored to their current condition.

| **Binary (2 states)** | Logistic Regression | AUC | **0.8113** |
| | | Accuracy | **72.56%** |

# [R] CDC Diabetes Health Indicators Analysis - Predictive Modeling

## Overview

This project focuses on analyzing and building robust classification models to predict the risk of diabetes based on the Centers for Disease Control and Prevention (CDC) Health Indicators dataset.

---

## Key Tasks & Project Features

* **Exploratory Data Analysis (EDA):** Performed extensive data exploration to extract insights and confirm the statistical relationship between health features and the diabetes outcome.
* **Data Preprocessing & Imbalance Handling:** Applied advanced sampling techniques to address the severe class imbalance, a critical step for developing reliable predictive models.
* **Multi-class Classification Model:** Developed a model to predict three diabetes risk states: Non-diabetic, Pre-diabetic, and Diabetic.
* **Binary Classification Model:** Simplified the problem to classify individuals into 'Non-diabetic' vs. 'Diabetic or Pre-diabetic' for broader risk assessment.

---

## Methodology

| Phase | Method/Technique Used | Description |
| :--- | :--- | :--- |
| **Data Preprocessing** | Data Cleaning & Variable Selection | Renamed necessary variables, removed duplicates, and classified variables into quantitative and qualitative types to support subsequent analysis. |
| **Data Visualization** | EDA (Histograms, Boxplots, Density Plots) | Explored data distributions and characteristics to inform further analysis steps. |
| **AB Testing** | Resampling & Permutation ANOVA | Applied AB testing methods: resampling to check independence of qualitative variables and permutation ANOVA to assess group differences when traditional ANOVA assumptions are not met. |
| **Handling Imbalanced Data** | Sampling Techniques | Among all methods evaluated (Undersampling, Oversampling, SMOTE, Class Weight, and their combinations), the **combination method (Undersampling + SMOTE / Undersampling + Oversampling)** performed the best overall, achieving Accuracy: 0.51, Kappa: 0.27, Macro-F1: 0.13. |
| **Multi-class Modeling** | Logistic Regression, Random Forest, Naive Bayes | Predicted diabetes status (`Non-diabetes`, `Pre-diabetes`, `Diabetes`) using: <br>• Top 10 variables most correlated with the target <br>• Health indicators only (`gen_hlth`, `high_bp`, `bmi`, `diff_walk`, `high_chol`, `heart_diseaseor_attack`, `phys_hlth`). |
| **Binary Modeling** | Logistic Regression, Random Forest, Naive Bayes | Simplified the task to a binary classification problem (diabetes vs. non-diabetes) due to the low number of Pre-diabetes cases. Applied sampling techniques to train effective models and identify the best-performing binary classifier. |

---

## Key Results
<p align="center">
  <strong>Multi-class classification problem with highly correlated features</strong>
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

<p align="center">
  <strong>Multi-class classification problem with health-related features</strong>
</p>

<div align="center">

| Model                         | Accuracy | Kappa   | Macro-F1 |
|-------------------------------|---------|---------|----------|
| Multinomial Logistic Regression | 0.5058  | 0.2586  | 0.1252   |
| Random Forest                  | 0.7761  | 0.6641  | 0.4704   |

</div>

**Observations:**  
- The **Random Forest** model has a Macro-F1 score nearly four times higher than that of **Multinomial Logistic Regression**, indicating better handling and balance across classes.  
- Random Forest also outperforms Multinomial Logistic Regression in **Accuracy** and **Kappa**, with values of 0.7761 and 0.6641 respectively, demonstrating superior accuracy and overall performance.


<p align="center">
  <strong>Binary classification problem</strong>
</p>

<div align="center">

<img width="468" height="563" alt="image" src="https://github.com/user-attachments/assets/80812c4a-ec2f-42a9-9a02-b074e5808a42" />

</div>

**Observations:**
The **Logistic Regression** model achieved an **AUC of 0.81**, indicating good and reliable discriminative ability between classes.

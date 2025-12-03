# [R] CDC Diabetes Health Indicators Analysis - Predictive Modeling

## Overview

This project focuses on analyzing and building robust classification models to predict the risk of diabetes based on the Centers for Disease Control and Prevention (CDC) Health Indicators dataset.

---

## Dataset

- **File:** `diabetes_012_health_indications_BRFSS2015.csv`  
- **Source:** BRFSS 2015 survey by CDC  
- **Size:** 253,680 survey responses  
- **Target variable:** `diabetes_012` (3 classes)  
  - 0: Non-diabetes  
  - 1: Pre-diabetes  
  - 2: Diabetes  
- **Class imbalance:** Severe; Non-diabetes (213,703) >> Pre-diabetes (4,631) + Diabetes (35,346)  
- **Features:** 21 variables including health indicators, lifestyle, and demographics  
  - Quantitative:  
    - `bmi` – body mass index  
    - `men_hlth` – number of days in past 30 days mental health was not good  
    - `phys_hlth` – number of days in past 30 days physical health was not good  
  - Qualitative: remaining 18 variables (e.g., `high_bp`, `high_chol`, `smoker`, `stroke`, `age`, `sex`, `education`)  

---

## Methodology

| Phase | Method/Technique Used | Description |
| :--- | :--- | :--- |
| **Data Preprocessing** | Data Cleaning & Variable Selection | <br>• Renamed necessary variables <br>• Removed duplicates <br>• Classified variables into quantitative and qualitative types to support subsequent analysis. |
| **Data Visualization** | EDA (Histograms, Boxplots, Density Plots) | Explored data distributions and characteristics to inform further analysis steps. |
| **AB Testing** | Resampling & Permutation ANOVA | Applied AB testing methods: <br>• **Resampling method:** Checks independence of qualitative variables <br>• **Permutation ANOVA:** Assesses group differences when traditional ANOVA assumptions are not met. |
| **Handling Imbalanced Data** | Sampling Techniques | Among all methods evaluated (Undersampling, Oversampling, SMOTE, Class Weight, and their combinations), the **combination method (Undersampling + SMOTE / Undersampling + Oversampling)** performed the best overall, achieving Accuracy: 0.51, Kappa: 0.27, Macro-F1: 0.13. |
| **Multi-class Modeling** | Logistic Regression, Random Forest, Naive Bayes | Predicted diabetes status (`Non-diabetes`, `Pre-diabetes`, `Diabetes`) using: <br>• Top 10 variables most correlated with the target <br>• Health indicators only (`gen_hlth`, `high_bp`, `bmi`, `diff_walk`, `high_chol`, `heart_diseaseor_attack`, `phys_hlth`). |
| **Binary Modeling** | Logistic Regression, Random Forest, Naive Bayes | Simplified the task to a binary classification problem (diabetes vs. non-diabetes) due to the low number of Pre-diabetes cases. Applied sampling techniques to train effective models and identify the best-performing binary classifier. |

---

## Results
<h3 align="center">
  <strong>1. A/B testing</strong>
</h3>

**Qualitative Variables:** All showed p-values close to 0.  

**Quantitative Variables:** ment_htlh, bmi, phys_htlh also showed p-values close to 0.  

**Observations:**  
- All qualitative variables having p-values near 0 indicate that each independent variable is statistically significant in relation to the target variable (diabetes). This shows that these features play an important role in predicting diabetes.  
- The quantitative variables with p-values near 0 suggest significant differences in the means of ment_htlh, bmi, and phys_htlh across the target groups.  

**Practical Insights:**  
- **Body Indicators:** Individuals with high BMI, high blood pressure, or high cholesterol are at higher risk of diabetes. Managing weight and controlling blood pressure/cholesterol are crucial for prevention.  
  - Healthy lifestyle choices (exercise, low-salt diet, reduced animal fat) can help reduce risk.  
  - Regularly monitor blood pressure and cholesterol, especially for high-risk groups.  
- **Habits:** Engaging in regular exercise and avoiding smoking lowers risk and improves overall health.  
- **Lifestyle:** Poor self-reported health, cardiovascular disease, or history of stroke increases diabetes risk. Maintaining overall physical and mental health is essential for prevention.  
- **Age and Socioeconomic Factors:** Diabetes risk increases with age, especially above 55, and is higher among individuals with lower income or education.  
  - Regular health check-ups, nutrition education, and encouragement of physical activity are recommended.  
  - Improve access to affordable healthcare, healthy food, and community health education programs.  

**Modeling Strategy:**  
Although all independent variables are statistically significant, optimizing the classification model requires:  
- **Data Balancing:** To prevent bias towards majority classes (e.g., "Non-Diabetes"), ensure minority groups ("Pre-Diabetes" and "Diabetes") are adequately represented without reducing overall model performance.  
- **Feature Importance Assessment:** Use feature importance metrics and analyze coefficients to evaluate the influence of each variable on predictions.

<h3 align="center">
  <strong>2. Multi-class classification problem with highly correlated features</strong>
</h3>

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

<h3 align="center">
  <strong>3. Multi-class classification problem with health-related features</strong>
</h3>

<div align="center">

| Model                         | Accuracy | Kappa   | Macro-F1 |
|-------------------------------|---------|---------|----------|
| Multinomial Logistic Regression | 0.5058  | 0.2586  | 0.1252   |
| Random Forest                  | 0.7761  | 0.6641  | 0.4704   |

</div>

**Observations:**  
- The **Random Forest** model has a Macro-F1 score nearly four times higher than that of **Multinomial Logistic Regression**, indicating better handling and balance across classes.  
- Random Forest also outperforms Multinomial Logistic Regression in **Accuracy** and **Kappa**, with values of 0.7761 and 0.6641 respectively, demonstrating superior accuracy and overall performance.


<h3 align="center">
  <strong>4. Binary classification problem</strong>
</h3>

<div align="center">

<img width="468" height="563" alt="image" src="https://github.com/user-attachments/assets/80812c4a-ec2f-42a9-9a02-b074e5808a42" />

</div>

**Observations:**
The **Logistic Regression** model achieved an **AUC of 0.81**, indicating good and reliable discriminative ability between classes.

---

## Conclusion
- Diabetes risk is significantly influenced by lifestyle habits, age, education, income, and overall health indicators.  
- For multi-class classification, using only health-related features, **Random Forest** achieves the best performance, enabling early identification of Non-diabetic, Pre-diabetic, or Diabetic individuals.  
- For binary classification (diabetic vs. non-diabetic), **Logistic Regression** provides a reliable and interpretable model.  
- Early detection allows individuals to adjust their lifestyle and supports healthcare professionals in making informed treatment decisions.  
- Public health strategies should emphasize early screening, promoting healthy habits, and improving healthcare accessibility for at-risk populations.

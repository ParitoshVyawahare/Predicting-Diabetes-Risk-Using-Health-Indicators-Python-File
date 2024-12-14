# Predicting Diabetes Risk Using Health Indicators

This project leverages machine learning techniques to predict diabetes risk using health, lifestyle, and demographic indicators. It explores various models and selects the best-performing one for robust predictions and actionable insights.

---

## Table of Contents
- [A. Problem Statement and Definition](#a-problem-statement-and-definition)
- [B. Data Exploration, Visualization, and Processing](#b-data-exploration-visualization-and-processing)
- [C. Model Exploration, Selection, and Performance Evaluation](#c-model-exploration-selection-and-performance-evaluation)
- [D. Hyperparameter Tuning and Diagnostics](#d-hyperparameter-tuning-and-diagnostics)
- [E. Conclusion](#e-conclusion)

---

## A. Problem Statement and Definition

### Problem Statement
Diabetes is a growing global health concern, affecting millions worldwide. Early diagnosis and classification into categories such as Non-Diabetic, Pre-Diabetic, and Diabetic are crucial for preventing complications and enabling timely treatment. However, working with large datasets and understanding the key factors behind diabetes risk can be challenging.

### Objective
To build a machine learning model that predicts an individual's diabetes status based on health, lifestyle, and demographic factors. The model should:
1. Provide accurate predictions.
2. Identify key features contributing to diabetes risk.

### Why is this Important?
Unmanaged diabetes can lead to severe health complications such as:
- Cardiovascular diseases
- Kidney failure
- Blindness

Predictive analytics can help healthcare professionals identify at-risk individuals and create personalized prevention or treatment plans, significantly reducing complications.

### Real-Life Example
In a healthcare clinic, patient data like BMI, blood pressure, cholesterol levels, and physical activity are collected. Analyzing this data manually for thousands of patients is impractical. A machine learning model can:
- Classify patients as Non-Diabetic, Pre-Diabetic, or Diabetic.
- Prioritize high-risk patients for medical attention.
- Suggest lifestyle changes for Pre-Diabetic individuals.

---

## B. Data Exploration, Visualization, and Processing

### Data Overview
- **Dataset**: Contains 253,680 rows and 22 features, including health indicators, lifestyle factors, and demographic variables.
- **Target Variable**: `Diabetes_012` (values: 0 for Non-Diabetic, 1 for Pre-Diabetic, 2 for Diabetic).

### Key Cleaning Steps
- Removed 23,899 duplicate rows, reducing the dataset size to 229,781 rows.
- Verified no missing values or invalid categories.

### Feature Analysis

#### Health Indicators
- **High BP**: Binary feature (0: No, 1: Yes). ~45% have high blood pressure.
- **BMI**: Continuous feature. Average BMI: 28.69 (range: 12.0 to 98.0).
- **Heart Disease or Attack**: Binary feature. ~10% have heart disease.

#### Lifestyle Factors
- **Smoker**: Binary feature. ~46% are smokers.
- **Physical Activity**: Binary feature. ~73% engage in physical activity.

#### Accessibility to Care
- **Any Healthcare**: Binary feature. ~95% have access to healthcare.
- **Doctor Cost**: Binary feature. ~10% skipped doctor visits due to cost.

#### General Health
- **General Health**: Ordinal feature (1: Excellent to 5: Poor). Most rate their health as Good or Very Good.
- **Mental Health**: Continuous feature. Average unhealthy days: 3.5 (range: 0 to 30 days).

### Feature Selection
#### Features Removed
1. **Cholesterol Check**: Low variability.
2. **Heavy Alcohol Consumption**: Minimal predictive value.
3. **Fruits & Veggies Consumption**: Weak correlations.
4. **Any Healthcare**: Near-constant feature.

#### Features Kept
- General Health, High BP, BMI, Difficulty Walking, Age, Education, Income, and Physical Activity.

---

## C. Model Exploration, Selection, and Performance Evaluation

### Models Explored
1. **Logistic Regression**
2. **Random Forest**
3. **XGBoost**

### Results Summary

| Model               | Train Accuracy | Test Accuracy | Class 0 F1 | Class 1 F1 | Class 2 F1 |
|---------------------|----------------|---------------|------------|------------|------------|
| Logistic Regression | 83.1%          | 82.9%         | 90%        | 0%         | 25%        |
| Random Forest       | 98.8%          | 81.9%         | 90%        | 1%         | 28%        |
| XGBoost             | 84.8%          | 83.1%         | 91%        | 0%         | 28%        |

### Model Selection
- **XGBoost** was selected due to its consistent performance and potential for optimization.
- It achieved the best balance of accuracy and F1-scores for diabetes prediction.

---

## D. Hyperparameter Tuning and Diagnostics

### Tuning Process
- Used GridSearchCV with parameters:
  - `learning_rate`: [0.01, 0.1]
  - `n_estimators`: [100, 200]
  - `max_depth`: [3, 5]
  - `subsample`: [0.8, 1.0]
  - `colsample_bytree`: [0.8, 1.0]

### Best Parameters
- **`colsample_bytree`: 0.8**
- **`learning_rate`: 0.1**
- **`max_depth`: 5**
- **`n_estimators`: 100**
- **`subsample`: 1.0**

### Results After Tuning
- **Validation Accuracy**: 83.7%
- **Test Accuracy**: 83.3%
- Improved feature importance and robustness while avoiding overfitting.

---

## E. Conclusion

### Advantages
- **High Accuracy**: Consistent performance across datasets.
- **Feature Interpretability**: Clear insights into key factors influencing diabetes risk.
- **Scalability**: Suitable for large datasets.

### Disadvantages
- **Pre-Diabetic Prediction**: Requires improvement for minority class handling.
- **Computational Cost**: Tuning XGBoost can be resource-intensive.

### Final Remarks
The XGBoost model is robust, interpretable, and deployable in real-world healthcare settings. It provides reliable predictions and actionable insights, making it an effective tool for diabetes risk classification.

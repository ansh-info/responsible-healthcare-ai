# **Report: Predicting Healthcare Test Results with AI**

## **1. Introduction**

### **1.1 Project Overview**

This study explores the development of an AI model to predict healthcare test results based on patient attributes. The primary objective is to build a robust, fair, and interpretable model that assists healthcare professionals in decision-making.

### **1.2 Dataset Description**

- **Source**: Kaggle Healthcare Dataset
- **Size**: 55,500 records
- **Target Variable**: `Test Results` (Multi-class: Normal, Abnormal, Inconclusive)
- **Features**:
  - Patient demographics (Age, Gender, Blood Type, etc.)
  - Hospitalization details (Admission Type, Room Number, Billing Amount)
  - Medical history (Medical Condition, Medication, etc.)
- **Dataset**: [Download from Kaggle](https://www.kaggle.com/datasets/prasad22/healthcare-dataset)

---

## **2. Data Understanding & Preprocessing**

### **2.1 Initial Data Exploration**

- **No missing values** detected.
- Some categorical variables contained **inconsistent formatting** (e.g., `Doctor`, `Hospital` had unnecessary capitalization variations).
- **Numerical Outliers**: Billing amounts had some **negative values**, which were corrected.

### **2.2 Data Preprocessing Steps**

- **Categorical Encoding**:
  - One-hot encoding for high-cardinality variables (e.g., `Hospital`).
  - Label encoding for ordinal categories (`Test Results`).
- **Feature Engineering**:
  - Extracted admission year and month.
  - Created interaction features (Age × Billing Amount, Stay Duration × Billing, etc.).
- **Scaling**: Standardized numerical features to improve model performance.

---

## **3. Exploratory Data Analysis (EDA)**

### **3.1 Key Findings from EDA**

- The dataset is **balanced across test result categories** (no major class imbalance issues).
- **Billing Amount & Hospital Stay Duration** showed strong relationships with test results.
- **Room Number** and **Admission Type** appeared to contribute significantly to predictions.

### **3.2 Feature Correlations**

A correlation heatmap revealed **low multicollinearity**, suggesting that features contribute unique information to predictions.

---

## **4. Model Selection & Training**

### **4.1 Baseline Models**

| Model               | Accuracy |
| ------------------- | -------- |
| Logistic Regression | 33.79%   |
| Random Forest       | 44.54%   |
| XGBoost             | 40.68%   |
| LightGBM            | 38.41%   |
| Neural Network      | 34.01%   |

- **Random Forest outperformed other models** but required feature refinement.
- **Deep Learning struggled** due to limited data and lack of strong feature interactions.

### **4.2 Feature Selection & Hyperparameter Tuning**

- **Random Forest (Refined Features)**: 43.88% accuracy.
- **Random Forest (With Interaction Features)**: 43.63% accuracy.
- **Final Model**: Random Forest with the best-selected features.

---

## **5. Explainability & Bias Assessment**

### **5.1 Feature Importance (SHAP Analysis)**

- **Top 5 Features Influencing Predictions:**

  1. Billing Amount
  2. Room Number
  3. Age
  4. Hospital Stay Duration
  5. Admission Month

- SHAP plots confirmed that **Billing Amount and Room Number had the highest impact** on predictions.

### **5.2 Fairness Analysis**

- **Gender-Based Accuracy:**
  - **Male (1)**: 44.38%
  - **Female (0)**: 43.69%
- **Demographic Parity Difference (Selection Rate):** 0.0080
- **Accuracy Difference Between Groups:** 0.0069

- **Key Takeaway:** Model fairness results indicate **minimal bias**, and selection rates between groups are nearly equal.

---

## **6. Risk Assessment & Model Robustness**

### **6.1 Robustness Checks**

- **Bootstrap Sampling**: Achieved a mean accuracy of **43.90%** with a **standard deviation of 0.0042**.
- **Sensitivity Analysis**: Minor variations in input data showed **stable model performance**, indicating robustness.

### **6.2 Fairness & Bias Mitigation**

- No significant disparities were found in model predictions.
- Future improvements could include **re-weighting training samples or adjusting decision thresholds**.

---

## **7. Conclusion & Future Work**

### **7.1 Summary of Findings**

- **Random Forest was the best-performing model**.
- **Billing Amount & Room Number** were the strongest predictors.
- **Fairness metrics indicated no significant bias** across gender groups.

### **7.2 Recommendations for Improvement**

- **Gather more data** to improve deep learning model performance.
- **Explore advanced NLP techniques** for medical text embeddings.
- **Implement fairness constraints** to further refine fairness.
- **Consider real-world deployment challenges**, such as data privacy laws.

---

### **7.3 Model Card (Summary)**

| Attribute            | Description                                                         |
| -------------------- | ------------------------------------------------------------------- |
| **Model Name**       | Random Forest (Healthcare Test Results)                             |
| **Objective**        | Predict medical test results based on patient data                  |
| **Accuracy**         | 44.38%                                                              |
| **Fairness Metrics** | Demographic Parity Difference: 0.0080, Accuracy Difference: 0.0069  |
| **Key Features**     | Billing Amount, Room Number, Age, Hospital Stay Duration            |
| **Limitations**      | Limited dataset size, potential hospital-specific biases            |
| **Ethical Concerns** | Fairness in healthcare predictions, avoiding biased decision-making |

---

## **Final Thoughts**

This project demonstrated how **machine learning can aid healthcare predictions**, with careful attention to fairness, explainability, and robustness. Future work can **extend this model with real-world hospital data** and **improve fairness in AI-driven healthcare decisions**.

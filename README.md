# Tabular Kaggle Project

## Define Project

**Project Link:**  
Santander Customer Satisfaction Dataset (Kaggle)

This project aims to predict whether a customer is dissatisfied using anonymized numerical features. The dataset comes from a Kaggle competition where the objective is to identify unhappy customers early based on their behavior and account-related data.

The dataset contains 76,020 observations and 371 columns, including an ID column, 369 numerical features, and a binary target variable (`TARGET`). The target is highly imbalanced, with approximately 4% of customers labeled as dissatisfied.

---

## Data Loading and Initial Look

The dataset was loaded from `train.csv`.

- Number of rows: 76,020  
- Number of features: 371  

Missing Values:  
- No missing values were detected in the dataset.

Feature Types:  
- All features are numerical and anonymized (e.g., `var15`, `saldo_var30`).

Outliers:  
- Some features contain extreme values, which is expected in financial data.  
- Outliers are defined as values significantly outside the typical range of a feature.

Class Imbalance:  
- ~96% satisfied (`TARGET = 0`)  
- ~4% dissatisfied (`TARGET = 1`)  

Target:  
- Binary classification problem  
- `0` → satisfied customers  
- `1` → dissatisfied customers  

---

## Data Visualization

Given the large number of features, plotting every variable is impractical and would reduce clarity. Instead, a subset of representative features was examined along with the target distribution.

Observations:  
- The target distribution confirms strong class imbalance.  
- Individual features show limited separation between classes.  
- Predictive patterns likely emerge from combinations of multiple features rather than any single variable.  

---

## Data Cleaning and Preperation for Machine Learning

The following preprocessing steps were performed:

- Removed the `ID` column, as it does not contribute to prediction  
- Verified that no missing values required handling  
- Applied feature scaling using `StandardScaler`  
- Confirmed that no categorical encoding was necessary  

Rescaling:  
- Important for models such as Logistic Regression  
- All features were standardized  

---

## Machine Learning

### Problem Formulation

- Removed non-informative columns (e.g., `ID`)  
- Defined `TARGET` as the prediction variable  
- Split the dataset into training and test sets (80/20)  
- Used stratified sampling to preserve class distribution  

---

### Train ML Algorithm

Three models were trained:

1. Logistic Regression with class balancing  
2. Random Forest with class balancing  
3. Gradient Boosting  

---

### Evaluate Performance on Validation Sample

Performance was evaluated using:

- Accuracy  
- Precision  
- Recall  
- F1 Score  
- ROC AUC  

Results:

**Logistic Regression**
- Accuracy ≈ 0.68  
- Precision ≈ 0.09  
- Recall ≈ 0.77  
- F1 Score ≈ 0.16  
- AUC ≈ 0.80  

**Random Forest**
- Accuracy ≈ 0.94  
- Precision ≈ 0.16  
- Recall ≈ 0.11  
- F1 Score ≈ 0.13  
- AUC ≈ 0.76  

**Gradient Boosting**
- Accuracy ≈ 0.96  
- Precision ≈ 0.15  
- Recall ≈ 0.003  
- F1 Score ≈ 0.007  
- AUC ≈ 0.84  

---

### Apply ML to the Challenge Test Set

The trained models were applied to a hold-out test set to simulate performance on unseen data.

A confusion matrix was generated for Logistic Regression:
[[9941 4661]
[ 141 461]]

This indicates:
- Strong recall for dissatisfied customers  
- A high number of false positives  

---

## Conclusion

The primary challenge in this dataset is severe class imbalance, which makes accuracy a misleading metric.

Logistic Regression performed best for detecting dissatisfied customers because it prioritizes recall through class balancing. While this leads to more false positives, it ensures that a larger proportion of dissatisfied customers are correctly identified.

Random Forest and Gradient Boosting achieved higher overall accuracy but were less effective at capturing the minority class.

Future improvements could include:

- Resampling techniques such as SMOTE  
- Hyperparameter tuning  
- Advanced ensemble models such as XGBoost or LightGBM  
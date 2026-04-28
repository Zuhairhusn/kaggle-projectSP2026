# Tabular Kaggle Project

## Define Project

**Project Link:**  
Santander Customer Satisfaction Dataset (Kaggle)

This project focuses on predicting whether a bank customer is dissatisfied based on anonymized numerical features. The dataset comes from the Santander Customer Satisfaction Kaggle competition, where the goal is to identify unhappy customers early.

The dataset contains 76,020 rows and 371 columns, including an ID column, 369 numerical features, and a binary target variable (`TARGET`). The target is highly imbalanced, with only about 4% of customers labeled as dissatisfied.

---

## Data Loading and Initial Look

The dataset was loaded from `train.csv`.

- Number of rows: 76,020  
- Number of features: 371  

Missing Values:
- No significant missing values detected.

Feature Types:
- All features are numerical.
- Feature names are anonymized (e.g., `var15`, `saldo_var30`).

Outliers:
- Some extreme values exist due to financial variables.
- Outliers are defined as unusually large or small values compared to the general distribution of each feature.

Class Imbalance:
- Yes, the dataset is highly imbalanced:
  - ~96% satisfied (0)
  - ~4% dissatisfied (1)

Target:
- Classification problem
- `TARGET = 0` → satisfied  
- `TARGET = 1` → dissatisfied  

---

## Data Visualization

Due to the large number of features (369), full visualization of every feature is not practical.

Instead:
- Feature distributions were inspected for general patterns.
- The imbalance between classes was confirmed visually.

Observations:
- Most features do not show clear separation individually.
- The signal for prediction likely comes from combinations of features rather than single variables.

---

## Data Cleaning and Preperation for Machine Learning

Steps performed:

- Removed `ID` column (not useful for prediction)
- No missing values required handling
- Applied feature scaling using `StandardScaler`
- No categorical features present, so no one-hot encoding was needed

Rescaling:
- Important for Logistic Regression
- Applied to all features

---

## Machine Learning

### Problem Formulation

- Removed non-useful columns (`ID`)
- Target variable used: `TARGET`
- Data split into:
  - Training set (80%)
  - Test set (20%)
- Stratified split used to preserve class imbalance

---

### Train ML Algorithm

Three models were trained:

1. Logistic Regression (with class balancing)
2. Random Forest (with class balancing)
3. Gradient Boosting

---

### Evaluate Performance on Validation Sample

Metrics used:
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

The model was trained and evaluated on a hold-out test set.

A confusion matrix was generated for Logistic Regression:
[[9941 4661]
[ 141 461]]

This shows:
- High recall for dissatisfied customers
- Large number of false positives

---

## Conclusion

- The dataset is highly imbalanced, making accuracy unreliable.
- Logistic Regression performed best for detecting dissatisfied customers.
- There is a clear trade-off between recall and precision.
- Ensemble methods achieved higher accuracy but failed to capture the minority class effectively.

Future improvements could include:
- Oversampling techniques (e.g., SMOTE)
- Hyperparameter tuning
- More advanced models like XGBoost
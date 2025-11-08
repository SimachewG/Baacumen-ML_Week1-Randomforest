### German Credit Risk Prediction Using Logistic Regression

### Assignment Overview

This project aims to build a predictive model to determine whether a credit applicant is a **good** or **bad** credit risk using the German Credit dataset from the UCI Machine Learning Repository. Logistic Regression is used as the primary method due to its interpretability and suitability for binary classification.

A secondary goal is to determine a **cost-sensitive decision threshold** because misclassifying a bad applicant as good is **5× more costly** than the reverse.

## Dataset

* **Source:** [UCI Machine Learning Repository: German Credit Data](https://archive.ics.uci.edu/ml/datasets/statlog+german+credit+data)
* **Size:** 1000 instances, 20 features
* **Target Variable:** `class`

  * 1 = Good credit risk
  * 0 = Bad credit risk

### Features

The dataset contains both **numerical** and **categorical** variables including:

## Assignement Steps

### 1. Data Loading and Preparation

* Dataset loaded using `pandas`.
* Target variable encoded: Good = 1, Bad = 0.
* Identified numerical and categorical features.
* Split the data into predictors (`X`) and target (`y`).

### 2. Preprocessing

* **Numerical features:** Standardized using `StandardScaler`.
* **Categorical features:** One-hot encoded using `OneHotEncoder`.
* Preprocessing combined using `ColumnTransformer`.

### 3. Train-Test Split

* Split the dataset into training and test sets (70%-30%) with `stratify=y` to maintain class distribution.

### 4. Model Building

* Logistic Regression used with `liblinear` solver.
* Preprocessing and model combined in a `Pipeline` for efficiency.

### 5. Model Evaluation (Default Threshold = 0.5)

* Confusion Matrix and Classification Report calculated.
* Metrics considered:

  * Accuracy
  * Precision, Recall, F1-score for both classes
  * ROC-AUC Score
* Top positive and negative **feature coefficients** identified to interpret the influence of variables.

### 6. Cost-Sensitive Threshold Selection

* Misclassifying a bad applicant as good is **5× worse** than misclassifying a good applicant as bad.
* Optimal threshold determined by minimizing the **expected cost**:

### 7. Results and Interpretation

#### Default Threshold (0.5)

* Accuracy: 0.74
* ROC-AUC: 0.78
* Model favors predicting good applicants, but some bad applicants are misclassified.

#### Optimal Cost-Sensitive Threshold (~0.954)

* Reduces risk by **not approving any bad applicants**.
* Overall accuracy drops (0.40) due to rejecting many good applicants.
* Demonstrates the trade-off between **financial risk** and **revenue opportunity**.

#### Feature Insights

* **Positive Influence:** Purpose, checking account status, savings accounts
* **Negative Influence:** Poor credit history, certain property types, risky purposes.


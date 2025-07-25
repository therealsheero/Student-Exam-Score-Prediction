# Student Exam Score Prediction

This project aims to predict a student's final grade (`G3`) using their demographic, academic, and behavioral features, based on two Portuguese student datasets. After training and evaluating 15+ models, **Bayesian Ridge Regression** was selected for deployment due to its near-perfect performance.

---

## Project Structure

```

├── Training&Prediction.ipynb             # Model training and evaluation, make predictions on new student data, feature engineering and transformation functions
├── student-mat.csv      # Student data (math class)
├── student-por.csv      # Student data (Portuguese class)
├── scaler.pkl           # Saved feature scaler (StandardScaler)
├── feature_names.pkl    # Feature order used during model training
├── bayesian_ridge_model.pkl  # Final trained Bayesian Ridge model

````

---

## Steps Followed

### 1. Data Loading and Merging
- Loaded both `student-mat.csv` and `student-por.csv`.
- Selected relevant features (`G1`, `G2`, etc).
- Merged rows based on unique student identifiers where appropriate.

### 2. Data Preprocessing
- Converted categorical variables using binary and **One-Hot Encoding**.
- Engineered several custom features:
  - `ParentEdu` = `Medu + Fedu`
  - `TotalAlcohol` = `Dalc + Walc`
  - `G1_G2_Avg` = mean of G1 and G2
  - `StudyFreeTimeRatio`, `TravelStudyRatio`, `HighFamRel`, etc.
- Scaled numeric features using `StandardScaler`.
- Saved `scaler.pkl` and `feature_names.pkl` for consistent inference.

### 3. Model Training and Evaluation
- Trained 15+ models:
  - Linear Regression, Ridge, Lasso, ElasticNet, Random Forest, SVM, XGBoost, CatBoost, LGBM, etc.
- Evaluated models using:
  - Mean Absolute Error (MAE)
  - Mean Squared Error (MSE)
  - Root Mean Squared Error (RMSE)
  - R² Score
- Visualized results via bar plots, pie charts, and learning curves.
- Final model: **Bayesian Ridge Regression**

### 4. Saving Artifacts
- Saved the trained model: `bayesian_ridge_model.pkl`
- Saved the feature scaler and feature list for prediction consistency.

### 5. Single Prediction Inference
- Used `Training&Prediction.ipynb` to test a sample student row from the dataset.

---

## Model Performance

**Bayesian Ridge Regression**

| Metric        | Training | Testing  |
|---------------|----------|----------|
| MAE           | 0.000001 | 0.0145   |
| MSE           | 0.000000 | 0.0003   |
| RMSE          | 0.000002 | 0.0172   |
| R² Score      | 1.0000   | 0.9999   |

**Conclusion**: The Bayesian Ridge model achieved almost perfect generalization, indicating high stability and performance even on unseen data.

---

## How to Predict a New Student's Score

Make sure the input dictionary inside `Training&Prediction.ipynb` is filled with a new student’s data (like one row from the CSV). The script will:

1. Apply feature engineering.
2. Encode features.
3. Scale numerics.
4. Predict the `G3` score.
5. Print predicted score and compare it to actual if known.

---

## Dataset Source

* UCI Machine Learning Repository – [Student Performance Data Set](https://archive.ics.uci.edu/ml/datasets/Student+Performance)

---


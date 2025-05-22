# Machine-Learning---1
(Multiple Linear Regression vs Polynomial Linear Regression)


# 📊 Student Performance EDA & Regression Analysis

## 📁 Dataset Overview

The dataset includes student academic scores and demographic data:

* Gender
* Race/Ethnicity
* Parental Level of Education
* Lunch Type
* Test Preparation Course
* Math Score
* Reading Score
* Writing Score

### 🧾 Sample Records

```
| Gender | Race | Parental Education | Lunch | Test Prep | Math | Reading | Writing |
|--------|------|---------------------|--------|------------|------|---------|---------|
| Female | B    | Bachelor's Degree   | Standard | None     | 72   | 72      | 74      |
| Female | C    | Some College        | Standard | Completed| 69   | 90      | 88      |
| Female | B    | Master's Degree     | Standard | None     | 90   | 95      | 93      |
| Male   | A    | Associate's Degree  | Free/Reduced | None  | 47   | 57      | 44      |
| Male   | C    | Some College        | Standard | None     | 76   | 78      | 75      |
```

---

## 🔍 Part 1: Exploratory Data Analysis (EDA)

### 🧹 Data Preprocessing

* **Ordinal Encoding** of Parental Education:

  ```
  Some High School: 0
  High School: 1
  Some College: 2
  Associate's Degree: 3
  Bachelor's Degree: 4
  Master's Degree: 5
  ```
* **Binary Encoding**:

  * Gender: Female = 0, Male = 1
  * Lunch: Standard = 1, Free/Reduced = 0
  * Test Prep: None = 0, Completed = 1
* **One-Hot Encoding**: Race/Ethnicity Groups A to E

### 📈 Correlation with Math Score

| Feature                 | Correlation       | Interpretation      |
| ----------------------- | ----------------- | ------------------- |
| Reading Score           | 0.8176            | ✅ Strong Positive   |
| Writing Score           | 0.8026            | ✅ Strong Positive   |
| Test Preparation Course | 0.1777            | ✅ Mild Positive     |
| Parental Education      | 0.1594            | ✅ Mild Positive     |
| Race Group E            | 0.2059            | ✅ Mild Positive     |
| Lunch                   | -0.3509           | ✅ Moderate Negative |
| Race Groups A-D         | -0.0920 to 0.0501 | ❌ Weak              |
| Gender                  | -0.1680           | ❌ Mild Negative     |

### ✅ Handling Multicollinearity

High correlation between reading and writing scores prompted the creation of:

```python
avg_literacy_score = (reading_score + writing_score) / 2
```

This reduces redundancy while retaining predictive power.

---

## 📊 Part 2: Multiple Linear Regression

### ⚙️ Features Used

* avg\_literacy\_score
* Test Preparation Course
* Parental Education
* Lunch
* Gender
* Race/Ethnicity (One-hot)

### 📉 Model Evaluation

| Metric   | Change         |
| -------- | -------------- |
| R² Score | ↓ \~1.7%       |
| MAE      | ↑ \~0.24 units |

Despite a minor trade-off, the model maintains high predictive accuracy (4–5 units average error) and gains better coefficient stability.

### 💡 Insights

* `avg_literacy_score` is the strongest predictor.
* Multicollinearity was reduced, making results more interpretable.
* Demographic features still offered useful information.

---

## 📈 Part 3: Polynomial Regression

### 🧠 Feature Refinement

* ❌ Dropped: Race, Gender → Weak correlation
* ❌ Dropped: Binary/Categorical features → Not suitable for polynomial terms

### ✅ Selected Features:

* Parental Education
* Reading Score
* Writing Score
* avg\_literacy\_score

### 🧾 Dataset Preview

```
| Parental Education | Math Score | Reading | Writing | Avg Literacy |
|--------------------|------------|---------|---------|---------------|
| 4                  | 72         | 72      | 74      | 73.0          |
| 2                  | 69         | 90      | 88      | 89.0          |
| 5                  | 90         | 95      | 93      | 94.0          |
| 3                  | 47         | 57      | 44      | 50.5          |
| 2                  | 76         | 78      | 75      | 76.5          |
```

### 📊 Model Performance (Reduced Data)

| Metric   | Value  |
| -------- | ------ |
| R² Score | 0.6832 |
| Adj. R²  | 0.6767 |
| MAE      | 7.4106 |
| RMSE     | 8.7799 |

### 📊 Model Performance (Complete Data)

| Metric   | Value  |
| -------- | ------ |
| R² Score | 0.8725 |
| Adj. R²  | 0.8643 |
| MAE      | 4.3502 |
| RMSE     | 5.5710 |

### 📌 Justification for Dropping Features

* Binary/categorical variables (e.g., gender, race) were dropped due to incompatibility with polynomial expansion.
* Race and gender also showed weak correlation with the target, making them poor predictors.
* The refined feature set enhanced learning of complex patterns without overfitting.

---

## ✅ Conclusion

Polynomial regression significantly improved performance. With careful feature selection and collinearity handling, the final model achieved:

* Higher R² and lower error rates
* More stable and interpretable coefficients
* Better generalization capacity

---

> 🔚 End of README

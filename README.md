# Titanic Dataset – Exploratory Data Analysis (EDA)

Comprehensive exploratory data analysis performed on the Titanic passenger dataset to understand survival patterns, feature distributions, missing values, and outliers.

---

## Problem Statement

The objective of this analysis is to explore passenger-level data from the Titanic and identify patterns that influenced survival.

The focus is on:

* Understanding data structure and quality
* Analyzing relationships between features and survival
* Detecting missing values and outliers
* Extracting insights useful for predictive modeling

---

## Dataset

**Dataset Used:** Titanic Dataset

* Total Rows: **891**
* Total Columns: **12**

### Features Overview

| Column      | Description                                        |
| ----------- | -------------------------------------------------- |
| PassengerId | Unique identifier                                  |
| Survived    | Survival status (0 = No, 1 = Yes)                  |
| Pclass      | Passenger class (1 = First, 2 = Second, 3 = Third) |
| Name        | Passenger name                                     |
| Sex         | Gender                                             |
| Age         | Age in years                                       |
| SibSp       | Number of siblings/spouses aboard                  |
| Parch       | Number of parents/children aboard                  |
| Ticket      | Ticket number                                      |
| Fare        | Ticket fare                                        |
| Cabin       | Cabin number                                       |
| Embarked    | Port of embarkation (C, Q, S)                      |

---

## Data Overview

* Age has **177 missing values**
* Cabin has **687 missing values**
* Embarked has **2 missing values**
* No duplicate rows detected

Numeric summary statistics show:

* Average age ≈ 29.7 years
* Average fare ≈ 32.20
* Survival rate ≈ 38.4%

---

## Data Wrangling

### Missing Values

Identified missing values using:

```python
df.isnull().sum()
```

Key findings:

* Cabin column is mostly missing (over 75%)
* Age has moderate missingness
* Embarked has minimal missingness

This has direct implications for modeling.

---

## Univariate Analysis

Examined individual feature distributions.

### Age Distribution

* Most passengers were between 20–40 years old.
* Distribution slightly right-skewed.

### Fare Distribution

* Highly right-skewed.
* Extreme high-fare values present.
* Suggests income/class imbalance.

### Survival by Gender

* Females had significantly higher survival rates.
* Males had higher mortality.

This is one of the strongest visible survival signals.

### Age by Survival

* Younger passengers showed slightly better survival.
* Children appear prioritized.

### Fare vs Passenger Class

* First class paid significantly higher fares.
* Strong separation between classes.

### Embarkation Port Distribution

* Majority boarded at Southampton (S).
* Smaller proportions from Cherbourg (C) and Queenstown (Q).

---

## Missing Values Visualization

Used a heatmap to visualize missing data patterns.

Key observation:

* Cabin column largely unusable without heavy imputation.
* Age missingness appears randomly distributed.

---

## Bivariate Analysis

### Correlation Matrix

Analyzed correlation among numeric variables:

* Pclass negatively correlated with Fare.
* Pclass negatively correlated with Survival.
* Fare positively correlated with Survival.

Interpretation:

* Higher class → Higher fare → Higher survival probability.

### Pairplot Analysis

Examined relationships among:

* Age
* Fare
* Pclass
* Survived

Clear separability visible across class and fare levels.

---

## Categorical Feature Analysis

### Gender Distribution

* More males than females onboard.
* Despite being fewer, females had higher survival rate.

### Passenger Class Distribution

* Majority of passengers were in 3rd class.
* 1st class had significantly better survival rates.

### Survival by Class

Clear gradient:

* 1st Class → Highest survival
* 2nd Class → Moderate survival
* 3rd Class → Lowest survival

Socioeconomic status strongly influenced survival.

---

## Outlier Detection

### 1. Boxplot Method (Visual)

Detected extreme values in:

* Fare
* Age (very old passengers)
* SibSp (large families)

---

### 2. Z-Score Method

Used threshold = 3.

Detected **20 outliers** in Age and Fare.

High-fare passengers were extreme cases (e.g., fares above 200–500).

---

### 3. IQR Method

Applied on Fare:

* Identified **116 Fare outliers**

Fare distribution is heavily skewed and contains significant high-value extremes.

---

## Key Insights

1. Gender was the strongest survival predictor.
2. Passenger class heavily influenced survival.
3. Fare correlates with class and survival.
4. Age has moderate influence.
5. Cabin column is mostly unusable due to missing values.
6. Fare distribution is highly skewed with many outliers.
7. Third-class passengers faced the highest mortality.

---

## Technical Stack

* Python
* Pandas
* Matplotlib
* Seaborn
* SciPy

---

## How to Run

Install dependencies:

```bash
pip install pandas matplotlib seaborn scipy
```

Run the notebook or script:

```bash
python titanic_eda.py
```

---

## Limitations

* No imputation performed in this stage.
* No feature engineering (e.g., family size, title extraction).
* No modeling included.
* Cabin feature not leveraged due to missing data.
* Outliers detected but not treated.

---

## Next Steps

* Perform missing value imputation.
* Engineer features such as:

  * Family size
  * Title extraction from Name
  * IsAlone indicator
* Encode categorical variables.
* Build predictive models (Logistic Regression, Random Forest, etc.).
* Evaluate using cross-validation.

---

## Conclusion

This EDA establishes a strong foundation for predictive modeling.

Clear survival patterns emerge across gender, class, and fare, making this dataset suitable for classification modeling after appropriate preprocessing and feature engineering.

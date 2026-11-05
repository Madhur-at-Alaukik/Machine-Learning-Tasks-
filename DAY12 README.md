# Machine Learning – Daily Task Update
## Module 3: Data Analysis and Feature Engineering
## Day 12: Preparing a Loan Approval Dataset for Machine Learning

For Day 12, I worked with a Loan Approval Prediction dataset. The dataset contains applicant and financial details that can be used to predict the loan decision. The target column is `loan_status`.

### 1. Load and inspect the dataset

```python
import pandas as pd
import numpy as np

df = pd.read_csv("loan_approval_dataset.csv")

# Remove extra spaces from column names
df.columns = df.columns.str.strip()

print(df.head())
print(df.shape)
print(df.info())
print(df.isnull().sum())
```

The dataset columns include:

- `loan_id`
- `no_of_dependents`
- `education`
- `self_employed`
- `income_annum`
- `loan_amount`
- `loan_term`
- `cibil_score`
- `residential_assets_value`
- `commercial_assets_value`
- `luxury_assets_value`
- `bank_asset_value`
- `loan_status`

The missing-value check showed zero missing values in all 13 columns, so no missing-value imputation was required at that point.

### 2. Check duplicate records

```python
print(df.duplicated().sum())

df = df.drop_duplicates()

print(df["loan_id"].duplicated().sum())
```

The first check finds exact duplicate rows. The second checks whether the loan identifier is repeated. These checks are useful because duplicate observations can affect analysis and model training.

### 3. Check and correct data types

```python
print(df.dtypes)

num_cols = [
    "no_of_dependents",
    "income_annum",
    "loan_amount",
    "loan_term",
    "cibil_score",
    "residential_assets_value",
    "commercial_assets_value",
    "luxury_assets_value",
    "bank_asset_value"
]

for col in num_cols:
    df[col] = pd.to_numeric(df[col], errors="coerce")

print(df[num_cols].dtypes)
print(df.isnull().sum())
```

This checks that numerical fields are stored as numbers. If an invalid value is found, `errors="coerce"` converts it to a missing value, which should then be investigated.

### 4. Check categorical values

```python
cat_cols = ["education", "self_employed", "loan_status"]

for col in cat_cols:
    print(col)
    print(df[col].value_counts(dropna=False))
```

This helps identify inconsistent labels, extra spaces or unexpected categories.

```python
for col in cat_cols:
    df[col] = df[col].astype("string").str.strip()

print(df["education"].value_counts())
print(df["self_employed"].value_counts())
print(df["loan_status"].value_counts())
```

Removing surrounding spaces standardizes values without changing their meaning.

### 5. Inspect numerical values and potential outliers

```python
print(df[num_cols].describe())

print(df[df["income_annum"] < 0])
print(df[df["loan_amount"] < 0])
print(df[~df["cibil_score"].between(300, 900)])
```

These checks help find values that may be invalid. The CIBIL score check flags values outside the commonly used 300–900 range; flagged records should be checked against the dataset documentation.

Potential outliers can also be found with the IQR method:

```python
for col in num_cols:
    q1 = df[col].quantile(0.25)
    q3 = df[col].quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    count = ((df[col] < lower) | (df[col] > upper)).sum()

    print(col, "Potential outliers:", count)
```

Outliers were inspected rather than automatically deleted. High income, large loans or high asset values may be genuine observations.

### 6. Separate features and target

The model should learn from applicant information and predict the loan decision.

- **Features (`X`):** Input columns used to make a prediction.
- **Target (`y`):** The column the model is expected to predict.

The loan ID is an identifier, so it is not used as a predictive feature.

```python
X = df.drop(columns=["loan_id", "loan_status"])
y = df["loan_status"]

print(X.head())
print(y.value_counts())
```

### 7. Split the dataset

The data is split into training and testing sets. The model learns from the training set and is evaluated on the test set.

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42,
    stratify=y
)

print(X_train.shape)
print(X_test.shape)
```

- `test_size=0.2` reserves 20% of the data for testing.
- `random_state=42` makes the split reproducible.
- `stratify=y` helps preserve the class proportions in both sets.

### 8. Encode categorical features

Most machine learning algorithms need numerical input. One-hot encoding converts categories into numerical indicator columns.

```python
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer

cat_features = ["education", "self_employed"]
num_features = [col for col in X.columns if col not in cat_features]

preprocessor = ColumnTransformer(
    transformers=[
        ("cat", OneHotEncoder(handle_unknown="ignore"), cat_features),
        ("num", "passthrough", num_features)
    ]
)

X_train_encoded = preprocessor.fit_transform(X_train)
X_test_encoded = preprocessor.transform(X_test)

print(X_train_encoded.shape)
print(X_test_encoded.shape)
```

The encoder is fitted using training data only. The same fitted encoder transforms the test data. This prevents the test set from influencing the learned preprocessing.

### 9. Final checks

```python
print("Training rows:", X_train_encoded.shape[0])
print("Testing rows:", X_test_encoded.shape[0])

print("Training target distribution:")
print(y_train.value_counts(normalize=True))

print("Testing target distribution:")
print(y_test.value_counts(normalize=True))
```

At this point, the features are separated, categorical columns are encoded and the data is split for model training and evaluation.

### Practice task

1. Load the loan dataset and inspect its shape and columns.
2. Check missing values and duplicate rows.
3. Inspect categorical values and numerical ranges.
4. Separate `loan_status` from the input features.
5. Split the data into training and testing sets.
6. Encode categorical columns using a preprocessing step fitted only on training data.

**Practical objective:** Prepare a real loan approval dataset for classification while checking data quality and avoiding preprocessing leakage.

**Dataset note:** The steps above describe the Loan Approval Prediction dataset used in this task. No outlier removal or model training result is claimed in this Day 12 README.

**GeeksforGeeks references**
- [Scikit-learn train_test_split](https://www.geeksforgeeks.org/machine-learning/ml-sklearn-model-selection-train-test-split/)
- [One-Hot Encoding](https://www.geeksforgeeks.org/machine-learning/ml-one-hot-encoding/)
- [Pandas DataFrame](https://www.geeksforgeeks.org/python/python-pandas-dataframe/)

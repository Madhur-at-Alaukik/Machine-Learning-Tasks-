# Machine Learning – Daily Task Update
## Day 11: Data Cleaning and Missing Values

### 1. Data Quality and Inconsistent Records

**Data quality** describes how suitable a dataset is for analysis and machine learning. Good-quality data should be accurate, complete, consistent and valid.

- **Accuracy:** Values should correctly represent the real information.
- **Completeness:** Required information should be present.
- **Consistency:** The same information should follow the same format throughout the dataset.
- **Validity:** Values should follow the rules and allowed ranges of the field.

An **inconsistent record** contains information that is represented differently from other records even though it may have the same meaning. For example, `Indore`, `indore` and ` Indore ` may refer to the same city. Inconsistent units, date formats, spelling and category labels can also create problems.

Before changing records, identify whether the values are genuinely equivalent. Standardizing text should not merge categories that have different meanings.

```python
df.columns = df.columns.str.strip()
df["location"] = df["location"].str.strip().str.title()
```

The first line removes extra spaces from column names. The second removes surrounding spaces and standardizes capitalization in a text column.

### 2. Missing-Value Patterns

A missing value means that a value was not recorded or is unavailable. The reason for missingness matters because it can affect which cleaning method is appropriate.

- **MCAR – Missing Completely At Random:** The probability of a value being missing is unrelated to observed or unobserved data. For example, a random technical failure may cause some entries to be lost.
- **MAR – Missing At Random:** Missingness is related to another variable that is available in the dataset. For example, one age group may be less likely to answer a particular survey question.
- **MNAR – Missing Not At Random:** Missingness is related to the value that is missing itself. For example, people with very high incomes may be less likely to report their income.

These categories describe the mechanism that may have caused the missing values. A missing-value count alone cannot tell which pattern is present. Understanding the source and context of the data is often necessary.

### 3. Dropping Versus Imputing Missing Values

There are two broad ways to handle missing data.

**Dropping** means removing records or columns that contain missing values. It can be reasonable when only a small number of records are affected and removing them will not remove important information or create bias.

```python
# Remove rows containing at least one missing value
df = df.dropna()

# Remove columns containing missing values
df = df.dropna(axis=1)
```

Dropping too many rows reduces the amount of information available for analysis. It can also change the distribution of the data if the missingness is related to particular groups or outcomes.

**Imputation** means replacing missing values with estimated or selected values. It keeps the affected records, but the replacement may introduce uncertainty or reduce natural variation.

```python
df["income"] = df["income"].fillna(df["income"].median())
```

The choice between dropping and imputing depends on the amount of missing data, the reason values are missing, the importance of the column and the effect on the dataset. Missing values should not automatically be replaced with zero because zero may be a valid measurement with a different meaning.

### 4. Mean, Median and Mode Imputation

Imputation replaces a missing value with a chosen value. Three basic statistical methods are mean, median and mode imputation.

**Mean imputation:** Replaces missing numerical values with the arithmetic average of the available values.

```python
df["income"] = df["income"].fillna(df["income"].mean())
```

It is simple and can be useful when the numerical data is reasonably symmetric and does not contain strong outliers. Extreme values can pull the mean away from the centre, making it less representative.

**Median imputation:** Replaces missing numerical values with the middle value after sorting the available observations.

```python
df["income"] = df["income"].fillna(df["income"].median())
```

The median is less affected by extreme values and is often more appropriate for skewed numerical data. It can be useful for values such as income, prices and property sizes.

**Mode imputation:** Replaces missing values with the most frequently occurring value.

```python
df["education"] = df["education"].fillna(df["education"].mode()[0])
```

Mode imputation is commonly used for categorical data, such as education level or employment type. It can increase the frequency of the most common category, so that effect should be considered.

The method should be selected according to the data distribution and the meaning of the column. For ML workflows, imputation statistics must be calculated from training data only and then applied to validation or test data.

### 5. Duplicate Records

A **duplicate record** is a repeated observation in a dataset. It may be an exact copy of another row or a record that repeats the same real-world entity using a different identifier or formatting.

Duplicates can distort counts, summary statistics and model training because repeated observations receive additional weight.

```python
# Count fully duplicated rows
print(df.duplicated().sum())

# Remove fully duplicated rows
df = df.drop_duplicates()
```

A duplicate check should be based on the meaning of the data. Two rows with identical feature values are not necessarily duplicate real-world observations. When an identifier exists, it may be useful to check whether that identifier is repeated as well.

### 6. Data Type Correction

A data type determines how a value is stored and which operations can be performed on it. A number stored as text cannot be reliably used in numerical calculations until it is converted.

Common examples include:
- Integer values stored as strings.
- Decimal measurements stored as strings.
- Dates stored as ordinary text.
- Categorical values stored in inconsistent formats.

```python
df["income"] = pd.to_numeric(df["income"], errors="coerce")
df["date"] = pd.to_datetime(df["date"], errors="coerce")
```

The `errors="coerce"` option converts values that cannot be parsed into missing values. Those newly created missing values should be inspected rather than ignored. Data type correction should preserve the original meaning of a column; for example, an identification number may look numeric but should often remain a string because arithmetic on it has no meaning.

### 7. Outlier Detection and Treatment

An **outlier** is an observation that is unusually far from most other observations. It can be caused by a data-entry error, a measurement problem or a genuine but uncommon case.

The **Interquartile Range (IQR)** method uses quartiles to identify potential outliers:

- Q1 is the 25th percentile.
- Q3 is the 75th percentile.
- IQR = Q3 − Q1.
- Lower limit = Q1 − 1.5 × IQR.
- Upper limit = Q3 + 1.5 × IQR.

Values outside these limits are flagged for investigation.

```python
q1 = df["income"].quantile(0.25)
q3 = df["income"].quantile(0.75)
iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outliers = df[
    (df["income"] < lower) |
    (df["income"] > upper)
]
```

The **Z-score** expresses how many standard deviations an observation is from the mean:

```python
from scipy.stats import zscore

df["income_zscore"] = zscore(df["income"])
potential_outliers = df[df["income_zscore"].abs() > 3]
```

A common rule flags absolute Z-scores greater than 3, although this rule is more suitable when the distribution is reasonably close to normal.

Outlier treatment may involve correcting verified errors, retaining valid extreme observations, capping extreme values at defined limits or removing records when there is a clear reason. Outliers should not be deleted automatically: a rare value may contain important information.

### 8. Robust Statistics

**Robust statistics** are statistical measures or methods that are less sensitive to extreme observations or departures from assumptions.

The mean and standard deviation can change substantially when a dataset contains very large or very small values. The median and IQR are generally more resistant to these extremes.

For example, in the values `[10, 20, 30, 40, 1000]`, the mean is 220, while the median is 30. The extreme value has a large effect on the mean but does not change the median as much.

Robust measures are useful when numerical data is skewed or contains extreme observations. They do not make a dataset automatically correct; the meaning and source of unusual values still need to be checked.

### 9. Data Leakage During Cleaning

**Data leakage** occurs when information that should not be available to a model during prediction is used during training or model evaluation. Cleaning and preprocessing can cause leakage when they use information from the test set.

For example, calculating a median from the complete dataset before splitting it allows the test observations to influence the value used to fill missing data.

A safer process is:

1. Separate the training and test data.
2. Calculate the imputation value using training data only.
3. Use that same learned value to transform the test data.
4. Keep the test data out of decisions that fit or select preprocessing steps.

The same rule applies to operations such as scaling, feature selection and transformations that learn statistics from the dataset. In Scikit-learn, a Pipeline can help keep preprocessing and model training together so that transformations are fitted correctly within training workflows.

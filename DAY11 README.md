# Machine Learning – Daily Task Update
## Day 11: Data Cleaning and Data Quality

Raw datasets are not always ready for machine learning. They may contain missing values, duplicate records, inconsistent text, incorrect data types or unusual values. Data cleaning is the process of identifying these problems and deciding how to handle them before analysis or model training.

### 1. Data quality and inconsistent records

Data quality describes how accurate, complete, consistent and reliable the data is.

Inconsistent records can represent the same information in different ways. For example, the city name may appear as `Indore`, `indore` and ` INDORE `. These values should be checked and standardized when they refer to the same category.

```python
df["location"] = df["location"].str.strip().str.title()
```

This removes spaces at the beginning and end and standardizes capitalization.

### 2. Missing-value patterns

A missing value means that information was not recorded. It is useful to understand why values are missing before choosing a method.

- **MCAR (Missing Completely At Random):** The missingness is unrelated to the data. Example: a random system failure.
- **MAR (Missing At Random):** Missingness is related to other observed information. Example: one age group is less likely to provide an optional field.
- **MNAR (Missing Not At Random):** Missingness is related to the missing value itself. Example: people with very high incomes may be less likely to report their income.

These patterns describe the reason values are missing; they are not simply percentages of missing data.

### 3. Dropping versus imputing missing values

There are two common approaches:

- **Dropping:** Remove rows or columns that contain missing values when doing so does not remove too much useful information.
- **Imputing:** Fill missing values with a selected replacement when keeping the records is important.

```python
# Remove rows containing missing values
df = df.dropna()

# Fill missing values with a selected value
df["price"] = df["price"].fillna(df["price"].median())
```

Dropping too many records can reduce the dataset or introduce bias. Imputation can also affect the data, so the method should match the column and the reason for missingness.

### 4. Mean, median and mode imputation

- **Mean:** The average of numerical values. It is often useful when data is fairly symmetric and does not contain strong outliers.
- **Median:** The middle value after sorting. It is often more suitable for skewed numerical data or data with extreme values.
- **Mode:** The most frequent value. It can be used for categorical data and some discrete numerical columns.

```python
df["income"] = df["income"].fillna(df["income"].mean())
df["price"] = df["price"].fillna(df["price"].median())
df["city"] = df["city"].fillna(df["city"].mode()[0])
```

Choose an imputation method based on the data. Do not assume that zero is a safe replacement for every missing value.

### 5. Duplicate records

Duplicate records are repeated observations. They can give some observations more influence than intended.

```python
print(df.duplicated().sum())

df = df.drop_duplicates()
```

Before deleting records, check whether identical-looking rows really represent the same observation. An identifier column can help with this check.

### 6. Data type correction

Sometimes a numerical value is stored as text, or a date is stored as a string. Correct data types make calculations and analysis possible.

```python
df["price"] = pd.to_numeric(df["price"], errors="coerce")
df["date"] = pd.to_datetime(df["date"], errors="coerce")
```

With `errors="coerce"`, values that cannot be converted become missing values. Check them after conversion rather than ignoring them.

### 7. Outlier detection and treatment

An outlier is a value that is unusually far from most observations. It may be a data-entry mistake, a rare but valid case or an unusual event.

One common method is the Interquartile Range (IQR):

```python
q1 = df["price"].quantile(0.25)
q3 = df["price"].quantile(0.75)
iqr = q3 - q1

lower_limit = q1 - 1.5 * iqr
upper_limit = q3 + 1.5 * iqr

outliers = df[
    (df["price"] < lower_limit) |
    (df["price"] > upper_limit)
]
```

Values outside the limits are potential outliers, not automatically errors. Investigate them before deciding whether to correct, keep, cap or remove them.

### 8. Robust statistics

Robust statistics are less affected by extreme values.

- The mean can change considerably when an extreme value is present.
- The median is generally less affected by extreme values.
- Standard deviation is sensitive to extreme values.
- IQR is generally more resistant to extreme values.

For example, in `[10, 20, 30, 40, 1000]`, the mean is 220 while the median is 30. This is one reason the median is often used when numerical data is skewed.

### 9. Data leakage during cleaning

Data leakage happens when information that should not be available during prediction influences model training or evaluation.

For example, calculating an imputation mean from the complete dataset before splitting it allows test data to influence preprocessing.

A safer process is:
1. Split the dataset into training and test sets.
2. Learn imputation values and other preprocessing settings using training data only.
3. Apply those same settings to the test data.
4. Evaluate the model on the test data.

The same principle applies to scaling, feature selection and other preprocessing steps that learn information from data.

### Practice task

1. Inspect a dataset and count missing values.
2. Check for inconsistent categories and duplicate rows.
3. Compare mean and median for a numerical column.
4. Find potential outliers using IQR.
5. Check data types and convert columns where needed.
6. Explain why preprocessing should be fitted on training data only.

**Practical objective:** Identify common data quality problems and choose suitable cleaning methods without losing useful information or causing data leakage.

**GeeksforGeeks references**
- [Handling Missing Values in Pandas](https://www.geeksforgeeks.org/python/working-with-missing-data-in-pandas/)
- [Removing Duplicates in Pandas](https://www.geeksforgeeks.org/python-pandas-dataframe-drop_duplicates/)
- [Pandas Data Cleaning](https://www.geeksforgeeks.org/python/data-cleaning-in-python/)

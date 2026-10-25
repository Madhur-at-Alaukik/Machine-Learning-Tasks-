# Machine Learning – Daily Task Update
## Day 10: Pandas and Data Manipulation

### 1. What Is Pandas?
Pandas is a Python library for working with labelled, tabular, and time-series data. It is widely used for loading datasets, inspecting data, cleaning values, filtering records, grouping, joining tables, and preparing data for visualization and Machine Learning.

Install and import:

```bash
python -m pip install pandas openpyxl
```

```python
import pandas as pd
```

`openpyxl` is commonly used by Pandas to read and write `.xlsx` Excel files.

### 2. Series and DataFrame
A **Series** is a one-dimensional labelled array. A **DataFrame** is a two-dimensional table with labelled rows and columns.

```python
import pandas as pd

marks = pd.Series([80, 90, 85], name="marks")
students = pd.DataFrame({
    "name": ["Asha", "Ravi", "Mina"],
    "marks": [80, 90, 85]
})

print(marks)
print(students)
```

A DataFrame can contain columns with different data types, such as text, integers, floating-point numbers, and dates.

### 3. Reading CSV and Excel Files
```python
df_csv = pd.read_csv("students.csv")
df_excel = pd.read_excel("students.xlsx")

print(df_csv.head())
```

Other useful options include `sep=` for a different delimiter, `encoding=` for text encoding, and `sheet_name=` for selecting an Excel sheet.

Always check the file path and inspect the loaded data rather than assuming it was interpreted correctly.

### 4. Inspecting a Dataset
Common inspection methods:
- `head()` and `tail()`: Preview rows.
- `shape`: Number of rows and columns.
- `columns`: Column names.
- `dtypes`: Column data types.
- `info()`: Non-null counts and data types.
- `describe()`: Summary statistics for selected columns.
- `isna().sum()`: Missing-value counts.

```python
print(df_csv.head())
print(df_csv.shape)
print(df_csv.columns)
print(df_csv.dtypes)
print(df_csv.info())
print(df_csv.describe(include="all"))
print(df_csv.isna().sum())
```

Dataset inspection should happen before cleaning or analysis because it helps reveal missing values, unexpected types, and inconsistent columns.

### 5. Selecting Columns and Rows
```python
df = pd.DataFrame({
    "name": ["Asha", "Ravi", "Mina"],
    "marks": [80, 90, 85],
    "city": ["Indore", "Bhopal", "Indore"]
})

print(df["name"])                # One column as a Series
print(df[["name", "marks"]])     # Multiple columns as a DataFrame
print(df.loc[0, "name"])         # Label-based selection
print(df.iloc[0, 1])             # Position-based selection
```

`loc` selects by index and column labels; `iloc` selects by integer position. An index label is not necessarily the same as a row's position.

### 6. Filtering and Sorting
Boolean filtering selects rows that meet a condition.

```python
passed = df[df["marks"] >= 85]
indore_students = df[df["city"] == "Indore"]
top_indore = df[(df["city"] == "Indore") & (df["marks"] >= 85)]

sorted_df = df.sort_values("marks", ascending=False)
print(passed)
print(top_indore)
print(sorted_df)
```

Use `&` for element-wise AND and `|` for element-wise OR, and wrap each condition in parentheses. Do not use Python's `and` or `or` for combining Pandas Series conditions.

### 7. Creating and Updating Columns
A new column can be calculated from existing columns.

```python
df["passed"] = df["marks"] >= 40
df["bonus_marks"] = df["marks"] + 5
```

Derived columns are useful for feature engineering, but ensure that they make sense for the problem and do not accidentally use information that would not be available at prediction time.

### 8. Grouping and Aggregation
`groupby()` splits rows into groups, applies an operation, and combines the results. It is useful for group-level summaries.

```python
sales = pd.DataFrame({
    "region": ["North", "South", "North", "South"],
    "sales": [100, 150, 200, 120]
})

summary = sales.groupby("region")["sales"].agg(["sum", "mean", "count"])
print(summary)
```

This returns total sales, average sales per record, and the number of records for each region.

### 9. Merging, Joining and Concatenation
**Merge:** Combines tables using one or more matching keys, similar to a database join.

```python
customers = pd.DataFrame({
    "customer_id": [1, 2],
    "name": ["Asha", "Ravi"]
})
orders = pd.DataFrame({
    "customer_id": [1, 1, 2],
    "amount": [500, 300, 700]
})

merged = pd.merge(customers, orders, on="customer_id", how="left")
print(merged)
```

Common merge types:
- `inner`: Only matching keys.
- `left`: All keys from the left table plus matches.
- `right`: All keys from the right table plus matches.
- `outer`: All keys from both tables.

**Concatenation:** Stacks objects along rows or columns rather than matching records by a key.

```python
combined_rows = pd.concat([df, df], ignore_index=True)
```

Before merging, check key uniqueness and row counts; duplicate keys can create more rows than expected.

### 10. Date and Time Processing
Use `pd.to_datetime()` to convert date strings into datetime values.

```python
df_dates = pd.DataFrame({
    "order_date": ["2026-01-05", "2026-02-10", "2026-02-20"]
})

df_dates["order_date"] = pd.to_datetime(df_dates["order_date"])
df_dates["year"] = df_dates["order_date"].dt.year
df_dates["month"] = df_dates["order_date"].dt.month
df_dates["day_name"] = df_dates["order_date"].dt.day_name()

print(df_dates)
```

Date parsing may need options such as `format=` or handling of invalid values. Time zones matter when timestamps represent real-world events across regions.

### 11. Handling Missing Values
Pandas represents missing values using markers such as `NaN`, `None`, or `NaT`, depending on data type.

```python
print(df_csv.isna().sum())
cleaned = df_csv.dropna()
```

Dropping all rows with missing values is only one possible approach. Other strategies include filling with a meaningful constant, median, mode, or a model-based estimate. Choose a strategy based on the data and problem rather than replacing every missing value with zero.

For ML, learn imputation values from training data only and apply the same transformation to validation, test, and future data to avoid leakage.

### 12. Exporting Data
```python
df_csv.to_csv("processed_data.csv", index=False)
df_csv.to_excel("processed_data.xlsx", index=False)
```

`index=False` avoids exporting the DataFrame index as an additional column when it is not needed.

### 13. Practical Exercise: Sales Data Analysis
Create or load a sales dataset and complete these tasks:
1. Inspect rows, columns, data types, and missing values.
2. Filter records for one region.
3. Sort sales from highest to lowest.
4. Calculate total and average sales by region.
5. Merge sales with customer information using a customer ID.
6. Extract month and year from order dates.
7. Export the processed dataset to CSV.

### 14. Key Takeaways
- A Series is one-dimensional; a DataFrame is two-dimensional.
- Inspect data before changing it.
- Use selection and Boolean filtering to retrieve records.
- `groupby()` summarizes data by category.
- `merge()` combines tables by keys; `concat()` stacks data along an axis.
- Date-time conversion enables date-based analysis.
- Missing values require a considered strategy.
- Exporting creates reusable processed datasets.

**Practical Objective:** Load, inspect, filter, aggregate, combine, and export real-world tabular data using Pandas as a foundation for exploratory data analysis and ML.

**GeeksforGeeks References:**
- [Pandas Tutorial](https://www.geeksforgeeks.org/python/pandas-tutorial/)
- [Pandas Series](https://www.geeksforgeeks.org/python/python-pandas-series/)
- [Pandas DataFrame](https://www.geeksforgeeks.org/python/python-pandas-dataframe/)
- [Pandas GroupBy](https://www.geeksforgeeks.org/python/pandas-groupby/)
- [Pandas Merge, Join and Concatenate](https://www.geeksforgeeks.org/pandas/difference-between-merge-and-join-in-pandas/)
# Machine Learning – Daily Task Update
## Day 10: Exploring and Manipulating Data with Pandas

NumPy is great for numerical arrays. Real datasets, however, usually have column names, mixed data types, dates and missing entries. Pandas gives us a convenient table-like structure for inspecting and preparing that kind of data before visualization or model training.

### 1. Meet Series and DataFrames
A **Series** is a one-dimensional collection with labels. A **DataFrame** is a two-dimensional table whose columns can hold different types of data.

\`\`\`python
import pandas as pd

marks = pd.Series([80, 90, 85], name="marks")
students = pd.DataFrame({
    "name": ["Asha", "Ravi", "Mina"],
    "marks": [80, 90, 85],
    "city": ["Indore", "Bhopal", "Indore"]
})

print(marks)
print(students)
\`\`\`

Install Pandas with \`python -m pip install pandas openpyxl\`. The \`openpyxl\` package is commonly used for working with Excel \`.xlsx\` files.

### 2. Load a file and inspect it before changing anything
\`\`\`python
df = pd.read_csv("students.csv")
print(df.head())
print(df.shape)
print(df.columns)
print(df.dtypes)
print(df.info())
print(df.describe(include="all"))
print(df.isna().sum())
\`\`\`

Useful inspection tools include:
- \`head()\` and \`tail()\`: preview the first or last rows.
- \`shape\`: number of rows and columns.
- \`columns\`: column names.
- \`dtypes\`: data types inferred for each column.
- \`info()\`: non-null counts and memory information.
- \`describe()\`: summary statistics.
- \`isna().sum()\`: missing-value counts.

For Excel files, use \`pd.read_excel("students.xlsx")\`. Check the path, column names and inferred types rather than assuming the file loaded exactly as intended.

### 3. Select a useful part of the table
\`\`\`python
print(df["name"])                 # One column: Series
print(df[["name", "marks"]])      # Several columns: DataFrame
print(df.loc[0, "name"])          # Label-based selection
print(df.iloc[0, 1])              # Position-based selection
\`\`\`

\`loc\` uses index and column labels, while \`iloc\` uses integer positions. An index label does not always equal a row's position, especially after filtering or sorting.

### 4. Filter rows and sort results
Boolean filtering is one of the most common operations in data analysis.

\`\`\`python
passed = df[df["marks"] >= 40]
indore_students = df[df["city"] == "Indore"]
top_indore = df[
    (df["city"] == "Indore") & (df["marks"] >= 85)
]

sorted_df = df.sort_values("marks", ascending=False)
print(top_indore)
print(sorted_df)
\`\`\`

Use \`&\` for element-wise AND and \`|\` for element-wise OR. Put each condition in parentheses. Python's \`and\` and \`or\` operators are not suitable for combining Pandas Series conditions.

### 5. Add calculated columns
You can create a new column from values already in the table.

\`\`\`python
df["passed"] = df["marks"] >= 40
df["bonus_marks"] = df["marks"] + 5
\`\`\`

In ML, derived columns may become features. Before using one, ask whether it would genuinely be available at the time a prediction is made. A feature containing information from the future can leak the answer into the model and produce misleading evaluation results.

### 6. Summarize groups of records
\`groupby()\` splits data into groups, applies an aggregation and combines the results. For example, we might want total and average sales by region.

\`\`\`python
sales = pd.DataFrame({
    "region": ["North", "South", "North", "South"],
    "sales": [100, 150, 200, 120]
})

summary = sales.groupby("region")["sales"].agg(
    ["sum", "mean", "count"]
)
print(summary)
\`\`\`

This gives the total, average and number of records for each region. Grouping is useful for answering questions before building a model, such as which regions have the highest average sales.

### 7. Combine related tables
A customer table and an order table may share a customer ID. A merge connects rows using that key.

\`\`\`python
customers = pd.DataFrame({
    "customer_id": [1, 2],
    "name": ["Asha", "Ravi"]
})
orders = pd.DataFrame({
    "customer_id": [1, 1, 2],
    "amount": [500, 300, 700]
})

merged = pd.merge(
    customers, orders, on="customer_id", how="left"
)
print(merged)
\`\`\`

Common merge types are \`inner\` (matching keys only), \`left\` (all left rows and any matches), \`right\` (all right rows and matches) and \`outer\` (all keys from both tables). Check whether keys are unique: duplicate keys can multiply rows during a merge.

\`pd.concat()\` serves a different purpose: it stacks objects along rows or columns rather than matching records by a key.

### 8. Make dates useful
Dates often arrive as strings. Convert them before extracting date parts or sorting chronologically.

\`\`\`python
df["order_date"] = pd.to_datetime(df["order_date"])
df["year"] = df["order_date"].dt.year
df["month"] = df["order_date"].dt.month
df["day_name"] = df["order_date"].dt.day_name()
\`\`\`

If the source has an unusual date format, you may need to provide \`format=\`. Real event timestamps may also require attention to time zones.

### 9. Decide what to do with missing values
Pandas can represent missing data with markers such as \`NaN\`, \`None\` or \`NaT\`. Start by counting missing values:

\`\`\`python
print(df.isna().sum())
\`\`\`

You may remove some incomplete rows with \`dropna()\`, fill values with a justified constant or summary statistic, or use a more advanced imputation method. Replacing every missing value with zero is rarely a safe default because zero may have a real meaning.

For ML, calculate imputation values using the training data only, then apply the same transformation to validation, test and future data. This helps prevent data leakage.

### 10. Save the processed result
\`\`\`python
df.to_csv("processed_students.csv", index=False)
df.to_excel("processed_students.xlsx", index=False)
\`\`\`

Using \`index=False\` prevents the DataFrame index from being written as an extra column when it is not needed.

### Practice task: explore a small sales dataset
1. Load a CSV and inspect its rows, columns, types and missing values.
2. Filter the records for one region and sort them by sales.
3. Calculate total and average sales for each region.
4. Merge sales with a customer table using a customer ID.
5. Extract the month from each order date.
6. Choose a reasonable approach for missing values and explain why.
7. Export the cleaned table to a new CSV file.

**Practical objective:** Load, inspect, filter, summarize, combine and export tabular data as preparation for exploratory data analysis and machine learning.

**GeeksforGeeks references**
- [Pandas Tutorial](https://www.geeksforgeeks.org/python/pandas-tutorial/)
- [Pandas Series](https://www.geeksforgeeks.org/python/python-pandas-series/)
- [Pandas DataFrame](https://www.geeksforgeeks.org/python/python-pandas-dataframe/)
- [Pandas GroupBy](https://www.geeksforgeeks.org/python/pandas-groupby/)
- [Pandas Merge, Join and Concatenate](https://www.geeksforgeeks.org/pandas/difference-between-merge-and-join-in-pandas/)
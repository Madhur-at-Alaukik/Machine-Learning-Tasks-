# Machine Learning – Daily Task Update
## Day 13: Exploratory Data Analysis and Feature Engineering

### 1. Univariate, Bivariate and Multivariate Analysis

**Exploratory Data Analysis (EDA)** is the process of examining a dataset to understand its structure, distributions, relationships and unusual observations before building a machine learning model.

EDA can be performed at three levels:

**Univariate analysis** studies one variable at a time. It helps describe the distribution, typical value, spread, missing values and unusual observations of a feature. Numerical variables can be examined using summary statistics, histograms and box plots. Categorical variables can be examined using frequency tables and bar charts.

**Bivariate analysis** studies the relationship between two variables. Examples include comparing income with loan amount, or examining loan status across education categories. Scatter plots, grouped summaries, box plots and correlation values can help describe these relationships.

**Multivariate analysis** examines three or more variables together. It helps identify relationships that may not be clear when variables are studied separately. Grouped comparisons, correlation heatmaps and plots using color or size to represent additional variables can support this analysis.

EDA describes patterns in the available data. A pattern or association found during EDA should not automatically be interpreted as a causal relationship.

### 2. Feature-Target Relationships

A **feature** is an input variable used by a model to make a prediction. The **target** is the value the model is expected to predict.

Feature-target analysis examines how each input feature relates to the target. For a numerical target, this may involve examining scatter plots, distributions and correlation. For a categorical target, numerical features can be compared across target classes, while categorical features can be examined using group counts or proportions.

For example, in a loan approval dataset:
- Features may include annual income, loan amount, CIBIL score and asset values.
- The target may be loan status.
- Analysis can compare the distributions of income or CIBIL score for approved and rejected cases.

A feature may show a relationship with the target without being sufficient on its own to make accurate predictions. The relationship should also be checked for data leakage: a feature must not contain information that would only become available after the prediction decision.

### 3. Correlation Analysis

**Correlation** measures the strength and direction of association between two variables. It is commonly used during EDA to understand whether numerical features move together.

The Pearson correlation coefficient ranges from -1 to +1:
- **Positive correlation:** Higher values of one variable tend to occur with higher values of the other.
- **Negative correlation:** Higher values of one variable tend to occur with lower values of the other.
- **Near-zero correlation:** Little or no linear association is detected.

A correlation matrix shows pairwise correlations among numerical columns and can be displayed as a heatmap.

Correlation is useful for identifying possible redundant features or relationships worth investigating. However, it has limitations:
- Pearson correlation measures linear association and may miss non-linear patterns.
- Outliers can strongly affect correlation values.
- Correlation does not establish causation.
- A low correlation with the target does not necessarily mean a feature has no predictive value.
- Relationships among several features can be more complex than pairwise correlations show.

### 4. Feature Creation and Transformation

**Feature engineering** is the process of creating or transforming input variables so that they represent useful information for a model.

**Feature creation** combines or derives information from existing columns. For example, total assets could be calculated by adding several asset-value columns when that total is meaningful for the problem.

```python
df["total_assets"] = (
    df["residential_assets_value"]
    + df["commercial_assets_value"]
    + df["luxury_assets_value"]
    + df["bank_asset_value"]
)
```

**Feature transformation** changes the representation or scale of a feature. Examples include applying a logarithmic transformation to a highly skewed positive variable, converting a date into separate components, or converting a measurement into a meaningful ratio.

A derived feature should have a clear meaning and should be available at the time the model is expected to make its prediction. Transformations should be selected based on the data distribution and the requirements of the model.

### 5. Date/Time Feature Extraction

Date and time columns can contain information about trends, cycles and timing. A timestamp can be separated into useful components such as year, month, day, weekday or hour.

```python
df["date"] = pd.to_datetime(df["date"])

df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["day"] = df["date"].dt.day
df["weekday"] = df["date"].dt.dayofweek
```

These features can help a model represent seasonal or calendar-related patterns. The components selected should match the problem. For example, month may be useful for seasonal behaviour, while hour may be useful for hourly demand.

Date-derived features must respect the prediction time. Using a date or timestamp that contains information from after the event being predicted can cause target leakage.

### 6. Feature Selection Fundamentals

**Feature selection** is the process of choosing which existing features should be used as model inputs. The goal is to retain useful information while reducing irrelevant, redundant or noisy features.

Feature selection can:
- Reduce unnecessary complexity.
- Make models easier to interpret.
- Reduce training time and memory use.
- Help limit overfitting when irrelevant features are removed.

Feature selection is different from feature engineering. Feature engineering creates or transforms features; feature selection chooses among available features.

Selection decisions should be made using training data only. Choosing features after looking at test-set performance can leak information from the test set into the modelling process.

### 7. Low-Variance and Redundant Features

A **low-variance feature** has values that are nearly the same for most observations. Because it changes very little, it may provide limited information for distinguishing records. A constant feature is an extreme case of zero variance.

Low variance does not always mean a feature is useless. A rare category or an uncommon indicator may be important for a particular prediction problem, so the context should be considered before removing it.

**Redundant features** contain overlapping information. For example, two columns may measure nearly the same quantity or have a very strong correlation. Redundant inputs can make a model more complex and may make some model coefficients harder to interpret.

Correlation analysis can help identify possible redundancy, but highly correlated features should not automatically be removed. Their definitions, usefulness and behaviour with the chosen model should be examined.

### 8. Categorical Encoding

Categorical features contain labels rather than numerical measurements. Many ML algorithms require these values to be converted into numerical representations.

**One-hot encoding** creates a separate binary column for each category. A row receives 1 in the column corresponding to its category and 0 in the other category columns.

For example, a feature with values `Graduate` and `Not Graduate` can become two indicator columns.

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(handle_unknown="ignore")
```

One-hot encoding does not create an artificial ranking between categories. It can, however, create many columns when the original feature contains many distinct categories.

**Ordinal encoding** assigns integer values to categories that have a meaningful order. It should be used only when that order is real and understood. Assigning arbitrary numbers to unordered categories can make some models interpret a false numerical relationship.

Encoding must be fitted using training data only. Categories that appear later in validation, test or production data should be handled deliberately.

### 9. High-Cardinality Categorical Features

A categorical feature has **high cardinality** when it contains a large number of distinct categories. Examples can include customer IDs, product codes, postcodes or website URLs.

One-hot encoding a high-cardinality column may create a very large number of features. Many categories may also have only a few observations, which can make patterns difficult to estimate reliably.

Possible approaches include grouping rare categories when appropriate, using domain-based grouping, applying suitable encoding methods or excluding identifiers that do not contain useful predictive information.

The correct approach depends on what the category represents. A high number of unique values is not, by itself, a reason to remove a feature.

### 10. Target Encoding and Its Leakage Risks

**Target encoding** replaces a category with a statistic calculated from the target values associated with that category. For a classification task, this may be the proportion of positive target examples within each category. For a regression task, it may be the average target value.

For example, a category may be represented by the historical approval rate for that category. This can provide a compact numerical representation for a high-cardinality feature.

The main risk is **target leakage**. If the target statistics are calculated using the same rows that are later used to train the model, each row's target can influence its own encoded feature. This can produce overly optimistic training results.

Target encoding should be calculated using training folds only. Out-of-fold encoding calculates category statistics from other folds and applies them to the held-out fold. Validation and test data must be transformed using mappings learned from the relevant training data, with a defined fallback for unseen categories.

### 11. Class Imbalance Overview

**Class imbalance** occurs when target classes have substantially different numbers of observations. For example, a dataset may contain many more approved loans than rejected loans.

A model trained on imbalanced data may favour the majority class and perform poorly on the minority class. High overall accuracy can hide this problem.

The class distribution should be inspected before training. Evaluation should consider precision, recall and F1-score for each class, along with the confusion matrix. The appropriate approach depends on the problem and the cost of different prediction errors.

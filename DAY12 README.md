# Machine Learning – Daily Task Update
## Day 12: Data Visualization

### 1. Matplotlib and Seaborn

**Data visualization** represents data using charts and plots so that distributions, comparisons, patterns and relationships can be examined.

**Matplotlib** is a general-purpose Python plotting library. It provides control over figures, axes, labels, titles, legends, ticks and plot appearance. It is useful when a chart needs detailed customization.

**Seaborn** is built on Matplotlib and provides a higher-level interface for statistical visualization. It works naturally with Pandas DataFrames and makes it easier to create charts such as distribution plots, categorical comparisons and correlation heatmaps.

```python
import matplotlib.pyplot as plt
import seaborn as sns
```

Both libraries can be used together. Seaborn creates the statistical chart, while Matplotlib can be used to adjust labels, titles, figure size and other display details.

### 2. Bar, Line and Area Charts

**Bar chart:** Uses rectangular bars to compare values across categories. The length or height of a bar represents the value for that category. Bar charts are suitable for comparing quantities such as sales by region or number of applications by status.

```python
sns.barplot(data=df, x="education", y="income")
plt.xlabel("Education")
plt.ylabel("Average Income")
plt.show()
```

When comparing categories, use clear labels and a consistent scale. A bar chart normally uses a zero baseline because differences in bar length are interpreted visually.

**Line chart:** Connects data points in a meaningful order. It is commonly used to show how a numerical value changes over time, such as monthly revenue or daily temperature. The order of points matters; a line chart is not usually appropriate for unrelated categories.

```python
plt.plot(df["month"], df["sales"])
plt.xlabel("Month")
plt.ylabel("Sales")
plt.show()
```

**Area chart:** Similar to a line chart, but the area between the line and the baseline is filled. It emphasizes the magnitude of a value over an ordered sequence. Stacked area charts can show how several components contribute to a total over time, but overlapping areas can make exact comparisons difficult.

### 3. Histograms and Density Plots

**Histogram:** Shows the distribution of a numerical variable by dividing its values into intervals called bins. The height of each bar represents the number or proportion of observations within a bin.

A histogram helps examine the centre, spread, skewness, gaps, peaks and possible extreme values in a numerical column.

```python
sns.histplot(data=df, x="income", bins=20)
plt.xlabel("Annual Income")
plt.show()
```

The selected bin width affects the appearance of the distribution. Too few bins can hide useful detail, while too many can make random variation look like a pattern.

**Density plot:** Shows a smoothed estimate of the distribution of a numerical variable. It provides a continuous curve rather than separate bars.

```python
sns.kdeplot(data=df, x="income", fill=True)
plt.xlabel("Annual Income")
plt.show()
```

Density plots are useful for comparing distribution shapes, but the smoothing bandwidth affects the curve. A density value represents estimated concentration, not the number of observations at an exact value.

### 4. Scatter Plots

A **scatter plot** displays pairs of numerical observations as points. One variable is placed on the horizontal axis and another on the vertical axis.

It helps examine:
- Whether two variables appear to move together.
- Whether the relationship is positive, negative or weak.
- Whether the relationship is linear or curved.
- Whether clusters or unusual observations are present.

```python
sns.scatterplot(data=df, x="income_annum", y="loan_amount")
plt.xlabel("Annual Income")
plt.ylabel("Loan Amount")
plt.show()
```

A scatter plot can reveal association, but it does not establish that one variable causes a change in another. Overlapping points may also hide how many observations share similar values.

### 5. Box and Violin Plots

**Box plot:** Summarizes a numerical distribution using quartiles. The box extends from Q1 to Q3, and the line inside it marks the median. The interquartile range is the distance between Q1 and Q3. Whiskers extend according to the plotting method, and individual points beyond them may be displayed as potential outliers.

```python
sns.boxplot(data=df, x="loan_status", y="loan_amount")
plt.show()
```

Box plots are useful for comparing the centre and spread of a numerical variable across categories. They do not show every detail of the distribution, such as multiple peaks.

**Violin plot:** Combines a box-plot-style summary with a density shape. The width of the violin indicates where observations are more concentrated.

```python
sns.violinplot(data=df, x="loan_status", y="loan_amount")
plt.show()
```

Violin plots can show differences in distribution shape, including multiple concentrations. Their appearance depends on density estimation and smoothing, so they should be interpreted alongside the sample size and underlying data.

### 6. Correlation Heatmaps

A **correlation heatmap** uses colors to represent correlation values between numerical variables. Correlation measures the strength and direction of an association.

The Pearson correlation coefficient ranges from -1 to +1:
- +1 indicates a perfect positive linear relationship.
- -1 indicates a perfect negative linear relationship.
- 0 indicates no linear relationship.

```python
correlation = df.select_dtypes(include="number").corr()

sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm",
    center=0
)

plt.show()
```

Heatmaps make it easier to identify pairs of numerical features with strong positive or negative correlations. Correlation does not prove causation, and a low Pearson correlation does not rule out a non-linear relationship.

### 7. Chart Selection

The chart should match the type of data and the question being examined.

| Purpose | Suitable chart |
|---|---|
| Compare values across categories | Bar chart |
| Show change over ordered time | Line chart |
| Show totals or contributions over time | Area chart |
| Examine a numerical distribution | Histogram or density plot |
| Examine the relationship between two numerical variables | Scatter plot |
| Compare spread and possible outliers across groups | Box plot |
| Compare distribution shapes across groups | Violin plot |
| Examine correlations among numerical variables | Correlation heatmap |

Choosing a chart based only on appearance can hide important information. The purpose of the visualization should determine the chart type.

### 8. Visualization Limitations and Misleading Graphs

A chart can communicate data clearly, but poor design or inappropriate choices can create a misleading impression.

Common issues include:

- **Misleading axis scales:** A truncated axis can make small differences appear very large.
- **Unequal intervals:** Irregular spacing on an axis can distort the visual relationship.
- **Inappropriate chart types:** A line joining unrelated categories can suggest an order or continuity that does not exist.
- **Overloaded charts:** Too many categories, colors or labels can make patterns difficult to interpret.
- **Missing context:** Omitting units, sample size, time period or data source can lead to incorrect conclusions.
- **Correlation mistaken for causation:** A visible relationship does not prove that one variable causes another.
- **Small or biased samples:** A visually clear chart can still represent incomplete or unrepresentative data.

A good visualization should use accurate scales, clear titles, axis labels, units and legends where needed. The chart should show the data without hiding relevant context or exaggerating differences.


## Additional Learning — Visualizing a Model's Confusion Matrix

A confusion matrix can also be displayed as a heatmap-style chart. This provides a visual way to compare actual classes with the classes predicted by a classifier.

In the loan approval model exercise, the matrix was:

| Actual / Predicted | Approved | Rejected |
|---|---:|---:|
| Approved | 485 | 43 |
| Rejected | 118 | 203 |

The vertical axis represents the actual class and the horizontal axis represents the predicted class. The diagonal cells contain correct predictions, while the other cells contain incorrect predictions.

```python
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay
import matplotlib.pyplot as plt

cm = confusion_matrix(y_test, y_pred)

display = ConfusionMatrixDisplay(
    confusion_matrix=cm,
    display_labels=model.classes_
)

display.plot()
plt.show()
```

The chart makes it easier to see which class the model predicts correctly and where it makes mistakes. It is important to read the axis labels before interpreting the cells, because reversing actual and predicted labels changes the meaning of the results.

# Machine Learning – Daily Task Update
## Module 2: Mathematics and Statistics
## Day 6: Descriptive Statistics and Distributions

### 1. Population, Sample and Sampling Bias
A **population** is the complete group we want to understand. A **sample** is a subset selected from that population. We often study a sample because collecting data from every member of a population is expensive or impractical.

**Example:** All customers of a company form the population; 500 surveyed customers form a sample.

A sample should represent the population. **Sampling bias** occurs when the selection method systematically favors some members or outcomes, making conclusions less reliable.

**Example:** Surveying only premium customers to estimate satisfaction among all customers can produce a biased estimate.

### 2. Mean, Median and Mode
**Mean:** The arithmetic average; add all values and divide by the number of values.

`Mean = Sum of values / Number of values`

**Median:** The middle value after sorting the data. For an even number of observations, it is the average of the two middle values.

**Mode:** The most frequent value. A dataset may have one mode, multiple modes, or no uniquely most frequent value.

Example dataset: `2, 3, 3, 4, 18`
- Mean = 6
- Median = 3
- Mode = 3

The large value 18 pulls the mean upward, while the median is more resistant to extreme observations.

### 3. Range, Variance and Standard Deviation
**Range** is the difference between the largest and smallest values.

`Range = Maximum − Minimum`

**Variance** measures the average squared deviation from the mean. Population variance divides by `N`; sample variance commonly divides by `n - 1` to estimate population variance.

Population variance: `σ² = Σ(xᵢ − μ)² / N`

Sample variance: `s² = Σ(xᵢ − x̄)² / (n − 1)`

**Standard deviation** is the square root of variance. It measures spread in the same units as the original data.

A high standard deviation indicates more spread around the mean, but interpretation depends on the distribution and context.

### 4. Quartiles, Percentiles and IQR
Quartiles divide sorted data into four parts:
- Q1: approximately the 25th percentile.
- Q2: the median, or 50th percentile.
- Q3: approximately the 75th percentile.

A percentile describes the position below which a given percentage of observations falls. Exact percentile calculations can differ slightly between software methods.

**Interquartile range (IQR):**

`IQR = Q3 − Q1`

IQR measures the spread of the middle 50% of the data and is relatively resistant to extreme values.

### 5. Outliers
An outlier is an observation unusually far from the general pattern of the data. Outliers may reflect data-entry errors, measurement issues, rare valid events, or a different population.

A common IQR rule flags values below `Q1 − 1.5 × IQR` or above `Q3 + 1.5 × IQR`.

This rule identifies potential outliers, not automatically incorrect values. Investigate them before removing or changing them.

### 6. Common Distributions
**Normal distribution:** A symmetric, bell-shaped distribution described by its mean and standard deviation. In an ideal normal distribution, the mean, median, and mode are equal.

**Uniform distribution:** Values within a specified interval have equal density (for a continuous uniform distribution).

**Skewed distribution:** An asymmetric distribution.
- **Right-skewed:** A longer tail extends toward larger values.
- **Left-skewed:** A longer tail extends toward smaller values.

Income and transaction amounts are often right-skewed, though real data may have other shapes.

### 7. Z-Scores
A z-score expresses how many standard deviations an observation is from the mean.

`z = (x − μ) / σ`

For sample-based analysis, the sample mean and sample standard deviation are often substituted.

- `z = 0`: At the mean.
- `z = 1`: One standard deviation above the mean.
- `z = -2`: Two standard deviations below the mean.

Z-scores help compare values on different scales, but they do not automatically prove that an observation is an outlier.

### 8. Calculate Statistics with Python
```python
import statistics as stats

data = [2, 3, 3, 4, 18]

print("Mean:", stats.mean(data))
print("Median:", stats.median(data))
print("Mode:", stats.mode(data))
print("Sample variance:", stats.variance(data))
print("Sample standard deviation:", stats.stdev(data))
print("Range:", max(data) - min(data))
```

The variance and standard deviation functions above use sample formulas. The dataset is small, so the output should be interpreted as a description of these observations rather than a strong conclusion about a larger population.

### 9. Identify Potential Outliers Using IQR
```python
import numpy as np

data = np.array([10, 12, 13, 14, 15, 16, 18, 80])

q1 = np.percentile(data, 25)
q3 = np.percentile(data, 75)
iqr = q3 - q1

lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

outliers = data[(data < lower_bound) | (data > upper_bound)]

print("Q1:", q1)
print("Q3:", q3)
print("IQR:", iqr)
print("Potential outliers:", outliers)
```

Quartile interpolation conventions may vary between tools. The IQR method should be used as a diagnostic aid, not an automatic data-cleaning rule.

### 10. Visualize a Distribution
```python
import matplotlib.pyplot as plt

data = [10, 12, 13, 14, 15, 16, 18, 80]

plt.hist(data, bins=5, edgecolor="black")
plt.title("Distribution of Values")
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.show()

plt.boxplot(data)
plt.title("Box Plot of Values")
plt.ylabel("Value")
plt.show()
```

A histogram shows how observations are distributed across intervals. A box plot summarizes the median, quartiles, and potential outliers according to its plotting convention.

### 11. Comparing Two Datasets
When comparing datasets, inspect:
- Center: mean and median.
- Spread: range, variance, standard deviation, and IQR.
- Shape: symmetry, skewness, and multiple peaks.
- Unusual values: possible outliers or data errors.
- Sample size and data collection method.

Two datasets can have the same mean but very different spreads and distributions.

### 12. Key Takeaways
- A sample should represent the population to support reliable conclusions.
- Mean is sensitive to extreme values; median is more robust.
- Variance measures squared spread, while standard deviation uses the original units.
- Quartiles and IQR describe the middle of the distribution.
- The IQR rule flags potential outliers that need investigation.
- Z-scores describe distance from the mean in standard deviation units.
- Histograms and box plots complement numerical summaries.

**Practical Objective:** Calculate and interpret descriptive statistics, identify potential outliers, and describe distribution shape using numerical summaries and plots.

**GeeksforGeeks References:**
- [Measures of Central Tendency](https://www.geeksforgeeks.org/maths/measures-of-central-tendency/)
- [Variance and Standard Deviation](https://www.geeksforgeeks.org/maths/variance/)
- [Normal Distribution](https://www.geeksforgeeks.org/maths/normal-distribution/)
- [Z-Score](https://www.geeksforgeeks.org/maths/z-score/)
# Machine Learning – Daily Task Update
## Module 2: Mathematics and Statistics
## Day 6: Understanding Data with Descriptive Statistics

Before building a model, take time to understand the data it will learn from. Descriptive statistics give us a compact view of what is typical, how much values vary and whether a dataset contains unusual observations.

### 1. First, know which data you have
A **population** is the full group we want to understand. A **sample** is the subset we actually observe. If we want to understand the marks of every student in a college, all students form the population; a selected group forms a sample.

Data can also be described by its type:
- **Numerical:** values such as age, salary or temperature.
- **Categorical:** groups such as department, city or product type.
- **Discrete:** countable numerical values, such as number of visits.
- **Continuous:** measurements that can take values across a range, such as height.

The data type affects which summaries and charts make sense.

### 2. Describe the centre of a dataset
The **mean** is the arithmetic average: add the values and divide by the number of values.

\`\`\`python
values = [10, 12, 12, 14, 42]
mean_value = sum(values) / len(values)
print(mean_value)
\`\`\`

The **median** is the middle value after sorting the data. With an even number of observations, it is the average of the two middle values. The **mode** is the most frequently occurring value.

The mean is useful but can be pulled by unusually high or low observations. The median is often a better description of the centre when the distribution is strongly skewed. The mode is especially helpful for categorical data or repeated values.

### 3. Measure how spread out values are
Two datasets can have the same mean but very different levels of variation.

- **Range:** maximum minus minimum.
- **Variance:** average squared distance from the mean (the denominator depends on whether we describe a population or estimate from a sample).
- **Standard deviation:** square root of variance, expressed in the same units as the original data.
- **Interquartile range (IQR):** third quartile minus first quartile; it describes the spread of the middle half of the observations.

For a population, variance is commonly written as:

\[
\sigma^2 = \frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)^2
\]

Here, \(x_i\) is an observation, \(\mu\) is the population mean and \(N\) is the population size. Sample variance typically uses \(n-1\) in the denominator when estimating population variance from a sample.

### 4. Look at the shape, not just the average
A distribution describes how values are spread across possible outcomes.

- **Symmetric distribution:** the two sides have a similar shape.
- **Right-skewed distribution:** a longer tail extends toward larger values; income data often show this pattern.
- **Left-skewed distribution:** a longer tail extends toward smaller values.
- **Uniform distribution:** outcomes have roughly equal probability across a defined range.
- **Normal distribution:** a symmetric, bell-shaped distribution described by its mean and standard deviation.

Real data do not have to follow a normal distribution. Do not assume they do simply because a textbook example uses a bell curve.

### 5. Percentiles and possible outliers
A percentile indicates the point below which a given percentage of observations falls. The median is the 50th percentile; the first and third quartiles correspond to the 25th and 75th percentiles.

A common rule for flagging possible outliers uses the IQR:
- Lower fence: \(Q_1 - 1.5 \times IQR\)
- Upper fence: \(Q_3 + 1.5 \times IQR\)

Values beyond these fences are worth investigating, but they are not automatically errors. A large value may be genuine and important.

### 6. Calculate summaries with Python
\`\`\`python
import statistics

values = [10, 12, 12, 14, 42]

print("Mean:", statistics.mean(values))
print("Median:", statistics.median(values))
print("Population standard deviation:", statistics.pstdev(values))
print("Sample standard deviation:", statistics.stdev(values))
\`\`\`

For a real dataset, Pandas can provide a quick overview with \`df.describe()\`. NumPy also makes numerical calculations over arrays convenient.

### 7. Why these summaries matter for ML
Descriptive statistics can reveal inconsistent ranges, skewed variables, unexpected categories and possible data-entry errors. They help us choose useful visualizations and decide whether a transformation might be worth testing.

Statistics alone cannot tell us whether a feature is meaningful or whether one variable causes another. Use the summaries to form questions, then investigate the data and its context.

### Practice task
Use a small list of marks or salaries. Calculate the mean, median, range and standard deviation. Add one unusually large value and observe which summaries change the most. Explain why the mean and median tell different stories in that example.

**Practical objective:** Summarize a dataset's centre, spread and distribution shape, and recognize observations that deserve a closer look.

**GeeksforGeeks references**
- [Measures of Central Tendency](https://www.geeksforgeeks.org/maths/measures-of-central-tendency/)
- [Measures of Dispersion](https://www.geeksforgeeks.org/maths/measures-of-dispersion/)
- [Normal Distribution](https://www.geeksforgeeks.org/maths/normal-distribution/)
- [Statistics in Python](https://www.geeksforgeeks.org/python/statistics-functions-in-python/)
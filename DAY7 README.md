# Machine Learning – Daily Task Update
## Day 7: Probability, Bayes' Theorem and Hypothesis Testing

### 1. Basic Probability
Probability measures how likely an event is, from 0 (impossible) to 1 (certain).

For equally likely outcomes:

`P(A) = Number of outcomes in A / Total number of possible outcomes`

For a fair six-sided die, the probability of rolling a 4 is `1/6`.

**Complement rule:** `P(not A) = 1 − P(A)`.

**Addition rule:** `P(A ∪ B) = P(A) + P(B) − P(A ∩ B)`. If two events cannot happen together, their intersection probability is zero.

### 2. Independent and Dependent Events
Two events are **independent** if the occurrence of one does not change the probability of the other.

`P(A ∩ B) = P(A) × P(B)` for independent events.

Example: Two separate fair coin tosses are independent.

Events are **dependent** when one event changes the probability of another. Drawing two cards without replacement is a common example because the first draw changes the remaining deck.

### 3. Conditional Probability
Conditional probability measures the probability of event A given that event B has occurred.

`P(A | B) = P(A ∩ B) / P(B)`, provided `P(B) > 0`.

Example: If 30 of 100 students play football and 12 of those 30 also play basketball, then the probability that a student plays basketball given that they play football is `12/30 = 0.4`.

### 4. Bayes' Theorem
Bayes' theorem updates the probability of a hypothesis after observing evidence.

`P(A | B) = P(B | A) × P(A) / P(B)`

Where:
- `P(A)`: Prior probability of A.
- `P(B | A)`: Likelihood of observing B if A is true.
- `P(B)`: Overall probability of B.
- `P(A | B)`: Posterior probability of A after observing B.

**Example: medical screening (illustrative numbers):**
- 1% of a population has a condition.
- A test is positive for 90% of people with the condition.
- The test is falsely positive for 5% of people without the condition.

For a positive result:

`P(condition | positive) = (0.90 × 0.01) / ((0.90 × 0.01) + (0.05 × 0.99))`

This is approximately 15.4%, not 90%. The example shows why the base rate matters. These are illustrative values, not medical advice.

### 5. Random Variables and Probability Distributions
A **random variable** assigns a numerical value to an outcome of a random process.

- **Discrete random variable:** Takes countable values, such as the number of heads in three coin tosses.
- **Continuous random variable:** Can take any value within an interval, such as measured temperature.

A probability distribution describes the probabilities or density associated with possible values. Examples include Bernoulli, binomial, normal, and uniform distributions.

### 6. Sampling Distributions
A sampling distribution describes how a statistic, such as a sample mean, would vary across repeated samples from the same population.

The standard error measures the variability of a statistic across samples. For independent observations with finite variance, the standard error of the sample mean is commonly estimated as `s / √n`.

Larger samples often produce more stable estimates, but sample size does not automatically eliminate sampling bias or poor data quality.

### 7. Hypothesis Testing
Hypothesis testing uses sample data to assess a claim about a population.

- **Null hypothesis (H₀):** The default claim, often no difference or no effect.
- **Alternative hypothesis (H₁ or Hₐ):** The claim supported if the evidence is sufficiently inconsistent with H₀.
- **Significance level (α):** A threshold chosen before the test, often 0.05.
- **Test statistic:** A value calculated from sample data.
- **p-value:** Assuming the null hypothesis and the test assumptions are true, the probability of obtaining a test statistic at least as extreme as the observed one, according to the chosen test.

A p-value is not the probability that the null hypothesis is true, and it does not measure the size or practical importance of an effect.

### 8. Confidence Intervals
A confidence interval is a range produced by a method designed to cover the true population parameter at a specified long-run rate, such as 95%, when assumptions hold.

A 95% confidence procedure does not mean there is a 95% probability that a fixed parameter lies in this particular interval under the usual frequentist interpretation. The interval gives a range of values compatible with the data and method.

### 9. Type I and Type II Errors
- **Type I error:** Rejecting a true null hypothesis; its long-run probability is controlled by the significance level under the test assumptions.
- **Type II error:** Failing to reject a false null hypothesis.
- **Power:** Probability of rejecting the null when a specified alternative is true; power is `1 − β`, where β is the Type II error probability.

Reducing one error may increase the other unless sample size, design, or other factors change.

### 10. Correlation vs. Causation
**Correlation** measures association between variables. **Causation** means a change in one variable produces a change in another.

Two variables can be correlated because of coincidence, a common cause, reverse causality, or other factors. Correlation alone does not establish causation.

**Example:** Ice-cream sales and swimming incidents may both rise in hot weather. Temperature can influence both; buying ice cream does not necessarily cause swimming incidents.

### 11. Simulate Coin Tosses
```python
import random

trials = 10000
heads = 0

for _ in range(trials):
    if random.choice(["H", "T"]) == "H":
        heads += 1

print("Estimated probability of heads:", heads / trials)
```

The estimated proportion should usually be near 0.5 for a fair coin as the number of trials grows, but it will vary due to randomness.

### 12. Basic Hypothesis Test with SciPy
The following example compares the mean of one sample with a hypothetical reference mean. The data are illustrative.

```python
from scipy import stats

sample = [52, 49, 51, 53, 48, 50, 54, 52, 51, 49]
result = stats.ttest_1samp(sample, popmean=50)

print("t-statistic:", result.statistic)
print("p-value:", result.pvalue)
```

Interpret the p-value against a significance level selected in advance, and consider assumptions, effect size, confidence intervals, and the context. Do not treat statistical significance alone as proof of practical importance.

### 13. Correlation with Python
```python
from scipy.stats import pearsonr

study_hours = [1, 2, 3, 4, 5]
scores = [50, 55, 65, 70, 80]

correlation, p_value = pearsonr(study_hours, scores)
print("Pearson correlation:", correlation)
print("p-value:", p_value)
```

Pearson correlation measures linear association and is sensitive to outliers. A high correlation does not prove that study hours alone caused the scores.

### 14. Key Takeaways
- Probability quantifies uncertainty.
- Independence and dependence describe how events relate.
- Conditional probability and Bayes' theorem update probabilities using evidence.
- Sampling distributions describe the variability of statistics across samples.
- A p-value is interpreted under the null hypothesis and test assumptions.
- Type I and Type II errors are different risks.
- Correlation does not prove causation.

**Practical Objective:** Solve basic probability problems, apply Bayes' theorem, understand hypothesis testing terminology, and interpret correlation carefully.

**GeeksforGeeks References:**
- [Probability](https://www.geeksforgeeks.org/maths/probability/)
- [Bayes' Theorem](https://www.geeksforgeeks.org/maths/bayes-theorem/)
- [Hypothesis Testing](https://www.geeksforgeeks.org/maths/hypothesis-testing/)
- [Correlation](https://www.geeksforgeeks.org/maths/correlation/)
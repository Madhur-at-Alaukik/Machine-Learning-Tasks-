# Machine Learning – Daily Task Update
## Day 7: Probability, Bayes' Theorem and Hypothesis Testing

Statistics helps us describe data we have observed. Probability helps us reason about uncertain outcomes, while hypothesis testing gives us a structured way to assess whether data provides evidence against a claim. These ideas appear in ML evaluation, experimentation and decision-making.

### 1. Start with events and uncertainty
Probability measures how likely an event is, from 0 (impossible) to 1 (certain). For equally likely outcomes:

\[
P(A)=\frac{\text{number of outcomes in }A}{\text{number of possible outcomes}}
\]

For a fair six-sided die, the probability of rolling a 4 is \(1/6\). This calculation assumes each side is equally likely.

Useful relationships include:
- **Complement:** \(P(\text{not }A)=1-P(A)\).
- **Addition:** for mutually exclusive events, \(P(A\cup B)=P(A)+P(B)\).
- **Conditional probability:** \(P(A\mid B)=P(A\cap B)/P(B)\), when \(P(B)>0\).
- **Independence:** if A and B are independent, \(P(A\cap B)=P(A)P(B)\).

Events that are mutually exclusive cannot occur together; independent events do not change one another's probability. Those ideas are different, so do not use the terms interchangeably.

### 2. Conditional probability and Bayes' theorem
Conditional probability asks how likely an event is when we already know another event has occurred. Bayes' theorem reverses a conditional relationship:

\[
P(A\mid B)=\frac{P(B\mid A)P(A)}{P(B)}
\]

Imagine a screening test for a rare condition. Even if a test is fairly accurate, a positive result does not automatically mean that the person has the condition. The answer also depends on how common the condition is and on the test's false-positive rate. This is why base rates matter.

Bayes' theorem is useful for updating beliefs when new evidence arrives. It is a foundation for some probabilistic ML methods, but real applications require careful assumptions and reliable data.

### 3. Random variables and expected value
A random variable assigns a numerical value to an outcome. Its **expected value** is the long-run average we would expect over many repetitions under the assumed probability model.

For a discrete random variable:

\[
E[X]=\sum_x xP(X=x)
\]

A fair die has expected value \(3.5\), even though a single roll can never show 3.5. Expected value describes an average across repeated trials, not a guaranteed result for one trial.

### 4. From a question to a hypothesis test
Suppose a team claims that a new website layout increases the average number of completed sign-ups. A hypothesis test provides a framework for checking whether observed data is inconsistent with a baseline assumption.

- **Null hypothesis (\(H_0\)):** the default claim, often that there is no difference or effect.
- **Alternative hypothesis (\(H_1\)):** the competing claim being investigated.
- **Significance level (\(\alpha\)):** the threshold chosen in advance for rejecting the null hypothesis, often 0.05.
- **Test statistic:** a quantity calculated from the sample data.
- **p-value:** assuming the null hypothesis and test assumptions are true, the probability of observing a result at least as extreme as the one obtained.

A p-value is not the probability that the null hypothesis is true. A small p-value is evidence against the null under the test assumptions, but it does not tell us whether an effect is large or practically important.

### 5. Errors and interpretation
A **Type I error** occurs when we reject a true null hypothesis. A **Type II error** occurs when we fail to reject a false null hypothesis. Statistical power is the probability of detecting an effect of a specified size under the assumptions of the test.

Sample size, variability, the chosen significance level and the actual effect size all influence the result. Report effect sizes and confidence intervals where appropriate rather than relying only on whether a p-value is below a threshold.

### 6. Correlation is not the same as causation
Correlation measures how variables move together. Pearson's correlation coefficient, \(r\), ranges from -1 to +1 and describes the strength and direction of a linear relationship.

- Near +1: strong positive linear relationship.
- Near -1: strong negative linear relationship.
- Near 0: little linear relationship, though a nonlinear relationship may still exist.

Ice-cream sales and swimming activity may rise together in warm weather. That does not prove one causes the other; temperature may influence both. Correlation is useful for exploring data, but causal conclusions need stronger evidence and appropriate study design.

### Practice task
Work through a simple probability example: calculate the chance of rolling an even number on a fair die, then calculate the chance of rolling an even number twice in a row, assuming the rolls are independent. Finally, explain why a positive screening result depends on both test accuracy and the condition's prevalence.

**Practical objective:** Calculate basic probabilities, interpret Bayes' theorem and explain the meaning and limits of hypothesis tests and correlation.

**GeeksforGeeks references**
- [Probability](https://www.geeksforgeeks.org/maths/probability/)
- [Bayes' Theorem](https://www.geeksforgeeks.org/maths/bayes-theorem/)
- [Hypothesis Testing](https://www.geeksforgeeks.org/maths/hypothesis-testing/)
- [Correlation](https://www.geeksforgeeks.org/maths/correlation/)
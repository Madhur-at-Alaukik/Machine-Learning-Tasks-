# Machine Learning – Daily Task Update
## Day 8: Linear Algebra, Calculus and the Idea of Optimization

A machine-learning model often represents data as numbers, combines those numbers using mathematical operations and adjusts its parameters to reduce error. Linear algebra helps us represent and transform data; calculus helps us understand how a quantity changes; optimization uses that information to improve a model.

### 1. Represent data with scalars, vectors and matrices
A **scalar** is a single number, such as 5. A **vector** is an ordered collection of numbers, and a **matrix** is a two-dimensional arrangement of values.

\[
x=\begin{bmatrix}2\\3\\4\end{bmatrix},\qquad
A=\begin{bmatrix}1&2\\3&4\end{bmatrix}
\]

In ML, a row of a dataset may be represented as a feature vector, while an entire dataset can be represented as a matrix. Each column might correspond to a feature such as age, income or number of visits.

### 2. The operations that show up often
**Addition:** vectors or matrices of compatible shapes can be added element by element.

**Scalar multiplication:** multiply every element by the same number.

**Dot product:** multiply corresponding vector entries and add the results.

\[
a\cdot b=\sum_i a_i b_i
\]

For example, if feature values are \([2,3]\) and weights are \([0.5,4]\), their dot product is \(2(0.5)+3(4)=13\). A simple linear model combines features and weights this way, then may add a bias term.

**Matrix multiplication:** combines rows of the first matrix with columns of the second. The inner dimensions must match. If A has shape \(m\times n\) and B has shape \(n\times p\), the product has shape \(m\times p\).

Dimensions matter: many numerical bugs come from multiplying arrays with incompatible shapes.

### 3. Why weights matter in a model
A basic linear prediction can be written as:

\[
\hat{y}=w_1x_1+w_2x_2+\cdots+w_nx_n+b
\]

The \(x\) values are input features, the \(w\) values are learned weights, \(b\) is a bias term and \(\hat{y}\) is the prediction. Training tries to find parameter values that make predictions useful for the task.

Weights do not automatically reveal causal importance, and their interpretation can depend on feature scaling and relationships between variables. Still, this equation connects data tables to models.

### 4. A first look at derivatives
A derivative measures how quickly a function changes as its input changes. For example, if \(f(x)=x^2\), then \(f'(x)=2x\). At \(x=3\), the slope is 6.

A **partial derivative** measures how a function changes with respect to one variable while treating other variables as fixed. This matters when a loss function depends on many model parameters.

The **gradient** collects these partial derivatives into a vector. It points in the direction of steepest local increase for a differentiable function. To reduce a loss, gradient-based methods move in the opposite direction.

### 5. Gradient descent: improve a model step by step
Imagine a loss function that measures the gap between predictions and actual answers. Gradient descent repeatedly adjusts parameters in a direction expected to reduce this loss.

\[
\theta_{\text{new}}=\theta_{\text{old}}-\eta\nabla J(\theta)
\]

Here, \(\theta\) represents the parameters, \(J(\theta)\) is the loss and \(\eta\) is the learning rate.

- If the learning rate is too small, training may be slow.
- If it is too large, updates may jump past a good solution or fail to settle.
- The loss surface may have flat regions or other challenges, so optimization is not guaranteed to find a global minimum in every problem.

This is the core idea behind many training procedures, although practical algorithms may use batches, momentum or other improvements.

### 6. One numerical step
For \(f(x)=x^2\), the derivative is \(2x\). Starting at \(x=4\) with learning rate \(\eta=0.1\), one gradient-descent step gives:

\[
x_{\text{new}}=4-0.1(2\times4)=3.2
\]

The function value falls from \(16\) to \(10.24\). This small example shows how a gradient can guide an update.

### Practice task
1. Calculate the dot product of \([1,2,3]\) and \([4,5,6]\).
2. Check the shapes of a \(2\times3\) matrix multiplied by a \(3\times2\) matrix.
3. Differentiate \(f(x)=3x^2+2x\).
4. Perform one gradient-descent step on \(f(x)=x^2\) from \(x=2\) using learning rate 0.1.
5. Explain what the learning rate controls.

**Practical objective:** Understand the numerical structures used to represent features and weights, and describe how gradients can guide model training.

**GeeksforGeeks references**
- [Linear Algebra](https://www.geeksforgeeks.org/maths/linear-algebra/)
- [Matrix Multiplication](https://www.geeksforgeeks.org/maths/matrix-multiplication/)
- [Derivatives](https://www.geeksforgeeks.org/maths/derivatives/)
- [Gradient Descent](https://www.geeksforgeeks.org/machine-learning/gradient-descent-in-machine-learning/)
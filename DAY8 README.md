# Machine Learning – Daily Task Update
## Day 8: Linear Algebra, Calculus and Optimization

### 1. Scalars, Vectors and Matrices
A **scalar** is a single number, such as `5`.

A **vector** is an ordered collection of numbers, such as `[2, 4, 6]`. It can represent features for one observation or parameters in a mathematical model.

A **matrix** is a rectangular arrangement of numbers in rows and columns. A matrix with `m` rows and `n` columns has shape `(m, n)`.

In ML, a feature matrix often stores observations in rows and features in columns, though conventions depend on the library and model.

### 2. Vector Operations
Vectors can be added or subtracted when they have compatible dimensions. Scalar multiplication multiplies every component by the same number.

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(a + b)   # [5 7 9]
print(a * 2)   # [2 4 6]
```

### 3. Dot Product
The dot product multiplies corresponding components and adds the results.

`a · b = Σ aᵢbᵢ`

For `[1, 2, 3]` and `[4, 5, 6]`, the dot product is `1×4 + 2×5 + 3×6 = 32`.

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
print(np.dot(a, b))  # 32
```

Dot products are central to linear models because predictions often combine features and learned weights.

### 4. Matrix Multiplication and Transpose
Matrix multiplication is possible when the number of columns in the first matrix equals the number of rows in the second. If A has shape `(m, n)` and B has shape `(n, p)`, then `A @ B` has shape `(m, p)`.

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print(A @ B)
print(A.T)
```

`A.T` is the transpose, which swaps rows and columns. In NumPy, `*` performs element-wise multiplication for arrays; `@` performs matrix multiplication.

### 5. Vector Norms and Distance
A norm measures the magnitude of a vector. The Euclidean (L2) norm is:

`||x||₂ = √(Σ xᵢ²)`

The Euclidean distance between vectors `x` and `y` is `||x − y||₂`.

```python
x = np.array([3, 4])
y = np.array([0, 0])

print(np.linalg.norm(x))       # 5.0
print(np.linalg.norm(x - y))   # 5.0
```

Distance measures are used in clustering, nearest-neighbor methods, and other algorithms. Features on very different scales can dominate distance calculations, so scaling may be important.

### 6. Functions and Derivatives
A function maps input values to output values. A derivative measures the instantaneous rate of change of a function with respect to its input.

For `f(x) = x²`, the derivative is `f'(x) = 2x`. At `x = 3`, the derivative is 6.

The derivative's sign indicates local direction:
- Positive derivative: function increases locally.
- Negative derivative: function decreases locally.
- Zero derivative: a stationary point, which may be a minimum, maximum, or another type of point.

### 7. Partial Derivatives and Gradients
When a function depends on multiple variables, a partial derivative measures change with respect to one variable while holding the others fixed.

The **gradient** is the vector of partial derivatives. It points in the direction of steepest local increase for a differentiable function under the usual Euclidean geometry.

For a loss function `L(w₁, w₂)`, the gradient is:

`∇L = [∂L/∂w₁, ∂L/∂w₂]`

Optimization algorithms use gradient information to adjust model parameters.

### 8. Loss Functions
A loss function measures how far a model's prediction is from the desired outcome, according to a chosen measure.

Examples:
- **Mean Squared Error (MSE):** Average squared difference between numerical predictions and targets.
- **Mean Absolute Error (MAE):** Average absolute difference.
- **Cross-entropy loss:** Commonly used for classification models that produce probabilities.

A loss function defines what the optimization procedure attempts to minimize. It is not always the same as the final evaluation metric.

### 9. Gradient Descent
Gradient descent is an optimization algorithm that updates parameters in the direction opposite to the gradient to reduce the loss.

`w_new = w_old − η × ∇L(w_old)`

Here, `η` is the learning rate.

**Basic steps:**
1. Initialize parameters.
2. Calculate the loss.
3. Calculate the gradient.
4. Update parameters in the negative gradient direction.
5. Repeat until a stopping condition is reached.

A learning rate that is too small can make learning slow. A rate that is too large may overshoot a minimum or cause divergence.

### 10. Simple Gradient Descent Example
Minimize `f(w) = (w − 3)²`. Its derivative is `2(w − 3)`, and the minimum is at `w = 3`.

```python
w = 0.0
learning_rate = 0.1

for step in range(20):
    gradient = 2 * (w - 3)
    w = w - learning_rate * gradient

print("Estimated minimum:", w)
print("Final loss:", (w - 3) ** 2)
```

The value of `w` should move toward 3. With this learning rate, it approaches the minimum gradually.

### 11. Effect of Learning Rate
- **Very small rate:** Stable but slow progress.
- **Suitable rate:** Progresses toward a useful minimum.
- **Very large rate:** May jump across the minimum and fail to converge.

The suitable learning rate depends on the loss surface, parameter scale, and optimization method.

### 12. Practical Exercises
1. Create vectors and matrices using NumPy.
2. Calculate dot products and Euclidean distances.
3. Perform matrix multiplication and transpose operations.
4. Plot `f(x) = (x − 3)²`.
5. Implement gradient descent for this function with different learning rates.
6. Compare the final parameter and loss for each learning rate.

### 13. Key Takeaways
- Scalars, vectors, and matrices represent numbers and structured numerical data.
- Dot products combine corresponding vector values and are common in linear models.
- Matrix dimensions determine whether matrix multiplication is valid.
- Derivatives and gradients describe how a function changes.
- Loss functions quantify prediction errors.
- Gradient descent updates parameters to reduce loss, and learning-rate choice matters.

**Practical Objective:** Perform basic linear algebra operations and explain how gradients, loss functions, and gradient descent support ML model training.

**GeeksforGeeks References:**
- [Matrix Operations](https://www.geeksforgeeks.org/maths/matrix/)
- [Dot Product](https://www.geeksforgeeks.org/maths/dot-product/)
- [Gradient Descent](https://www.geeksforgeeks.org/machine-learning/gradient-descent-in-linear-regression/)
- [Derivatives](https://www.geeksforgeeks.org/maths/derivatives/)
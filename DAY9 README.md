# Machine Learning – Daily Task Update
## Module 3: Data Analysis and Feature Engineering
## Day 9: NumPy Fundamentals

### 1. What Is NumPy?
NumPy (Numerical Python) is a Python library for efficient numerical computing. Its central data structure is the multidimensional `ndarray`, which stores elements in a regular array structure and supports vectorized operations, aggregation, and linear algebra.

Install NumPy if required:

```bash
python -m pip install numpy
```

Import it using the common alias:

```python
import numpy as np
```

### 2. Python Lists vs. NumPy Arrays
Python lists can hold objects of different types. NumPy arrays are generally designed for efficient operations on homogeneous numerical data and offer vectorized computations.

```python
numbers = [1, 2, 3]
array = np.array([1, 2, 3])

print(numbers * 2)  # [1, 2, 3, 1, 2, 3]
print(array * 2)    # [2 4 6]
```

Multiplying a list by 2 repeats its elements; multiplying a numeric NumPy array by 2 scales each element.

### 3. Creating Arrays
```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([[1, 2, 3], [4, 5, 6]])

print(a)
print(b)
print(np.zeros((2, 3)))
print(np.ones((2, 2)))
print(np.arange(0, 10, 2))
print(np.linspace(0, 1, 5))
```

- `array()` converts input data to an array.
- `zeros()` creates an array filled with zeros.
- `ones()` creates an array filled with ones.
- `arange()` creates values with a specified step.
- `linspace()` creates a specified number of evenly spaced values between endpoints.

### 4. Dimensions, Shape, Size and Data Type
- `ndim`: Number of dimensions.
- `shape`: Length of each dimension.
- `size`: Total number of elements.
- `dtype`: Element data type.

```python
a = np.array([[1, 2, 3], [4, 5, 6]])

print(a.ndim)   # 2
print(a.shape)  # (2, 3)
print(a.size)   # 6
print(a.dtype)
```

The shape `(2, 3)` means two rows and three columns.

### 5. Indexing and Slicing
NumPy uses zero-based indexing. For a two-dimensional array, use one index per dimension.

```python
a = np.array([[10, 20, 30], [40, 50, 60]])

print(a[0, 1])   # 20
print(a[1, :])   # [40 50 60]
print(a[:, 0])   # [10 40]
print(a[:, 1:3])
```

Basic slices often produce views that share memory with the original array. Changing a view can therefore change the original array. Use `.copy()` when an independent copy is required.

### 6. Reshaping Arrays
`reshape()` changes the shape without changing the element count. The new shape must contain the same total number of elements.

```python
a = np.arange(1, 7)
matrix = a.reshape(2, 3)

print(matrix)
print(matrix.reshape(3, 2))
```

Using `reshape(-1, 1)` or `reshape(1, -1)` lets NumPy infer one dimension from the element count.

### 7. Vectorization
Vectorization applies operations to whole arrays without writing an explicit Python loop for each element.

```python
values = np.array([10, 20, 30, 40])
discounted = values * 0.9
print(discounted)
```

Vectorized operations are often faster and more concise than Python loops because numerical work can run in optimized compiled code.

### 8. Broadcasting
Broadcasting allows NumPy to perform operations on arrays with compatible shapes without manually copying smaller arrays.

For each dimension, sizes must either be equal or one of them must be 1; dimensions are compared from the right.

```python
matrix = np.array([[1, 2, 3], [4, 5, 6]])
row = np.array([10, 20, 30])

print(matrix + row)
```

The row vector is broadcast across both rows. Incompatible shapes raise an error.

### 9. Aggregation Functions
NumPy provides functions for summaries and reductions:
- `np.sum()`: Sum.
- `np.mean()`: Mean.
- `np.median()`: Median.
- `np.min()` and `np.max()`: Minimum and maximum.
- `np.std()` and `np.var()`: Standard deviation and variance.
- `np.sum(array, axis=0)`: Reduce across rows, returning column totals.
- `np.sum(array, axis=1)`: Reduce across columns, returning row totals.

```python
data = np.array([[10, 20, 30], [40, 50, 60]])

print(np.mean(data))
print(np.sum(data, axis=0))  # Column totals
print(np.sum(data, axis=1))  # Row totals
```

By default, NumPy's variance and standard deviation functions use population normalization (`ddof=0`). Set `ddof=1` for the common sample estimate when appropriate.

### 10. Random Number Generation
NumPy provides random sampling for simulations, test data, and reproducible experiments.

```python
rng = np.random.default_rng(42)

print(rng.integers(1, 7, size=5))
print(rng.random(3))
print(rng.normal(loc=0, scale=1, size=4))
```

A fixed seed makes results reproducible for the same generator and compatible environment. Random data generated this way is useful for learning, not for security-sensitive randomness.

### 11. Basic Linear Algebra
```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print(A + B)       # Element-wise addition
print(A @ B)       # Matrix multiplication
print(A.T)         # Transpose
print(np.linalg.det(A))
print(np.linalg.norm(np.array([3, 4])))
```

The `numpy.linalg` module provides linear algebra operations, including determinants, norms, solving linear systems, and decompositions.

### 12. Practical Exercises
1. Create 1D, 2D, and 3D arrays and inspect their shapes.
2. Select specific rows, columns, and slices.
3. Reshape a one-dimensional array into a matrix.
4. Compare a loop-based calculation with a vectorized calculation.
5. Demonstrate broadcasting between a matrix and a row vector.
6. Calculate mean, standard deviation, and totals along each axis.
7. Perform matrix multiplication and calculate vector distance.

### 13. Key Takeaways
- NumPy provides efficient multidimensional numerical arrays.
- `shape`, `ndim`, `size`, and `dtype` describe array structure.
- Indexing and slicing select array elements; slices may share memory.
- Reshaping changes dimensions without changing the element count.
- Vectorization and broadcasting simplify numerical operations.
- Aggregation functions summarize data, and `numpy.linalg` supports linear algebra.

**Practical Objective:** Create, inspect, transform, summarize, and calculate with NumPy arrays, preparing for data manipulation and ML algorithms.

**GeeksforGeeks References:**
- [NumPy Tutorial](https://www.geeksforgeeks.org/python/numpy-tutorial/)
- [NumPy Array](https://www.geeksforgeeks.org/python/numpy-ndarray/)
- [NumPy Broadcasting](https://www.geeksforgeeks.org/python/numpy-broadcasting/)
- [NumPy Random](https://www.geeksforgeeks.org/python/numpy-random/)
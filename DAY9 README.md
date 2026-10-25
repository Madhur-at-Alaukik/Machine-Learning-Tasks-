# Machine Learning – Daily Task Update
## Module 3: Data Analysis and Feature Engineering
## Day 9: NumPy — Working with Numerical Data

Python lists are fine for learning, but data analysis often requires calculations over many numerical values. NumPy provides efficient arrays and mathematical operations that make this work easier. It also underpins many scientific Python libraries.

### 1. Create your first array
Install NumPy if needed, then import it using the conventional alias \`np\`.

\`\`\`bash
python -m pip install numpy
\`\`\`

\`\`\`python
import numpy as np

marks = np.array([78, 85, 91, 67])
print(marks)
print(type(marks))
print(marks.shape)
print(marks.dtype)
\`\`\`

A NumPy array stores values in a structured, usually homogeneous data type. The \`shape\` tells you its dimensions, while \`dtype\` tells you the element type. These details matter when preparing arrays for ML libraries.

### 2. Build arrays in different shapes
\`\`\`python
zeros = np.zeros((2, 3))
ones = np.ones((2, 2))
sequence = np.arange(0, 10, 2)
evenly_spaced = np.linspace(0, 1, 5)

print(zeros)
print(ones)
print(sequence)       # [0 2 4 6 8]
print(evenly_spaced)  # Five values from 0 to 1
\`\`\`

- \`zeros()\` and \`ones()\` create arrays filled with a constant.
- \`arange()\` creates values using a step size, excluding the stop value.
- \`linspace()\` creates a specified number of evenly spaced values across an interval, including endpoints by default.

### 3. Let arrays handle repeated calculations
NumPy supports vectorized operations: apply an operation to an entire array without writing an explicit Python loop.

\`\`\`python
marks = np.array([60, 70, 80, 90])
adjusted = marks + 5
percentage = marks / 100

print(adjusted)
print(percentage)
print(np.mean(marks))
print(np.max(marks))
print(np.std(marks))
\`\`\`

The original array is not changed by \`marks + 5\`; the expression creates a result. NumPy also provides \`sum\`, \`min\`, \`median\`, \`var\` and \`std\`.

### 4. Select the values you need
Indexing accesses an individual element; slicing selects a range. In a two-dimensional array, use a comma to separate row and column selection.

\`\`\`python
data = np.array([
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
])

print(data[0, 1])   # 20
print(data[1])      # Second row
print(data[:, 0])   # First column
print(data[:2, 1:]) # First two rows, columns 2 onward
\`\`\`

NumPy slices often create **views** into the original array rather than independent copies. Changing a view can therefore change the original data. Use \`.copy()\` when you need a separate array.

### 5. Filter using conditions
Boolean indexing selects values that meet a condition.

\`\`\`python
marks = np.array([35, 72, 41, 28, 90])
passed = marks[marks >= 40]
print(passed)  # [72 41 90]
\`\`\`

Combine conditions with \`&\` and \`|\`, putting each condition in parentheses:

\`\`\`python
selected = marks[(marks >= 40) & (marks < 80)]
print(selected)
\`\`\`

This is useful for selecting records that meet multiple criteria before further analysis.

### 6. Understand dimensions and reshaping
The number of dimensions is available through \`ndim\`, and the number of elements through \`size\`.

\`\`\`python
values = np.arange(12)
matrix = values.reshape(3, 4)

print(matrix.shape)  # (3, 4)
print(matrix.ndim)   # 2
print(matrix.size)   # 12
\`\`\`

A reshape must preserve the total number of elements. An array of 12 values can become a 3-by-4 matrix, but not a 5-by-3 matrix.

### 7. Broadcasting and matrix operations
Broadcasting lets NumPy perform operations on compatible shapes without manually repeating every value. Adding a scalar to a matrix, for example, adds it to every element. More complex shapes are compatible when their dimensions match or one of them is 1, comparing from the right.

For linear algebra, \`@\` performs matrix multiplication:

\`\`\`python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
print(A @ B)
\`\`\`

Do not confuse \`A * B\`, which multiplies corresponding elements, with \`A @ B\`, which performs matrix multiplication.

### Practice task
Create an array of marks for ten students. Calculate the mean and standard deviation, select the marks above the mean and reshape the values into a suitable matrix. Check the shape and data type at each step.

**Practical objective:** Create, inspect, slice, filter and transform NumPy arrays, and understand the difference between element-wise operations and matrix multiplication.

**GeeksforGeeks references**
- [NumPy Tutorial](https://www.geeksforgeeks.org/python/numpy-tutorial/)
- [NumPy Array](https://www.geeksforgeeks.org/python/numpy-ndarray/)
- [NumPy Indexing and Slicing](https://www.geeksforgeeks.org/python/numpy-indexing/)
- [NumPy Broadcasting](https://www.geeksforgeeks.org/python/numpy-broadcasting/)
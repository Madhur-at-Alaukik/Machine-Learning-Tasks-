# Machine Learning – Daily Task Update
## Day 4: Python Collections and Functions

### 1. What Are Collections?
Collections store multiple values in a single object. Python's main built-in collection types are lists, tuples, sets, and dictionaries. They differ in ordering, mutability, and how values are accessed.

### 2. Lists
A list is an ordered, mutable collection that allows duplicate values.

```python
marks = [75, 82, 91, 82]
print(marks[0])   # 75
marks.append(88)
marks[1] = 85
print(marks)
```

Indexes start at 0. Negative indexing starts from the end, so `marks[-1]` accesses the final item. Lists support methods such as `append()`, `remove()`, `sort()`, and `pop()`.

### 3. Tuples
A tuple is an ordered collection that cannot be reassigned item by item after creation.

```python
coordinates = (10, 20)
print(coordinates[0])
```

Tuples are useful for fixed groups of values. A tuple can contain a mutable object, so immutability of a tuple does not automatically make every object inside it immutable.

### 4. Sets
A set stores unique elements and is useful for membership checks and set operations. Sets do not support positional indexing.

```python
numbers = {1, 2, 2, 3}
print(numbers)       # {1, 2, 3}
print(2 in numbers)  # True

a = {1, 2, 3}
b = {3, 4, 5}
print(a | b)  # Union
print(a & b)  # Intersection
print(a - b)  # Difference
```

Set display order should not be relied upon. Elements must be hashable.

### 5. Dictionaries
A dictionary stores key-value pairs. Keys are unique and must be hashable.

```python
student = {
    "name": "Asha",
    "age": 21,
    "marks": 88
}

print(student["name"])
student["marks"] = 92
student["city"] = "Indore"
print(student.get("grade", "Not assigned"))
```

Use `get()` when a key may not exist and you want a default value rather than a `KeyError`.

### 6. Collection Comparison

| Collection | Ordered | Mutable | Duplicates | Access |
|---|---|---|---|---|
| List | Yes | Yes | Allowed | Index |
| Tuple | Yes | No (structure) | Allowed | Index |
| Set | No positional order | Yes | Not stored as duplicates | Membership |
| Dictionary | Insertion order | Yes | Keys unique | Key |

### 7. Indexing and Slicing
Indexing selects one item. Slicing selects a range using `sequence[start:stop:step]`; the stop index is excluded.

```python
values = [10, 20, 30, 40, 50]
print(values[1])     # 20
print(values[1:4])   # [20, 30, 40]
print(values[:3])    # [10, 20, 30]
print(values[::2])   # [10, 30, 50]
print(values[::-1])  # reversed copy
```

### 8. Mutable vs. Immutable Objects
Mutable objects can be changed after creation; lists, sets, and dictionaries are common examples. Immutable objects cannot be changed in place; integers, floats, strings, and tuples (as containers) are common examples.

```python
first = [1, 2]
second = first
second.append(3)
print(first)  # [1, 2, 3]
```

Both variables refer to the same list. If an independent shallow copy is needed, use `first.copy()` or `first[:]` for a list.

### 9. Functions
A function is a reusable block of code that performs a task. Define it using `def`. Parameters receive input values; `return` sends a result back to the caller.

```python
def calculate_average(numbers):
    if not numbers:
        return None
    return sum(numbers) / len(numbers)

print(calculate_average([70, 80, 90]))  # 80.0
```

A function that reaches the end without a `return` statement returns `None`.

### 10. Parameters and Arguments
- **Parameter:** A name in the function definition.
- **Argument:** The actual value passed when calling the function.
- **Default argument:** A parameter value used when no argument is supplied.
- **Keyword argument:** An argument passed by parameter name.

```python
def greet(name, message="Welcome"):
    return f"{message}, {name}!"

print(greet("Riya"))
print(greet(name="Aman", message="Hello"))
```

Avoid mutable default values such as `items=[]` unless you deliberately want shared state between calls.

### 11. Lambda, `map()`, and `filter()`
A lambda is a small anonymous function expression, commonly used for simple operations.

```python
square = lambda x: x * x
print(square(5))  # 25
```

`map()` applies a function to each item; `filter()` retains items that satisfy a condition. In Python 3, both return iterators.

```python
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x * x, numbers))
evens = list(filter(lambda x: x % 2 == 0, numbers))

print(squares)  # [1, 4, 9, 16, 25]
print(evens)    # [2, 4]
```

List comprehensions are often easier to read for these simple cases.

### 12. Comprehensions
A comprehension creates a collection from an iterable, optionally filtering or transforming items.

```python
numbers = [1, 2, 3, 4, 5]
squares = [n * n for n in numbers]
evens = [n for n in numbers if n % 2 == 0]
unique_lengths = {len(word) for word in ["cat", "dog", "apple"]}
```

Dictionary comprehensions can create key-value mappings:

```python
squares_by_number = {n: n * n for n in range(1, 5)}
```

### 13. Recursion
Recursion occurs when a function calls itself to solve a smaller version of a problem. A recursive solution needs a base case to stop the calls.

```python
def factorial(n):
    if n < 0:
        raise ValueError("n must be non-negative")
    if n <= 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # 120
```

Deep recursion can hit Python's recursion limit; an iterative solution is often more appropriate for large inputs.

### 14. Practical Exercises
1. Find the minimum and maximum values in a list.
2. Remove duplicates while preserving the original order.
3. Count each word's frequency using a dictionary.
4. Write reusable functions for mean, minimum, and maximum.
5. Check whether a word is a palindrome.
6. Implement factorial using both iteration and recursion.
7. Use a comprehension to select even numbers and square them.

**Example: remove duplicates while preserving order**

```python
values = [3, 1, 3, 2, 1, 4]
unique_values = list(dict.fromkeys(values))
print(unique_values)  # [3, 1, 2, 4]
```

### 15. Key Takeaways
- Lists, tuples, sets, and dictionaries have different use cases.
- Indexing starts at zero; slicing excludes the stop index.
- Mutable objects can change in place, which affects references.
- Functions support reuse and organization; `return` provides a result.
- Lambda, `map()`, `filter()`, and comprehensions support concise transformations.
- Recursion needs a base case.

**Practical Objective:** Select the right collection, manipulate data safely, and write reusable functions for common operations.

**GeeksforGeeks References:**
- [Python Data Structures](https://www.geeksforgeeks.org/python/python-data-structures/)
- [Python Functions](https://www.geeksforgeeks.org/python/python-functions/)
- [Python Lambda](https://www.geeksforgeeks.org/python/python-lambda/)
- [Python List Comprehension](https://www.geeksforgeeks.org/python/python-list-comprehension/)
- [Recursion in Python](https://www.geeksforgeeks.org/python/recursion-in-python/)
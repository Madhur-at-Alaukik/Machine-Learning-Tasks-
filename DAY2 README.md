# Machine Learning – Daily Task Update
## Day 2: Python Variables, Data Types and Operators

### 1. Python Syntax, Indentation and Comments
Python syntax is the set of rules used to write valid Python code. Python uses indentation (spaces at the beginning of a line) to define blocks of code, such as the body of a function or conditional statement.

```python
# This is a single-line comment
marks = 80

if marks >= 40:
    print("Pass")
```

The indented `print()` line belongs to the `if` block. Inconsistent indentation can cause an `IndentationError`.

Comments begin with `#` and help explain code. Python ignores comments during normal execution.

### 2. Variables
A variable is a name that refers to a value or object. Variables let us store and reuse information.

```python
student_name = "Aarav"
age = 21
percentage = 82.5
is_enrolled = True
```

**Naming rules:**
- Names can contain letters, digits, and underscores.
- A name cannot begin with a digit.
- Names are case-sensitive: `marks` and `Marks` are different.
- Python keywords such as `if`, `for`, and `class` cannot be used as variable names.
- Use meaningful `snake_case` names, such as `total_marks`.

Python is dynamically typed, meaning the type is associated with the value and a variable can later refer to a value of another type.

### 3. Basic Python Data Types
**Integer (`int`):** Whole numbers, such as `10`, `-4`, and `0`.

**Floating-point (`float`):** Numbers with a fractional part, such as `3.14` or `-0.5`.

**String (`str`):** Text enclosed in single or double quotes, such as `"Python"`.

**Boolean (`bool`):** Logical values `True` and `False`.

```python
age = 21
height = 1.72
name = "Riya"
is_student = True

print(type(age))
print(type(height))
print(type(name))
print(type(is_student))
```

`type()` reports the type of an object. In ML work, correct data types matter because calculations and transformations depend on them.

### 4. Type Conversion
Type conversion changes a value from one type to another when the conversion is valid.

```python
age_text = "21"
age_number = int(age_text)

price_text = "149.50"
price = float(price_text)

marks = 85
marks_text = str(marks)

print(age_number + 1)  # 22
print(price)           # 149.5
print(marks_text)      # 85
```

`int()`, `float()`, `str()`, and `bool()` are common conversion functions. Invalid conversions can raise errors; for example, `int("hello")` raises a `ValueError`.

**Important:** `input()` returns text (`str`). Convert it when numerical operations are required.

### 5. Input and Output
`input()` reads text from the user. `print()` displays information.

```python
name = input("Enter your name: ")
age = int(input("Enter your age: "))

print("Name:", name)
print("Next year, you will be", age + 1)
```

If the user enters `20`, the age is converted to the integer `20` before addition.

### 6. Arithmetic Operators
Arithmetic operators perform mathematical calculations.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `+` | Addition | `8 + 3` | `11` |
| `-` | Subtraction | `8 - 3` | `5` |
| `*` | Multiplication | `8 * 3` | `24` |
| `/` | Division | `8 / 3` | `2.666...` |
| `//` | Floor division | `8 // 3` | `2` |
| `%` | Remainder | `8 % 3` | `2` |
| `**` | Exponentiation | `2 ** 3` | `8` |

Division by zero raises `ZeroDivisionError`. Floor division rounds down to the next integer when both operands are integers; for negative values, “down” means toward negative infinity.

### 7. Comparison Operators
Comparison operators compare values and return a Boolean result.

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

```python
marks = 75
print(marks >= 40)  # True
print(marks == 100) # False
```

**`=` vs. `==`:** `=` assigns a value to a variable; `==` checks whether two values are equal.

### 8. Logical Operators
Logical operators combine or reverse Boolean expressions.
- `and`: True when both conditions are true.
- `or`: True when at least one condition is true.
- `not`: Reverses a Boolean result.

```python
age = 22
has_id = True

print(age >= 18 and has_id)  # True
print(age < 18 or has_id)    # True
print(not has_id)            # False
```

### 9. Assignment Operators
Assignment operators store or update values.

```python
count = 10
count += 2   # count = count + 2
count -= 1
count *= 3
print(count)  # 33
```

Other augmented operators include `/=`, `//=`, `%=`, and `**=`.

### 10. Operator Precedence
Python follows precedence rules to decide which operations happen first. Parentheses can make the intended order clearer.

```python
result1 = 2 + 3 * 4       # 14
result2 = (2 + 3) * 4     # 20
```

Multiplication is performed before addition in the first expression. Use parentheses when they improve readability.

### 11. F-Strings
F-strings insert values or expressions directly into a string using curly braces.

```python
name = "Aarav"
marks = 87.456

print(f"{name} scored {marks:.2f}%")
```

Output:

```text
Aarav scored 87.46%
```

The format specifier `.2f` displays two digits after the decimal point.

### 12. Practical Programs
**A. Percentage calculator**

```python
obtained = float(input("Enter marks obtained: "))
maximum = float(input("Enter maximum marks: "))

if maximum > 0:
    percentage = obtained / maximum * 100
    print(f"Percentage: {percentage:.2f}%")
else:
    print("Maximum marks must be greater than zero.")
```

**B. Simple-interest calculator**

```python
principal = float(input("Principal amount: "))
rate = float(input("Annual rate (%): "))
time = float(input("Time in years: "))

simple_interest = principal * rate * time / 100
print(f"Simple interest: {simple_interest:.2f}")
```

**C. Celsius to Fahrenheit**

```python
celsius = float(input("Temperature in Celsius: "))
fahrenheit = (celsius * 9 / 5) + 32
print(f"Temperature in Fahrenheit: {fahrenheit:.2f}")
```

### 13. Key Takeaways
- Variables store references to values, and meaningful names improve readability.
- Common basic types include `int`, `float`, `str`, and `bool`.
- `input()` returns a string, so convert user input before numeric calculations.
- `=` assigns a value, while `==` compares values.
- Arithmetic, comparison, logical, and assignment operators support calculations and decision-making.
- F-strings make output formatting readable.

**Practical Objective:** Write small Python programs that accept input, convert types, perform calculations, compare values, and display formatted results.

**GeeksforGeeks References:**
- [Python Variables](https://www.geeksforgeeks.org/python/python-variables/)
- [Python Data Types](https://www.geeksforgeeks.org/python/python-data-types/)
- [Python Operators](https://www.geeksforgeeks.org/python/python-operators/)
- [Python Input and Output](https://www.geeksforgeeks.org/python/taking-input-in-python/)
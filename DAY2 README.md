# Machine Learning – Daily Task Update
## Day 2: Python Basics — Values, Variables and Expressions

Before working with datasets, we need to be comfortable storing information, changing it and checking the results. Today's examples use small values, but the same ideas later help us work with thousands of rows of data.

### 1. Write a small Python program
Python code is usually read from top to bottom. Indentation is meaningful: it shows which statements belong together, especially inside conditions, loops and functions. Use consistent four-space indentation.

\`\`\`python
# A comment explains the code to a reader.
name = "Asha"
marks = 86
print(f"{name} scored {marks} marks.")
\`\`\`

A comment begins with \`#\`. Comments are most useful when they explain intent or a non-obvious decision rather than repeat every line in English.

### 2. Variables are names for values
A variable gives a value a useful name so we can reuse it.

\`\`\`python
student_name = "Ravi"
age = 20
attendance = 0.92
is_enrolled = True
print(student_name, age, attendance, is_enrolled)
\`\`\`

Python infers the type from the assigned value. Variable names are case-sensitive, cannot begin with a digit and should describe what the value represents. \`total_marks\` is usually clearer than \`tm\`.

### 3. Meet the basic data types
| Type | What it represents | Example |
|---|---|---|
| \`int\` | Whole numbers | \`42\` |
| \`float\` | Numbers with a decimal part | \`3.14\` |
| \`str\` | Text | \`"Machine Learning"\` |
| \`bool\` | True/false values | \`True\` |
| \`NoneType\` | Absence of a value | \`None\` |

Check a value's type with \`type()\`:

\`\`\`python
price = 99.5
print(type(price))  # <class 'float'>
\`\`\`

You will also meet collections such as lists and dictionaries in later lessons. They are useful when one variable needs to hold multiple values or named pieces of information.

### 4. Get input and convert it
The \`input()\` function reads text from the user. Even if someone types a number, the result is a string until we convert it.

\`\`\`python
first = float(input("Enter the first number: "))
second = float(input("Enter the second number: "))
print("Sum:", first + second)
\`\`\`

Use \`int()\` for whole-number input and \`float()\` when decimal values are possible. Conversion can fail if the input is not a valid number, so robust programs should handle that possibility.

### 5. Operators let values work together
Arithmetic operators perform calculations:

\`\`\`python
a, b = 17, 5
print(a + b)   # 22
print(a - b)   # 12
print(a * b)   # 85
print(a / b)   # 3.4
print(a // b)  # 3: floor division
print(a % b)   # 2: remainder
print(a ** b)  # 1419857
\`\`\`

Comparison operators such as \`==\`, \`!=\`, \`>\`, \`<\`, \`>=\` and \`<=\` return a Boolean result. Logical operators \`and\`, \`or\` and \`not\` combine Boolean expressions.

\`\`\`python
marks = 72
attendance = 0.82
print(marks >= 40)  # True
print(marks >= 40 and attendance >= 0.75)
\`\`\`

Assignment operators such as \`=\`, \`+=\` and \`-=\` store or update a variable's value. Do not confuse \`=\` (assignment) with \`==\` (comparison).

### 6. Make output easier to read
An f-string lets you place variable values inside a string by writing \`f\` before the opening quote.

\`\`\`python
name = "Mina"
score = 91.456
print(f"{name}'s score is {score:.2f}.")
\`\`\`

The format \`:.2f\` displays two digits after the decimal point. Clear output helps when checking results or presenting analysis.

### 7. A few useful habits
- Choose names that explain what a value means.
- Convert input to the required type before doing calculations.
- Use parentheses when an expression becomes difficult to read.
- Add comments where they explain a decision or a tricky step.
- Test small examples before combining everything into a larger program.

### Practice task
Write a marks calculator that asks for a student's name and marks in three subjects. Convert the marks to numbers, calculate the total and average, and display a sentence using an f-string. Try decimal marks too, and check that the output is readable.

**Practical objective:** Store values, identify common data types, accept input, perform calculations and format output.

**GeeksforGeeks references**
- [Python Variables](https://www.geeksforgeeks.org/python/python-variables/)
- [Python Data Types](https://www.geeksforgeeks.org/python/python-data-types/)
- [Python Operators](https://www.geeksforgeeks.org/python/python-operators/)
- [Python Input and Output](https://www.geeksforgeeks.org/python/taking-input-in-python/)
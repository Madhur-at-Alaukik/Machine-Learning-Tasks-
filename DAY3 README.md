# Machine Learning – Daily Task Update
## Day 3: Conditional Statements and Loops

### 1. Boolean Expressions
A Boolean expression is an expression that evaluates to `True` or `False`. It is used to make decisions in a program.

```python
age = 19
print(age >= 18)  # True
```

Boolean expressions often use comparison operators such as `>`, `<`, `==`, and `!=`, or logical operators such as `and`, `or`, and `not`.

### 2. The `if` Statement
An `if` statement runs a block of code only when its condition is true.

```python
marks = 72

if marks >= 40:
    print("Pass")
```

The condition is checked first. If it evaluates to `True`, the indented block executes; otherwise, it is skipped.

### 3. `if-else`
`else` provides an alternative block when the `if` condition is false.

```python
number = 7

if number % 2 == 0:
    print("Even")
else:
    print("Odd")
```

The modulo operator `%` returns the remainder. A number divisible by 2 has remainder 0.

### 4. `if-elif-else`
Use `elif` to test multiple conditions in order. Only the first matching branch is executed.

```python
marks = 83

if marks >= 90:
    grade = "A"
elif marks >= 75:
    grade = "B"
elif marks >= 60:
    grade = "C"
else:
    grade = "D"

print(grade)  # B
```

Conditions should be arranged carefully. For grading, checking `marks >= 60` before `marks >= 90` would incorrectly classify high marks as C.

### 5. Nested Conditions
A nested condition is an `if` statement placed inside another conditional block. It is useful when a second decision depends on the first.

```python
age = 20
has_id = True

if age >= 18:
    if has_id:
        print("Entry allowed")
    else:
        print("ID required")
else:
    print("Entry not allowed")
```

Avoid unnecessary nesting when a simple logical expression is clearer.

### 6. The `for` Loop
A `for` loop iterates over the items in a sequence or other iterable, such as a list, string, or range.

```python
for name in ["Asha", "Ravi", "Mina"]:
    print(name)
```

The loop runs once for each item.

### 7. The `range()` Function
`range()` generates a sequence of integers, often used in loops.

- `range(stop)`: starts at 0 and stops before `stop`.
- `range(start, stop)`: starts at `start` and stops before `stop`.
- `range(start, stop, step)`: advances by `step`.

```python
for number in range(1, 6):
    print(number)
```

Output: `1 2 3 4 5` on separate lines. The ending value 6 is excluded.

### 8. The `while` Loop
A `while` loop repeats while its condition remains true.

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

The variable changes each time, so the condition eventually becomes false. If the condition never becomes false and the loop is not interrupted, the program may run indefinitely.

**`for` vs. `while`:**
- Use `for` when iterating over a collection or known range.
- Use `while` when repetition depends on a condition or user input.

### 9. `break`, `continue`, and `pass`
- **`break`:** Immediately exits the nearest enclosing loop.
- **`continue`:** Skips the rest of the current iteration and moves to the next iteration.
- **`pass`:** Does nothing; it is a placeholder where Python syntax requires a statement.

```python
for number in range(1, 6):
    if number == 3:
        continue
    if number == 5:
        break
    print(number)
```

Output: `1`, `2`, `4`. The value 3 is skipped, and the loop ends at 5.

### 10. Nested Loops and Patterns
A nested loop is a loop inside another loop. For each iteration of the outer loop, the inner loop runs through its iterations.

```python
for row in range(1, 4):
    for column in range(1, 4):
        print("*", end=" ")
    print()
```

Output:

```text
* * *
* * *
* * *
```

Nested loops are useful for grids, tables, and combinations, but can become slow when both loops process large collections.

### 11. Practical Programs
**A. Largest of three numbers**

```python
a = float(input("First number: "))
b = float(input("Second number: "))
c = float(input("Third number: "))

if a >= b and a >= c:
    largest = a
elif b >= a and b >= c:
    largest = b
else:
    largest = c

print("Largest:", largest)
```

**B. Multiplication table**

```python
number = int(input("Enter a number: "))

for i in range(1, 11):
    print(f"{number} x {i} = {number * i}")
```

**C. Factorial using a loop**

The factorial of a non-negative integer `n` is the product of all integers from 1 to `n`. By definition, `0! = 1`.

```python
n = int(input("Enter a non-negative integer: "))

if n < 0:
    print("Factorial is not defined for negative integers.")
else:
    factorial = 1
    for i in range(1, n + 1):
        factorial *= i
    print("Factorial:", factorial)
```

**D. Prime-number check**

A prime number is an integer greater than 1 with exactly two positive divisors: 1 and itself.

```python
n = int(input("Enter an integer: "))

if n < 2:
    is_prime = False
else:
    is_prime = True
    for divisor in range(2, int(n ** 0.5) + 1):
        if n % divisor == 0:
            is_prime = False
            break

print("Prime" if is_prime else "Not prime")
```

It is sufficient to test divisors up to the square root of `n`: if a larger factor exists, it must pair with a smaller factor.

**E. Fibonacci sequence**

Each Fibonacci number after the first two is the sum of the previous two numbers.

```python
terms = int(input("Number of terms: "))
a, b = 0, 1

for _ in range(max(0, terms)):
    print(a, end=" ")
    a, b = b, a + b
print()
```

### 12. Key Takeaways
- Conditions control which code blocks run.
- `if`, `elif`, and `else` handle alternative paths.
- `for` iterates over items; `while` repeats while a condition is true.
- `range()` excludes its stop value.
- `break`, `continue`, and `pass` have different purposes.
- Loops can automate repeated calculations, including factorials, prime checks, and sequences.

**Practical Objective:** Use conditions and loops to solve simple logic problems and explain the flow of execution.

**GeeksforGeeks References:**
- [Python If-Else](https://www.geeksforgeeks.org/python/python-if-else/)
- [Python For Loops](https://www.geeksforgeeks.org/python/loops-in-python/)
- [Python While Loop](https://www.geeksforgeeks.org/python/python-while-loop/)
- [Python Break, Continue and Pass](https://www.geeksforgeeks.org/python/break-continue-and-pass-in-python/)
# Machine Learning – Daily Task Update
## Day 4: Organizing Data with Collections and Functions

Once a program has more than a few values, separate variables become awkward. Python collections keep related information together, and functions give a task a name so it can be reused. Both ideas are useful when preparing data for analysis.

### 1. Pick a collection that fits the job
**List:** An ordered, changeable collection. Lists can contain duplicate values.

\`\`\`python
marks = [78, 91, 84, 78]
marks.append(88)
print(marks)
print(marks[0])  # First item
\`\`\`

List positions start at zero. Negative indexes count from the end, so \`marks[-1]\` returns the last item.

**Tuple:** An ordered collection that cannot be reassigned item by item after creation.

\`\`\`python
coordinates = (10, 25)
print(coordinates[0])
\`\`\`

**Set:** A collection of unique values. Sets help remove duplicates or check membership, but they do not provide stable positional indexing.

\`\`\`python
cities = {"Indore", "Bhopal", "Indore"}
print(cities)  # Each city appears once
\`\`\`

**Dictionary:** Stores values using keys. It is handy when each value has a label.

\`\`\`python
student = {"name": "Asha", "marks": 86, "city": "Indore"}
print(student["name"])
student["marks"] = 90
\`\`\`

Use \`student.get("email")\` when a key might not exist and you want to avoid a \`KeyError\`.

### 2. Loop through a collection
Collections become more useful when we process their contents.

\`\`\`python
marks = [78, 91, 84, 65]
total = 0
for mark in marks:
    total += mark

average = total / len(marks)
print(f"Average: {average:.2f}")
\`\`\`

For dictionaries, \`items()\` gives you each key and value:

\`\`\`python
student = {"name": "Asha", "marks": 86}
for key, value in student.items():
    print(f"{key}: {value}")
\`\`\`

### 3. Turn repeated steps into a function
A function groups statements under a name. It can accept inputs (parameters) and return a result.

\`\`\`python
def calculate_average(values):
    if not values:
        raise ValueError("Please provide at least one value.")
    return sum(values) / len(values)

marks = [78, 91, 84]
print(calculate_average(marks))
\`\`\`

The function works with different lists, so we do not need to rewrite the calculation each time. A \`return\` statement sends a value back to the caller; \`print()\` only displays something.

Functions can also have default parameters:

\`\`\`python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print(greet("Mina"))
print(greet("Ravi", "Welcome"))
\`\`\`

Choose names that describe the task, keep functions focused and validate inputs when invalid values would cause confusing results.

### 4. A shorter way to build a list
A list comprehension creates a list from an iterable, optionally applying a condition.

\`\`\`python
marks = [35, 72, 41, 28, 90]
passed = [mark for mark in marks if mark >= 40]
squared = [number ** 2 for number in range(1, 6)]
print(passed)
print(squared)
\`\`\`

The first example keeps passing marks. Comprehensions are concise, but a normal loop is often easier to understand when the logic has several steps.

### 5. Lambda, map and filter
A **lambda** is a small anonymous function. It is useful for short operations, not a replacement for every named function.

\`\`\`python
double = lambda number: number * 2
print(double(6))
\`\`\`

\`map()\` applies a function to each item; \`filter()\` keeps items for which a condition is true. In Python 3, both return iterators, so convert to a list if you need all results immediately.

\`\`\`python
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda n: n * 2, numbers))
evens = list(filter(lambda n: n % 2 == 0, numbers))
print(doubled)
print(evens)
\`\`\`

For many beginner tasks, a list comprehension is more readable than combining \`map()\`, \`filter()\` and lambda expressions.

### 6. Recursion: a function that calls itself
Recursion solves a problem by reducing it to a smaller version of the same problem. It needs a **base case** so that calls eventually stop.

\`\`\`python
def factorial(n):
    if n < 0:
        raise ValueError("n must be non-negative")
    if n in (0, 1):
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # 120
\`\`\`

Recursion is useful for some tree and divide-and-conquer problems. For straightforward repetition, a loop is often simpler and avoids Python's recursion-depth limit.

### Practice task
Create a dictionary for a student with a name, marks in several subjects and a city. Write functions to calculate the average and return a list of passed subjects. Test the functions with an empty list and explain how your code handles it.

**Practical objective:** Select suitable Python collections and write reusable functions to process grouped data.

**GeeksforGeeks references**
- [Python Lists](https://www.geeksforgeeks.org/python/python-list/)
- [Python Dictionaries](https://www.geeksforgeeks.org/python/python-dictionary/)
- [Python Functions](https://www.geeksforgeeks.org/python/python-functions/)
- [List Comprehension](https://www.geeksforgeeks.org/python-list-comprehension/)
- [Lambda, Map and Filter](https://www.geeksforgeeks.org/python/python-map-function/)
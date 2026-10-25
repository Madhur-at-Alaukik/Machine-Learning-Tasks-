# Machine Learning – Daily Task Update
## Day 5: OOP, Files, Exceptions and Git

### 1. Object-Oriented Programming (OOP)
Object-Oriented Programming organizes code around objects that combine data and behavior. In Python, a class defines the structure and behavior of objects, while an object is an instance of a class.

### 2. Classes, Objects, Attributes and Methods
- **Class:** A blueprint for creating objects.
- **Object:** An instance created from a class.
- **Attribute:** Data associated with an object.
- **Method:** A function defined in a class.

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def display(self):
        print(f"{self.name}: {self.marks}")

student1 = Student("Asha", 88)
student1.display()
```

`self` refers to the current instance. `__init__()` initializes instance attributes when an object is created.

### 3. Inheritance and Encapsulation
**Inheritance** lets a class reuse or extend behavior from another class.

```python
class Person:
    def __init__(self, name):
        self.name = name

class Student(Person):
    def study(self):
        print(f"{self.name} is studying")

s = Student("Aman")
s.study()
```

**Encapsulation** means keeping data and related operations together and controlling how internal state is accessed. Python uses conventions such as `_internal_name`; a leading double underscore triggers name mangling but does not provide absolute privacy.

### 4. Modules and Packages
A **module** is a Python file that can define functions, classes, and variables. A **package** organizes related modules, commonly in a directory.

```python
import math
print(math.sqrt(25))

from statistics import mean
print(mean([10, 20, 30]))
```

Imports allow code to be reused instead of rewritten.

### 5. Exception Handling
An exception is an error condition that interrupts normal program flow. `try` and `except` allow a program to handle expected errors; `else` runs if no exception occurred, and `finally` runs whether an exception occurred or not.

```python
try:
    number = int(input("Enter an integer: "))
    print(100 / number)
except ValueError:
    print("Please enter a valid integer.")
except ZeroDivisionError:
    print("The number must not be zero.")
finally:
    print("Program finished.")
```

Catch specific exceptions where possible. Avoid silently catching every exception because it can hide bugs.

### 6. File Handling
Python can read and write text files. Use `with open(...)` because the context manager closes the file even if an error occurs.

```python
with open("notes.txt", "w", encoding="utf-8") as file:
    file.write("Machine Learning notes\n")

with open("notes.txt", "r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

Common modes:
- `r`: Read an existing file.
- `w`: Write, replacing existing contents.
- `a`: Append to the end.
- `x`: Create a new file and fail if it already exists.

Use a correct path and an explicit encoding for text files.

### 7. CSV and JSON
**CSV (Comma-Separated Values)** is a simple tabular format suitable for rows and columns.

```python
import csv

rows = [
    {"name": "Asha", "marks": 88},
    {"name": "Ravi", "marks": 91}
]

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.DictWriter(file, fieldnames=["name", "marks"])
    writer.writeheader()
    writer.writerows(rows)
```

**JSON (JavaScript Object Notation)** represents structured data using objects, arrays, strings, numbers, booleans, and null values.

```python
import json

student = {"name": "Asha", "marks": 88}

with open("student.json", "w", encoding="utf-8") as file:
    json.dump(student, file, indent=4)

with open("student.json", "r", encoding="utf-8") as file:
    loaded_student = json.load(file)

print(loaded_student)
```

CSV is often convenient for flat tables; JSON is useful for nested structures and API data. JSON object keys are strings.

### 8. Virtual Environments and `pip`
A virtual environment isolates the packages installed for one project.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install numpy
python -m pip freeze > requirements.txt
```

`pip` installs packages. `requirements.txt` records package versions for easier recreation of an environment. Do not commit secrets such as API keys or passwords.

### 9. Git and GitHub
**Git** is a version-control system that records changes to files. **GitHub** hosts Git repositories online and supports collaboration.

Key concepts:
- **Repository:** Project files and their history.
- **Working directory:** Your current files.
- **Staging area:** Changes selected for the next commit.
- **Commit:** A saved snapshot with a message.
- **Branch:** An independent line of development.
- **Remote:** A hosted repository, often named `origin`.
- **Push:** Send local commits to a remote.
- **Pull:** Fetch and integrate remote changes.

Common commands:

```bash
git init
git status
git add .
git commit -m "Add Python practice exercises"
git remote -v
git push
```

For a new local repository, configure your identity if needed:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the email you intend to associate with your commits. Git does not automatically upload files when you commit; `push` sends commits to the remote.

### 10. Practical Exercises
1. Create a `Student` class with name, marks, and a display method.
2. Write and read a text file.
3. Save student records to CSV and JSON.
4. Handle invalid numeric input and missing files.
5. Create a virtual environment and install NumPy.
6. Initialize a Git repository, commit a README, and push it to a repository you control.

### 11. Key Takeaways
- Classes and objects group data and behavior.
- Inheritance supports reuse; encapsulation organizes access to internal state.
- Modules and packages help structure projects.
- Exception handling lets programs respond to expected errors.
- Context managers make file handling safer.
- CSV and JSON serve different data-storage needs.
- Virtual environments isolate dependencies.
- Git tracks history; GitHub hosts repositories; commits and pushes are different actions.

**Practical Objective:** Build a small organized Python program, save data in common file formats, handle basic errors, and understand the Git workflow.

**GeeksforGeeks References:**
- [Python OOP Concepts](https://www.geeksforgeeks.org/python/python-oops-concepts/)
- [Python Exception Handling](https://www.geeksforgeeks.org/python/python-exception-handling/)
- [File Handling in Python](https://www.geeksforgeeks.org/python/file-handling-python/)
- [CSV in Python](https://www.geeksforgeeks.org/python/working-csv-files-python/)
- [Git Tutorial](https://www.geeksforgeeks.org/git/git-tutorial/)
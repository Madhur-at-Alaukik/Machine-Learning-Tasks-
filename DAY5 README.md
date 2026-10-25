# Machine Learning – Daily Task Update
## Day 5: Writing Maintainable Python — Classes, Files and Error Handling

A useful project does more than run once. It should be understandable, handle common problems and keep its data somewhere reliable. Today connects everyday programming skills that help turn small scripts into projects you can maintain.

### 1. Handle errors without hiding them
A program may receive invalid input, fail to find a file or encounter a value it cannot convert. Python uses exceptions to represent many such problems.

\`\`\`python
try:
    age = int(input("Enter your age: "))
except ValueError:
    print("Please enter a whole number.")
else:
    print(f"Your age is {age}.")
\`\`\`

The code in \`try\` is attempted first. The matching \`except\` handles the specified exception, while \`else\` runs only if no exception occurred. A \`finally\` block can be used for cleanup that must happen either way.

Catch the errors you know how to handle. A broad \`except:\` can hide bugs and make debugging harder.

### 2. Read and write files safely
Files let a program keep information after it finishes. Use \`with open(...)\` so Python closes the file automatically.

\`\`\`python
with open("notes.txt", "w", encoding="utf-8") as file:
    file.write("Learning Python for ML\\n")

with open("notes.txt", "r", encoding="utf-8") as file:
    contents = file.read()
print(contents)
\`\`\`

Common modes include \`"r"\` to read, \`"w"\` to write or replace contents, and \`"a"\` to append. Be careful with \`"w"\`: it overwrites existing content. Use clear paths and specify an encoding for text files.

### 3. Work with CSV and JSON data
CSV is a common format for rows and columns. Python's built-in \`csv\` module can read it without an extra package.

\`\`\`python
import csv
with open("students.csv", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row["name"], row["marks"])
\`\`\`

JSON is useful for structured data such as configuration files and API responses.

\`\`\`python
import json
student = {"name": "Asha", "marks": [80, 90, 85]}

with open("student.json", "w", encoding="utf-8") as file:
    json.dump(student, file, indent=2)

with open("student.json", "r", encoding="utf-8") as file:
    loaded_student = json.load(file)
print(loaded_student["marks"])
\`\`\`

CSV values are commonly read as strings, so convert them to numeric types before calculating statistics. JSON supports common structures such as dictionaries, lists, strings, numbers, booleans and null values.

### 4. Organize related behavior with classes
A class defines data and behavior that objects of a particular kind share. Classes are not necessary for every small script, but they can help when a project has related state and operations.

\`\`\`python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def average(self):
        if not self.marks:
            return 0
        return sum(self.marks) / len(self.marks)

student = Student("Asha", [80, 90, 85])
print(student.name)
print(student.average())
\`\`\`

- A **class** describes a type of object.
- An **object** is an instance of a class.
- \`__init__\` initializes an object when it is created.
- \`self\` refers to the current object.
- A **method** is a function defined inside a class.

Keep the design simple. A class is most helpful when it makes related information and behavior easier to understand together.

### 5. Keep project dependencies separate
A virtual environment prevents one project's package versions from interfering with another project's setup.

\`\`\`powershell
python -m venv .venv
.\\.venv\\Scripts\\Activate.ps1
python -m pip install pandas numpy
python -m pip freeze > requirements.txt
\`\`\`

On macOS or Linux, activation is typically \`source .venv/bin/activate\`. A teammate can install recorded dependencies with \`python -m pip install -r requirements.txt\`. Do not commit the virtual environment folder itself; it can be recreated from the project files and dependency list.

### 6. Use Git to track changes
Git records changes over time, making it easier to see what changed and return to earlier versions.

\`\`\`bash
git init
git status
git add .
git commit -m "Add initial Python practice"
\`\`\`

A common workflow is to inspect changes with \`git status\`, stage the files you intend to save, and create a commit with a clear message. When connected to GitHub, you can push commits so they are available remotely.

Do not put passwords, API keys, private datasets or other secrets into a repository. If a secret is committed, deleting it from the latest file alone may not remove it from history.

### 7. Bring the pieces together
Create a student-record program that reads a CSV file, handles a missing file gracefully, calculates averages and writes a JSON summary. Use a class only if it makes the program clearer. Track the source files with Git and keep dependencies documented.

**Practical objective:** Save and load structured data, handle expected errors, organize related code and track project changes.

**GeeksforGeeks references**
- [Python File Handling](https://www.geeksforgeeks.org/python/file-handling-python/)
- [Python Exceptions](https://www.geeksforgeeks.org/python/python-exception-handling/)
- [Python Classes and Objects](https://www.geeksforgeeks.org/python/python-classes-and-objects/)
- [CSV in Python](https://www.geeksforgeeks.org/python/working-csv-files-python/)
- [Git Tutorial](https://www.geeksforgeeks.org/git/git-tutorial/)
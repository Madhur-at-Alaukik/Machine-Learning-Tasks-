# Machine Learning – Daily Task Update
## Day 3: Making Decisions and Repeating Work in Python

Programs become useful when they can react to different inputs and repeat a task without copying the same code again and again. Conditions handle decisions; loops handle repetition. Both are common in data preparation and in the logic around ML applications.

### 1. Start with a true-or-false question
A Boolean expression evaluates to either \`True\` or \`False\`.

\`\`\`python
marks = 68
passed = marks >= 40
print(passed)  # True
\`\`\`

Comparison operators include \`==\`, \`!=\`, \`>\`, \`<\`, \`>=\` and \`<=\`. Combine conditions with \`and\`, \`or\` and \`not\`.

\`\`\`python
marks = 68
attendance = 0.82
eligible = marks >= 40 and attendance >= 0.75
print(eligible)
\`\`\`

### 2. Use conditions when the program needs a choice
An \`if\` statement runs a block only when its condition is true. \`elif\` checks another possibility, while \`else\` handles the remaining case.

\`\`\`python
marks = float(input("Enter marks: "))

if marks >= 90:
    grade = "A"
elif marks >= 75:
    grade = "B"
elif marks >= 40:
    grade = "C"
else:
    grade = "Needs improvement"

print(f"Grade: {grade}")
\`\`\`

The order matters. Python checks conditions from top to bottom and executes the first matching branch. Checking \`marks >= 40\` before \`marks >= 90\` would incorrectly assign grade C to a score of 95.

### 3. Choose the right kind of loop
Use a **for loop** to visit items in a sequence or repeat a task a known number of times. Use a **while loop** when repetition depends on a condition that may change.

\`\`\`python
subjects = ["Maths", "Python", "Statistics"]
for subject in subjects:
    print(f"Today's subject: {subject}")
\`\`\`

The \`range()\` function generates a sequence of integers. Its stop value is excluded:

\`\`\`python
for number in range(1, 6):
    print(number)  # 1 through 5
\`\`\`

A \`while\` loop keeps running while its condition is true:

\`\`\`python
attempts = 0
while attempts < 3:
    print("Attempt", attempts + 1)
    attempts += 1
\`\`\`

Update the condition or the values it depends on; otherwise, a while loop may never end.

### 4. Change how a loop behaves
- \`break\` exits the loop immediately.
- \`continue\` skips the rest of the current iteration and moves to the next one.
- \`pass\` is a placeholder statement that does nothing.

\`\`\`python
for number in range(1, 8):
    if number == 3:
        continue
    if number == 6:
        break
    print(number)
\`\`\`

This prints 1, 2, 4 and 5. Use these statements when they make the logic clearer; too many branches inside a loop can make it hard to follow.

### 5. Put the ideas together: a small data check
Suppose you have marks and want to count how many students passed.

\`\`\`python
marks_list = [35, 72, 41, 28, 90, 64]
passed_count = 0

for marks in marks_list:
    if marks >= 40:
        passed_count += 1

print(f"Students who passed: {passed_count}")
\`\`\`

The loop visits each mark, the condition checks the threshold and the counter records how many satisfy it. This small pattern appears in larger data-processing tasks too.

### 6. Mistakes worth checking
- Using \`=\` where a comparison \`==\` is needed.
- Forgetting the colon after \`if\`, \`elif\`, \`else\`, \`for\` or \`while\`.
- Incorrect indentation.
- Creating a while loop whose condition never becomes false.
- Misunderstanding the stop value in \`range(start, stop)\`.

### Practice task
Write a program that asks for five marks, stores them in a list and prints whether each student passed. Then calculate how many passed and how many did not. Try boundary values such as 39, 40 and 41 to check your conditions.

**Practical objective:** Use Boolean expressions, conditional branches and loops to solve small decision-making and counting problems.

**GeeksforGeeks references**
- [Python If-Else](https://www.geeksforgeeks.org/python/python-if-else/)
- [Python For Loops](https://www.geeksforgeeks.org/python/for-loops-in-python/)
- [Python While Loop](https://www.geeksforgeeks.org/python/python-while-loop/)
- [Break, Continue and Pass](https://www.geeksforgeeks.org/python/break-continue-and-pass-in-python/)
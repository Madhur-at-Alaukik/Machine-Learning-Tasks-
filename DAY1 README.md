# Machine Learning – Daily Task Update
## Day 1: Getting Oriented with AI, Machine Learning and Python

When people say an app uses AI, they might mean a video recommendation, a camera that spots a person, or a tool that answers questions. Before writing models, it helps to understand what these examples have in common and how a typical ML project comes together.

### 1. Start with a real problem
Imagine a college wants to estimate which students may need academic support. It could create fixed rules, such as flagging everyone below a certain mark. That is traditional programming: a person defines the rules and the computer follows them.

Machine Learning takes another route. We collect examples from the past, choose useful information from those examples, and train an algorithm to learn patterns. The trained model can estimate an outcome for a new student. Its prediction is not automatically correct; it must be tested against data it has not already seen.

**Traditional programming:** data + rules written by a developer → result  
**Machine Learning:** examples + learning algorithm → trained model; new data + model → prediction

Neither approach is always better. Clear, stable rules may be easiest to program directly. ML is useful when patterns are difficult to describe with a short list of rules and enough relevant data is available.

### 2. A few terms you will keep seeing
Consider a table containing house area, number of bedrooms, age of the property and sale price.

- **Dataset:** the complete collection of records.
- **Observation or row:** one house in the table.
- **Feature:** an input that may help make a prediction, such as area or age.
- **Target or label:** the value we want to predict, such as sale price.
- **Algorithm:** the method used to learn from examples.
- **Model:** the result of fitting the algorithm to training data.
- **Training:** the process of fitting the model.
- **Inference:** using the trained model to predict an outcome for new input.

We can write a prediction as \`ŷ = f(X)\`. Here, \`X\` represents the input features, \`f\` is the trained model and \`ŷ\` is the predicted value.

### 3. How AI, ML, deep learning and data science fit together
These terms overlap, but they are not interchangeable.

- **Artificial Intelligence (AI)** is the broad field of building systems that perform tasks associated with human intelligence, such as reasoning, perception or language understanding.
- **Machine Learning (ML)** is one approach within AI. A system learns patterns from data instead of relying entirely on hand-written rules.
- **Deep Learning** is a type of ML that uses neural networks with multiple layers. It is common in image recognition, speech and language applications.
- **Data Science** is the wider practice of collecting, preparing, exploring and interpreting data. It may use statistics, visualization, ML and domain knowledge.

Deep learning is part of ML, and ML is part of AI. Data science overlaps with all of them rather than fitting neatly inside just one.

### 4. Three common learning setups
The learning setup depends on what information is available and what we want the model to do.

**Supervised learning** uses examples that include the correct answer.
- **Classification** predicts a category, such as spam or not spam.
- **Regression** predicts a number, such as a house price.

**Unsupervised learning** looks for structure when the task does not provide a target label. Clustering, for example, can group customers with similar purchasing patterns.

**Reinforcement learning** involves an agent taking actions in an environment and receiving rewards or penalties. The agent learns a strategy that aims to maximize longer-term reward.

| Approach | What the model learns from | Example |
|---|---|---|
| Supervised | Inputs paired with known answers | Predicting a house price |
| Unsupervised | Patterns or structure in data | Grouping similar customers |
| Reinforcement | Feedback from actions | Learning a game strategy |

### 5. Where ML appears in everyday work
ML is used to recommend products, flag suspicious transactions, recognize objects in images, forecast demand, classify messages and support medical-image analysis. These are examples of decision support, not guarantees that a system will always be right. Data quality, evaluation and responsible use matter as much as the algorithm.

### 6. The usual ML workflow
1. Define the question and decide what a useful answer looks like.
2. Gather data that is relevant to the question.
3. Inspect the dataset and correct obvious data-quality problems.
4. Separate the features from the target.
5. Split the data into training and test sets.
6. Fit an appropriate model using the training data.
7. Evaluate it on the held-out test data.
8. Use it for new predictions and keep checking how well it performs.

Keep the test set separate while developing the model. Repeatedly adjusting a model based on test results can make its reported performance look better than it really is.

### 7. Get Python ready
Python is widely used for ML because its syntax is readable and libraries such as NumPy, Pandas and scikit-learn make common tasks easier. You can start in a browser with Google Colab or work locally in VS Code.

Open [Google Colab](https://colab.research.google.com/), create a notebook and run:

\`\`\`python
print("Hello, Machine Learning!")
\`\`\`

For a local Windows setup, install Python and VS Code first, then run these commands in PowerShell:

\`\`\`powershell
python --version
python -m venv .venv
.\\.venv\\Scripts\\Activate.ps1
python -m pip install jupyter
jupyter notebook
\`\`\`

A virtual environment keeps packages for one project separate from those of another. If the \`python\` command is not recognized, check the installation or try \`py --version\`.

### 8. Try it yourself
1. Run the print statement in Colab or your local environment.
2. Choose a prediction problem you have seen in real life.
3. Write down possible features and the result you would want to predict.
4. Decide whether it sounds like classification, regression, clustering or reinforcement learning.
5. Explain in your own words why a test set is needed.

### What to remember
The goal today is not to memorize every AI term. It is to understand the journey from a real-world problem to a dataset, a trained model and a prediction. Later lessons will build the Python, statistics and data-handling skills needed to make that journey practical.

**Practical objective:** Explain the main ML learning setups, identify features and targets, and run a basic Python program.

**GeeksforGeeks references**
- [AI vs. Machine Learning vs. Deep Learning](https://www.geeksforgeeks.org/artificial-intelligence/difference-between-artificial-intelligence-vs-machine-learning-vs-deep-learning/)
- [Machine Learning Tutorial](https://www.geeksforgeeks.org/machine-learning/machine-learning/)
- [Python Programming Language Tutorial](https://www.geeksforgeeks.org/python/python-programming-language-tutorial/)
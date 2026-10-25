# Machine Learning – Daily Task Update
## Day 1: AI, Machine Learning and Python Environment Setup

### 1. What Is Artificial Intelligence (AI)?
Artificial Intelligence (AI) is a field of computer science that focuses on building systems capable of performing tasks that normally require human intelligence. These tasks include reasoning, learning, problem-solving, understanding language, recognizing images, and making decisions.

**Example:** A virtual assistant understands a spoken question and provides a response. A camera system detects people and vehicles in a video.

### 2. What Is Machine Learning (ML)?
Machine Learning is a branch of AI in which a computer learns patterns from data and uses those patterns to make predictions or decisions instead of relying only on manually written rules.

**Example:** An email spam filter learns from examples of spam and legitimate emails and predicts whether a new email is spam.

**Important terms:**
- **Dataset:** A collection of examples or records used for analysis or model training.
- **Feature:** An input variable used to make a prediction.
- **Label/Target:** The outcome the model is expected to predict.
- **Algorithm:** A procedure used to learn patterns from data.
- **Model:** The learned result produced after training an algorithm.
- **Training:** The process of learning patterns from examples.
- **Prediction/Inference:** Using a trained model to produce an output for new input.

### 3. What Is Deep Learning?
Deep Learning is a specialized branch of Machine Learning that uses neural networks with multiple layers to learn complex patterns. It is widely used for image recognition, speech processing, language tasks, and other problems involving complex data.

**Example:** An object-detection model identifies people, cars, bottles, or other objects in an image.

### 4. What Is Data Science?
Data Science combines programming, statistics, domain knowledge, and analytical methods to extract useful information from data. It may include collecting data, cleaning it, exploring patterns, creating visualizations, building ML models, and communicating findings.

**Example:** A company analyzes customer activity to understand why customers leave and may build a model to predict future customer churn.

### 5. AI vs. ML vs. Deep Learning vs. Data Science
- **AI:** The broad field of building intelligent systems.
- **ML:** A way to learn patterns from data.
- **Deep Learning:** ML that uses multilayer neural networks.
- **Data Science:** The wider process of extracting insights from data; it overlaps with AI and ML but is not simply a subfield of either.

**Relationship:** Deep Learning is part of ML, and ML is part of AI. Data Science overlaps with these fields.

### 6. Traditional Programming vs. Machine Learning
In traditional programming, a developer writes explicit rules that process input data to produce an output. In Machine Learning, an algorithm learns useful patterns from examples and uses the resulting model on new data.

**Traditional programming:** Input + manually written rules → Output

**Machine Learning:** Training examples + learning algorithm → Trained model; new input + trained model → Prediction

**Example:** A rule-based spam filter may block emails containing a particular phrase. An ML spam filter learns patterns from labelled examples and combines multiple signals.

| Traditional Programming | Machine Learning |
|---|---|
| Rules are mainly written by a programmer. | Patterns are learned from data. |
| Works well when rules are clear and stable. | Useful when patterns are difficult to specify manually. |
| Output depends on programmed logic. | Output depends on learned patterns and model design. |

### 7. Main Types of Machine Learning
**A. Supervised Learning:** Learns from labelled examples, where inputs and correct target values are provided.
- **Classification:** Predicts a category, such as spam/not spam.
- **Regression:** Predicts a numerical value, such as a house price.

**B. Unsupervised Learning:** Finds patterns or structure in data without a provided target label for the learning task.
- **Clustering:** Groups similar records.
- **Dimensionality reduction:** Represents data with fewer dimensions while preserving useful information.

**C. Reinforcement Learning:** An agent learns actions by interacting with an environment and receiving rewards or penalties. The aim is to learn a policy that maximizes cumulative reward.

| Type | Learning Signal | Example |
|---|---|---|
| Supervised | Known labels | Predicting house prices |
| Unsupervised | Structure in data | Customer segmentation |
| Reinforcement | Rewards from interaction | Learning to play a game |

### 8. Real-World Applications of ML
- **Healthcare:** Supporting image analysis and risk prediction.
- **Finance:** Detecting potentially fraudulent transactions.
- **Retail:** Recommending products and forecasting demand.
- **Cybersecurity:** Detecting suspicious activity.
- **Computer vision:** Detecting people, vehicles, and safety equipment.
- **Language processing:** Classifying text, translating, and answering questions.

### 9. Features, Labels, Training and Prediction
Consider a house-price dataset with columns for area, number of bedrooms, age, and price.
- **Features (X):** Area, bedrooms, and age.
- **Target (y):** House price.
- **Observation:** One row representing one house.
- **Training data:** Examples used to fit the model.
- **Test data:** Separate examples used to estimate performance on unseen data.
- **Prediction:** The estimated price for a new house.

A model can be represented as `ŷ = f(X)`, where `X` is the input, `f` is the trained model, and `ŷ` is the predicted output.

**Basic ML workflow:**
1. Define the problem and target.
2. Collect relevant data.
3. Inspect and clean the data.
4. Separate features and target.
5. Split data into training and testing sets.
6. Train a suitable algorithm.
7. Evaluate the model on unseen data.
8. Use the model for new predictions and monitor its performance.

Do not use test data to repeatedly tune the model, because that can make the final evaluation overly optimistic.

### 10. Python Development Environment
Python is a general-purpose programming language widely used in data analysis and ML because it is readable and has a large ecosystem of libraries.

**Common tools:**
- **Python:** Runs the code.
- **VS Code:** Code editor.
- **Jupyter Notebook:** Interactive environment for code, output, notes, and charts.
- **Google Colab:** Hosted notebook environment that runs in a browser.
- **pip:** Installs Python packages.
- **Virtual environment:** Keeps project dependencies separate from other projects.

**Quick start with Google Colab:** Open https://colab.research.google.com/, create a notebook, and run:

```python
print("Hello, Machine Learning!")
```

**Local setup in Windows PowerShell** (after installing Python and VS Code):

```powershell
python --version
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install jupyter
jupyter notebook
```

If `python` is not recognized, try `py --version` or install Python from https://www.python.org/downloads/.

### 11. Practical Exercises
1. Set up a Python environment using Colab or VS Code.
2. Write a program that displays your name, degree, company, and role.
3. Create a calculator that accepts two numbers.
4. Choose a real-world prediction problem and identify its features, target, ML type, and evaluation approach.

### 12. Key Takeaways
- AI is the broad field; ML is one approach within AI, and Deep Learning is a type of ML.
- Supervised learning uses labelled examples, unsupervised learning discovers structure, and reinforcement learning learns through rewards.
- Features are inputs; labels or targets are outcomes to predict.
- Training creates a model, while inference uses the trained model on new input.
- Python, notebooks, virtual environments, and packages form the basic ML development environment.

**Practical Objective:** Explain the basic AI/ML terminology, identify a simple ML workflow, and run a Python program in a working development environment.

**GeeksforGeeks References:**
- [AI vs. Machine Learning vs. Deep Learning](https://www.geeksforgeeks.org/artificial-intelligence/difference-between-artificial-intelligence-vs-machine-learning-vs-deep-learning/)
- [Machine Learning Tutorial](https://www.geeksforgeeks.org/machine-learning/machine-learning/)
- [Python Tutorial](https://www.geeksforgeeks.org/python/python-programming-language-tutorial/)
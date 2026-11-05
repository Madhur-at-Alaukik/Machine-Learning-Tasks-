# Machine Learning – Daily Task Update
## Module 4: Supervised Machine Learning
## Day 13: Training and Comparing Classification Models

For Day 13, I used the prepared Loan Approval Prediction dataset to train a classification model. The target column is `loan_status`, which contains the loan decision. The goal is to learn from the applicant information and predict whether a loan is approved or rejected.

### 1. Understand the classification problem

This is a **binary classification** problem because the target has two classes:

- Approved
- Rejected

The input features include details such as income, loan amount, loan term, CIBIL score and asset values. The `loan_id` column is an identifier and should not be used as a predictive feature.

### 2. Train a Logistic Regression model

Logistic Regression is a classification algorithm that estimates the probability of a class. It is a useful first model because it provides a simple baseline for comparison.

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)

model.fit(X_train_encoded, y_train)

print("Model trained successfully!")
```

- `fit()` trains the model using the training data.
- `max_iter=1000` allows more iterations for the model to converge.

### 3. Make predictions

After training, use the test features to predict loan status.

```python
y_pred = model.predict(X_test_encoded)

print("Actual values:")
print(y_test.head(10).tolist())

print("Predicted values:")
print(y_pred[:10])
```

The test set is kept separate from model training so that evaluation measures performance on data the model did not learn from.

### 4. Check model accuracy

Accuracy measures the proportion of test predictions that were correct.

```python
from sklearn.metrics import accuracy_score

accuracy = accuracy_score(y_test, y_pred)

print("Model Accuracy:", round(accuracy * 100, 2), "%")
```

Accuracy is useful, but it should not be the only metric considered. A model can have good overall accuracy while performing poorly on one class.

### 5. Understand the classification report

```python
from sklearn.metrics import classification_report

print(classification_report(y_test, y_pred))
```

The report contains:

- **Precision:** Of the predictions made for a class, how many were correct?
- **Recall:** Of the actual examples in a class, how many did the model identify?
- **F1-score:** A balance between precision and recall.
- **Support:** Number of actual test examples in each class.

For loan approval, check the metrics for both Approved and Rejected classes.

### 6. Read the confusion matrix

```python
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay
import matplotlib.pyplot as plt

cm = confusion_matrix(y_test, y_pred)

display = ConfusionMatrixDisplay(
    confusion_matrix=cm,
    display_labels=model.classes_
)

display.plot()
plt.show()
```

The rows represent actual labels and the columns represent predicted labels.

For the Logistic Regression run shared during this task, the confusion matrix was:

| Actual / Predicted | Approved | Rejected |
|---|---:|---:|
| Approved | 485 | 43 |
| Rejected | 118 | 203 |

From this matrix:

- 485 approved loans were predicted correctly.
- 43 approved loans were predicted as rejected.
- 118 rejected loans were predicted as approved.
- 203 rejected loans were predicted correctly.

The accuracy from these counts is:

```text
(485 + 203) / (485 + 43 + 118 + 203) × 100
= 81.04%
```

The model identified approved loans more successfully than rejected loans in this test run. In particular, 118 rejected loans were predicted as approved. This is why it is important to check class-wise precision and recall rather than relying only on accuracy.

### 7. Train a Decision Tree model

A Decision Tree makes a prediction by asking a sequence of questions based on feature values. It can learn non-linear decision rules and is relatively easy to visualize.

```python
from sklearn.tree import DecisionTreeClassifier

dt_model = DecisionTreeClassifier(
    max_depth=10,
    random_state=42
)

dt_model.fit(X_train_encoded, y_train)

dt_pred = dt_model.predict(X_test_encoded)

print("Decision Tree Accuracy:",
      accuracy_score(y_test, dt_pred) * 100)

print(classification_report(y_test, dt_pred))
```

The `max_depth` parameter limits how deep the tree can grow. Limiting depth can help control overfitting.

### 8. Train a Random Forest model

Random Forest combines predictions from multiple Decision Trees. Each tree is trained using a sample of the training data and a selection of features. The final classification is based on the trees' combined vote.

```python
from sklearn.ensemble import RandomForestClassifier

rf_model = RandomForestClassifier(
    n_estimators=100,
    random_state=42
)

rf_model.fit(X_train_encoded, y_train)

rf_pred = rf_model.predict(X_test_encoded)

print("Random Forest Accuracy:",
      accuracy_score(y_test, rf_pred) * 100)

print(classification_report(y_test, rf_pred))
```

- `n_estimators=100` creates a forest of 100 trees.
- `random_state=42` makes the random process reproducible.

### 9. Compare the models

Use the same train-test split for all models so that the comparison is fair.

```python
results = {
    "Logistic Regression": accuracy_score(y_test, y_pred),
    "Decision Tree": accuracy_score(y_test, dt_pred),
    "Random Forest": accuracy_score(y_test, rf_pred)
}

for name, score in results.items():
    print(name, ":", round(score * 100, 2), "%")
```

Compare the classification reports and confusion matrices as well as accuracy. A model with a higher accuracy is not automatically the best choice if it performs poorly on an important class.

### Practice task

1. Train Logistic Regression, Decision Tree and Random Forest models.
2. Generate predictions for the same test set.
3. Compare their accuracy scores.
4. Read precision, recall and F1-score for both loan classes.
5. Plot a confusion matrix for each model.
6. Note which model makes fewer incorrect approvals and incorrect rejections.

**Practical objective:** Train multiple classification algorithms and compare their performance using accuracy, classification reports and confusion matrices.

**Result recorded:** Logistic Regression achieved 81.04% accuracy based on the confusion matrix shared for this task. Decision Tree and Random Forest were set up as comparison exercises; their final scores were not recorded here.

**GeeksforGeeks references**
- [Logistic Regression](https://www.geeksforgeeks.org/machine-learning/understanding-logistic-regression/)
- [Decision Tree](https://www.geeksforgeeks.org/machine-learning/decision-tree/)
- [Random Forest](https://www.geeksforgeeks.org/machine-learning/random-forest-algorithm-in-machine-learning/)
- [Confusion Matrix](https://www.geeksforgeeks.org/machine-learning/confusion-matrix-machine-learning/)

# Machine Learning – Daily Task Update
## Module 4: Supervised Machine Learning
## Day 14: Model Evaluation, Cross-Validation and Hyperparameter Tuning

After training more than one model, the next step is to evaluate the results carefully and improve the model settings. For the Loan Approval Prediction task, this means checking whether the model performs consistently and whether its settings can be improved without using the test set for tuning.

### 1. Why model evaluation matters

A model should not be selected using only its training performance. It must also perform well on data that was not used to train it.

For a classification problem, common evaluation metrics are:

- **Accuracy:** Percentage of all predictions that are correct.
- **Precision:** How many predictions for a particular class were correct.
- **Recall:** How many actual examples of a class were identified.
- **F1-score:** Harmonic mean of precision and recall.
- **Confusion matrix:** Shows correct and incorrect predictions for each class.

In the loan dataset, both Approved and Rejected predictions should be checked. A wrong approval and a wrong rejection can have different consequences.

### 2. Understand overfitting and underfitting

**Overfitting** happens when a model learns the training data too closely, including noise or details that do not generalize. It may perform very well on training data but poorly on unseen data.

**Underfitting** happens when a model is too simple to learn the important patterns. It performs poorly on both training and test data.

A useful first check is to compare training and test accuracy:

```python
train_pred = rf_model.predict(X_train_encoded)
test_pred = rf_model.predict(X_test_encoded)

print("Training accuracy:",
      accuracy_score(y_train, train_pred))

print("Testing accuracy:",
      accuracy_score(y_test, test_pred))
```

A large gap can be a sign of overfitting, although the result should be interpreted with the model and dataset in mind.

### 3. Understand cross-validation

A single train-test split can give a result that depends on which rows happen to be in the test set. Cross-validation gives a more stable estimate by repeating training and validation across different folds.

In **k-fold cross-validation**, the training data is divided into k parts. The model trains on k-1 parts and validates on the remaining part. This process repeats until each part has been used for validation.

```python
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier

rf_model = RandomForestClassifier(
    n_estimators=100,
    random_state=42
)

scores = cross_val_score(
    rf_model,
    X_train_encoded,
    y_train,
    cv=5,
    scoring="accuracy"
)

print("Fold scores:", scores)
print("Average accuracy:", scores.mean())
```

This example evaluates a Random Forest using five folds. For a more reliable workflow, preprocessing should be included inside a Scikit-learn Pipeline so that the encoder is fitted separately inside each fold. The next section demonstrates this approach.

### 4. Understand hyperparameters

**Parameters** are values a model learns during training, such as the weights in Logistic Regression.

**Hyperparameters** are settings chosen before or during model selection. They control how the model learns.

Examples:

| Model | Hyperparameter | Purpose |
|---|---|---|
| Decision Tree | `max_depth` | Limits tree depth |
| Random Forest | `n_estimators` | Number of trees |
| Random Forest | `max_depth` | Maximum depth of each tree |
| Logistic Regression | `C` | Controls regularization strength |

Different settings can lead to different results. The best values should be selected using training data and validation, not by repeatedly checking the test set.

### 5. Hyperparameter tuning with GridSearchCV

Grid Search tries the parameter combinations provided in a grid and evaluates them using cross-validation.

The following example places preprocessing and the Random Forest inside one Pipeline. This is important because the encoder is fitted only on each fold's training portion during cross-validation.

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder
from sklearn.pipeline import Pipeline
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import GridSearchCV

cat_features = ["education", "self_employed"]
num_features = [col for col in X_train.columns if col not in cat_features]

preprocessor = ColumnTransformer(
    transformers=[
        ("cat", OneHotEncoder(handle_unknown="ignore"), cat_features),
        ("num", "passthrough", num_features)
    ]
)

pipeline = Pipeline(steps=[
    ("preprocessor", preprocessor),
    ("model", RandomForestClassifier(random_state=42))
])

param_grid = {
    "model__n_estimators": [100, 200],
    "model__max_depth": [None, 10, 20],
    "model__min_samples_split": [2, 5]
}

grid_search = GridSearchCV(
    pipeline,
    param_grid,
    cv=5,
    scoring="accuracy",
    n_jobs=-1
)

grid_search.fit(X_train, y_train)

print("Best parameters:", grid_search.best_params_)
print("Best cross-validation score:", grid_search.best_score_)
```

The `model__` prefix tells GridSearchCV that the parameter belongs to the model step of the Pipeline.

### 6. Evaluate the tuned model on the test set

The test set should be used after model selection is complete. It gives a final evaluation on data that was not used to choose the hyperparameters.

```python
from sklearn.metrics import accuracy_score, classification_report
from sklearn.metrics import ConfusionMatrixDisplay
import matplotlib.pyplot as plt

best_model = grid_search.best_estimator_

test_pred = best_model.predict(X_test)

print("Test accuracy:",
      accuracy_score(y_test, test_pred))

print(classification_report(y_test, test_pred))

ConfusionMatrixDisplay.from_estimator(
    best_model,
    X_test,
    y_test
)

plt.show()
```

The final test score may be different from the cross-validation score. That is normal because they are calculated on different data.

### 7. Important points to remember

- Use the same test set only for final evaluation.
- Do not select hyperparameters by repeatedly checking test performance.
- Put data preprocessing inside a Pipeline when using cross-validation.
- Compare precision, recall and F1-score for both classes.
- A higher accuracy does not always mean a safer or more useful loan prediction model.
- Keep a record of the model settings and evaluation results so the experiment can be repeated.

### Practice task

1. Compare training and test accuracy for a model.
2. Run five-fold cross-validation on the training data.
3. Create a Pipeline that includes preprocessing and a Random Forest.
4. Use GridSearchCV to try different values of `n_estimators`, `max_depth` and `min_samples_split`.
5. Evaluate the selected model once on the test set.
6. Compare the tuned model's classification report and confusion matrix with the earlier Logistic Regression result.

**Practical objective:** Understand model generalization, use cross-validation to compare settings and tune a classifier without leaking test data into model selection.

**Note:** This README introduces the next practical learning step. No cross-validation or hyperparameter tuning result is claimed as completed until the code is run.

**GeeksforGeeks references**
- [Overfitting and Underfitting](https://www.geeksforgeeks.org/machine-learning/underfitting-and-overfitting-in-machine-learning/)
- [Cross-Validation](https://www.geeksforgeeks.org/machine-learning/cross-validation-in-machine-learning/)
- [GridSearchCV](https://www.geeksforgeeks.org/machine-learning/hyperparameter-tuning/)
- [Scikit-learn Pipeline](https://www.geeksforgeeks.org/machine-learning/scikit-learn-pipeline/)

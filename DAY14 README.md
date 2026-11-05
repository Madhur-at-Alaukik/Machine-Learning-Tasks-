# Machine Learning – Daily Task Update
## Day 14: ML Workflow and Problem Formulation

### 1. Supervised, Unsupervised and Reinforcement Learning

Machine learning methods are commonly grouped according to the type of feedback or information available during training.

**Supervised learning** uses examples that contain input features and known target values. The model learns a relationship between inputs and targets so it can predict targets for new observations. Classification and regression are supervised-learning tasks.

Examples include predicting loan approval from applicant information and estimating house prices from property features.

**Unsupervised learning** uses data without a supplied target label. The objective is to identify structure or patterns in the data, such as groups of similar observations or unusual records.

Examples include customer segmentation and clustering similar documents.

**Reinforcement learning** involves an agent that interacts with an environment, takes actions and receives rewards or penalties. The agent learns a policy for choosing actions in order to maximize cumulative reward over time.

Examples include game-playing agents and systems that learn control strategies through interaction.

The three approaches differ in the type of learning signal: known target labels, structure in unlabelled data, or rewards from interaction with an environment.

### 2. Regression and Classification

**Regression** predicts a numerical quantity. The predicted output is generally continuous, such as a price, temperature, demand or delivery time.

Examples:
- Predicting the selling price of a house.
- Estimating monthly sales.
- Predicting the time required for a delivery.

**Classification** predicts a class or category. The output may be one of two classes or one among several classes.

Examples:
- Predicting whether a loan is approved or rejected.
- Classifying an email as spam or not spam.
- Identifying the type of an image.

The target column determines the problem type. Predicting a number is generally regression, while predicting a category is classification. The choice of model and evaluation method should match the problem type.

### 3. Features, Targets and Predictions

A **feature** is an input variable used by a model to make a prediction. A dataset can contain one feature or many features. Features may be numerical or categorical.

The **target** is the value the model is intended to predict. In supervised learning, the target is known for the training examples.

A **prediction** is the model's output for an input observation. It may be a numerical estimate in regression or a predicted class in classification. Some classifiers can also return class probabilities.

For a loan approval dataset:
- Features may include annual income, loan amount, loan term and CIBIL score.
- Target may be loan status.
- Prediction may be Approved or Rejected.

Identifiers that only distinguish records should not automatically be used as predictive features. A feature should have a meaningful relationship to the problem and be available at the time a prediction is made.

### 4. Problem Formulation

**Problem formulation** means converting a real-world requirement into a clear machine learning task. It should be completed before selecting an algorithm because the problem definition determines what data, target, model type and evaluation approach are appropriate.

A well-defined problem should identify:

1. **Objective:** What decision, estimate or outcome should the model support?
2. **Prediction unit:** What does one row or observation represent?
3. **Target:** What exact value should be predicted?
4. **Features:** Which information will be available when the prediction is made?
5. **Problem type:** Is the task classification, regression or another learning problem?
6. **Success measure:** How will model performance be assessed?
7. **Constraints:** Are there limits related to data availability, prediction time, interpretation or the cost of errors?

For example, "predict loan approval" is more useful when defined precisely: predict the loan status for each application using the applicant and financial information available at the time the application is assessed.

Problem formulation should also reflect the business objective. A technically accurate prediction may not be useful if it does not support the decision or outcome the organisation needs.

### 5. Dataset Splitting

Dataset splitting separates observations into different subsets for model development and evaluation.

**Training set:** Used to fit the model. The model learns its parameters from this data.

**Validation set:** Used during model development to compare approaches or select settings. It provides feedback without using the final test set.

**Test set:** Kept separate until the final evaluation. It estimates how the selected model performs on data that was not used to train or select it.

A common approach is to reserve a portion of the dataset for testing and use the remaining data for training and validation. The exact proportions depend on the dataset size and task.

For classification, a **stratified split** can help preserve the approximate proportion of each target class in the subsets. A split should also respect the data structure: related observations or time-ordered records may require a group-based or time-aware approach rather than an ordinary random split.

The test set should not be repeatedly used to choose features, model settings or preprocessing methods. Doing so makes it part of the development process and weakens the final evaluation.

### 6. Baseline Models

A **baseline model** is a simple reference point used to judge whether a more advanced model provides meaningful improvement.

For classification, a basic baseline may always predict the most frequent class. For regression, a baseline may predict the mean or median target value from the training data.

A baseline is useful because a model's score has little meaning without a reference. If a complex model performs no better than a simple baseline, its additional complexity may not be justified.

The baseline must use only information available in the training data. Its evaluation should use the same validation or test strategy as the models being compared.

### 7. Training and Inference

**Training** is the process in which a model uses training data to learn its parameters. During training, the model adjusts these parameters according to its learning method and objective.

**Inference** is the process of using a trained model to generate predictions for new input data. Inference does not normally involve learning new model parameters.

A typical sequence is:

1. Prepare the training data.
2. Fit the model using the training examples.
3. Save or retain the fitted model and required preprocessing steps.
4. Provide new input data in the expected format.
5. Apply the same preprocessing and generate predictions.

The preprocessing used during inference must match the preprocessing used during training. For example, categorical encoding and numerical transformations should use the fitted training transformations rather than being recalculated independently for every new input.

### 8. Model Lifecycle and Business Objectives

The **machine learning model lifecycle** describes the stages involved in developing and using a model.

A typical lifecycle includes:
1. Understand the problem and business objective.
2. Identify and collect relevant data.
3. Inspect, prepare and transform the data.
4. Define features and target.
5. Split the data and establish a baseline.
6. Train suitable models.
7. Evaluate and compare model performance.
8. Select a model according to the objective and constraints.
9. Use the model to generate predictions.
10. Review its performance and limitations as the environment or data changes.

A **business objective** describes the practical outcome that the model is intended to support. It should be connected to the model's target and evaluation criteria.

For example, a loan approval prediction system should not be judged only by overall accuracy. The effects of incorrect approvals and incorrect rejections, the quality of the available data and the need for human review may also matter.

A successful ML workflow connects the technical prediction task with the real decision it is intended to support. Model performance, practical usefulness and limitations should all be considered.


## Additional Learning — Training and Evaluating Logistic Regression

A Logistic Regression classifier was trained on the prepared loan dataset. Although its name includes "regression", it is commonly used for classification. It estimates class probabilities and assigns a class according to its decision rule.

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)

model.fit(X_train_encoded, y_train)

y_pred = model.predict(X_test_encoded)
```

- `fit()` trains the model using the training features and target.
- `predict()` generates class predictions for the test features.
- `max_iter=1000` allows the optimization process more iterations to converge.

The predictions were evaluated using accuracy and a classification report.

```python
from sklearn.metrics import accuracy_score, classification_report

print("Accuracy:", accuracy_score(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

The classification report includes precision, recall, F1-score and support for each class. These class-wise values are important when the model may perform differently for approved and rejected applications.

For the confusion matrix shared during this exercise, the counts were:

| Actual / Predicted | Approved | Rejected |
|---|---:|---:|
| Approved | 485 | 43 |
| Rejected | 118 | 203 |

Based on these counts, the model correctly predicted 485 approved cases and 203 rejected cases. It incorrectly predicted 43 approved cases as rejected and 118 rejected cases as approved.

The accuracy calculated from the matrix is:

```text
(485 + 203) / (485 + 43 + 118 + 203) × 100 = 81.04%
```

Accuracy gives the proportion of all test predictions that were correct. It does not show how well each class was identified, so it should be considered together with precision, recall, F1-score and the confusion matrix.

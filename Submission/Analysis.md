# Analysis Overview
This analysis is meant to determine which neural network models would be best used to determine if applicants for grants that are most likely to succeed. 

- Application Type
- Affiliation
- Classification
- Use Case
- Organization
- Status
- Income Amount
- Special Considerations
- Ask Amount

Loan Size
Interest Rate
Borrower Income
Debt to Income Ratio
Number of Accounts
Derogatory Marks
The data was very imbalanced with 96.8% of accounts not being at risk of defaulting. As a result, after the data was scaled, the dataset needed to be stratified on the loan status when the train_test_split was run to ensure that both the training and testing data sets had accurate ratios of borrower loan statuses.

The models that were used include:

Mathematical Models
Logistic Regression
Support Vector Machine (SVM)
k-Nearest Neighbor
Tree-based Models
Decision Tree
Random Forest
Extra Trees
Ada Boost
Gradient Boosting
XGBoost
LightGBM

## Results
### Data pre-processing
Target:
- Was the charity able to complete their goal with the funding?

Features:
- Application Type
    - Binned items with a value count under 250 into an "Other" category
- Affiliation
- Classification
    - Binned items with a value count under 300 into an "Other" category
- Use Case
- Organization
- Status
- Income Amount
- Special Considerations
- Ask Amount

Variables that were removed:
- Name
- EIN
### Trained Models
    Network 1:
    - Layers:
    - Nodes per layer:
    - Loss:
    - Accuracy:
    - Summary:

    Network 2:
    - Layers:
    - Nodes per layer:
    - Loss:
    - Accuracy:
    - Summary:

    Network 3:
    - Layers:
    - Nodes per layer:
    - Loss:
    - Accuracy:
    - Summary:

    Network 4:
    - Layers:
    - Nodes per layer:
    - Loss:
    - Accuracy:
    - Summary:

    Network 5:
    - Layers:
    - Nodes per layer:
    - Loss:
    - Accuracy:
    - Summary:

    Keras-Tuner Results:
    - Layers:
    - Nodes per layer:
    - Loss:
    - Accuracy:
    - Summary:

    Network 6:
    - Pre-processing changes:
    - Layers:
    - Nodes per layer:
    - Loss:
    - Accuracy:
    - Summary:



## Summary
Looking at the models, they all perform about the same. While some of the more complex tree models (i.e. Ada Boost, XGBoost, Light GBM, etc.) have marginally higher accuracy, presicion, and recall scores than the Logistic Regression model, the difference is relatively minor. The Logistic Regression had an Area Under the Curve (AUC) score of 0.996 in addition to an accuracy of 0.99, precision of 0.88, and a recall of 0.97. With the score results, and how close the results are to the tree-models, the Logistic Regression is the best model to use. Because the Logistic Regression is a very explainable model, it should be preferred over the other models given the low risk of either Type 1 or Type 2 errors and because no other model is significantly better.

If the bank were to want to decrease the risk of a Type 1 error where they think an account is at risk of defaulting when it isn't, the best model would be one of the following models:

Ada Boost,
Gradient Boosting,
XGBoost,
Light GBM,
k-Nearest Neighbor, or
Support Vector Machine.
All of the listed models had a recall score of 0.99. However, the Logistic Regression had a recall of 0.97. So while the listed models would have a decreased risk of a Type 1 error, the difference isn't that impactful.

On the other hand, if the bank wanted to decrease the risk of a Type 2 error where they think an account is not at risk of defaulting when it is, all models perform around the same with a precision score of 0.88 or 0.89, so there is no real difference between models in that regard.

As a final recommendation, the Logistic Regression is the best model to use.
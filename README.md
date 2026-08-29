# DS 301 Final Project: Credit Card Default Prediction

## Team Members
* Chung Vong (Simon)
* Maria
* Eduardo
* Gabriel

## Resources
* **Research Paper:** [Predicting Default of Credit Card Clients Using Three Supervised Machine Learning Algorithms](https://thomshu.github.io/ThomsonPorfolio.github.io/Media/MLArticle.pdf)
* **Dataset:** [UCI Default of Credit Card Clients](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients)
* **Canva Presentation:** [[https://canva.link/el13qjq8yakgjbr](https://canva.link/jre8jlc8xigbc66)](https://canva.link/jre8jlc8xigbc66)

## Project Overview

This project predicts whether a credit card client will default on the next monthly payment. It was developed for the **DS 301 Final Project** and follows a classification research paper using the public **Default of Credit Card Clients** dataset.

The project has two main goals:
1. Reproduce the methodology and main results presented in the research article.
2. Provide a significant group contribution by introducing and tuning a new classification model to optimize the recall metric.

The models compared are:
- Decision Tree (Article)
- K-Nearest Neighbors / KNN (Article)
- Support Vector Machine / SVM (Article)
- **Logistic Regression (Our Group Contribution)**

## Dataset Summary
We utilized the UCI Taiwan Credit Card dataset. Following the article's cleaning process, observations with undocumented values in the `EDUCATION` or `MARRIAGE` variables were removed.

| Item | Value |
|---|---:|
| Original observations | 30,000 |
| Removed observations | 399 |
| Final observations | 29,601 |
| Input features | 23 |
| Default rate | 22.3% |
| Target | Default next month (0 = No, 1 = Yes) |

## Project Methodology

### 1. Article Reproduction
The reproduction follows the main steps described in the paper:
* Remove undocumented categorical values.
* Split the data into 80% training and 20% testing (Stratified).
* Standardize the features using `StandardScaler` (fitted only on training data to avoid leakage).
* Apply random oversampling using `resample` to balance the training data.
* Train and evaluate Decision Tree, KNN, and SVM models using the parameters reported in the paper.

### 2. Group Contribution (Logistic Regression)
To fulfill the course requirements and improve the original methodology, our group introduced **Logistic Regression** as a fourth model. 
* We explicitly created, tuned, trained, and evaluated this model on the same balanced dataset. 
* We utilized `GridSearchCV` with Stratified 3-Fold cross-validation to find the best regularization parameter (`C=0.01`).
* Our goal was to test if a simpler, probabilistic linear model could identify more actual default cases (maximize Recall) compared to the article's models.

## Results

## The project has two main goals:

1. Reproduce Decision Tree, K-Nearest Neighbors (KNN), and Support Vector Machine (SVM) using the methodology and best parameters reported by the paper.
2. Add Logistic Regression as the group's classification contribution and compare it fairly with the reproduced models.

## Research Questions

- Can the main workflow and results of the selected paper be reproduced?
- Which of the three published models performs best for the default class?
- What additional insight does Logistic Regression provide when it uses the same cleaned data and test set?

## Dataset

The project uses the [Default of Credit Card Clients dataset](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) from the UCI Machine Learning Repository, dataset ID 350.

The records describe credit card clients from Taiwan and include credit limits, demographic variables, payment status, bill amounts, previous payment amounts, and the next-month default target.

| Item | Value |
|---|---:|sa
| Removed undocumented rows | 399 |
| Final observations | 29,601 |
| Input features | 23 |
| No-default clients | 22,996 (77.7%) |
| Default clients | 6,605 (22.3%) |
| Target | Default next month: 0 or 1 |

The 399 rows were removed because they contained undocumented values in `EDUCATION` or `MARRIAGE`, following the cleaning rule used in the selected paper.

## Methodology

The reproduction follows these steps:

1. Load the local Excel dataset, with UCI dataset ID 350 as an online fallback.
2. Remove the `ID` column.
3. Remove undocumented `EDUCATION` and `MARRIAGE` values.
4. Create a stratified 80% training and 20% testing split.
5. Fit `StandardScaler` only on the training data.
6. Apply random oversampling only to the training data.
7. Train Decision Tree, KNN, and SVM with the best parameters reported by the paper.
8. Evaluate accuracy, precision, recall, F1-score, and confusion matrices for the default class.

A fixed random state of `42` is used because the paper does not report its original train-test split seed. Small differences from the published results are therefore expected.

## Article Models

| Model | Best parameters reported by the paper |
|---|---|
| Decision Tree | `criterion='entropy'`, `max_depth=None`, `max_features=9`, `splitter='best'` |
| KNN | `n_neighbors=1`, `metric='euclidean'`, `weights='uniform'` |
| SVM | `kernel='rbf'`, `C=10` |

## Group Contribution: Logistic Regression

Logistic Regression was added as a fourth binary classification model. It was implemented separately from the three reproduced article models so the contribution is easy to identify in the notebook.

The group tested:

- `C = [0.01, 0.1, 1, 10, 100]`
- `solver='liblinear'`
- `max_iter=3000`
- Three-fold stratified cross-validation
- Default-class F1-score as the selection metric

The best configuration used `C=0.01`.

## Final Results

| Role | Model | Accuracy | Precision | Recall | F1-score |
|---|---|---:|---:|---:|---:|
| Published in paper | Decision Tree | 0.740 | 0.420 | 0.410 | 0.410 |
| Published in paper | KNN | 0.730 | 0.400 | 0.380 | 0.390 |
| Published in paper | **SVM** | **0.760** | **0.480** | 0.580 | **0.520** |
| Our reproduction | Decision Tree | 0.735 | 0.404 | 0.399 | 0.401 |
| Our reproduction | KNN | 0.723 | 0.379 | 0.377 | 0.378 |
| Our reproduction | **SVM** | **0.757** | **0.464** | 0.566 | **0.510** |
| **Group contribution** | **Logistic Regression** | 0.696 | 0.390 | **0.645** | 0.486 |

### Contribution Compared with Reproduced SVM

| Metric | Reproduced SVM | Logistic Regression | Change |
|---|---:|---:|---:|
| Accuracy | 0.757 | 0.696 | -0.062 |
| Precision | 0.464 | 0.390 | -0.074 |
| Recall | 0.566 | 0.645 | **+0.079** |
| F1-score | 0.510 | 0.486 | -0.024 |

SVM remained the best balanced model according to F1-score. Logistic Regression did not improve the best overall F1-score, but it improved recall by `0.079`. This means it identified a larger proportion of clients who actually defaulted, while also producing more false positives.

## Limitations

- The dataset represents clients from one Taiwanese bank and an older historical period.
- Random oversampling repeats minority-class observations and may increase overfitting.
- The project does not include probability calibration or a financial cost matrix.
- The models were not evaluated on a second credit-risk dataset.
- The final predictions should not be used alone for automatic credit decisions.

## Future Work

- Test Random Forest, XGBoost, and neural networks.
- Perform a broader hyperparameter search with cross-validation.
- Compare SMOTE, class weighting, and other sampling strategies.
- Adjust the classification threshold according to the bank's business objective.
- Evaluate the financial costs of false positives and false negatives.
- Improve interpretability and identify the variables that contribute most to default predictions.
- Test the methodology on newer data or another credit-risk dataset.
- Create a controlled application for practical model testing.

## Instructions on How to Run the Code
1. **Clone the repository** to your local machine or download it as a ZIP file.
2. **Install the required Python libraries** using pip: `pip install pandas numpy matplotlib seaborn scikit-learn ucimlrepo xlrd`
3. **Verify data location:** Ensure that the dataset file (`default_of_credit_card_clients.xls` or `.csv`) is placed inside the `data/` folder. (If the file is missing, the code will automatically attempt to fetch it from the UCI repository).
4. **Open the Notebook:** Open the file `DS301_Final_Project_credit_default.ipynb` (located inside the `models/` folder) using Jupyter Notebook, JupyterLab, or Google Colab.
5. **Execute the code:** Run all cells sequentially from top to bottom. Note that the Support Vector Machine (SVM) training cell and the `GridSearchCV` process for Logistic Regression may take a few minutes to complete.

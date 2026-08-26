# DS 301 Final Project: Credit Card Default Prediction

## Team Members
* Chung Vong (Simon)
* Maria
* Eduardo
* Gabriel

## Resources
* **Research Paper:** [Credit Default Mining Using Combined Machine Learning and Heuristic Approach](https://thomshu.github.io/ThomsonPorfolio.github.io/Media/MLArticle.pdf)
* **Dataset:** [UCI Default of Credit Card Clients](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients)
* **Canva Presentation:** https://canva.link/el13qjq8yakgjbr

## Project Overview

This project predicts whether a credit card client will default on the next monthly payment. It was developed for the **DS 301 Final Project** and follows a classification research paper using the public **Default of Credit Card Clients** dataset from the UCI Machine Learning Repository.

The project has two main goals:

1. Reproduce the methodology and main results presented in the research article.
2. Improve the original methodology while keeping the same dataset and model families.

The models compared are:

- Decision Tree
- K-Nearest Neighbors (KNN)
- Support Vector Machine (SVM)

  ## Repository Structure and Components
* `data/` : A folder containing the dataset file (`default-of-credit-card-clients.csv`).
* `models/` : A folder containing our Jupyter Notebook (`DS301_Final_Project.ipynb`) with all the ML modeling work, including data preprocessing, feature scaling, baseline reproduction (KNN), and our contributions (SMOTE, Logistic Regression, Tuned Decision Tree).
* `Project Report.pdf` : A detailed project report outlining our motivation, methodology, challenges, and significant improvements.

## Research Paper

**Title:** *Predicting Default of Credit Card Clients Using Three Supervised Machine Learning Algorithms*

**Authors:** Thomson Ly, Rene Schuller, Katarina Simanic, and Sukhpreet Singh  
**Institution:** University of Windsor

The article investigates two main questions:

- Which hyperparameters have the strongest impact on each model?
- Which supervised machine learning model is the most effective for predicting credit card default?

The article concluded that SVM produced the best result among the three models. However, it also reported that the F1-score for predicting default clients was still relatively low.

## Dataset

The project uses the [Default of Credit Card Clients dataset](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) from the UCI Machine Learning Repository.

The dataset contains credit card information collected from clients in Taiwan. Its variables include:

- Credit limit
- Age and demographic information
- Payment status from previous months
- Monthly bill amounts
- Previous payment amounts
- Default status for the next month

### Dataset Summary

| Item | Value |
|---|---:|
| Original observations | 30,000 |
| Removed observations | 399 |
| Final observations | 29,601 |
| Input features | 23 |
| Default rate | 22.3% |
| Target | Default next month: 0 or 1 |

The 399 observations were removed because they contained undocumented values in the `EDUCATION` or `MARRIAGE` variables, following the cleaning process described in the article.

## Project Methodology

### Article Reproduction

The reproduction follows the main steps described in the paper:

1. Remove the ID column and undocumented categorical values.
2. Split the data into 80% training and 20% testing.
3. Standardize the features using `StandardScaler`.
4. Apply random oversampling to the training data.
5. Use 3-fold `GridSearchCV` to tune each model.
6. Evaluate the models using accuracy, precision, recall, F1-score, and confusion matrices.

The article's hyperparameter search includes:

- **Decision Tree:** criterion, splitter, maximum depth, and maximum number of features.
- **KNN:** number of neighbors, weights, and distance metric.
- **SVM:** kernel type and the regularization parameter `C`.

The complete article reproduction requires **6,156 model fits**:

- Decision Tree: 5,796 fits
- KNN: 342 fits
- SVM: 18 fits

## Group Contribution

Our contribution improves the original evaluation process without changing the dataset or the three model families.

### 1. One-Hot Encoding

The variables `SEX`, `EDUCATION`, and `MARRIAGE` are treated as categorical features instead of continuous numerical values. This was also suggested as future work in the article.

### 2. Fold-Safe Oversampling

In the improved version, oversampling happens inside each cross-validation training fold. This reduces the risk of data leakage between training and validation data.

### 3. F1-Focused Model Selection

The article selects hyperparameters mainly using accuracy. Our improved version uses the default-class F1-score because the dataset is imbalanced and the default class is the most difficult class to predict.

### 4. Additional Hyperparameters

The improved experiments also evaluate parameters such as minimum samples per leaf, class weights, additional K values, and SVM gamma settings.

## Results

### Default-Class F1-Score

| Model | Article | Our Reproduction | Improved Method |
|---|---:|---:|---:|
| Decision Tree | 0.410 | 0.392 | **0.523** |
| KNN | 0.390 | 0.380 | **0.469** |
| SVM | 0.520 | 0.514 | **0.534** |

Our reproduction follows the same general pattern as the article: **SVM is the strongest model**. The small differences are expected because the article does not provide its random seed or every implementation detail.

### Improved Method Results

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---:|---:|---:|---:|
| Decision Tree | 0.768 | 0.483 | 0.572 | 0.523 |
| KNN | 0.681 | 0.373 | **0.632** | 0.469 |
| SVM | **0.776** | **0.498** | 0.575 | **0.534** |

### Main Result Highlights

- SVM remained the strongest overall model.
- The reproduced SVM obtained accuracy of approximately 0.760 and F1-score of 0.514.
- The improved SVM increased the F1-score to 0.534.
- Decision Tree showed the largest F1 improvement, increasing from 0.392 to 0.523.
- KNN achieved the highest recall, 0.632, but produced lower precision and accuracy.
- The improved method increased the default-class F1-score for all three models.

These results show that the best model depends on the project objective. KNN detects more default clients, while SVM provides a better overall balance between precision, recall, F1-score, and accuracy.

## Challenges

### Class Imbalance

Only around 22.3% of the clients are in the default class. Because of this imbalance, a model can have acceptable accuracy while still missing many clients who will default.

### Exact Reproduction

The article does not provide its random seed or every software and implementation detail. Therefore, our results are close to the published results but not exactly identical.

### Computational Cost

The original hyperparameter grids require thousands of model fits. SVM is especially expensive because it processes a large dataset with different kernels and values of `C`.

### Data Leakage Risk

Applying oversampling before cross-validation can allow repeated observations to appear in different folds. The improved pipeline addresses this problem by applying oversampling only inside each training fold.

### Metric Trade-Offs

Improving recall can create more false positives and reduce precision or accuracy. In a real financial project, the cost of each error would need to be considered before selecting the final model.

## Main Learnings

- Accuracy is not enough for an imbalanced classification problem.
- Precision, recall, and F1-score provide important information about the minority class.
- Preprocessing must be fitted only on training data to avoid data leakage.
- Oversampling should be included inside the cross-validation pipeline.
- Categorical variables should be encoded according to their real meaning.
- GridSearchCV helps compare hyperparameters systematically, but it can require significant computational time.
- The metric used during model selection should match the real objective of the project.
- Reproducing a scientific article does not always produce identical numbers. A clear and documented methodology is essential for explaining the differences.

## Team and Presentation Responsibilities

| Participant | Main Responsibility |
|---|---|
| Simon | Project motivation, research questions, and article overview |
| Gabriel | Dataset, cleaning, preprocessing, and reproduction workflow |
| Eduardo | Group contribution, hyperparameter tuning, and results |
| Maria | Challenges, learning points, conclusion, and Q&A |

## Repository Structure

```text
.
├── README.md
├── DS301_Final_Project.ipynb
├── DS301_Final_Project_Presentation.pptx
├── MLArticle.pdf
└── data/
    └── default_of_credit_card_clients.xls
```

## Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Imbalanced-learn
- UCI ML Repository package

## How to Run the Project

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <your-repository-folder>
```

### 2. Install the Required Packages

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn ucimlrepo xlrd jupyter
```

### 3. Start Jupyter Notebook

```bash
jupyter notebook
```

Open `DS301_Final_Project.ipynb` and run the cells in order.

> **Important:** The complete GridSearchCV process can take several minutes, especially for SVM. The notebook first tries to download the dataset from UCI and uses the local file in the `data` folder as a fallback.

## Limitations

- The dataset represents clients from one Taiwanese bank and one historical period.
- The article does not provide all details needed for an exact reproduction.
- Random oversampling can increase overfitting because it repeats minority-class observations.
- The project does not include probability calibration or financial cost analysis.
- The final F1-score is still moderate, so the model should not be used alone for automatic credit decisions.

## Future Work

- Compare standard scaling with min-max scaling.
- Test 5-fold cross-validation.
- Evaluate SMOTE and other imbalance-handling methods.
- Tune classification thresholds.
- Add probability calibration.
- Compare Random Forest, XGBoost, and neural networks.
- Create a financial cost matrix for false positives and false negatives.
- Test the methodology on a more recent credit-risk dataset.

## References

1. Ly, T., Schuller, R., Simanic, K., & Singh, S. *Predicting Default of Credit Card Clients Using Three Supervised Machine Learning Algorithms*. University of Windsor.
2. UCI Machine Learning Repository. [Default of Credit Card Clients](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients).

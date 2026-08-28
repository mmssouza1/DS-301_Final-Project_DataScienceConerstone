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

### Final Results at a Glance
| Role | Model | Accuracy | Precision | Recall | F1-Score |
|---|---|---:|---:|---:|---:|
| Published in article | SVM | 0.760 | 0.480 | 0.580 | 0.520 |
| Our reproduction | SVM | 0.757 | 0.464 | 0.566 | 0.510 |
| **GROUP CONTRIBUTION** | **Logistic Regression** | **0.696** | **0.390** | **0.645** | **0.486** |

### Main Result Highlights
- The reproduction supports the main finding of the selected article: SVM is the strongest of the three published models overall, achieving a reproduced F1-score of 0.510.
- However, our contributed **Logistic Regression model significantly improved Recall (0.645)** compared to the reproduced SVM (0.566). 
- This means Logistic Regression successfully identified more real default cases. In a financial context where missing a high-risk client is costly, this contribution is highly valuable, despite a slight drop in overall accuracy and precision.

## Challenges & Main Learnings
* **Class Imbalance:** Only 22.3% of clients default. Accuracy alone is misleading; precision, recall, and F1-score are critical.
* **Exact Reproduction:** The article did not report its random split seed, making exact numerical reproduction impossible (small variances are expected).
* **Metric Trade-Offs:** Oversampling and prioritizing Recall inherently increased false positives (lowering Precision). We learned that a new model can be valuable even if it doesn't produce the highest F1-score, depending on business priorities.
* **Data Leakage:** We ensured the `StandardScaler` was fitted strictly on the training set before testing.

## Team and Presentation Responsibilities
| Participant | Main Responsibility |
|---|---|
| Simon | Project motivation, research questions, and article overview |
| Gabriel | Dataset, cleaning, preprocessing, and reproduction workflow |
| Eduardo | Group contribution (Logistic Regression), hyperparameter tuning, and results |
| Maria | Challenges, learning points, conclusion, and Q&A |

## Repository Structure 
    .
    ├── README.md
    ├── Project Report.pdf
    ├── Project Presentation File.pdf
    ├── data/
    │   └── default_of_credit_card_clients.csv
    └── models/
        └── DS301_Final_Project_credit_default.ipynb

## Instructions on How to Run the Code
1. **Clone the repository** to your local machine or download it as a ZIP file.
2. **Install the required Python libraries** using pip: `pip install pandas numpy matplotlib seaborn scikit-learn ucimlrepo xlrd`
3. **Verify data location:** Ensure that the dataset file (`default_of_credit_card_clients.xls` or `.csv`) is placed inside the `data/` folder. (If the file is missing, the code will automatically attempt to fetch it from the UCI repository).
4. **Open the Notebook:** Open the file `DS301_Final_Project_credit_default.ipynb` (located inside the `models/` folder) using Jupyter Notebook, JupyterLab, or Google Colab.
5. **Execute the code:** Run all cells sequentially from top to bottom. Note that the Support Vector Machine (SVM) training cell and the `GridSearchCV` process for Logistic Regression may take a few minutes to complete.

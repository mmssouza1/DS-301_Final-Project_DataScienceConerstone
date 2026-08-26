# DS 301 Final Project: Credit Card Default Prediction

## Team Members
* Chung Vong (Simon)
* Maria
* Eduardo
* Gabriel

## Project Summary
This repository contains the code, dataset, and final report for our Machine Learning Classification project. The objective of this project is to predict potential credit card defaults. We successfully reproduced the machine learning baseline models from the research paper *"Credit Default Mining Using Combined Machine Learning and Heuristic Approach"* (Islam et al.). 

Furthermore, we provided significant contributions to the baseline methodology by addressing class imbalance using SMOTE and applying hyperparameter tuning (GridSearchCV) on classification models such as Logistic Regression and Decision Trees to heavily optimize the recall metric.

## Resources
* **Research Paper:** [Credit Default Mining Using Combined Machine Learning and Heuristic Approach](https://thomshu.github.io/ThomsonPorfolio.github.io/Media/MLArticle.pdf)
* **Dataset:** [UCI Default of Credit Card Clients](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients)

## Repository Structure and Components
* `data/` : A folder containing the dataset file (`default-of-credit-card-clients.csv`).
* `models/` : A folder containing our Jupyter Notebook (`Final_Project.ipynb`) with all the ML modeling work, including data preprocessing, feature engineering, paper reproduction, and our contributions.
* `Project Report.pdf` : A detailed project report outlining our motivation, methodology, challenges, and significant improvements.
* `Project Presentation File.pdf` : The presentation slides summarizing our findings and learning outcomes.

## Instructions on How to Run the Code
1. Clone or download this repository to your local machine.
2. Ensure that you have the dataset named `default-of-credit-card-clients.csv` placed exactly inside the `data/` folder.
3. Install the required Python programming libraries (if not already installed): `pandas`, `numpy`, `scikit-learn`, and `imblearn`.
4. Open the `Final_Project.ipynb` file located in the `models/` folder using Jupyter Notebook, Google Colab, or any compatible Python environment.
5. Run all the cells sequentially from top to bottom. The code is fully structured to automatically execute data preprocessing, followed by the paper reproduction models, and finally our contributed models.

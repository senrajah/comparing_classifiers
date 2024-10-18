# Comparing Classifiers
 My goal is to compare the performance of the classifiers (k-nearest-neighbors, logistic regression, decision trees, and support vector machines). I will use a dataset related to the marketing of bank products over the telephone. 

The notebook can be located below
https://github.com/senrajah/comparing_classifiers/blob/main/comparing_classifiers_bank.ipynb

### Business Objective  

The business objective consist of leveraging the dataet supplied by a portuguese bank regarding past direct marketing campaign. Using this dataset of 17 campaigns and over 79,354 contacts, our goal is create a model capable of predicting the success of marketing campaign. The success in this case is define as the number of people accepting to purchase the product (a long-term deposit with good interest rates).  

To do so, we will compare the classification methods of:  
- K-nearest neighbors (KNN)
- Logistic Regression (LR)
- Decision Trees (DT)
- Support Verctor Machines (SVM)

### Building the models

First we developed a baseline model with a dummyClassifier just to set a benchmark.

Then we built 4 different models with 4 different classifiers without any specific paramters, so that they use their defaults. We produced their fit time, train accuracy, test accuracy, ROC score, etc so as to see how those simple model performed.

Now the third steps is to use their hyperparamters and CV techniques to fine tune all the 4 classifier by using several params and check their output of fit time, train accuracy, test accuracy, ROC score etc.

After building the models with different set of parameters then we get the best parameters for each model and compare their results.

### Scoring the Model

Before beginning our exploration of various models, it is important to define the criterias we will monitor and compare for our final conclusion. To do so, we will explore the various scoring track during our exploration.  

As referred in the paper 'Using Data Mining for Bank Direct Marketing: An Application of the CRISP-DM Methodology' by Moro, S. & Laureano, M.S. The AUC_ROC offers a great way to track the performance of our model in our business context. The AUC plots the False Positive Rate (FPR) versus the True Positive Rate (TPR). This measure will allow to track the number of clients the model miss identified as purchasers of the product (false positive) while maximizing the real buyers of the product. In the business context, such approahc makes sense as you are looking to limit the resources spent on non-buyers hence you are hoping to have a low FPR to maximize your campaigns profitability.  

In addition, we will track the Accuracy, F1, Precision and Recall to better understand the overall performance of each model. To understand the cost behind each model, we will also collect the run time of each model to better track the tradeoff of accuracy vs time.

| Model         | ROC AUC   | Accuracy | F1       | Precision | Recall   | Fit Time  |
|---------------|-----------|----------|----------|-----------|----------|-----------|
| Baseline_Model| 0.5       | 0.887594 | 0.0      | 0.0       | 0.0      | 0.0s      |
| Simple_lgr    | 0.656887  | 0.887594 | 0.0      | 0.0       | 0.0      | 0.07s     |
| knn           | 0.574829  | 0.877317 | 0.105077 | 0.291803  | 0.064075 | 0.0s      |
| svm           | 0.554438  | 0.887756 | 0.008578 | 0.6       | 0.00432  | 110.95s   |
| dtree         | 0.57565   | 0.863154 | 0.129696 | 0.227437  | 0.090713 | 0.18s     |
| grid_lgr      | 0.65536   | 0.600388 | 0.258113 | 0.163091  | 0.618431 | 0.88s     |
| grid_knn      | 0.595757  | 0.88549  | 0.070913 | 0.402985  | 0.038877 | 138.61s   |
| grid_svm      | 0.59053   | 0.768    | 0.340909 | 0.258621  | 0.5      | 59.96s    |
| grid_dtree    | 0.642184  | 0.887756 | 0.067249 | 0.510204  | 0.035997 | 452.65s   |

### Summary Findings

It is important to note that the data at hand was class imbalanced with approximately 89% of 'no' and 11% of 'yes'. Considering this fact, we saw the best model to be the logistic regression and decision tree respectively. Furthermore, the SVM was only performed on a subset of of 5,000 observations since it required tremendous amounts of run time to perform a grid search analysis. To ensure comparative models, I employed Gridsearch to optimize the parameters at hand of each model. 

Overall, I would select a logistic regression as a predictive model. Although not perfect, it improves the chances of accurately identifying product purchasers for the telemarketing campaign. Its AUC_ROC was of 65% and an F1 score of 25%. As mentioned the runner up was the decision tree with an AUC_ROC of 64.7% but an F1 score of 4.5% and a much higher run time.


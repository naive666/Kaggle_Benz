# Kaggle_Benz
A Summary For Kaggle Featured Prediction Competition: Mercedes-Benz Greener Manufacturing


[![license](https://img.shields.io/github/license/:user/:repo.svg)](LICENSE)
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

## Table of Content

- [Background](#background)
- [ML_Model 1](#ml-model-1)
- [ML_Model 2](#ml-model-2)
- [DP_Model]()
- [Results]()
- [Summary]()
- [Contributor]()
- [License]()

## Background
[Mercedes-Benz Greener Manufacturing](https://www.kaggle.com/c/mercedes-benz-greener-manufacturing/overview) is a Kaggle featured competition held two years ago with $25,000 prize money. The contestants were asked to make predictions based on the given datasets. The [train](/data/train.csv) dataset contains 4209 examples and 378 features each. Only less than 10 features are categorical, and the remainings are sparse features, and moreover none of the features has NaN or outliers, which is a good chance for practicing. Following the same data distribution, the [test](/data/test.csv) set has also 4209 blanks that need to predict. In this repository, I will show three models applying different methods to reduce feature dimensions and make predictions. The best model is the second one, which scores 0.54998 of R2_score in the final private leaderboard.


## ML Model 1
[This](/ML_Model_1) model use Random Forest Regressor to reduce the feature dimensions. The followings are brief summary of this method.
- [Feature Selection](/ML_Model_1/data_review.ipynb)
  - Set total epoch number to 3000
  - Use KFold to do cross validation in each epoch
  - Randomly pick up 10 features from the entire feature sets with bootstrap for each epoch
  - Use these 10 features to train, then record the r2_score of each epoch
  - Record the feature importance of each feature in every epoch
  - Select the top 5 features for each epoch and store the feature importance in an array of shape (epoch, 5) 
  - After finishing first 30 epochs, judge if the r2_score is higher than the average of previous 30 epoch, if true, record this epoch, otherwise omit it
  
- [Model](/ML_Model_1/model.ipynb) 
  - Use pd.factorize() to encoder the categorical features. One can also use labelencoder to get the same result
  - Use GridSearch to train Random Forest Regressor and XGBoost models
- [Result](/ML_Model_1/model_result)
  - Score 0.52 in private leaderboard.
- [Submission](/ML_Model_1/my_submission1.csv)

- Summary
  -  This model could be improved by the following aspects:
    - The Random Forest Regressor parameters could be tune
    - I factorize the categorical features first, then use model to selecting features
    - In each epoch, select over 10 features
    - I could try more than 7 features in the predict models

- Warning
  - After finishing this model, I found I made several mistakes. Since most features are encoded by 0 and 1, it is reasonable to guess some columns together represents one feature(This is like our factorize process). In order to correct the mistake, the second method comes up
  
## ML Model 2
[This](/ML_Model_2) model does not apply sophisticate feature reduction methods, it uses tsvd, pca, FastIca to select 12 features.
- [Model](/ML_Model_2/feature_selection3.ipynb)
  - Concat train data and test data
  - Use LabelEncoder to transfer categorical features to numerical
  - Use tsvd, pca, FastIca to choose 12 features respectively, be careful that pca is not a good choice for spase data since it need centralize.
  - Create a stacked model composited by one Lasso, one gradient boost regressor and one Lasso to do final prediction.
  - Create another model of XGBoost
  - Train the selected 12 features to XGBoost and the stacked model respectively
  - Calculate the R2 score
  
- Result
  - Unfortunately, XGBoost model get 0.39 while the stacked model scores 0.45, neither is a good score. It seems I should not reduce the features so much. 

- [Revised Model](/ML_Model_2/feature_selection4.ipynb)
  - Since most of our features are sparse, I should try not to reduce the feature, just use the original entire features. Let's look at what happen.
  - Model
    - Concat train data and test data
    - Use LabelEncoder to transfer categorical features to numerical
    - Create the same stacked model, and use this to train.
    - Calculate the R2 Score

- Result
  - Bravado! I get 0.5498 in final private leaderboard which approaches top 100 in this competition! 
  
- [Submission](/ML_Model_2/my_submission2.csv)

- Summary 
  - It seems plausible that feature reduction has negative effect to the result. I guess this is because most features are sparse in this competition which means several particular columns represent one feature in the original dataset. Since the sparsity, it will not take too much space while runing the model. However, in the general cases one should do feature reduction
  
## Deep Learning Model







# Kaggle_Benz
A Summary For Kaggle Featured Prediction Competition: Mercedes-Benz Greener Manufacturing


[![license](https://img.shields.io/github/license/:user/:repo.svg)](LICENSE)
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

## Table of Content

- [Background](#background)
- [ML_Model 1](#ml-model-1)
- [ML_Model 2]()
- [DP_Model]()
- [Results]()
- [Summary]()
- [Contributor]()
- [License]()

## Background
[Mercedes-Benz Greener Manufacturing](https://www.kaggle.com/c/mercedes-benz-greener-manufacturing/overview) is a Kaggle featured competition held two years ago with $25,000 prize money. The contestants were asked to make predictions based on the given datasets. The [train](/data/train.csv) dataset contains 4209 examples and 378 features each. Only less than 10 features are categorical, and the remainings are sparse features, and moreover none of the features has NaN or outliers, which is a good chance for practicing. Following the same data distribution, the [test](/data/test.csv) set has also 4209 blanks that need to predict. In this repository, I will show three models applying different methods to reduce feature dimensions and make predictions. The best model is the second one, which scores 0.54998 of R2_score in the final private leaderboard.


## ML Model 1
[This]() model use Random Forest Regressor to reduce the feature dimensions. The followings are brief summary of this method.
- Feature Selection
  - Set total epoch number to 3000
  - Use KFold to do cross validation in each epoch
  - Randomly pick up 10 features from the entire feature sets with bootstrap for each epoch
  - Use these 10 features to train, then record the r2_score of each epoch
  - Record the feature importance of each feature in every epoch
  - Select the top 5 features for each epoch and store the feature importance in an array of shape (epoch, 5) 
  - After finishing first 30 epochs, judge if the r2_score is higher than the average of previous 30 epoch, if true, record this epoch, otherwise omit it
  
 - Model 
  - Use pd.factorize() to encoder the categorical features. One can also use labelencoder to get the same result
  - Use GridSearch to train Random Forest Regressor and XGBoost models

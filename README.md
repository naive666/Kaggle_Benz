# Kaggle_Benz
A Summary For Kaggle Featured Prediction Competition: Mercedes-Benz Greener Manufacturing


[![license](https://img.shields.io/github/license/:user/:repo.svg)](LICENSE)
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

## Table of Content

- [Background](Background)
- [ML_Model 1]()
- [ML_Model 2]()
- [DP_Model]()
- [Results]()
- [Summary]()
- [Contributor]()
- [License]()

## Background
[Mercedes-Benz Greener Manufacturing](https://www.kaggle.com/c/mercedes-benz-greener-manufacturing/overview) is a Kaggle featured competition held two years ago with $25,000 prize money. The contestants were asked to make predictions based on the given datasets. The [train]() dataset contains 4209 examples and 378 features each. Only less than 10 features are categorical, and the remainings are sparse features, and moreover none of the features has NaN or outliers, which is a good chance for practising. Following the same data distribution, the [test]() set has also 4209 blanks need to predict. In this respository, I will show three models applying different methods to reduce feature dimensions and make predictions. The best model is the second one, which scores 0.54998 of R2_score in the final private leaderboard.


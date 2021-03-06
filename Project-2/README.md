# Project 2 - Ames Housing Data and Kaggle Challenge

## Problem Statement

There are many variables involved when predicting the price of a house on sale. However there are many features present and some might be more important than others in predicting house price.

Using the Ame Housing Dataset for individual residential properties sold from 2006 to 2010 and with 70 columns of different features relating to houses, we are creating a suitable regression model that will predict the price of a house in Ame and find the top features.

This is done by using the train.csv and test.csv dataset from DSI Kaggle Competition and comparing the RMSE scores from the different regression models.The final model chosen can be used to help buyers, sellers and real estate agents predict house price in Ames, Iowa.

## Executive Summary

- Data cleaning
- Columns are sorted into Categorical, Ordinal and Continuous types.
- Exploratory Data Analysis on 70 features and elimination by inference using data visualization.
- Use Regression models to predict 'SalePrice' of residential properties from train.csv and test.csv
- Use best regression model for Kaggle Competition

### Contents:

**A. Data Cleaning & EDA notebook Contents:**
1. Standard Imports
2. Data Import for train.csv
3. Data Import for test.csv
4. Data Cleaning for train dataset
5. Data Cleaning for test dataset
6. Sorting the columns into Continuous or (Categorical & Ordinal)
7. Addressing outliers
8. Continuous Variables EDA & Inference
9. Categorical & Ordinal Variables EDA & Inference
10. Adding 'age of house' column
11. Mapping values to Ordinal columns
12. Choosing Features based on inference from EDA
13. Export data for cleaned train and test dataset

**B. Preprocessing & modelling notebook Contents:**
1. Standard Imports
2. Data Import for train & test data
3. Splitting train dataset into train & holdout sets
4. Preprocessing X_train with StandardScaler & pd.get_dummies
5. Preprocessing X_test with StandardScaler & pd.get_dummies
6. Baseline Score
7. Cross validation & Linear Regression
8. LassoCv & Lasso Regression on holdout set
9. RidgeCv & Ridge Regression on holdout set
10. Comparing RMSE of different Regression models on holdout set
11. Preprocessing on train set
12. Fit the entire Train set and predict the Test set
13. Create Submission to Kaggle
14. Result Obtained from Kaggle Submission
15. Conclusions
16. Recommendations

## Data Dictionary
[Provided Data Dictionary](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)

## Conclusions:
- The above chosen variables can estimate the prediction of 'SalePrice' with a RMSE of 30591 usd
- Exploratory Data Analysis helps to eliminate obvious variables that do not help in predicting 'SalePrice' by visual inference
- There is a balance between how many Outliers should be removed or stay in the dataset, they will affect prediction of 'SalePrice' and the unseen data might have outlier datapoints too.
- Even though Ordinal columns are categorical, they can be mapped with values to show order and be used in Standard Scaling to reflect relationship to each other
- Lasso & Ridge Regression introduce regularization and helps avoid overfitting like the Linear Regression.
- Lasso Regression produced a better RMSE score that Ridge Regression as Lasso will shrink the unimportant features to 0, this minimises RMSE.

## Recommendations:
- Interested buyers may use this model to predict the estimate 'SalePrice' for houses in Ames.
- Sellers may use this model to predict how much they can offer their houses for sale.
- In addition, Real estate agents can estimate which features contribute to 'SalePrice' and may provide advice to to buyers/sellers why that house is priced at that estimated value.

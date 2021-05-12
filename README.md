# General Assembly Projects

### Project 1: SAT & ACT Participation Analysis
<br>`pandas | numpy | matplotlib | seaborn`
 - Used the above Python packages to conduct Exploration Data Analysis to analyse the participation rates and scores in different USA states.
 - Provided recommendations to improve participation rates based on insights generated from datasets


### Project 2: Predicting Housing Prices with Regression
<br>`pandas | numpy | matplotlib | seaborn | sklearn`

 - Visual inference from Exploratory Data Analysis help eliminate features that do not help in predicting continuous labels (‘SalePrices’).
 - Different regression models are used for continuous prediction. Lasso Regression was the best regression model in this project with a Root Mean Square Error (RMSE) of 30591 usd.

### Project 3: Classification & Natural Language Processing of Subreddit thread
<br>`pandas | numpy | matplotlib | seaborn | sklearn | nltk | beautifulsoup | wordcloud`

 - Two subreddit threads r/harrypotter and r/FantasticBeasts are scrapped from Reddit using a Reddit API.
 - Text data is cleaned using various Natural Language Processing (NLP) packages.
 - WordClouds were generated to observe frequency of word occurrence.
 - Different Classification models are used to classify the Two subreddit threads based on ‘bag-of-words’ model.
 - Random Forest Classifier with CountVectorizer was the best classification model as it has the lowest difference between train and test set, meaning it can generalise well to unseen data.

### Project 4: Kaggle Competition on West Nile Virus Prediction
<br>`pandas | numpy | matplotlib | seaborn | sklearn | SMOTE`
 - This is a group project.
 - There are 3 datasets provided in this Kaggle Competition.
 - Data cleaning is done and only 2 out of the 3 dataset were merged as the remaining dataset were not conclusive in observing any relationship with the prediction task
 - Visual inference from Exploratory Data Analysis helped to identify important features and further feature engineering were conducted.
 - SMOTE/ADASYN the dataset as there were imbalanced classes for this binary classification
 - Random Forest Classifier with ADASYN was the best classification model as it has the lowest difference between train and test set, meaning it can generalise well to unseen data.


### Capstone Project: Text Generation & Classification of Coursera reviews
<br>`pandas | numpy | matplotlib | seaborn | sklearn | keras | nltk | spaCy | textblob | google_trans_new | wordcloud | Google Colab`
 - Language of the text data is detected using spaCy and translated using google_trans_new.
 -  Text data is cleaned using various Natural Language Processing (NLP) packages.
 - WordClouds were generated to observe frequency of word occurrence.
 - Different Classification models are used to classify ratings of reviews based on ‘bag-of-words’ model.
 - Multinomial Naïve Bayes model was the best classification model as it showed the lowest fall-out rate at 46.7% .
 - Character-based text generation is conducted using different Recurrent Neural Networks(RNN)
 - Different type of model topology and RNN type are used to compare accuracy scores of models and how coherent the text generated was
 - RNN model with 2 Long short-term memory (LSTM) layers with a Dropout of 0.2 is the best RNN model as it was the most coherent and highest accuracy with 71.9% on test data

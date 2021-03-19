## Project 3: Reddit Classifier Project 🧙

### Problem Statement 
Harry Potter began as a series of seven fantasy novels by J. K. Rowling and later expanded into a multimedia franchise. The multimedia franchise includes eight fantasy films, video games and themed attractions that have found commercial success worldwide. Following the release of another spin-off book and new film franchise- Fantastic Beasts and Where to Find Them, the franchise as a whole has been rebranded as Wizarding World.

In this project, we attempt to find out if there are distinct fandoms for the different book series by classifying 2 subreddits `r/harrypotter` and `r/FantasticBeasts` based on their posts. If there is a distinct fandom for FantasticBeasts too, this shows there are business opportunities to grow revenue in developing merchandise, themed attractions etc... for FantasticBeasts fandom too!

### Executive Summary 
In this project, r/harrypotter and r/FantasticBeasts posts are scrapped using Reddit API.The Reddit API will scrap 25 posts per request. To obtain sufficient data, a for loop is used in the Reddit API and time.sleep() function at the end of your loop to allow for a break in between requests. From the JSON format from reddit, the data are converted to Pandas DataFrame and then saved as a csv files to run in this Jupyter Notebook.

Now the reddit posts are organised as a structured data. Many information are obtained from this scrap like userid, timing of scrapping post, date of post, selftext (which are posts) and titles. Columns like 'title', 'selftext' and 'subreddit' are chosen from the dataframe. 'title' and 'selftext' contain the text data which will contain words in identifying the subreddit. 'subreddit' is the name of the `r/harrypotter` and `r/FantasticBeasts` thread and will be mapped to 1 and 0 respectively, this is our target array and what we are trying to accurately classify.

The 'title' and 'selftext' columns are 'combined'. If there are duplicated 'combined' posts and there are insufficient words in the 'combined' posts, these rows will dropped. Hyperlink is removed from the 'combined' posts and they are plotted on WordClouds - visual representations of words that give greater prominence to words that appear more frequently. This provides a visual signal of which words may help in classifying the different subreddit. `r/harrypotter` and `r/FantasticBeasts` posts are then combined into 1 dataframe and split into random train and test subsets using train_test_split. Further data cleaning is done to convert into lowercase words, remove symbols and digits, generate the root form of the inflected words using stemming.

Pipelines consisting of either a CountVectorizer or TfidVectorizer(preprocessors that convert text data into numerical data) and a Classification algorithm are used. Each pipeline run through GridSearchCV to find the best parameters from the range of parameters chosen. The model with the best parameters is fit with train set and predicted with test set.

There are different metrics for establishing the best classification for this project. For this project, accuracy score of the train set, accuracy score of the test set, differences in the accuracy score between train & test set and the sensitivity are considered. Differences in the accuracy score between train & test set refer to how well the model can generalise to unseen data. There were many Classification Algoritms considered for example, Logistic Regression, KNN Classifier, Multinomial Naive Bayes Classification, Bagging Classifier, Random Forest Classifier and Extra Trees Classifier.

Based on the above considerations, **Random Forest Classifier and Countvectorizer** showed the highest sensitivity 88.6% and better ability to generalise to unseen data compared to other models, the delta between train and test accuracy score is 5.6%. Hence, through the **Random Forest Classifier and Countvectorizer** model there is a sensitivity of 88.6% in classifying the `r/harrypotter` and `r/FantasticBeasts` subreddits. The fandom in `r/FantasticBeasts` are distinct from `r/harrypotter` and there are opportunities to market specific merchandise to this fandom and grow revenue.

### Data Dictionary 
* data dictionary in df.csv dataset with both `r/harrypotter` and `r/FantasticBeasts` posts

|column   | data type  | description  | ||
|---|---|---|---|---|
| subreddit  | int64  | 1 for harrypotter subreddit and 0 for FantasticBeasts subreddit |  || 
| combine  |  str |  texts in the subreddit posts and title | ||

### Conclusion &  Recommendation 

#### A. Based on models

`1. Best Model - Random Forest Classifier with CountVectorizer(preprocessing)`
Based on sensitivity, which is True Positive/(True Positive + False Negative), Random Forest Classifier with CountVectorizer(preprocessing) has the highest sensitivity in classifying the `r/harrypotter` from `r/FantasticBeasts`.
In addtion, this model has the lowest difference in accuracy score('delta' column) between train data and test data which is the unseen data, this means the model can generalise to unseen data compared to other models.
Random Forest Classifier splits on the largest drop in gini impurity for classification

`2. Overfitting - K-Nearest Neighbors & Bagging Classifier`
These models have the largest difference in accuracy score('delta' column) between train data and test data.
The accuracy score on train set are 0.99 which shows signs of overfitting. So even though accuracy score is high on train set, these models did not perform well on test set/unseen data.
They have low bias and high variance based on the scores

`3. Logistic Regression & Multinomial Naive Bayes`
These models also show high sensitivity but did not perform as well as Random Forest Classifier with CountVectorizer(preprocessing)

`4. Extra Trees Classifier`
This model showed better performance with preprocessor Countvectorizer than with Tfidvectorizer. But this might be because it builds multiple trees and splits nodes using random subsets of features and nodes are split on random splits, not best splits on based on the largest drop in gini impurity.

#### B. Based on preprocessor
In comparing CountVectorizer and TfidVectorizer, both convert text data into vectors.From the above scores, it does not show if CountVectorizer or TfidVectorizer is better or significant in impacting the specificity, accuracy score as compared to the Classification ML Algorithms.


#### To further improve accuracy of **Random Forest Classifier with CountVectorizer(preprocessing)** model:
- increase the stop words
- optimize by tuning the model futher with different hyperparameters
- find out words that contribute to misclassified predictions, the False Positives and False Negatives

The fandom in `r/FantasticBeasts` are distinct from `r/harrypotter` and there are opportunities to market specific merchandise to FantasticBeasts fandom and grow revenue.

### Sources:
 - [`/r/harrypotter`](https://www.reddit.com/r/harrypotter)
 - [`/r/FantasticBeasts`](https://www.reddit.com/r/FantasticBeasts)

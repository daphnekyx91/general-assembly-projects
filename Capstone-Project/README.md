# Problem Statement

Coursera is a massive open online course (MOOC) platform that offers online courses, certifcations in collaboration with other recognised universities and business organisations. As the courses are conducted online, they are highly accessible to students around the world. 

There has been a surge in MOOC participation and service providers, and the MOOC industry is forecasted to reach USD 18925.18 million and 100 million learners by 2026. With the rise of the 4th Industrial revolution, more employers are upgrading their skillsets to deal with the ever-changing technological disruption in their industries. In addition, due to the unfortunate outbreak of Covid-19 in 2020, momentum towards online learning as exponentially grown as it reduces the risk associated with in-person teaching.

As MOOCs are conducted remotely, feedback from the course content are in the form of `rating` and `reviews` submitted by students.
In this project, we attempt to analyse what are the `reviews` that leads to the different `rating` *(For example, why did this reviewer rate 5(highest)) but the other reviewer rate less than 5* and find the best classification models that can classify submitted `reviews` to their corresponding `rating`.From understanding what words help to classify 5.0 rating, we can improve MOOC satisfaction.

In addition, this project also attempt to generate fake positive reviews using Recurrent Neural Network.

# Data Dictionary

| Column       | Data Type | Description                                                                     |   |   |
|--------------|-----------|---------------------------------------------------------------------------------|---|---|
| name         | object    | Course name                                                                     |   |   |
| institution  | object    | Institution or Organisation offering the course                                 |   |   |
| course_url   | object    | Course URL                                                                      |   |   |
| course_id    | object    | Course ID                                                                       |   |   |
| reviews      | object    | Course review                                                                   |   |   |
| reviewers    | object    | Name of reviewer who wrote the review                                           |   |   |
| date_reviews | object    | date when the review was posted                                                 |   |   |
| rating       | float64   | Rating score given by the reviewer to the course which ranges from 1.0 to   5.0 |   |   |

# Executive Summary

In this capstone project, datasets **Coursera_courses.csv** and **Coursera_reviews.csv** are used from [Kaggle](https://www.kaggle.com/imuhammad/course-reviews-on-coursera?select=Coursera_reviews.csv). **Coursera_courses.csv** contains data like the course name and institutions while **Coursera_reviews.csv** contain reviews and rating left by each reviewer.
Both of the datasets are merged on the 'key' column. Now the dataset is combined into 1 dataframe.

There were reviews left in other languages and a combination of NLP libraries are used to translate `reviews` to english.
**Regular Expression** is used to clean up the text. **nltk.corpus** is used to filter out the non-english `reviews`.
**SpaCy** is used to detect the different languages. **google_trans_new** is a free python API for google translate,
the non-english `reviews` are translated in separate batches to prevent exceeding the request limit.

After the translation is complete, duplicated posts are removed and minimum 'count of words'= 5 are used. `Reviews` with `rating` 5.0 are mapped to 1 while `Reviews` with `rating`less than 5.0 are mapped to 0. The `reviews` are further preprocessed to remove digits, symbols and url links. `Reviews` with and without `rating` 5 and plotted on **WordClouds** - visual representations of words that give greater prominence to words that appear more frequently. This provides a visual signal of which words may help in classifying the 2 types of reviews. **pyLDAvis** is also used to interprete possible topics from the `reviews`.

The dataframe is then split into random train and test subsets using train_test_split.The `reviews` are preprocessed further using Porter Stemmer to generate the root form of the inflected words. Countvectorizer is used to convert the text in `reviews` to numerical data before using different Classification models for binary classification.

## Classification modelling

There were many Classification models used: Logistic Regression, MultinomialNB Classification, Decision Tree Classifier, Random Forest Classifier, AdaBoost Classifier, XGBoost Classifier. With high accuracy score and ability to generalise to unseen data compared to other models (the delta between train and test accuracy score) and low False Positive rate as our consideration, **Multinomial NB** showed the high accuracy in classifying the `Reviews` with `rating` 5.0 (mapped to 1) and `Reviews` with `rating`less than 5.0 (mapped to 0) and has the lowest False Positive rate.

| Classification   model       | Train Accuracy | Test Accuracy |   Delta  | Sensitivity | Fall-out |  AUC |
|------------------------------|:--------------:|:-------------:|:--------:|-------------|----------|:----:|
| Logistic Regression          |     0.83917    |    0.83254    |  0.00664 |   0.96203   |  0.60244 | 0.82 |
| Multinomial NB               |     0.82185    |    0.81926    |  0.00260 |   0.90128   |  0.45628 | 0.81 |
| Decision Tree Classifier     |     0.77724    |    0.77701    |  0.00023 |   0.99158   |  0.94376 | 0.52 |
| Random Forest Classifier     |     0.77057    |    0.77060    | -0.00003 |      1      |     1    | 0.73 |
| Ada Boost Classifier         |     0.80684    |    0.80563    |  0.00121 |   0.97043   |  0.74795 | 0.77 |
| Gradient Boosting Classifier |     0.83205    |    0.82649    |  0.00556 |   0.95793   |  0.61507 | 0.81 |

Based on the above Classification model Scoreboard,

- All of the classification models have classification score same or better than the required Baseline Accuracy of 77%

 - `Descision Tree Classifier` & `Random Forest Classifier` performed poorly compared to other models for this dataset,
this is based on the accuracy scores are 77% and both models have high Fall-out rate (false positive rate) predict `reviews` to be mainly either False positive or True positive which predict to be target=1 `reviews`. target=0 `reviews` were not correctly classified as compared to other models. 
 - `Ada Boost Classifier` & `Gradient Boosting Classifier` both models performed better with higher accuracy scores and but the Fall-out rate is not the lowest. 
 - `Logistic Regression` & `Multinomial NB` produced high accuracy scores and ` Multinomial NB` produced the lowest Fall-out rate at 45% compared to the other models.
 
Hence, **`Multinomial NB`** is chosen as the best model to classify target=1 `reviews` and target=0 `reviews` for this dataset.

**`Multinomial`** NB is chosen as the best model to classify target=1 reviews and target=0 reviews for this dataset as it has the lowest fall-out rate.

From these classification models, reviews can be classified into target=1 reviews where rating= 5 when positive words: 'thank', 'recommend', 'phenomen', 'excelent' are used vice-versa when negative words: 'useless', 'horribl', 'poor', 'disappoint' are used.
There are reviews with less than 5.0 rating but the reviewers left positive words in the reviews, hence classification models will misclassify the post as False positives.
In order to improve MOOC satisfaction and based on the group of words, courses have to be 'really recommended', 'easy', reviewers feel 'thank'ful, 'realli enjoy' the material. Further analysis could be done to see whether its due to the course content, instructor or difficulty level.

## Character-Based Text Generation modelling

In addition to classification of  `reviews`, this Capstone project also explored Text generation using Recurrent Neural Network(RNN). With tutorials from [keras.io](https://keras.io/) and fine-tuning, the text generated were easily understood and were able to generate reviews-like text. However, more research and fine-tuning are required to produce grammatically correct reviews.

| model |           RNN type          |   Number of Characters   | epoch | train Loss | train Accuracy  | test Loss | test Accuracy | accuracy delta |             personal judgment             |
|:-----:|:---------------------------:|:------------------------:|:-----:|:----------:|:---------------:|:---------:|:-------------:|:--------------:|:-----------------------------------------:|
|   1   |            LSTM             |       27(alphabets)      |   10  |   2.4733   |      0.2929     |   2.5557  |     0.2691    |     0.0238     |               unintelligible              |
|   2   |            LSTM             |       27(alphabets)      |   50  |   0.7912   |      0.7586     |   1.0349  |     0.7039    |     0.0547     |        paragraphs with empty spaces       |
|   3   |            LSTM             |       27(alphabets)      |  100  |    0.754   |      0.7676     |   1.0838  |     0.6976    |      0.07      |           more variation in text          |
|   4   |            LSTM             | 36 (include punctuation) |  100  |   0.7858   |      0.7595     |   1.1328  |     0.6908    |     0.0687     |   spelling errors and able to understand  |
|   5   |             GRU             | 36 (include punctuation) |  100  |    0.826   |      0.7478     |   1.0881  |     0.6939    |     0.0539     |   spelling errors and able to understand  |
|   6   |            LSTM             | 36 (include punctuation) |   29  |   0.8817   |      0.7353     |   1.049   |     0.6981    |     0.0372     | early stopping - no meaning in paragraphs |
|   7   |             GRU             | 36 (include punctuation) |   24  |   0.8994   |      0.7283     |   1.0429  |     0.6994    |     0.0289     | early stopping - no meaning in paragraphs |
|   8   |           bi-LSTM           | 36 (include punctuation) |   27  |   0.8011   |      0.7574     |   1.093   |     0.6895    |     0.0679     | early stopping - no meaning in paragraphs |
|   9   | **2nd LSTM layer with dropout** | 36 (include punctuation) |  100  |   0.7139   |      0.778      |   0.9765  |     0.7186    |     0.0594     | **spelling errors and easiest to understand** |

From other model runs, **model 9** which is used in this notebook and **chosen as the model better-tuned to generate text.**

- `RNN type`: Researched that there are 2 popular recurrent cells: Long Short-Term Memory cell (LSTM) and the Gated Recurrent Unit cell (GRU). In addition, Bidirectional LSTM was used.LSTM (model 4) seems to perform better given other parameters are kept constant (against model 5). When additional LSTM layer was used, **model 9** produced the best result

- `Number of Characters`: Initially modelling only used 27 unique characters which are alphabets, but the generated text did not appear realistic as punctuation is used to convey and clarify the meaning of written language. In addition, it gives structure to the sentence, hence necessary punctuations are included. the final 36 characters are used.

- `epoch`: An epoch is an iteration over the entire x and y data provided. From the observation, more epoch allow more iteration over the train and test set, hence there were better `accuracy` and lower `loss` score in general as epoch increases. `epoch` were not increased beyond 100 as based on the `accuracy` and `loss` plot, they started to plateau after 60 `epoch`

- `train accuracy`, `test accuracy`, `delta`: the accuracy score of the train and test set are very close, given that the`delta` value is very low. this is similar to the the loss scores too. **model 9** shows the highest train and test accuracy.

- *`early stopping`*: they are implemented on model 6 (LSTM), model 7(GRU) and model 8(Bidirectional-LSTM) and hence have low epoch, however the text generated is less understood than text from models with 100 epoch

- `personal judgement`: even though many of the models' accuracy score plateau to 0.76, how effective the RNN model is judged by how readible the text it generates, from the different models too. In this scenario, even though **model 9** shows overfitting at 100 epoch, the text generated is the most understood.

**In conclusion**: Even though model 9 shows overfitting, it has the highest accuracy and lowest loss with the most understood text. By adding 1 extra layer of LSTM with dropout layers, the text became more readable & realistic. For future improvements, the LSTM model can be made more complex with more layers or include embedding too.

RNN models like LSTM and GRU can help to generate artifical reviews for MOOCs like coursera or e-commerce that has an online presence.RNN model can be fine-tuned further to produce more realistic text, hence increasing it credibility.

### References used in Character-Based Text Generation:
- [The Unreasonable Effectiveness of Recurrent Neural Networks by Andrej Karpathy](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
- [Text generation with an RNN tutorail from tensorflow.org](https://www.tensorflow.org/tutorials/text/text_generation)
- [Character-level text generation with LSTM from keras.io](https://keras.io/examples/generative/lstm_character_level_text_generation/)
- [Text Generation With RNN + TensorFlow from section.io](https://www.section.io/engineering-education/text-generation-nn/)
- [Tutorial from Tanner Gilbert](https://github.com/TannerGilbert/Tutorials/tree/master/Keras-Tutorials)
- [Text Generation With LSTM Recurrent Neural Networks in Python with Keras from Machine Learning Mastery](https://machinelearningmastery.com/text-generation-lstm-recurrent-neural-networks-python-keras/)
- [Character Level Text Generation from PredictiveHacks](https://predictivehacks.com/character-based-text-generation/)

#### Source links for MOOC industry:
 - [Source 1](https://www.mordorintelligence.com/industry-reports/massive-open-online-course-mooc-market)
 - [Source 2](https://theconversation.com/massive-online-open-courses-see-exponential-growth-during-covid-19-pandemic-141859)
 - [Source 3](https://www.investopedia.com/articles/investing/020615/20-industries-threatened-tech-disruption.asp)
 
#### Source links for rise of fake reviews generation:
 - [Source 4](https://www.forbes.com/sites/forbestechcouncil/2019/04/04/ai-generated-reviews-threaten-business-reputations/?sh=546eeeb27eb1)
 - [Source 5](https://hbr.org/2020/11/how-fake-customer-reviews-do-and-dont-work)
 - [Source 6](https://www.theverge.com/2017/8/31/16232180/ai-fake-reviews-yelp-amazon)
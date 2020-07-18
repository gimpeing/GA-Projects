# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Project 3: Web APIs & Classification

## Context and Problem Statement
Product review is widely available in this digital world. People tends to do research on product reviews prior to purchase. However, there is fake review which is written by professional to boost the sale of a particular product. Thus, how would the consumer able to differentiate true user's genuine review from fake review?

We can use Natural Language Processing (NLP) to train a classifier to best predict or differentiate the two.

To do this, content from two subreddits were collected to evaluate different classifier model (Logistic Regression and Naive Bayes) on this binary classification problem.
Subreddits selected are:
1. [nosleep](https://www.reddit.com/r/nosleep/)
2. [Thetruthishere](https://www.reddit.com/r/Thetruthishere/)

Reason for selecting the two subreddits are they are about horror 'story'. Content in `nosleep` is of made up horror stories , whereas `Thetruthishere` is true horror personal experience.

Accuracy score is used to evaluate the success of the model as on how effective the model is able to differentiate post from the two subbredits.

Once the model is able to classify and distinguish between these two subreddits, then it would be able to adapt similar approach to detect made up (fake) review of a product for consumer. 

## Executive Summary

### Contents

- [Data Collection](#Data-Collection)
- [Data Cleaning and Exploratory Data Analysis (EDA)](#Data-Cleaning-and-Exploratory-Data-Analysis-(EDA))
- [Preprocessing](#Preprocessing)
- [Modelling](#Modelling)
- [Model Evaluation](#Model-Evaluation)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [Sources](#Sources)


### Data Collection
**Data Collection** is done by webscraping using the `requests` library. By default, Reddit give 25 posts per request. To get enough data, I'll need to use a `for loop` to continuously scrap the data by including `time.sleep()` function at the end of each loop to allow for a break in between requests.

### Data Cleaning and Exploratory Data Analysis (EDA)
Cleaning involved removing duplicate post, removing post with null content. This is left with 834 posts from `nosleep` and 937 posts from `Thetruthishere`. It was observed that `nosleep` has much longer post content comnpared to `Thetruthishere`. Asides, CountVectorizer is used to find out the most frequent words appeared in the two subreddits. In addition, I also count the number of words in each post content. It can be clearly seen from the histogram that `nosleep` has way much longer post length compared to `Thetruthishere`. This indicated that make-up story is always much more lengthy that the true personal experience.

### Preprocessing
Pre-processing includes using Regex to remove html links, punctuation, non-letters word, lemmatizing, and removing stopwords. `Subreddit` column that indicate which subreddit the post originated from is converted into binary number by assigning `1` to `nosleep` and `0` to `Thetruthishere`. The data was divided into train set (75%) and test set (25%).

### Modelling
Baseline score, which is the null model by predicting the majority class is defined.
Baseline accuracy = *53%*

|Target Variable|Normalized Counts|
|---|---|
|1|0.529678|
|0|0.470322|

*where 1 equals `nosleep`, 0 equals `Thetruthishere`*

Two Vectorizer extraction techniques are used to transform the post's content (string of words) into numeric X matrix that is able to use for modeling are:
- CountVectorizer
- TfidfVectorizer

For each Vectorizer, two classification models are built:
- Multinomial Naive Bayes
- Logistic Regression

Model optimization was done by using GridSearchCV to identify the optimal hyperparameters and were built into the classificaiton models.

### Model Evaluation
Accuracy score was used to evaluate how well the classification model perform. This is because there is no greater detriment to false positive (actual post is `Thetruthishere` but predict it came from `nosleep`'s subreddit).
Generally, all models perform well with accuracy in the range of 92%-94%. They all outperform the baseline. New post from each subreddit were pulled to check how well the model generalize to unseen data. *Logistic Regression model using TfidfVectorizer* performs the best as it is able to predict equally well by having consistent accuracy score around **93%**


### Conclusions and Recommendations
**Results summary:**

|Classifier Model|Vectorizer|Test Accuracy|Unseen data Accuracy|Sensitivity|
|---|---|---|---|---|
|Logistic Regression|CountVectorizer|94.4%|92.7%|91.2%
|Multinomial Naive Bayes|CountVectorizer|92.1%|82.7%|90.8%
|Logistic Regression|TfidfVectorizer|**93.8%**|**93.3%**|91.6%
|Multinomial Naive Bayes|TfidfVectorizer|93.0%|84.0%|92.0%

**TfidfVectorizer + Logistic Regression** is the highest-performing model as apart from high accuracy score, it is able to generalize better to unseen data. This would be the model proposed to adapt to detect fake product review.

However, more refining work needs to be done. First, it cannot rely on just the Accuracy score to evalute how well the model perform. , sensitivity is another important metric to evaluate the model for fake review identification.

This is due to there is impacts of type II error, that is the **False Negative**. FN means predict it is true review, but in actual case, it is a fake review. This would put the consumer in an disadvantage position of falsely believe the content of the fake review. Thus, improving sensitivity is important as it reduces the FN.


### Sources
1. [nosleep Subreddit](https://www.reddit.com/r/nosleep/)
2. [Thetruthishere Subrreddit](https://www.reddit.com/r/Thetruthishere/)
3. [video on how to use Reddit's API](https://www.youtube.com/watch?v=5Y3ZE26Ciuk)


```python

```

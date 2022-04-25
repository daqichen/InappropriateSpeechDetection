# Final Project - Inappropriate Speech Detection
`COMP590-158-Spring 2022: Introduction to NLP`


## Purpose Statement

We are attempting to develop a language model that can identify problematic speech patterns. This issue is important for any major social media platforms, especially as the size of usergroups grows even larger day by day. 

All of us, as users of these platforms, are potential victims of cyberbullying and even hate speech. Not to mention, younger children are placed at even greater risks of being harmed by harassment and inappropriate content.

A show of hand, how many us are active on at least one of these listed social media platforms? 


## Data Overview

So, hopefully you are familiar with Twitter, since our dataset is a collection of tweets sent out by Twitter users and then tagged by multiple human raters via crowdsourcing. They were categorized into the following:

- Hate Speech
- Offensive
- Clean


### Data: Tweet Preprocessing

We had 17,000+ datapoints for Train and 7,000+ for Test. We conducted stemming to individual words using the PorterStemmer, kept stopwords and punctuations, since we believe they could carry some degree of significance in the prediction. And we also applied URL and User Mention Tagging. 

Here is a quick demonstration of the raw data, and the post-text-preprocessing data:

```
RT @VUULibrary: It is Shakespeare's birthday. Take a look at some Shakespearean works. http://t.co/JSy3UFfaIb

rt usertag : it is shakespear 's birthday . take a look at some shakespearean work . urltag
```

### Data: Data Encoding

Our project will be focusing on distinguishing between "__Inappropriate__" and "__Safe__" language patterns. 

Then, in order to convert text inputs into vector representations, we conducted BoW Feature Extraction using Count Vectorizer, which is a way to convert a given set of strings into a frequency representation. 

And then Tfidf Vectorizer for our final improved model, TF-IDF means Term Frequency - Inverse Document Frequency, which is based on the frequency of a word in the corpus but it also provides a numerical representation of how important a word is for statistical analysis.


## Models

Now that we have encoded our inputs, we are ready to construct and train our language models. We used a few modeling methods discussed in class:
- Naive Bayes
- Logistic Regression
- BERT, state-of-the-art transformer-based language model (from `HuggingFace`)


## Results

BERT had the best precision of >98%, meaning it generally doesn’t falsely classify safe tweets as inappropriate. So what BERT identify as inappropriate, is generally actually inappropriate. But a major downside is the speed of running the mdoel, as it takes hours to train.

Naive Bayes had the best recall score of >98%, but precision is quite low, meaning it is really conservative, or sensitive, so it tend to misclassify many safe tweets to be inappropriate.

Logistic Regression obtained the best test accuracy overall, at __95.7%__.

> In the context of this project, `percision` means "of all the tweets we predicted to be INAPPROPRIATE, how many were actually INAPPROPRIATE", `recall` means "of all the tweets that were actually INAPPROPRIATE, how many did we predict to be INAPPROPRIATE".


## Models (cont.)

We also challenged ourselves with modeling techniques beyond the content of this course, we applied __logistic regression__ with an L2 penalty to select the best features from `sklearn.feature_selection` package, then trained a Linear Support Vector Classification (SVC) model, it operates on optimizing the Hinge Loss, with the selected features to predict the labels.


Linear SVC didn’t exceed the others in performance with a test accuracy score of __94.3%__, but it reduced input dimensions and hence making the model less complex while maintaining an accuracy fairly close to Logistic Regression and BERT.

## Demo

We also decided to feed some demo data into the 4 trained models ourselves to see how it would behave, here are those examples.

| Index | Text for Prediction |  NB | LogReg | BERT| Linear SVC|
|:----------:|:-------------|:------:|:------:|:------:|:------:|
|0|'.@becky its a good day to be a tarheel'|1|0|0|0|
|1|'tf is this dook tenting tradition???'|1|1|0|0|
|2|'jesus what is this dook tenting tradition???'|1|0|1|0|
|3|'Some weights of the model checkpoint at bert-base-cased were not used.'|0|0|0|0|

## Authors

Daqi (Jen) Chen:
- Undergraduate Junior, CS & Stats
- Dataset selection, Preprocessing, Cleaning, Encoding and Feature Extraction (BoW and TFidf Vectorization), Construction of Naive Bayes, Logistic Regression, and BERT models, Design, Content, and Presentation of Final Poster.

Sam Ferguson:
- Undergraduate Junior, Math & Stats
- Naive Bayes, Written and Visual content of Mid-semester project presentation, Problem statement and Procedure descriptions, Analysis of model performance and metric comparisons, Content of Final Report.

Asiyah Ahmad:
- 1st Year PhD Student
- Written and Visual content of Spotlight slide, Design of Mid-semester project presentation, Design of Final Poster.

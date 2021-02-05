# Filtering Fake News in Reddit Posts

## Project Map
 - [Presentation Deck](./slides.pdf)
 - [Research](./research.md)
 - [Code](./code)
  - [Web Scraping](./code/01_scraping.ipynb)
  - [Exploratory Data Analysis](./code/02_eda.ipynb)
  - [Modeling](./code/03_modeling.ipynb)
 - [Images](./images)
  - [Model Architecture](./images/confusion_matrix.png)
 - [Data](./data)
  - [Reddit Posts](./data/raw.csv)

### Contents:
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Conclusions](#Conclusions)

### Problem Statement 

Social media platforms are being overwhelmed with fake news, conspiracy theories, and bots.  The need for content moderation has never been greater and machine learning is here to help.  The goal of this project is to build a binary classifier for the Reddit Data Team that classifies posts as "news" or "conspiracy theory".  Such a model can be used in conjunction with a human moderator to filter out dangerous conspiracy theories.

### Executive Summary

I optimized a Multinomial Naive Bayes Classifier to classify Reddit posts with 87% accuracy and 92% sensitivity.  The model was trained over 3000 Reddit post titles from r/news and r/conspiracy.  Logistic Regression and Gaussian Naive Bayes Classifiers were also considered, but ultimately the Multinomial Naive Bayes Classifier trained on monogram and bigram count vectorizations performed best.  The model, if regularly retrained, would serve as excellent first pass filter for conspiracy theory content moderation and would make the job of a human fact-checkers much easier.


### Conclusions

The final model was overfit scoring 98% accuracy on training data and 85% accuracy on testing data.  The overfitness of the conspiracy classifier is not a big deal and somewhat embraced by the model's design.  This model is not meant to be able to easily generalize to new data and should be retrained every few weeks so as to "catch up" on the latest headlines.  Ultimately 85% accuracy on testing data is a well performing model with medium to low variance.

Determining what is a satisfiable balance of accuracy and sensitivity was an arbitrary judgment.  If we were really commited to increasing the true positive rate to 1, we would have kept increasing the Naive Bayes alpha paramater and kept increasing the n-gram range of the Count Vectorizer.  However, these parameter increases come at the cost of the model's accuracy.  The final model keeps the range of n-grams from 1 to 2 and Naive Bayes smoothing parameter (alpha) at 2.

We recommend the following steps to the Reddit Data Team to improve their content moderation.

1. Implement the Multinomial Naive Bayes Classifier as laid out in this project.

2. Use the model *in conjunction* with a human moderator.  Leaving important content moderation entirely to a machine learning algorithm is always a bad idea.  Content moderation is supposed to empower community members to respect each other, not leave members feeling powerless.

3. Retrain the model on fresh news and conspiracy data every few weeks.
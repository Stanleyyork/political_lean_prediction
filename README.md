# Predicting Political Lean of a News Article
Stanley Stevens // December 2016 // GA Class Project

## OVERVIEW
### Idea
  - Use previously labeled (with political bias) news articles to train a supervised logistic regression model to classify new/other articles, with the ultimate goal of increasing self-awareness of my personal political views and grow into a more balanced and nuanced perspective (with the underlying assumption that “you are what you read”).

### Resources
- Github/Jupyter Notebooks - see above
- Training Data - [source](https://www.dropbox.com/s/6vwbaqwxnd5z8e6/training_data.csv?dl=0)
- Untrained Data - personal political articles I’ve read (count: 310 articles) - [source](https://dataclips.heroku.com/heuwkhqdpstqyonvfywticdmeuir-political_bookmarks.csv)
- More details (including exploration notes) - [source](https://docs.google.com/document/d/1GYnSqb1Qq60_JRr4x2G-FhF2Rl6hmLxO8EETNWUelgs/edit)
- Presentation - [source](https://www.dropbox.com/s/06afmarj5g6v06m/Predicting%20Political%20Lean%20of%20an%20Article.pdf?dl=0)

### Data Dictionary
- political lean: political bias of article (left, lean left, center, lean right, right, mixed not rated)
- cleaned_text: article text (no html)
- ugly_text: article text (including html)
- url_raw: full url of article
- url_clean: full url minus key/value pairs at end of url string
- url_domain: host/domain of article (e.g. cnn.com)
- title: title of article
- meta_description: mini summary of article
- issue: topic of article (e.g. economy, election, environment, healthcare, etc.)

## Model Selection
- Knn: by far the worst of the three models, with average accuracy scores in the 0.2 and 0.3s
- MultinomialNB: I explored Multinomial Naive Bayes up front using a number of different features and parameters, but it always seemed to underperform logistic regression by roughly 10-30% (though it was much faster, as to be expected)
- Logistic Regression
  - With the count vectorized params mentioned above: ngram and min_df)
  - I ended up exploring two models both using logistic regression but with different feature sets: Model A: Text+Domain+Url & Model B: Domain (only)
  - These two models had varying results. As you can see below, model B (domain only) seems to suggest that I read very few ‘Right’ articles, though model A (domain/url + text) suggests a more balanced reading. Anecdotally (by simply knowing what I read), I’d say it’s actually somewhere in the middle (mostly ‘lean left’, with maybe 10-15% right or right leaning articles) - though the point of this exercise is to gain a higher level of self-awareness, so my thought process would very well be biased in and of itself.

## Conclusion
###Challenges
- Collection process
  - First attempt at html content failed as it included political bias tags leading to an overfit model.
  - The overall collection process took approximately 10-15 human hours and somewhere between 50-100 processing hours.
- Despite a high accuracy (0.97), model B (logreg) is potentially overfitting using url/domain
- Over classification of Right (possibly due to more ‘Right’ articles, need to explore more)

###Successes
- Had a mixed accuracy for model A (logreg) of 0.91, though when I applied it to my own (untrained) data, I was less confident in some of the classification

###Applied Solutions (future work)
- As mentioned above, I used 310 articles that I previously classified as ‘politics’, and it seems to be mostly correct (anecdotally about 65-75%), which with some further improvement, I will apply to my reading habits/tracking website.
- 310 Articles - data source (csv)
- I would also like to connect it to facebook and twitter (and pull in articles they’ve posted) to allow people to see where they stand from a political bias perspective
- A next step for both of the above will be to suggest articles from a different perspective so as to get a more balanced and nuanced view of the world.
- It will also probably be useful to create a model that detects if an article is a political article, so I can run it against any news article and accurately predict if this model is even relevant.

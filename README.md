# [2024 Scotiabank DS Discovery Days / AI-Kathon] (https://uwaterloo.ca/statistics-and-actuarial-science/events/scotiabank-data-science-discovery-days-2024)
## ⭐ Team Triangle of Statness (2nd Place) ⭐

# Theme
Using AI to derive business insights from customer feedback

# Background

As a young and talented data scientist, you've recently joined the customer advocacy team, collaborating with like-minded analysts. Your team's primary goal is to analyze customer feedback to enhance the customer experience.

In reviewing Scotiabank's mobile app customer reviews, you noted datasets containing irrelevant reviews from external sources. Your team's objective is to segregate and eliminate these irrelevant "Easter egg" reviews, then focus on detecting popularity of 20 selected topics to discover the relevant reviews. Moreover, you're responsible for deriving insights and formulating recommendations to improve customer experience based on your data analysis. This will require you to analyze the data, identify patterns and trends, and develop business strategies to improve customer experience.

## Tasks

Your team needs to use advanced analytics/AI approach to analyze customer app review to improve customer experience based on the given available data. Furthermore, you need to look for any insights from the data that can help you conduct business analysis to answer the following questions:

* What are frequent and popular topics among Scotiabank mobile app review, can you **identify the popularity of 20 topics among given topics from data dictionary**, how did you arrive at the conclusion?
* What are some of the **customers' needs** for Scotia mobile app? **desired features, pain points**?
* If you are looking to build/fix one feature in Scotiabank mobile app to improve customer
experience what will that be?
* Are there some external sources of customer reviews mixed with the data? Can you identify
those **“Easter egg”** reviews and what are those reviews about?
* Can you make any long-term suggestions to improve customer experience?
* How did you arrive at the conclusions?

# The Data

* 9175 records in the dataset
* Each record is a customer app review, one ID column (REVIEW_ID) to uniquely identify a customer review
* Description of column (sheet one) and potential topics (sheet two) are available in data dictionary

# Our Solution

## Easter Eggs
The first step was identifying Easter eggs since irrelevant input tends to produce inaccurate output. Any review with an obvious presence of banking-related terms was removed. Then LLM, namely ChatGPT, was used to label the completely irrelevant reviews as Easter eggs. By iteratively applying this **divide and conquer** strategy, the problem of finding Easter eggs was simplified into a series of binary decisions, significantly reducing the initial complexity.


## Data Cleaning

The next step was cleaning the reviews. Cleaning the reviews was essentially removing words that do not contribute to future analysis, which were decided based on the length, syntax, and relevance of each word. Words that meet any of the following criteria were removed:
1. Length: contains two or fewer characters
2. Syntax: is emoji, punctuation, or special characters
3. Relevance: does not relate to any specific topic but frequently appears in the reviews, such as “best” and “worst”


## Guided Bertopic Model

A guided **BERTopic** model was trained with the cleaned reviews and the list of seed words. The model generated around 100 topics with counts and words that represent that topic. Based on the representative words, the model-generated topics were manually classified into the 20 given topics. Before the manual classification, we attempted using keyword matching for further classification but received zero counts for some topics, so was aborted.

### Seed List

The seed words are weighted higher in the model and used more frequently in the output representative words for each topic, thus increasing the accuracy of the model. The list of seed words was initially generated by tokenizing the given topic description, then modified manually to better capture the essence of each topic.

## Pain Points and Desired Features (details can be found in the slides)

### Filter Most-liked Review
Pain points and desired features fall between reviews that accurately represent users, which can be determined by the number of upvotes. By filtering reviews with many likes, we identified representative reviews for future analysis that further identified pain points, desired features, and recommendations.

### Sentiment Analysis for Pain Points/Desired Features/Recommendations:
A sentiment analysis was performed using the **RoBerta** model. The model evaluated the sentiment of each review by generating scores for positive, negative, and neutral sentiments. Next, the extremely negative reviews – those with a significant negative score – were identified and fed into the Berttopic model to identify the pain points. A similar process was conducted to identify desired features and recommendations.

In summary, this comprehensive process not only allowed us to filter out noise and irrelevant information but also discovered valuable insights from user reviews. Moving forward, these insights can inform strategic decision-making and product improvements.






---
layout: post
title: Predicting Marathon Runner Categories in Hong Kong
image: /img/run.jpg
---

Marathons have a rich, global, history that have inspired millions to get up and go running. I partly grew up in Boston, which basically shuts down on "Marathon Monday", so it has always been a part of my life whether I was running one or just watching. The idea for the modern marathon was inspired by the legend of an ancient Greek messenger who raced from the site of Marathon to Athens, a distance of about 40 kilometers, or nearly 25 miles, with the news of an important Greek victory over an invading army of Persians in 490 B.C . Few sports or organized 'anything' can claim such a cool history.

Each year around 70,000 people take to the streets of Hong Kong for their annual marathon but Barnabas Kiptum of Kenya holds the current record of 2 hours, 9 minutes, and 20 seconds (that is 4 minute, 56 second pace).

The race has two major groups that start at different times. The first is made up of the elite runners for both women and men. Inside this elite group are a few different categories. I set out to see if one could predict what category a runner was a part using their various pace times, official finish time, and the country they are from. It turns out, its pretty hard! Prior to splitting the set by gender, my model only predicted the correct category around 40% of the time. After splitting the group by gender, it climbed to about 50% of the time. That's OK though! I want to use the rest of the post to talk through how the model worked.

The Data

I leveraged a dataset of the 2016 Hong Kong Marathon, the set has many features but as I noted above, I wanted to focus on the runner's country and 10km, half-way, 30km and finishing time. There were a few various transformations I had to make in order to work with the data but the only major one was converting the aforementioned times to seconds in order to get away from timestamp formatting.

Visualizing the Finishers

<p align="center">
  <img src="/img/finishers.png"/>
</p>

Visualizing the Elite Men's Category

<p align="center">
  <img src="/img/male_elite.png"/>
</p>

The Method

Once splitting out the male finishers, I chose to use gradient boosting and specifically the XGBoost library for classification. I decided on XGBoost mainly because of it's speed but also it's well-known model performance on tabular datasets like this one. The XGBoost library leverages the [gradient boosting decision tree algorithm](https://en.wikipedia.org/wiki/Gradient_boosting). In the most simple terms, in my opinion, this algorithm is an ensemble technique where new models are added to correct the errors made by existing models.

Feature Importance

In order to visualize 'feature importance', I've leveraged xgboost's plot_importance. This allows us to visualize the F score for each feature leveraged. The metric "F Score" is the sum of how many times each feature is split on after the tree was constructed. While a simple metric, it allows one to easily see a ranking of each feature. 

<p align="center">
  <img src="/img/feat_import.png"/>
</p>

Visualizing Decisions
Next, we see our tree in motion. This is a nice and super clear visual of the 'splits' or 'decision' and the result of each. 

<p align="center">
	<img src="/img/plot_tree.png"/>
</p>


---

Data courtesy of <https://www.kaggle.com/melvincheung/hong-kong-marathon-2016>

You can view the code behind this post here: <https://github.com/dwightchurchill/DS-Unit-2-Project-2/blob/master/marathon_predictions.ipynb>

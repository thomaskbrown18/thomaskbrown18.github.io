---
layout: post
title:      "Sentiment Analysis on Financial News Headlines"
date:       2020-09-17 21:29:39 +0000
permalink:  sentiment_analysis_on_financial_news_headlines
---


## NLP Using Artificial Neural Networks

This past week, I started a project to build a neural network model that can determine the sentiment of financial news headlines.  The users of this model would be investment firms who want to keep track of the market sentiment of a set of various products, companies, or industries.

Below is the result of my work on the project and some of the exploration I did with the data.  Though this project was purely academic, in a real world scenario, this model could be quite useful to firms looking to keep track of a wide variety of news sources in order to make smart investing decisions.

The data is collected from Kaggle through this [link](https://www.kaggle.com/ankurzing/sentiment-analysis-for-financial-news).  It's a collection of 4,837 unique news headlines from various financial news sources. The headlines are split into three categories:
- __Positive__
- __Neutral__
- __Negative__

An example of a positive headline would be "With the new production plant the company would increase its capacity to meet the expected increase in demand and would improve the use of raw materials and therefore increase the production profitability."


While an example of a negative headline would be "The international electronic industry company Elcoteq has laid off tens of employees from its Tallinn facility ; contrary to earlier layoffs the company contracted the ranks of its office workers , the daily Postimees reported."


It's an interesting challenge that requires quite a bit of data manipulation to get the dataset to feed into a neural network.  By the end of this project, I hope to have a neural network that can not only correctly classify examples from the test set, but also work on a stream of new headlines streamed in from other sources.  

For this project, I chose to use a binary model for classification.  Positives were classivied as '1', while Negatives and Neutrals were tagged as '0'.  This fixed a part of a class imbalance problem as  there were very few negative headlines relative to the dataset as a whole, and it allowed me to test things on a 0 to 1 scale.  For example, when I test the fake headline 'Stocks rise for Tesla', I recieve an output like '.89' instead of an array of different values for each sentiment.  This makes testing easier and for my purposes, much more efficient.



## Text Cleaning and Exploration:


To start, it was necessary to clean the headlines by removing so-called 'stop words' like 'and', 'I', 'or', etc. . . 
This changed the headlines from looking like this. . . 
![Imgur](https://i.imgur.com/nuLcp34.png)
. . . to looking like this:<br>
![Imgur](https://i.imgur.com/CyS96as.png)
Lastly, I used a process called lemmatization to further break down the words into simpler forms.  Lemmatization will change a word like 'Running' into 'run'.  This simplification of the words makes it possible for the neural network later on to treat 'Running', 'run', 'ran', and 'runs' exactly the same, for example.  You lose some nuance in the sentance as you'll soon see, but it makes it much easier for the model to learn in the end.  Here are some headlines after lemmatization:<br>
![Imgur](https://i.imgur.com/6LZ8qtv.png)


## Exploratory Data Analysis:

While exploring the data, I created a wordcloud of the most common words in the series of headlines.  Here is the cloud for the negative headlines:<br>
![Imgur](https://i.imgur.com/8ArewsH.png)
While it may not be at all obvious that this is bad news, that's where the beauty of machine learning comes in.  It's possible for the algorithm to pick up on seemingly harmless words or patterns that may show up more often in negative headlines.

## Baseline with Vader:

For a baseline model, I used Vader, a common toolkit for sentiment analysis, but when fed these financial news headlines, it only performed at around 62% accuracy.  Next step would be to build a neural network and see if it would be possible to get a significantly higher score.

While Vader is known to be a powerful toolkit, it just didn't work that well with the financial news data.  Often times, it didn't pick up any sentiment at all from these headlines, positive or negative.  While it may work quite well for other sorts of user reviews or other sentiment analysis, it does not seem optimized for this purpose.

## Artificial Neural Network Model:
For my neural network model, I chose to use an embedding layer as my first layer in order to generate word embeddings.  This is a common approach to NLP problems as it groups similar words together.  Another advantage to this is that I was able to use the TensorFlow projector to display the embeddings my model created in three dimensional space.

Here is a projection of the word embeddings my model created from the training headlines:  

![Imgur](https://i.imgur.com/7cFOoab.png)

As you can see, there is some overlap, but there are two very distinct groups of words!  One set is most commonly associated with positive headlines, while the other is associated with negative headlines.  Neutral headlines will have a healthy mix from both blobs.

At the end of the day, I ended up with roughly 80% accuracy.  Not tremendous, but not bad at all for the amount of data used.  Usually neural networks, especially for NLP, do much better with enormous data sets.

Here is a plot that shows the models training accuracy, training loss, validation accuracy, and validation loss plotted over epochs or training cycles:

![Imgur](https://i.imgur.com/9M3JMz9.png)
![Imgur](https://i.imgur.com/2pFhn7d.png)

As you can see, validation accuracy never quite catches up to training accuracy, but using early stopping (automatically pausing the learning once validation loss stopped improving) prevented validation loss from getting much higher.  In earlier models before using early stopping, validation loss skyrocketed off the charts.

As a sanity check, I also tested the model on a set of very simple made up headlines.  Here are the results.  As a reminder, 1 is positive, 0 is negative, and .5 is neutral.  If you're wondering why the headlines look funny, it's because I already completed a simple form of lemmatization on them already.

![Imgur](https://i.imgur.com/ovLxUjd.png)


## Wrapping up the Project:

There's still a lot we can do with this modeling.  In the future, I'd like to complete the following analysis:
- A web application that collects and analyzes headlines from various financial news sources.  It would be great to have a website where individuals or firms could keep track of products, companies, or industries they're interested in keeping track of.
- Other neural network architecture types.  I think there's more work to do on LSTM models, GRU models, or other neural network architecture types.
- New types of sentiment analysis, such as breaking news vs an opinion piece on an older issue.  There are more ways of breaking down texts aside from positive vs negative.  It would be interesting to break down some of these divisions.  
- Rate different newspapers by sentiment value.  I think it would also be fun to see which newspapers have the most positive tone!  A more accurate model, more labeled data, and more training could make this very doable.


Overall, this was a fun challenge! Sentiment analysis is a fairly tried and true field of study, but it was a bit more of a challenge to try it with financial news headlines. The words that impart sentiment tend to be much different than those in (for example) Amazon reviews or other common test cases.

While 80% accuracy has some definite room for improvement, it's not a bad start considering the amount of labeled data that was available for this project. At some point, I'd love to come back to this with a larger dataset and more experience under my belt working with neural networks and take another crack at this project.

Thanks for reading, and let me know if you have any questions.

-Thomas


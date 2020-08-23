---
layout: post
title:      "Reuniting Pets and Owners with Machine Learning"
date:       2020-08-23 17:34:49 +0000
permalink:  reuniting_pets_and_owners_with_machine_learning
---


## Module 3 Project:

For my latest project, I used data from Austin's largest no-kill animal shelter to try to create a machine learning model that would predict the outcomes of animals as they are brought in to the shelter.  The Austin Animal Center takes in mostly dogs and cats, and almost all of these animals fall into the first three of the following categories:<br>
- Transfer           
- Adoption    
- Return to Owner            
- Euthanasia        
- Return to Owner     
- Died                 
- Rto-Adopt
- Missing
- Disposal  <br>

With an effective model, we can predict animals outcomes as they enter the shelter, and with that knowledge, run the shelter more efficiently leading to happier animals and shelter employees!

As the vast majority of the animals fell into either 'Adoption', 'Transfer', or 'Return to Owner', it made sense to focus on these exclusively.  There are instances of animals getting euthanized, but as this is a no-kill shelter, I filtered these outcomes out of the data set.  When animals are euthanized at this shelter, it is because they are badly sick or injured.  This is not a call that a machine learning algorithm can make from just a line of data.<br><br>

Here is a quick look at the top three outcomes over time for both dogs and cats:<br>
![Imgur](https://i.imgur.com/QjqDNdk.png)<br><br>
It's interesting to note how seasonality impacts how cats are adopted or transfered, while the same is not true for dogs.  Dogs also seem to be returned to owners much more frequently than cats.  Perhaps this is due to an increased rate of running away.

These heatmaps can also give you an idea of the different intake conditions and how they can relate to outcome:<br>
![Imgur](https://i.imgur.com/D8sSNbU.png)<br>
![Imgur](https://i.imgur.com/YhZCshO.png)<br>

## Data:

Data Source: https://www.kaggle.com/aaronschlegel/austin-animal-center-shelter-intakes-and-outcomes?select=aac_intakes_outcomes.csv

The data for this project has been generously provided by the city of Austin in their initiative for open data sources.  The data consists of roughly 80,000 rows where each row displays a different outcome of a given animal in a shelter.  For example, a row might have the data for a month old kitten, domestic short hair breed, that was taken in off the street in an injured condition and adopted a month later.  Each line tells the story of a different dog or cat's journey through the shelter.  
<br><br>

## Project Goals:

One of my main goals for this project was maximum recall when it comes to the 'return to owner' outcome. I wanted to be certain that we are giving maximum exposure to pets that need to be returned to their families. At the same time, though, we need to give exposure to animals that are likely to be adopted as well.  Maximum recall for RTO cannot be our only objective, though.  We need accuracy throughout the entire model to make sure we aren't biased towards one outcome or another.

Success Criteria: 
- Easy to understand/use machine learning model
- Easy to implement algorithm
- High recall when it comes to pets that can be returned to families

## Recall vs. Precision:

Measuring accuracy for multiclass classification problems can be tricky.  It's easy to get caught up in dizzying array of possible accuracy metrics one can use.  Here is the list I settled on for this ternary classification puzzle:
<br>
- __Training Accuracy__ 
    - General accuracy of the training set - useful to make sure you're not overfitting the model
- __Testing Accuracy__
    - Ratio of correct classifications to total classifications - useful metric, but there's more to dig into!
- __RTO Precision__ 
    - Ratio of correct RTO classifications to correct RTO + False positives 
    - Useful to make sure you're not biased too heavily and making too many false positives
- __RTO Recall__ 
    - Ratio of correct RTO classifications to correct RTO + the ones the model missed i.e. false negatives
    - Useful to see what ratio of the target class you're identifying, i.e. not missing anyone
- __Adoption Precision__ 
    - Same as RTO Precision but with the adoption metric
- __Adoption Recall__ 
    - Same as RTO Recall but with the adoption metric
<br>


A few things may stand out.  The first glaring issue is the lack of metrics around the 'Transfer' outcome.  I chose to ignore this as adoption and return to owner are the main important outcomes here.  In most cases, transferring an animal occurs when it can neither be adopted or returned to an owner.  For my model to be effective, I wanted to make sure that every pet with an owner searching for it got returned home, and every pet that is able to be adopted is adopted.  The above list of metrics tells me everything I need to know in that regard.


## Modeling:

For this project I built a few different models, but the ones that stood out were Random Forest due to ease of understanding and speed compared to some other models and XG Boost due to a slight increase in accuracy.  I tuned both models using number of trees, learning rate, max depth, and a few other hyperparameters.  At the end of the day, I was able to acheive roughly 80% accuracy overall for this ternary classification problem. <br><br>

While XG Boost was not the best model in every single criteria, even RTO recall, I chose it due to it being the second or third best consistantly.  It had no major shortfalls, whereas almost every single other model did.  For example, a simple decision tree may have had excellent RTO recall depending on how I tuned it, overall accuracy was lacking.  While this may not seem like a big deal, we are dealing with many thousands of animals, and a small percentage difference could lead to wildly different outcomes for hundreds of animals.  Even worse, it could lead to animals being adopted out that actually have their owners looking for them.


## Model Evaluation:

Here is the confusion matrix for the best performing model, the XG Boost:
![Imgur](https://i.imgur.com/Yl6jEZ8.png)

Additionally, I put together a chart to show the differences between the major models:
![Imgur](https://i.imgur.com/n3gEEoD.png)
As you can see, the XG Boost performed the best overall.  While it did not have the best performance in every single category, it is one of the more powerful machine learning models and had consistently excellent performance.  As such, it is the model I would recommend if the Austin Animal Center were to use it in their day to day operations.

## Conclusion: 
This exercise in model building has been quite informative.  While pets returned to owners are the smallest of the main groups, it's crucial they get the attention they need instead of being transfered out or adopted to another family.<br><br>

__Returning to Owner:__
- Pets that are the most likely to have their families looking for them should be put front and center on the website so families can find them easily.
- The XG Boost model can identify pets with families searching for them almost 85% of the time.  With this knowledge, they can be returned much more quickly than if the families had to search through the entire site or visit the shelter to search for their pet.

__Adoption:__
- Pets likely to be adopted should be a close second in terms of priority. 
- Recall for adoption is even higher.  With XG Boost, the shelter can identify 94% of animals that will be adopted.  The sooner they leave the shelter, the better, so it would be helpful to advertise these identified animals more heavily on the site compared to ones likely to be transferred.

__Data Collection:__
On top of that, we can improve data collection in the future to improve the model.  There are a few major areas that could help:
- Change color upon intake to one of 15 or so values instead of an arbitrarily chosen color.  This prior practice has resulted in over 500 different colors recorded in the dataset.
- Change location data to longitude and latitude data.  This makes it much easier to compare locations.  It can also help when implementing maps on the site.
- Include a measurement of temperament, perhaps on a scale of 1-10.  This can also help with adoption and RTO recall.
- Change breeds to a more standardized list as well.  Like color, this data collection method is too unwieldy to use effectively without heavy feature engineering.
<br>


Overall, though, this model should help the vast majority of pets find their way to owners.  With some work on the website and internal database applications, we can set up a system to help animals find their homes!

Thanks for reading,

-Thomas Brown

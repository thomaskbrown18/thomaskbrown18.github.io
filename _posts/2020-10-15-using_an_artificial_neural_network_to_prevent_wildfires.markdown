---
layout: post
title:      "Using an Artificial Neural Network to Prevent Wildfires"
date:       2020-10-16 01:55:41 +0000
permalink:  using_an_artificial_neural_network_to_prevent_wildfires
---


For my latest project, I chose to address the problem of wildfires. Over the past few years, there has been a shocking increase in wildfires, especially here in the states, and I thought it would be interesting to find a way to build something of a solution to the problem. I wrote a couple blog posts before on my data collection and exploratory data analysis phase of the project, but my general approach was as follows: 

First, I collected images to analyze using the Google Static Maps API.  My end goal was to build a neural network that can distinguish between areas that will experience wildfires vs. areas that have not.  I’m waiting on several satellite services that may have better imagery than Google Maps, but for now, Google was the only one I had access to.  I used a list of wildfires in Washington to collect satellite images of almost every single area in Washington that has had a wildfire in the past 12 years.  

After collecting these images, I did some exploratory data analysis to explore trends and groups of wildfires in Washington.  After that step, I went on to modeling.  I was hoping to build a model that can identify areas via satellite that is at risk of wildfire.

For this project, I chose to use a convolutional neural network. It's the industry standard for image recognition as it is able to pick up patterns and distinguish different images from each other. A convolutional neural network works by using filters that scan through images. At first, these filters are randomly weighted, but as the model learns and is refined, the filters begin to pick up patterns like edges, lines, shapes, or even color intensity (in the case of RGB images). I tried several versions of the convolutional neural network, and by the end, I had one that I was satisfied with. 

The model turned out to be 77% accurate on the training set and 69% accurate on the test set.  I think this level is reasonably accurate given how much of Washington is covered in relatively dry, flammable forest.  As you can see in the confusion matrix, much of the loss in accuracy is driven by the high false positive rate.  While this is not ideal, it's understandable given how many images in the non-wildfire category are still at moderate risk of wildfire.

Below is the chart showing training and testing accuracy and loss, as well as the confusion matrices for the training and test sets:

![Imgur](https://i.imgur.com/19Mb4YI.png) 

![Imgur](https://i.imgur.com/5BQCV55.png) 

![Imgur](https://i.imgur.com/fnKzt76.png)

- Accuracy refers to the ratio of correct predictions to incorrect predictions.
- Recall refers to the ratio of true positives to true positives plus false negatives.
- Precision refers to the ratio of true positives to true positives plus false positives.

It’s important to gain a healthy balance here in order to have trust in the model.  For example identifying everything as ‘high wildfire risk’ would lead to a recall of 100%, but precision would be unacceptably low.

## Deployment

At the end of training, my model was able to accurately predict wildfire risk of new locations as fed into the system. For example, I fed in the longitude and latitude of a location of a wildfire in California (the model has not seen any images from California so I thought it would be an interesting test), and it correctly identified the area as high risk.

![Imgur](https://i.imgur.com/iqeEwGF.png)

In the future, I would like to have this project linking to a live satellite feed and actively scanning areas, searching for high risk areas around the world, and sending alerts to local authorities as to the location of this newly discovered at risk area.  There is no reason this project could not be international in scope, provided with the right data.

There's a way to go before this project is fully deployable on a national or international level, but I believe it's a great start for a different take on wildfire prevention. Hopefully in the future, this project can be fully deployed and used by fire departments around the world. As I gain more expertise in handling image recognition tasks and collecting satellite imagery from more complex and thorough sources (e.g. NASA), I can't wait to come back to this project and develop the neural network to make it more and more accurate!

Thanks for reading, and please let me know if you have any questions or comments!

-Thomas Brown



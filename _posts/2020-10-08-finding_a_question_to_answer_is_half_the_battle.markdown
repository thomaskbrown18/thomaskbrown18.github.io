---
layout: post
title:      "Finding a Question to Answer is Half the Battle"
date:       2020-10-08 23:26:52 +0000
permalink:  finding_a_question_to_answer_is_half_the_battle
---


For my latest project, I wanted to tackle the challenge of collecting my own data, solving a relevant issue, and practicing skills I have only recently learned, particularly around artificial neural networks.  While it took some time to come to a decision, I eventually decided on attempting to make headway on the issue of wildfires on the West Coast, specifically Washington State (for now).

This topic is near to my heart as the last month has been terrible in terms of smoke and air quality here in the NorthWest.  My goal for this project is to find a way to help the state government predict and respond to wildfires more quickly.

The idea I had to respond to this issue is to find sites where wildfires have occurred, download satellite imagery of that location, and train a convolutional neural network to recognize areas that are at risk for wildfires.  With this information, I’m hoping state governments can use this neural network to scan areas via public satellite data and highlight areas that are at risk.  Perhaps they will be able to find areas that they did not know were at risk.  Armed with this information, firefighters will be able to prepare and respond much more effectively.

The above description is a massive oversimplification, so let’s break it down and explore some of the challenges and my approach to the problem.

# Finding the Data:

To start with, I used a list of wildfires in Washington from the department of natural resources.  After a bit of cleaning up, I had a list of over 10,000 locations (longitude and latitude) that have experienced wildfires.

Here’s a heatmap (literally) showing where most of the fires have occurred over the years: 
<br>
![Imgur](https://i.imgur.com/Oro3Dyd.png)
<br>
For proof of concept, I’m using Google Maps’ API.  The main advantage to this is that it allows a uniform type of picture.  The API is also easy to use and manipulate.  The main downside is the lack of ability to choose the time the satellite image was taken.  There are more advanced satellite imagery services out there, but I was not able to get access to them in time for this project.  If I did have the ability to choose when the satellite image was taken, I would set every picture to roughly a week before the wildfire in that area had occurred.

For each latitude and longitude pair in the list of over 10,000, I used a simple program in python to plug it into the API and download the satellite image at that location at a zoom level that shows roughly a square mile.  The images were then downloaded onto my hard drive.  This looping program was quite a bit more effective than doing each one by hand!

This was only half the equation, though.  In order to train the neural network to recognize areas prone to wildfires, I needed areas that have not experienced wildfires in order for it to learn what not to positively identify.  For this task, I generated 10,000 random values for latitude and longitude inside Washington state, and plugged those into the API as well to download them.

# Results:

After hours of the program downloading images for me, I was able to get about 20,000 examples in total of areas with and without wildfires.  Here are some examples of the satellite images I downloaded.

Here are a couple images of locations that have experienced wildfires:
<br><br>
![Imgur](https://i.imgur.com/fpKmnVI.png)
![Imgur](https://i.imgur.com/s2VjnAI.png)

<br><br>
And here are a couple that haven’t:
<br><br>
![Imgur](https://i.imgur.com/Uc5RAZg.png)  
![Imgur](https://i.imgur.com/MKnNl4l.png) 
 <br><br>

# Plan for the Neural Network:

Next up, I’ll be plugging these into a convolutional neural network, adjusting the architecture, and training it.  Hopefully in the future I’ll have access to a more robust satellite imagery dataset as well!

I’ll provide an update in my next blog post on the CNN results as well as other findings.

Thanks for reading, and please reach out if you have any questions or comments!

-Thomas


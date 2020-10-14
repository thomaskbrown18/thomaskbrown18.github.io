---
layout: post
title:      "EDA of Washington State Wildfires"
date:       2020-10-13 23:23:17 -0400
permalink:  eda_of_washington_state_wildfires
---


For my latest project I’ve decided to explore wildfires in Washington state. The ultimate goal of this project was to build a neural network that can identify areas at risk of wildfires. Before building any sort of neural network, though, it’s important to gain a deep understanding of the data you’re working with.

My source for this data was the Washington State DNR list of wildfires.  Each row of the data has the latitude, longitude, date, cause, acres burned, and all sorts of other information for each recorded wildfire in Washington over the past 12 years.

![df](https://i.imgur.com/ctkGm3P.png)

Before pulling satellite imagery of the locations, it first seemed like a great opportunity to use Folium to explore the location data.  Folium is a Python library used for creative mapping of data.  While I had a rough idea of where most of the fires were happening through standard bar plots like the one below, a map is a much better tool to tell where fires are occurring.

![Imgur](https://i.imgur.com/rKEBvua.png)

## Fires by Size

I thought it would be a great opportunity to see the distribution of different types of fires across the state.  First, I wanted to see the breakdown of small, medium, and large fires:

![Imgur](https://i.imgur.com/FnWfVNk.png)

- Yellow signifies a small fire (under 10 acres)
- Orange signifies a medium sized fire (10 to 500 acres)
- Red signifies a large fire (greater than 500 acres)

It’s interesting to see that most of the largest fires take place in that central band of the state.  

## Fires by Cause

Next, It seemed interesting to look at fire cause on a map.  The most common causes for fires are lightning, debris (from other fires), and (unfortunately) arson.  This map is especially important as it can help guide officials to the most likely spots where arson could be committed.  Here is the map:

![Imgur](https://i.imgur.com/jRITn47.png)

- Yellow signifies a lightning strike
- Blue signifies debris
- Red signifies arson

Luckily, it appears as though arson is less common in the middle of the state (the areas with the largest wildfires).  It looks like most arson is clustered around Spokane.  I never realized this was such a large issue, but hopefully the authorities are aware!

This was a great start for exploratory data analysis, but EDA is not the main focus of this project.  In my next blog post, I’ll be going through a neural network I built to identify areas at risk of wildfire.  The network uses satellite images of areas that have experienced wildfires in the past, and I’m hoping to train it to recognize signs of potential wildfire risk!

Stay tuned, and let me know if you have any questions!

-Thomas


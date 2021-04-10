---
date:   2020-06-03
tags:
  - R
author_profile: false
wide: true
excerpt: How to create graphs that let the data do the talking
toc: true
mathjax: true
published: false
---

The goal of data visualization is to let the data do the talking. Unobstructed and bare for the world, for all audiences, to 
unequivocally understand. Sometimes we tend to forget, or perhaps deprioritize, this important tenet of the data viz world. 
From my own experience as a data scientist, this can be the unintended consequence of learning the technical nuances of
how to build data visualizations. So much emphasis is placed on learning how the create a bar graph, line graph, or 
scatter plot, that we don't bother to ask ourselves: is my graph effective at relaying the message of my data in a simple 
way that a layperson can understand?

Creating the visual is half the battle. The other half is ensuring the above statement regarding viz comprehension rings true.
This post is a step by step tutorial on how to create a clean, minimalistic bar graph, line graph, and scatter plot that allows
your data to be in the spotlight, unambiguously, for all to see.

There are numerous data visualization packages and libraries that exist for the data scientist to choose from, such as ggplot, 
matplotlib, seaborn, or plotly. My personal preference for creating data visualizations is RStudio, so my weapon of choice is,
you guessed it! ggplot. I like the logical functionality of adding "layers" to a base visualization. You'll see what I'm 
referring to in a minute. 

---
title: MGMT 3125 - Introduction to Data Visualization
date:   2019-01-12
tags:
  - stockton university
  - tableau
author_profile: false
wide: true
excerpt: I currently teach this course. Repository for notes, lecture videos, and assignments
toc: true
mathjax: true
published: true
---

## Course Information

### Description

Introduction to Data Visualization provides an overview of business analytics, including the process of business intelligence and dashboard design, principles of data visualization, and effectively communicating data stories. The course uses Excel, Tableau and Rstudio.

This the first course with a comprehensive overview of the fundamental concepts and tools of business analytics to improve decision making and performance. This is a hands-on course that is designed to introduce both the principles of data visualization and industry standard data visualization software. Students will learn visual representation methods and techniques that increase the understanding of complex data models. Emphasis is placed on the identification of patterns, trends and notable differences in various datasets. Excel, Tableau and R are used to apply the abovementioned data visualization principles.

### Syllabus

* [Download here](/assets/mgmt_3125/MGMT3125_Spring2019_.pdf)

### Textbooks

* Storytelling with Data: A Data Visualization Guide for Business Professionals, by Cole Nussbaumer Knaflic, 1st edition, Wiley. ISBN-13: 978- 1119002253.

* Data Visualization: A Practical Introduction, by Kieran Healy. Princeton. ISBN-13: 978-0691181622. [Available online](http://socviz.co).

### Datasets

Datasets applicable to each assignment are provided under the respective assignment header, and all datasets are indexed here for reference.

* [IT tickets by month, location](/assets/mgmt_3125/week1/IT tickets by location, month (2017).xlsx)
* [World life expectancies](/assets/mgmt_3125/week3/Life Expectancy Final.xlsx)
* [Walmart retail sales](/assets/mgmt_3125/week7/Walmart Retail Sales 2012-2015.csv)
* [RMS Titanic](/assets/mgmt_3125/week7/titanic_clean_.csv)
* [Super Bowl 44 - 52 win probability](/assets/mgmt_3125/super_bowl44_52.csv)
* [Denver crime rates](/assets/mgmt_3125/week1/denver_crime.csv)
* [Sokol heart rate](/assets/mgmt_3125/week2/Sokol Heart Rate Data.csv)
* [Marriage by age](/assets/mgmt_3125/week3/marriage_by_age.zip)
* [American university data](/assets/mgmt_3125/week5/American University data.csv)

## Week 1 - 1/23

### Chapter 1: The importance of context

To consider context is strongly encouraged before building any visualization. The following are underlying situations to take into consideration:
* Who is your audience?
* What do you need them to know or do?
* How will you communicate? What is the medium of choice?

#### Exploratory vs. explanatory analysis
*	Exploratory: understanding the data to determine what is noteworthy to show the audience
* Explanatory: the specific story about the data to tell the audience

Too often the visualization author shows the exploratory analysis instead of the important explanatory analysis the audience needs to know.

#### The who, what and how of context

Who: Very important to understand the intended audience and how they perceive you. This will shape how you approach creating the visualization. 

* Helps to identify common ground to help relay your findings to your audience
* The more specific identification of the audience, the better. Just saying clients/key stakeholders usually isn't specific enough 

What: What do you need your audience to know? 

* Should be clear how you want your audience to react
* Take into account overall tone of visualization and/or presentation
* If you are analyzing and communicating the data, you are considered the 'subject matter expert'
* Be confident with your findings! Don't let fear of public speaking decrease your credibility

How: Mechanism of conveying the information
* Live presentations should have little detail considering you're available to answer questions
* Static documents demand generous detail to cover all the bases for possible client/stakeholder questions

#### The big idea

A single sentence summary of the study background information, issue the study is trying to solve, and the outcome of the study. Three components of The Big Idea:

* The idea must articulate your unique point of view
* The idea must convey what is at stake
* The idea must be a complete sentence

#### Storyboarding

Method of organizing ideas by creating a visual outline for the content of the visualization.

* Our minds do not think linearly, rather our thoughts are scattered. Time and effort must be put forth to organize them properly.
* Pen and paper work great for this task. Alternatively, if you have a Mac or iOS software, I recommend [MindNode](https://mindnode.com)

### Assignment 1 - Excel graphs

* [Assignment 1](/assets/mgmt_3125/week1/Assignment 1 - Excel Graphs_s19.pdf)
* [IT tickets](/assets/mgmt_3125/week1/IT tickets by location, month (2017).xlsx)

### Week 1 lecture slides

* [Week 1 lecture slides](/assets/mgmt_3125/week1/Week1_1_23_lecture.pdf)

## Week 2 - 1/30

### Chapter 2: Choosing an effective visualization

Choosing the right visualization is typically selected from 8 traditional methods. Knaflic elaborates on the scenarios that fit each visualization best.

#### The eight common visualizations

1. Simple text
* Works great for just a number or two.
* Refrain from taking up excessive space with a bar graph when simple text will suffice to compare two values.
* Be creative - make the font of the number you're trying to convey extremely large; also use color to your advantage by highlighting poignant parts of the study.

2. Table
* Useful to look at the raw data in the build phase, especially if the client/stakeholder requests it.
* Use light or minimal table borders so the observer can concentrate on the data
* Do not use tables for presentations; a well designed graph will convey insights much faster than a table with solely numerical values

3. Heatmap (also known as a treemap)
* Method of visualizing table data
* Use color saturation to create visual cues, shortening the amount of time it takes to get from initial observation to data insight

4. Scatterplot
* Effective for showing a relationship between two fields
* Include baseline statistics such as the median or average values so the observer can compare the plotted values with these summary statistics

5. Line graph
* Optimal for visualizing time series data and also more than one series of data (more than one line).
* I like visualizing summary statistics within a line graph, such as the average representing the average of the time series data, then the max and min values as a range of values that reach above and below the average.
* Line graphs do not need a zero baseline, because the graph is comparing data relative to each data point. Nonetheless, a good practice is to let the audience know you're baseline is non-zero.

6. Slopegraph
* Great for visualizing two time periods or points of comparison. Shows increases or decreases between two data points.
* Use a slope graph if you want to show increasing or decreasing values without showing what occurred in the middle of a particular timeframe.
*  Employ color to emphasize a trend that will be the focal point of your storytelling discussion.

7. Vertical bar graph
* Go-to visualization for plotting categorical data (the information is organized into groups).
* Viewers are so familiar with bar charts that this is the quickest chart to convey valuable data insights to people that matter. 
* Always needs to have a zero baseline, or else there will be misconceptions about the graph.
* Common decision is to preserve the axis labels or eliminate them entirely to label the data points. If you're focusing on big picture trends, then leave the axis labels. If you're focused on the specific numerical values, then label the data points directly. 

<!-- 8. Horizontal bar graph -->

#### Graphs to be avoided

Area Graphs
* Avoid area graphs, as human eyes are optimized for attributing quantitative value to two-dimensional space.
* Same principle applies with pie charts; replace pie charts with horizontal bar charts. 

Secondary y-axis: generally not a good idea
* Avoid the use of a secondary or right hand y-axis
* Don't show the second y-axis. Instead, label the data points that belong on this axis directory
* Pull the graphics apart vertically and have a separate y-axis for each (both along the left) but leverage the same x axis across both

There isn't a single correct visual display. Rather, there are different types of visuals that could meet a given need. The most important aspect of visual build/design is _What do you need your audience to know?_ Choose a visual display to make this abundantly clear.

### Assignment 2 - Introduction to Tableau

* [Assignment 2](/assets/mgmt_3125/week2/Assignment 2 - Intro Tableau s19.pdf)

### Week 2 lecture slides

* [Week 2 lecture slides](/assets/mgmt_3125/week2/Week2_1_30_lecture.pdf)

### Week 2 Videos

#### Tableau fundamentals

<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/4VzmdekIw00"
  frameborder="0" allowfullscreen></iframe>
  
#### Changing Tableau data sources

<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/yXqC_cGpIMg"
  frameborder="0" allowfullscreen></iframe>

## Week 3 - 2/6

### Chapter 3: Clutter is your enemy!

#### Cognitive load & clutter

* Cognitive load: Every single element added to a page takes up cognitive load on the part of the audience.
* Identify anything that doesn't add informative value. Remove these elements.
* Maximize the data ink ratio or signal to noise ratio to relieve cognitive load.

* Clutter: Visual elements that take up space but don't increase understanding.
* Why reduce clutter? Clutter makes visualizations more complicated than necessary

Employ the Gestalt Principles of Visual Perception to identify communicative elements and noisy elements. 

#### Gestalt Principles of visual perception

* Proximity: Tendency to think of physically close objects as belonging to a group.
* Similarity: Objects that are of similar color, shape, size, or orientation are perceived as related or belonging to a group.
* Enclosure: Objects that are physically enclosed together as belonging to a group.
* Closure: When parts of a whole are missing, our eyes fill in the gap; This principle renders chart borders and background shading unnecessary.
* Continuity: When looking at objects, our eyes seek the smoothest path and naturally create continuity in what we see even where it may not explicitly exist. 
* Connection: Connective property typically has a strong associate value than similar color, size, or shape.

Without obvious visual cues, the audience will typically start at the top left of a visualization, then move their eyes in a "Z" shape across the page or screen as they take in information

* Because of this, upper left justify text (title, axis, legends, etc).
* Generally, diagonal elements such as lines connecting text to visual attributes should be avoided.
* White space is akin to pauses in sentences; use white space strategically to draw attention to the parts of the page that are not white space. 
* Contrast: The more things we make different, the lesser the degree to which any of them stand out.

#### Decluttering strategies
* Remove chart border
* Remove gridlines
* Remove data markers
* Clean up axis labels
* Label data directly
* Leverage consistent color

Anytime you put information in front of an audience, you are creating cognitive load and asking them to use their brain power to process that information. Visual clutter creates excessive cognitive load that can hinder the transmission of your message. The Gestalt principles helps identify and remove unnecessary visual elements. Leverage alignment of elements and maintain white space to help make the interpretation of visuals a comfortable experience for the audience.

### Assignment 3 - Tableau Line and bar graphs

* [Assignment 3](/assets/mgmt_3125/week3/Assignment 3 - Line, bar graphs s19.pdf)

### Week 3 lecture slides

* [Week 3 lecture slides](/assets/mgmt_3125/week3/Week3_2_6_lecture.pdf)

### Week 3 Videos

#### Tableau bar graphs
<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/ey42xjtdtHw"
  frameborder="0" allowfullscreen></iframe>

#### Tableau line graphs
<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/ThTu-47Qd68"
  frameborder="0" allowfullscreen></iframe>
  
## Week 4 - 2/13

### Chapter 4: Focus your audience's attention

#### Actively engage the audience

Pre-attentive attributes
* Visualization attributes such as size, color, and position that are strategically employed to highly important aspects of the data. 
* Also used to create a visual hierarchy of elements to lead the audience through the information I want to communicate.

It is important to understand how our audience sees and processes information puts ourselves in a better position to communicate effectively. 

There are three types of memory that is important to understand for designing effective visual communication:
1. Iconic memory
* Information that that stays in memory for a fraction of a second before you sub-consciously decide to remove the memory or move it to short-term memory

2. Short-term memory
* People can keep about four chunks of visual information in their short-term memory at once
* Emphasizing a large amount of information on a visualization places an unnecessary burden on our audience, and thereby lose our ability to communicate effectively. 

3. Long-term memory
* Short term memory either goes to long term memory or our brain removes it. Aggregate of visual and verbal memory.
* Built up over a lifetime and is vitally important for pattern recognition and general cognitive processing. 

> By using pre-attentive attributes strategically, we can enable our audience to see what we want them to see before they even know they're seeing it!

When used sparingly, pre-attentive attributes can be extremely useful for:
* Drawing your audiences attention quickly to where you want them to look
* Creating a visual hierarchy of information

Some pre-attentive attributes grabs your attention, such as color and size, whereas italics achieve a milder emphasis. 

#### Create a visual hierarchy of information

There are variances within specific pre-attentive attributes that will draw attention with more or less strength
* For example, a bright blue will draw more attention than a muted blue. Both will draw more attention than light gray
* Leverage this variance to make the visuals scannable by emphasizing some components and de-emphasizing others. This establishes implicit instructions for the audience

Size:
* Relative size denotes relative importance
* If visualization attributes are equally important, then make them equally as big. Otherwise, if one this is really important, then make that BIG

Color:
* Don't make an attribute colorful just to make it colorful. Leverage color selectively as a strategic tool to highlight the important parts of the visualization. Use of color should always be intentional.
* Start out by creating a visualization with all shades of gray, then pick a single bold color to draw attention to where you want it. 
* Don't use black as a base color, as color stands out more against gray than black. 
* Use color sparingly and consistently
* Design with the colorblind in mind (blue and orange instead of green and red)
* Consider leveraging brand colors

Position:
* Without other visual cues, most members of an audience will start at the top-left and scan with their eyes in a zig-zag motion across the screen. 
* Top-left, top-right, bottom-left, bottom-right

### Assignment 4 - Calculated fields and parameters

* [Assignment 4](/assets/mgmt_3125/week4/Assignment 4 - Calculated Fields s19.docx .pdf)

### Week 4 lecture slides

* [Week 4 lecture slides](/assets/mgmt_3125/week4/Week4_2_13_lecture.pdf)

### Week 4 Videos

#### Tableau calculated fields

<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/DMgbqUQYiDo"
  frameborder="0" allowfullscreen></iframe>

#### Tableau parameters

<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/lmkA_pzcQ6Q"
  frameborder="0" allowfullscreen></iframe>
 
## Week 6 - 2/27

### Chapter 5: Think like a designer

This chapter explains how traditional design considerations are applied to create visualizations 
and persuade an audience to accept your visual designs. 

#### Highlight the important stuff

One main theme of the textbook is to employ preattentive attributes to draw attention to 
specific points of the visualization. This section sheds lights onto how much of the visual should 
be highlighted; as highlighted items in the visual increase, the power of highlighting effects to draw 
the audience to a specific talking point decreases. 

> At most, it is recommended only 10% of the visual design be highlighted - Universal Principles of Design (Lidwell, Holden, and Butler, 2003). 

**Bold**, _italics_, and <u>underline</u>
* Use for titles, labels, captions and short word sequences. Bold preferred over italics as this adds minimal noise to the visual.

Typeface
* Avoid using different fonts, as this can easily disrupt aesthetics. 

Color
* Highly effective when used strategically and sparingly to draw your audience to a visual attribute you want to emphasize. It is wise to make all other attributes gray, while making your important attribute(s) a color that stands in clear contrast such as bright blue, orange, or red. 

Size
* Size is another great preattentive to use to draw attention from your audience.

#### Eliminate distractions

Make spartan decisions as to which visual attributes are expendable. 

* Not all data is equally important.

* Consider if summarizing is appropriate instead of including extraneous detail.

* Ask yourself, would eliminating this attribute change anything? If the answer is no, then remove it!

* Push less important information to the background. Let your prominent attributes stand out. 

#### Don't overcomplicate 

> The more complicated a visualization looks, the more time the audience perceives it will take to understand and the less likely they are to spend time to understand it... between simple and complicated, favor simple. - Cole Knaflic

Make your visualization legible
* Use consistent, easily readable font. 

Use simple language
* Refrain from using convoluted jargon, and when in doubt, define a word or phase that isn't assumed to be common knowledge. 

#### Text is your friend

Use text in your visualization to provide context by labeling data points, introducing the visual, reinforcing key concepts, and ultimately to tell a cohesive story. 

Text elements in visuals that are necessary
* Title.
* Axis labels (unless the title conveys this in a straightforward manner).
* Short conclusive interpretive statement (see below)

> Don't assume the audience will intrepret the visual the same way you do. If there is a conclusion you want the audience to meet, state it plainly!

#### Aesthetics 

Beauty is one of the most important considerations for your audience to accept the message of your visual. Taking time to create visually appealing design means the audience will have more patience with the visual. 

Color
* We have already discussed the important of wise color use. Remember, use sparingly and strategically. 

Alignment
* Create clean vertical and horizontal lines that denote attribute organization.

White Space
* Preserve margins and don't add unnecessary elements just to fill in extra space.

### Assignment 5: Dashboard design and Tableau parameters

* [Assignment 5](/assets/mgmt_3125/week6/Assignment 5 - Dashboard, parameters s19_final_.pdf)

### Week 6 lecture slides

* [Week 6 lecture slides](/assets/mgmt_3125/week6/Week6_2_27_lecture.pdf)

### Week 6 Videos

#### Building Tableau dashboards

<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/5Em1ZTzfnPE"
  frameborder="0" allowfullscreen></iframe>
  
## Week 7 - 3/6

### Mid-term exam

* [Mid-term study guide](/assets/mgmt_3125/mid_term/Mid-term study guide_.pdf)

## Week 9 - 3/20

### Chapter 6: Dissecting model visuals

This chapter provides several examples of implementing the data visualization concepts explained
above by discussing the thought process behind why each visualization is effective.

As emphasized throughout this book, it is strongly encouraged to consider your audience. How will they process the information? What attributes of the visualization should be emphasized and de-emphasized? The following are very important to think about:

* Choice of visual
* Color
* Size
* Relative ordering of data
* Alignment and positioning of elements
* Use of words 

Examining each model visual will help reinforce the concepts of chapters 1 - 5. 

#### Model visual #1: Line graph

<img src="/assets/mgmt_3125/week6/c06f001.png" >

Words are used appropriately. Everything, including graph title, vertical and horizontal axis titles are present. The two lines are directly labeled so there is no need for a legend. The viewers eye's are drawn to the "Progress to date" trend due to the following pre-attentive attributes:

* Notable line size contrast
* Dark blue color
* Presence of data marker on final point
* Size of text

Notice how the author establishes a visual hierarchy of most significant to least significant with color: dark blue, light blue, dark gray, light gray. 

The author thought thinking about numbers in the thousands isn't intuitive, so the zeros in the y-axis label are preserved. 

#### Model visual #2: Annotated line graph with forecast

<img src="/assets/mgmt_3125/week6/c06f002.png" >

The difference between solid and dotted line distinguishes between actual data and forecast data. Clear labeling of actual and forecast helps clarify this distinction. 

Everything has been pushed to the background with the exception of the graph title, dates in the text annotation, data, data markers, and numeric data labels. Historical data points are not labeled, only the forecast data to give the viewer a clear understanding of forward-looking expectations.

#### Model visual #3: 100% stacked bars

<img src="/assets/mgmt_3125/week6/c06f003.png" >

The graph title, legend, and vertical y-axis title are all aligned in the upper-left-most position, creating a clean sense of organization on the left side of the graph. On the right side, the text at the top and the final red bars of data are aligned together. 

Red is used as the single attention grabbing color, while dark to light shades of gray push all other data to the background. The change over time in the percentage of projects that meet their goals is more difficult to compare considering there is no consistent baseline at either the top or bottom of the graph, but given this is lower priority comparison, that is ok. 

The graph uses supercategories (years to quarters) for organization and reference. The words at the top right reinforce what we should be paying attention to (from Q3 onward a significant amount of missed goals). 

#### Model visual #5: Horizontal stacked bars

<img src="/assets/mgmt_3125/week6/c06f005.png" >

A stacked bar graph makes sense due to the 3 categories of survey priorities (most important, 2nd most important, 3rd most important). The author uses a horizontal bar graph so the category names are easy to read. The categories are organized vertically in descending order by total % of development priorities. Words are used well, as all graph elements are titled and labeled. The x-axis is eliminated altogether. 

#### In closing

To create a habit of employing sound data visualization concepts into everyday workflow, we can learn from 
effective graphs and consider the design choices made to create them. This chapter reviewed the following concepts:

* Choice of graph
* Ordering of data
* Emphasize and de-emphasize graph components through color, thickness and size
* Alignment and positioning of elements
* Appropriate use of text

It is important to critically analyze the visualizations that you encounter to consider if each element/attribute in the visualization has purpose and is intentionally implemented. 

### Chapter 7: Lessons in storytelling

Great storytelling is an incredibly underrated and powerful and skill. The author can devote a great amount of time creating the perfect visualization, but if the author fails to communciate a compelling story, the message won't be as impactful, or worse, obfuscated.

This chapter is all about leveraging the power of storytelling to communicate effectively with data. 

### Week 9 lecture slides

* [Week 9 lecture slides](/assets/mgmt_3125/week9/Week9_3_20_lecture.pdf)

### Week 9 videos

#### Tableau Text Tables

<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/HNRdr_RvDWY"
  frameborder="0" allowfullscreen></iframe>

## Week 10 - 3/27

### R line graphs

### Week 10 lecture slides

* [Week 10 lecture slides](/assets/mgmt_3125/week10/Week10_3_27_lecture.pdf)

### Assignment 6: R line graphs
* [Assignment 6](/assets/mgmt_3125/week10/Assignment 6 - R line graphs.pdf)

## Week 12 - 4/10

### R bar graphs and scatter plots

### Week 12 lecture slides

* [Week 12 lecture slides](/assets/mgmt_3125/week12/Week12_4_10_lecture.pdf)

### Assignment 7: Rstudio bar graphs and scatter plots

* [Assignment 7](/assets/mgmt_3125/week12/Assignment 7 - R bar graphs scatter.pdf)

## Week 13 - 4/17

### Week 13 lecture slides

* [Week 13 lecture slides](/assets/mgmt_3125/week13/Week13_4_17.pdf)

### Uploading dashboards to Tableau Public

* [Publish to Tableau Public directions](/assets/mgmt_3125/week11/How to Publish to Tableau Public.pdf)

## Week 15 - 5/1

### Final project presentations


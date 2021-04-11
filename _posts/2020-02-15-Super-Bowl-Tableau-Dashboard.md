---
tags:
  - sports
  - tableau
  - r
author_profile: false
date:   2021-02-28
toc: false
classes: wide

excerpt: "Dashboard visualization of Super Bowl XXXIV - LV win probabilities and play descriptions"

---

<!-- <img src="/assets/Super-Bowl-Dashboard/foles.jpg" > -->

<iframe src = "https://public.tableau.com/views/SuperBowlWinProbabilities/SuperBowl44-53?:showVizHome=no&:embed=true" width="1030" height="830"></iframe>

<!-- https://public.tableau.com/views/SuperBowlWinProbabilities/SuperBowl44-53?:embed=y&:display_count=yes&publish=yes -->

The Dashboard was updated on 2/28/2020 with the addition of Super Bowl 55, and Super Bowl 34 - 43 data. The original post revolved around the Philadelphia Eagles winning Super Bowl 52. 
{: .notice--info}

## Introduction 

As a Giants fan, it was painful to watch the Philadelphia Eagles win their first Super Bowl victory. Gone are the days
of using the end all arguments question “How many Super Bowl rings do the Eagles have?” 
The idea is anathema to football fan that has a disdain for the birdgang (Giants, Cowboys, Redskins, Patriots, etc). 

But as someone who loves the game of Football, Super Bowl LII was an incredibly entertaining matchup that established several precedents: 
- 1,151 total offensive yardage (Patriots 613 and Eagles 513), 200 yards more than any previous Super Bowl.
- The Eagles are the first team in NFL history (regular season or postseason) to win a game despite allowing more than 600 yards.
- The Eagles are the 4th team in NFL history to win the Super Bowl after having a losing record the year before.
<br>
Source: [Sportingnews](http://www.sportingnews.com/nfl/news/super-bowl-52-eagles-patriots-stats-fast-facts-records-milestones/1kbmcltvjrukzzty6cpb8796y).

Considering how entertaining and important this game was, the following question arose: 

>What were the key plays, or the turning points, that had the most impact on game? How did the plays affect the likelihood of either team winning?

As with any data science project, the workflow begins with a good question.

I created a Tableau dashboard to visually answer this question. The time remaining in the game (independent variable) is plotted against win probability (dependent variable) to show the two team's likelihood of winning after each play. 

<!--The true value of Tableau is the ability to swap between Super Bowls in one view, and accessing each play description using tooltips. -->

## Data Source
Determining the right data source wasn't easy. American Football does not have the luxury of a statistically mature infastructure like Baseball. But I eventually found the open-source R package [nflscrapR](https://github.com/maksimhorowitz/nflscrapR), written by Makism Horowitz and Ron Yurko that scrapes data from the official NFL API.

### nflscrapR
The nflscrapR Github page provides several examples of querying the official NFL API to help new users hit the ground running. Two important aspects of the package are the following:
- Game level analysis.
- Data available after the 2009 season.

Discovering the data goes back to 2009 made me reassess the scope of my project: why not visualize key plays and win probabilities from _every_ Super Bowl between 2009 and present day?

|                 Super Bowl   | Date          | Away team             | Away team score| Home team            | Home team score|
|                    ---       | ---           |       ---             |  ---           |   ---                |    ---         | 
| Super Bowl LIII (53)         |3 February 2019| **New England Patriots**| **13**       | Los Angeles Rams     |  3             |
| Super Bowl LII (52)          |4 February 2018| **Philadelphia Eagles** | **41**       | New England Patriots | 33             |
| Super Bowl LI (51)           |5 February 2017|**New England Patriots** | **34**       | Atlanta Falcons      | 28             |
| Super Bowl 50                |7 February 2016|  Carolina Panthers      | 10           | **Denver Broncos**   | **24**         |
| Super Bowl XLIX (49)         |1 February 2015| **New England Patriots**| **28**       | Seattle Seahawks     | 24             |
| Super Bowl XLVIII (48)       |2 February 2014| **Seattle Seahawks**    | **43**       | Denver Broncos       | 8              |
| Super Bowl XLVII (47)        |3 February 2013| **Baltimore Ravens**    | **34**       | San Francisco 49ers  | 31             |
| Super Bowl XLVI (46)         |5 February 2012| **New York Giants**     | **21**       | New England Patriots | 17             |
| Super Bowl XLV (45)          |6 February 2011| Pittsburgh Steelers     | 25           | **Green Bay Packers**| **31**         |
| Super Bowl XLIV (44)         |7 February 2010| **New Orleans Saints**  | **31**       | Indianapolis Colts   | 17             |


## Data cleaning in R
This step is extremely important in the project workflow. Knowledgeable manipulation skills can save hours of work that can be devoted to data interpretation and implementing good data visualization practices.

Download the nflscrapR package directly from Github in RStudio:

```r
# need 'devtools' to download packages from Github
install.packages('devtools')
devtools::install_github(repo = "maksimhorowitz/nflscrapR")

# load the package
library(nflscrapR)
```

The following is R code for retrieving the win probability statistics for Super Bowl LII, and a quick ggplot line graph for exploratory data analysis. The complete R script is available [here](https://github.com/sokolj1/Super-Bowl-Data-Visualization/blob/master/data_visualization_nflscrapR.R).

```r
# import additional libraries for data viz and manipulation
library(ggplot2)
library(dplyr)

# extract the statistics for the last game of the 2017 season (Super Bowl LII)
super_bowl52 <- game_play_by_play(GameID = tail(extracting_gameids(2017, 
playoffs = TRUE), n = 1))

# queries time remaining after each play, home team win probability, away team win probability, and play description 
eagles_pats <- data.frame(super_bowl52$TimeSecs,super_bowl52$Home_WP_post,
super_bowl52$Away_WP_post, super_bowl52$desc)

# omit erroneous instances where home team win probability == away team win probability
eagles_pats_final <- na.omit(eagles_pats[!(eagles_pats$super_bowl52.Home_WP_post == eagles_pats$super_bowl52.Away_WP_post),])

# rename columns
colnames(eagles_pats_final) = c("time_remaining", "Home", 
"Away", "Play Description")

# ggplot of Super Bowl LII for EDA
ggplot(eagles_pats_final, aes(x = time_remaining,
y = Home)) + geom_line(aes(x = time_remaining, 
y = Home,color = "#c60c30"), size = 0.7) + 
geom_line(aes(x = time_remaining, y = Away, color = "#004953"), size = 0.7) + 
scale_x_reverse(breaks = c(3600, 3300, 3000, 2700, 2400, 2100, 1800, 1500, 1200, 900, 600, 300, 0), 
labels = c("Kickoff", "", "","End of Q1","","", "Halftime", "","","End of Q3","","","End of Regulation")) + scale_y_continuous(labels = scales::percent, limits = c(0.10,1)) + ylab("Win Probability") + xlab("") + 
ggtitle("Super Bowl LII Win Probability Chart") + 
scale_color_manual(values=c("#004953", "#c60c30"), labels = c("PHI", "NE")) + 
labs(color = "", caption = "Source: nflscrapR") + theme(panel.background = element_blank(), 
axis.line.x = element_line(colour = "#DCDCDC"), 
panel.grid.major.y = element_line(size=.1, color="#DCDCDC"), axis.ticks = element_blank())
```

<img src="../assets/Super-Bowl-Dashboard/sb_52_5_19_2019_ai.jpg" align="center" > 

A few noticeable observations is the Eagles commanded the greater win probability for a majority of the game, suggesting the Eagles were in the drivers seat with the exception of a few minutes in the first quarter and the final minutes of the game. Although this is a great visualization tool, the graphic doesn't provide context for the data itself, such as what play occurred that changed the win probability. This involves another layer of data complexity, preferably with plot interactivity. Tableau was my choice to incorporate an interactive data visualization solution. 

One nflscrapR attribute for game_play_by_play data is play description after each play, so this is ideal for providing the user context with respect to win probability. After extracting the win probablities and play description, the individual dataframes were concatenated using rbind(), then written to a [csv file](https://github.com/sokolj1/sokolj1.github.io/blob/master/assets/Super-Bowl-Dashboard/super_bowl46_52.csv). 

Perhaps the biggest challenge was extracting and tabluating the team scores data. nflscrapR only provides the possession team and defensive team scores. So the scores had to be organized by possession and defense for each team, then joined together by the common fields of TimeRemaining and Super Bowl.

```r
# PHI Score
# filters by possession team 
sb52_phi_pos <- super_bowl52 %>% filter(super_bowl52$posteam == "PHI")

# queries time remaining and scores when Philly possessed the ball 
sb52_phi_pos <- data.frame(sb52_phi_pos$TimeSecs, sb52_phi_pos$PosTeamScore)

# rename columns
colnames(sb52_phi_pos) = c("TimeRemaining", "Score")

# filters by defensive team 
sb52_phi_def <- super_bowl52 %>% filter(super_bowl52$DefensiveTeam == "PHI")

# queries time remaining and scores when Philly played defense
sb52_phi_def <- data.frame(sb52_phi_def$TimeSecs, sb52_phi_def$DefTeamScore) 

# rename columns
colnames(sb52_phi_def) = c("TimeRemaining", "Score")

# join both possession and defensive dataframes by common field TimeRemaining
sb52_phi_merge <- merge(sb52_phi_pos, sb52_phi_def, by = "TimeRemaining", all = TRUE)

```

The dataframe needs to be reversed to show beginning of the game counting down to the end; NA values also need to be removed.

```r
# reverses the dataframe so TimeRemaining is organized in decreasing order, also removes na values 
sb52_phi_scores  <- cbind(sb52_phi_merge[1], mycol = apply(sb52_phi_merge[-1], 1, max, na.rm = TRUE))
sb52_phi_scores <- sb52_phi_scores[dim(sb52_phi_scores)[1]:1,]

# rename columns
colnames(sb52_phi_scores) = c("TimeRemaining", "Away")
```

```r
# merge both PHI and NE Scores in one dataframe
sb52_scores <- merge(sb52_phi_scores, sb52_ne_scores, by = "TimeRemaining")
sb52_scores <- data.frame(sb52_scores[dim(sb52_scores)[1]:1,], rep("Super Bowl 52", nrow(sb52_scores)))
colnames(sb52_scores) = c("TimeRemaining", "Home", "Away","Super Bowl")
```

This code is just for tabluating the scores for the Philadelphia Eagles. Unfortunately, not all the data was clean. I cross validated the scores after each significant play with ESPN, and for a few games the scores were incorrect. A notable example was Super Bowl 50, so I had to manually correct the scores of the dataframe with the appropriate timeRemaining value. Albeit a tedious process, the result of rigourous data cleaning was another separate [csv file](https://github.com/sokolj1/sokolj1.github.io/blob/master/assets/Super-Bowl-Dashboard/super_bowl_scores.csv) that contains the time remaining, home and away scores, and corresponding Super Bowl. Now this data is ready for visualization. 

## Tableau Dashboard
The end product is the dashboard embeded using Tableau Public. The workbook can be downloaded by clicking on the 'download' icon on the bottom right corner of the dashboard.

Since I created this dashboard for a data visualization course, I incorporated the three major concepts learned during the course: Tufte's Principles, Kosslyn's Principles, and Cairo's Wheel. A few examples these ideas implemented are described below:

- Tufte's Principles: 
1. Above all else, show the data. The focus should be on the content of the data. 
2. Data-ink / total ink. One should maximize the data-ink ratio, within reason.
3. Emphasize important data elements using color.
<br>
- Kosslyn's Principles:
1. The color scheme should be cogent and simple to understand in context of the visualized data
2. Understanding breaks down once too much information. Provide neither too much or too little information.
3. Provide neither too much or too little information.
<br>
- Cairo's Wheel:
1. Functionality (0.9)  to Decoration (0.1): Measures the embellishment/decorative detail incorporated into the visualization.
2. Multidimensionality (0.7) to Familiarity (0.2): Assess the structure of the visualization and the dimensions used to access additional data
3. Density (0.7) to Lightness (0.3): Measures the granularity of the data. 

I hope this post serves as an example for how powerful Tableau dashboards can be for visualizing data.


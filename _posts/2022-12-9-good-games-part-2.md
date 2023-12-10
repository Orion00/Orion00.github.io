---
layout: post
title:  "Good Games Analysis: Part 2 (The Answers the Data Gave)"
author: Orion Bowers
description: "Insights about highest rated board games according to BoardGameGeek" 
image: "/assets/images/AIGenerated/freepik/catinbox.png"
---
# Introduction

In this installment, I'll talk you through jungle of the Exploratory Data Analysis I went through to discover the legendary city of gold: insights about popular board games. If you're curious where this data came from, check out my [other](/_posts/2022-11-17-good-games-part-1.md) post here.

The purposes of this post are

1. Discuss the factors in the dataset
2. Help you discover related variables in popular board games
3. Help you find some new games to play based on mechanics you enjoy playing with

With that out of the way, let's get to the data science stuff.

# Variables

Because of the one hot encoding I did to analyze mechanics, our dataset is 500 rows by 187 columns. You can view all the information in the first 12 rows. In no particular order, here's a breakdown of each variable:

![First 5 rows of dataset]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/full_data_head.png)

![First 5 rows of dataset](/assets/images/goodgames/full_data_head.png)

Rank - Rank between 1 (highest rated) and 500 (lowest rated)

Title - The name of the game so to speak

BGG_rating - Rating out of 10. Based on Average rating, but weighted towards 5.5/10 to prevent games with relatively few ratings to rise too high on the leaderboard. More information on Board Game Geek's [FAQ](https://boardgamegeek.com/wiki/page/BoardGameGeek_FAQ).

avg_rating - Rating out of 10. Average rating for that game calculated using BGG users. More information on BGG's [FAQ](https://boardgamegeek.com/wiki/page/BoardGameGeek_FAQ).

list_price - 

amazon_price - Price on Amazon.com. Updated several times a day.

year - Year released.

game_id - Unique identifier used by BGG to identify games.

min_players, max_players - Minimum and maximum number of players for the game.

playing_time - Typical playing time. It felt more descriptive than minimum and maximum playing time since playing times vary wildly. If no typical is listed, games seem to default to maximum playing time.

mechanics - List of mechanics for that game. Each mechanic is also one hot encoded in the rest of the data.

# Visualizations

## Insight: Some games are really long

Looking at the dataset, one of the first things I noticed was the inclusion of absurdly long playing times. One of my current favorite games to play is Arkham Horror: the Card Game (Rank 27 in this dataset). In my experience, it takes a good 2.5 hours to a single scenario, and there are about 8 missions in a scenario. That's a 20+ hour commitment to play the same game with the same people 8 times. When reporting playing time, Arkham Horror counted a single mission as the playing time, which seems reasonable. Not every game did that, resulting in skewing my beautiful plots.

![Minimum Number of Players vs Playing Time](/assets/images/goodgames/minPlayersvsPlayTime.png)
![Minimum Number of Players vs Playing Time, outliers removed](/assets/images/goodgames/minPlayersvsPlayTimeEdited.png)

![Minimum Number of Players vs Playing Time](/assets/images/goodgames/minPlayersvsPlayTime.png) ![Minimum Number of Players vs Playing Time, outliers removed](/assets/images/goodgames/minPlayersvsPlayTimeEdited.png)

[<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/minPlayersvsPlayTime.png" style="width:200px;"/>](/assets/images/goodgames/minPlayersvsPlayTime.png) [<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/minPlayersvsPlayTimeEdited.png" style="width:200px;"/>](/assets/images/goodgames/minPlayersvsPlayTimeEdited.png)

Sleepings Gods and The 7th Continent boast playing times of 20 hours and 16.67 hours respectively. Looking deeper into both, they're both campaign games like Arkham Horror. I've not played either game, but I feel it's safe to assume both don't require 15+ hours of play in one sitting.

Moving past the outliers, I was curious if there was a connection between the minimum number of players and the length of the game. Based on these plots, I'd say the play time for games with a minimum of 1 player is a little higher than games with a higher minimum, but it's hard to tell for sure.

What I can tell is that if you're looking to play popular games solo or with one other player, I'd recommend blocking out at least an hour. There are plenty of short 2 player games, but it seems the longer ones are higher rated on BGG.

I was also curious if games had gotten longer over the years. Ignoring games from before 1980, it looks like playing time has increased, but not by much. Modern game design has changed board games a lot but game length doesn't seem to have changed as much as I expected.

![Year Published vs Playing Time](/assets/images/goodgames/yearvsPlayTime.png)

## Insight: Some games are really expensive

Similar to playing time, there are some impressive outliers in the price department of these games. (Side note: I decided to use Amazon's price rather than the list price BGG provides because there were more games with an Amazon price than with a list price.)

![Year Published vs Amazon Price](/assets/images/goodgames/yearvsPrice.png)

Do you see the price of some of those games? $800 for some cardboard? While I do believe board games actually provide a superb bang for your buck, I don't know if I'll be spending $800 on a game anytime soon. Once again, some games may be reporting prices differently than others. Arkham Horror is listed at $23.88 on Amazon. What that doesn't include is the dozens of expansions, some of which are pricier than the base game. I'm not sure I want to add up how much I've spent on Arkham Horror, but I can somewhat mostly guarantee it's short of $800 (probably).

In addition to some interesting outliers, this plot does answer another question I had. Do games go up in price as the years go on? I would say yes, there is some sort of trend upward there. Is it a significant amount when considering inflation? I'm not sure. But my gut says yes, prices are going up.

## Insight: Some mechanics are more popular than others

Finally! My initial question. What mechanics are the most popular? Unfortunately it's not that simple to answer. You see, for fun I decided to make the same plot with the 500 top games, 100 top games, and 50 top games Board Game Geek has to offer. And the top mechanics changed! That's cheating!

[<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/mostFreqMechanics500.png" style="width:200px;"/>](/assets/images/goodgames/mostFreqMechanics500.png) [<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/mostFreqMechanics100.png" style="width:200px;"/>](/assets/images/goodgames/mostFreqMechanics100.png) [<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/mostFreqMechanics50.png" style="width:200px;"/>](/assets/images/goodgames/mostFreqMechanics50.png)

At the very least, there are a few mechanics that stick. Hand management (one of my personal favorite mechanics), 

## Insight: These variables do not correlate well with each other



Dashboard: EDA based on mechanics



# Wrapup

Bias
Next steps: Determine insights for hand management (most popular mechanic)
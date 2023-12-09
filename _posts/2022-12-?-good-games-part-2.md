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

Because of the one hot encoding I did to analyze mechanics, our dataset is 500 rows by 187 columns. You can view all the information in the first 12 rows.

![First 5 rows of dataset]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/full_data_head.png)

Rank - Rank between 1 and 500, 1 being highest rated

Title - Name of the game so to speak

BGG_rating - BoardGameGeek's ranking charts are ordered using the BGG Rating, which is based on the Average Rating, but with some alterations. To prevent games with relatively few votes climbing to the top of the BGG Ranks, artificial "dummy" votes are added to the User Ratings. These votes are currently thought to be 100 votes equal to the mid range of the voting scale: 5.5, but the actual algorithm is kept secret to avoid manipulation. The effect of adding these dummy votes is to pull BGG Ratings toward the mid range. Games with a large number of votes will see their BGG Rating alter very little from their Average Rating, but games with relatively few user ratings will see their BGG Rating move considerably toward 5.5. This is known as "Bayesian averaging" and a quick search of both BGG and/or the Web will reveal much discussion on the topic. You will see this rating listed in advanced searches, your game collection, and near the top, most right corner of game pages.

avg_rating - "The average of all the ratings from registered BGG users, calculated by adding up the individual ratings and dividing by the number of ratings. You will see this rating listed in advanced searches and near the top of game pages." [(FAQ)](https://boardgamegeek.com/wiki/page/BoardGameGeek_FAQ)

list_price - 

amazon_price - Price on amazon. Updated frequently.

year - Year released

game_id - Unique identifier used by BGG to store games

min_players, max_players - Minimum and maximum number of players for the game

playing_time_min - Average playing time. Felt more descriptive than minimum and maximum playing time since playing times vary wildly.

mechanics - List of mechanics. Each mechanic is also one hot encoded in the rest of the data.

# Visualizations

Max playing time: 20 hours. That's a full campaign of Arkham. Sleeping Gods	(1200) and The 7th Continent (1000).

Graphing by year, remove Go (-2000) and Chess (1475), Crokinole	(1876), Acquire	(1963), Dune (1979)

Fix Chess's playing time

Dashboard: EDA based on mechanics

Amazon Price vs list price


# Wrapup
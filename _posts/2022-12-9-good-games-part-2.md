---
layout: post
title:  "Good Games Analysis: Part 2 (The Answers the Data Gave)"
author: Orion Bowers
description: "Insights about highest rated board games according to BoardGameGeek" 
image: "/assets/images/AIGenerated/DALL-E/LoadedDie.png"
---
# Introduction

In this installment, I'll talk you through jungle of the Exploratory Data Analysis I went through to discover the legendary city of gold: insights about popular board games. If you're curious where this data came from, check out my [other](https://orion00.github.io/tinyproject/2022/11/17/good-games-part-1.html) post here.

The purposes of this post are

1. Discuss the factors in the dataset
2. Help you discover related variables in popular board games
3. Help you find some game mechanics you enjoy playing with

With that out of the way, let's get to the data science stuff.

# Variables

Because of the one hot encoding I did to analyze mechanics, our dataset is 500 rows by 187 columns. However, all the information is more easily readable just in the first 12 rows. In no particular order, here's a breakdown of each variable:

![First 5 rows of dataset]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/full_data_head.png)

Rank - Rank between 1 (highest rated) and 500 (lowest rated)

Title - The name of the game so to speak

BGG_rating - Rating out of 10. Based on Average rating, but weighted towards 5.5/10 to prevent games with relatively few ratings to rise too high on the leaderboard. More information on Board Game Geek's [FAQ](https://boardgamegeek.com/wiki/page/BoardGameGeek_FAQ).

avg_rating - Rating out of 10. Average rating for that game calculated using BGG users. More information on BGG's [FAQ](https://boardgamegeek.com/wiki/page/BoardGameGeek_FAQ).

list_price - Suggested retail price. It seems to be based on prices of several places to buy the game.

amazon_price - Price on Amazon.com. Updated several times a day. For my analysis, I decided to use Amazon's price rather than the list price BGG provides because there were over twice as many games with an Amazon price than with a list price. And Amazon's prices were a little cheaper.

year - Year released.

game_id - Unique identifier used by BGG to identify games.

min_players, max_players - Minimum and maximum number of players for the game.

playing_time - Typical playing time. It felt more descriptive than minimum and maximum playing time since playing times vary wildly. If no typical is listed, games seem to default to maximum playing time.

mechanics - List of mechanics for that game. Each mechanic is also one hot encoded in the rest of the data.

# Visualizations

## Insight: Some games are really long

Looking at the dataset, one of the first things I noticed was the inclusion of absurdly long playing times. One of my current favorite games to play is Arkham Horror: the Card Game (Rank 27 in this dataset). In my experience, it takes a good 2.5 hours to a single scenario, and there are about 8 missions in a campaign. That's a 20+ hour commitment to play the same game with the same people 8 times. When reporting playing time, Arkham Horror counted a single mission as the playing time, which seems reasonable. Not every game did that, resulting in skewing my beautiful plots.

[<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/minPlayersvsPlayTime.png" style="width:415px;"/>](/assets/images/goodgames/minPlayersvsPlayTime.png) [<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/minPlayersvsPlayTimeEdited.png" style="width:415px;"/>](/assets/images/goodgames/minPlayersvsPlayTimeEdited.png)


Sleepings Gods and The 7th Continent boast playing times of 20 hours and 16.67 hours respectively. Looking deeper into both, they're both campaign games like Arkham Horror. I've not played either game, but I feel it's safe to assume both don't require 15+ hours of play in one sitting.

Moving past the outliers, I was curious if there was a connection between the minimum number of players and the length of the game. Based on these plots, I'd say the play time for games with a minimum of 1 player is a little higher than games with a higher minimum, but it's hard to tell for sure.

What determine is that if you're looking to play popular games solo or with one other player, I'd recommend blocking off at least an hour. There are plenty of short 2 player games, but it seems the longer ones are higher rated on BGG.

I was also curious if games had gotten longer over the years. Ignoring games from before 1980, it looks like playing time has increased, but not by much. Modern game design has changed board games in many ways, but game length doesn't seem to have changed as much as I expected.

![Year Published vs Playing Time]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/yearvsPlayTime.png)


## Insight: Some games are really expensive

Similar to playing time, there are some impressive outliers in the price department of these games.

![Year Published vs Amazon Price]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/yearvsPrice.png)

Do you see the price of some of those games? $800 for some cardboard? While I do believe board games actually provide a superb bang for your buck, I don't know if I'll be spending $800 on a game anytime soon... 

...or will I? Arkham Horror is listed at $23.88 on Amazon. While that's true for the base game, what that price doesn't include is the 20 or 30 expansions, some of which are pricier than the base game. I'm not sure I want to add up how much I've spent on Arkham Horror, but I can somewhat mostly guarantee it's short of $800 (probably).

In addition to some interesting outliers, this plot does answer another question I had. Do games go up in price as the years go on? I would say yes, there is some sort of trend upward there. Is it a significant amount when considering inflation? I'm not sure. But my gut says yes, prices are going up.


## Insight: Some mechanics are more popular than others

Finally! My initial question. What mechanics are the most popular? For fun I decided to make the same plot with the 500 top games, 100 top games, and 50 top games Board Game Geek has to offer. 

[<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/mostFreqMechanics500.png" style="width:80%;margin: auto;"/>](/assets/images/goodgames/mostFreqMechanics500.png) [<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/mostFreqMechanics100.png" style="width:80%;margin: auto;"/>](/assets/images/goodgames/mostFreqMechanics100.png) [<img src="{{site.url}}/{{site.baseurl}}/assets/images/goodgames/mostFreqMechanics50.png" style="width:80%;margin: auto;"/>](/assets/images/goodgames/mostFreqMechanics50.png)

Some mechanics shifted up while others shifted down. As the games got higher rated, Solo games, Variable Setup, and End Game bonuses went up. More interesting were Income and Hexagon Grid based games. They went from not appearing on the list for 500 games, to ranks 6 and 8 for 50 games. That makes me think one two things. First, it's a fluke. The top games happen to all have the same mechanics. Second, (and more likely to me), the mechanics are fun but aren't super common. Using that intuition, I'll be checking out some Income and/or Hexagon Grid based games.

Some mechanics did stay on all three plots. Hand management, Variable Player Powers (one of my personal favorite mechanics), Dice Rolling, and Variable Set up all survived the cuts. Once again, I've got a few ideas as to why. First, they're fun mechanics. All 4 add randomization and longevity to a game, two important factors for a rating. Second, Those are very common mechanics. It's hard for me to think of a game that doesn't include at least one of those 4 mechanics (Arkham Horror has 3). Based on those thoughts, I feel those mechanics appeared on all three plots because they're more frequent than the mechanics that jumped up as the number of games decreased. Takeaway? Don't worry too much about getting games with those mechanics. Odds are, you'll end up having them no matter what game you try.


## Insight: These variables do not correlate well with each other

Honestly, I expected the variables in this dataset to be better predictors of each other than they are. Amazon price has a .97 correlation value with list price, but I'd hope it's that high because list price is partially based on amazon price! Past that, the next two highest correlation values are BGG rating and rank (-.93) and Player rating and BGG Rating (.65). In both cases, the second depends on the first. Ignoring variables that depend on each other, the only correlation pair that might be significant is list price and average rating, but that's only got a value of .59 (moderately correlated). It does make sense that as a game gets rated higher, prices go up. Or more games that are more expensive to produce (and thus are more pricey) tend to be higher rated. There may also be an additional variable like game company that affects both. Certain companies tend to cater towards either high end or low end games and that can affect their ratings and price.

![A Correlation Matrix of Numerical Variables]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/correlationMatrix.png)

Moving past correlation, this graph is an excellent descriptor for how BGG rating is calculated. If you recall from earlier (or scroll up a few times), you'll remember that BGG rating is a rating that weights games (especially games with a low number of reviews) closer to 5.5. You can visually see how each Average rating score was converted to a BGG rating. The further the distance between the two points in the same rank, the fewer the reviewers there are.

![Rank vs Rating by Rating Type]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/rankvsRating.png)


# Wrapup

After running through this analysis, I expected to see more useful trends. Honestly, things still feel pretty murky for me. I guess that makes sense. If getting your game to rank 1 was solved, we'd have a pretty similar looking top 50 list. Instead, there's a wide variety of mechanics, playing times, prices, and player counts for top games. And I can appreciate variety in games.

One thing you may want to know, I think this data is biased. Ratings are primarily by English speaking, board game enthusiasts who care enough about games to write reviews. If you don't fall into that category, the ratings may not work as well for you. Evidently I'm an English speaking board game enthusiast, so those people do exist. Who knows? Maybe I'll get around to writing a review one of these days.

If I were to continue this project, I'd run through some EDA for games with the top mechanics (Hand Management, Variable Player Powers, etc) and see if they're different than games without them. Luckily, that's something you can do if you're curious. You've got access to the [data](https://github.com/Orion00/goodgames/blob/main/data/full_data.csv), [web scraping scripts](https://github.com/Orion00/goodgames/blob/main/datacollection.py), [visualization script](https://github.com/Orion00/goodgames/blob/main/visualizations.py), and a [fancy dashboard](https://goodgamesdataexploration.streamlit.app/). See what you can find and let me know! There's some pretty great stuff out there if you look hard enough.
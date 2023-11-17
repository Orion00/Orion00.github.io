---
layout: post
title:  "Good Games Analysis: Part 1 (Data Collection and Cleaning)"
author: Orion Bowers
description: "Insights about highest rated board games according to BoardGameGeek" 
image: "/assets/images/AIGenerated/freekpik/catinbox.png"
---
# Introduction

Have you ever discovered a new favorite board game? Or rediscovered an old favorite?

I certainly have. Often, it's when my family or friends invite me to play a game with them. Sometimes the game is good and sometimes it isn't. Sometimes it's designed well but I don't particularly jive with it. I've begun a project where I can more easily discover new favorite games. Hopefully this project will be helpful to you as well.

Part 1 Overview

1. Document collection and cleaning for my board game data
2. Document ethical measures taken during data collection
3. Give a sneak peek into EDA for the data

With that out of the way, let's get to the data science stuff.

# Data Collection

## Phase 0: The Shoutout

Big shoutout to [Board Game Geek](https://boardgamegeek.com/) for having so much public data! It's a good community of people trying to share their hobby with others. Data is publicly available and they have an API for easy use. Without them, investigating board game mechanics becomes much more difficult.

## Phase 1: The Table
If you click on "Browse," then "[All Boardgames](https://boardgamegeek.com/browse/boardgame)" on the navbar for Board Game Geek, you'll be taken to a sorted list of each game they have in their database conveniently listed in table format.

For phase 1, I had to web scrape the first 500 on that list. After several hours of work in Python's Selenium, I realized I could use Pandas' `read_html()` to turn my hard-fought 30 lines of code into 1 line of code that executed more quickly. Putting my pride on the shelf, I used the simpler option, although I did preserve the code as a monument to my ignorance. 

As it turns out, because the column containing prices varied in formatting, `read_html()` wasn't able to read anything in for it. Thankfully, I was a newfound pro in Selenium, so after a few more hours of testing (and some help from an infamous AI), I was able to finish with a function that saved both types of prices if they existed in the table.

## Phase 2: The API
If you were paying attention, you may have noticed the tables didn't display all the information we need to figure out what makes a game top ranked. Instead, I had to turn to BGG's very own API for help. As far as my research can discover, there are two documentations for the same API, [one](https://boardgamegeek.com/wiki/page/BGG_XML_API&redirectedfrom=XML_API#) more robust than the [other](https://api.geekdo.com/xmlapi2).

Unfortunately for me, the initial table data didn't include the game's BGG id number. So I had to make 2 types of API calls, and essentially join all 3 datasets together. Table data joined with the first API dataset, which added a game id that I could search by for the second API call (As a side note, if you ever design a board game, please avoid using a "-" in the title. It'll save everyone a few hours figuring out how to work around it). Now having the game id, I was able to use a second API call which brought in the meat of the data. I decided limit myself by grabbing the play time, min and max player, and mechanics of each game, although there were far more options to choose from.

## Phase 3: The Scripts
Feel free to run my scripts [here](https://github.com/Orion00/goodgames) if you'd like a front row seat of the action. And by that, I mean alt-tabbing while Python does some heavy lifting for 10 or 15 minutes. You'll want to run `datacollection.py` (Phase 1) then `databuffing.py` (Phase 2).

As I was testing, I did discover discrepancies in my data as I scraped BGG's list. None of the games changed rank, but the prices did fluctuate by a few cents throughout the day. So be warned, prices won't be exactly the same if you decide to do this project yourself.

# Data Cleaning and Prep
Almost all the data cleaning was done as the data was being scraped and retrieved through API calls, so it's tough to point to one section of the code and say "that's where I did the dishes and the data got clean." It was more like handwashing dishes right after each meal.

My biggest banes while cleaning were definitely the title, year, and prices columns. `read_html()` read in the game's name, year, and description as one column, so I had to use regex to grab what I needed. The award of "most troubling titles" go to "Pulsar 2849," "1960: The Making of the President," and "Bruxelles 1893" because they contain a year as well. The award of "most vexing years" goes to "Go," reportedly released in year -2200. Thankfully, regex is one powerful dishsoap when it comes to data cleaning.

Mechanics are stored in both a column of lists as well as one hot encoded at the end of the data. Why? Because I'm not sure which will be easier to work with when it comes to visualizations.

# Ethical Considerations

Checking BGG's robots.txt, they ask for a crawl delay of 5 seconds. My scraper already took several seconds to process, so I wasn't too worried about adding a time delay at the end.

The API [terms of use](https://boardgamegeek.com/wiki/page/XML_API_Terms_of_Use) are fairly straightforward. Anyone can reproduce and publicly display the data as long as they a) don't use it commerically without permission, b) don't modify the data, c) credit Board Game Geek, and d) show off their sweet API logo.

<!-- <img src="{{site.url}}/{{site.baseurl}}/assets/images/AIGenerated/DALL-E/CatLaptop.png" alt="" style="width:100px;"/> -->
![Board Game Geek API logo]({{site.url}}/{{site.baseurl}}/assets/images/goodgames/bggAPILogo.jpeg)

In the API documentation, the author noted "if you send requests too frequently, the server will give you 500 or 503 return codes, reporting that it is too busy. Currently, a 5-second wait between requests seems to suffice." This seems more like advice if the requests aren't working and less like a specific time delay, so I used a short time delay (as well as the length of time it took to run the script) and didn't have any issues.

## Sneak Peek for EDA

My biggest question when starting this project was "what game mechanics make a popular game?" so of course, that was my first visual. While I don't think this visual tells it all, it did surprise me. I expected single player games to be far less popular and team based games to be far more popular.

![Most frequent mechanics of top 500 board games from Board Game Geek](/assets/images/goodgames/mostFreqMechanics.png)

Is this really the answer to my question? I guess we'll have to wait to find out.

# Wrap Up
So there you have it. Web scraping and APIs for one of my favorite hobbies. Stay tuned for Part 2: The Answers the Data Gave.
---
layout: post
title:      "Project 3: Housing Price Prediction"
date:       2020-01-28 00:48:25 +0000
permalink:  project_3_housing_price_prediction
---


This project focuses on housing data. A new start-up company, Pretend Houses, is looking to buy properties and rent them out in order to make a profit. As they're a start up company, they don't have much capital but they would like to buy several properties in a zip code to help manage their risk as they grow. It was my goal to recommend the 5 best zip codes for them to invest in.

## Decisions, Decisions

One of the first things I had to do what figure out what angle to approach this project from.  I haven't ever done anything with investing before and I've only ever bought one house: the one that I live in.  And I definitely didn't do any data science to figure out that we should get this one; I just saw the living room and liked how it looked.

I knew that I wanted to be ethical about my recommendations.  I wanted to avoid contributing to [gentrification](https://www.law.georgetown.edu/poverty-journal/blog/examining-the-negative-impacts-of-gentrification/) and I didn't want Pretend Houses to end up being [slumlords](https://definitions.uslegal.com/s/slumlord/).   I know that they'd like to turn a profit but, in order to avoid exploitation, I purposely left out zip codes with property values in the lowest quartile.

This presents problems, too, however.  If developers aren't willing to move in and create affordable housing for low-income people, then that causes issues, too.  It increases a lot of gaps including education (which relies on property taxes for some ungodly reason) and limits access to resources like businesses, parks, healthy food, doctors, etc.

It's not an easy problem to solve.  

As Pretend Houses was specifically looking to maximize their profits while minimizing risk, however, they didn't seem like the right company for the lowest income zip codes.  That would necessitate a more altruistic organization - probably a non-profit and/or government agency (which also causes [problems](https://www.city-journal.org/html/how-public-housing-harms-cities-12410.html).)

## Outside Impacts

Another thing that came into play was the knowledge of things that are difficult to include in housing price models.  For example, one of the zipcodes that my model recommended is on the coast of North Carolina.  Having lived in the southeast for nearly the entireity of my life, I would not recommend coastal properties to anyone.   Every year, hurricanes batter SC and NC and they're only getting more intense as climate change ramps up.  So, even though the historical data looks pretty good for that zip code, I would not say that it's a solid long term investment.  Same goes for all of the Florida zip codes that found their way into the top 10 zipcodes that were recommended by my model.

I suppose, one way I could control for that in the future is to just remove southeastern coastal properties before I even start doing any analysis.  But then it gets tricky: what about tornadoes in the midwest? Earthquakes and wildfires along the west coast? Heatwaves and droughts in the southwest?  Maybe we should all live in underground bunkers.

## Answers?
A bunch of these questions are more easily answered in real life.  If Pretend Houses was instead Actual Houses, their mission statement and vision would be a lot more well-developed.  I could get a better sense of what's important to them and what risks they're willing to take and which ones they aren't.  I think that because they're not real, it highlights the major importance of getting to know your company/industry.  It's really difficult to make good recommendations without having a good knowledge of the context surrounding the data.

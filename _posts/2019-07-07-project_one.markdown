---
layout: post
title:      "Project One"
date:       2019-07-07 18:00:14 -0400
permalink:  project_one
---


*The problem*:  Given the [King County housing data](https://www.kaggle.com/harlfoxem/housesalesprediction), come up with a model to predict the price of a house.  

In this project, I did a lot of things.

One of the hardest things I did was getting started.  It was really difficult to even know where to begin and so I fell back on the tactics that have worked for me as a math teacher and as a learner:
* Ignore the question
* *Do what you know how to do* <--- That's what this blog entry is about
* List out what you have/need
* Un-ignore the question
* Come up with a plan
* Revise, Revise, Revise
* Answer the question
* Make sure you've answered the question

Sometimes, the question being asked is just too much to take in all at once.  It's like trying to go to a far off destination without a map.  Instead of being overwhelmed by the whole problem at once, I just ignore the end goal for a little bit until I feel more oriented.   And that's exactly what I did with this project.  Before starting, I had some general idea of how to do it but it's sorta like if someone told me that my goal was to stand on the moon.  I mean, I know I need to take a rocket to the moon  but that's not enough of a plan to actually get me there.  

After ignoring the actual problem, I get to make one of my own.  This is the part I like best because it's easy to feel successful here.  For this project, the first thing I knew I had to do was look at the data (obviously).  It's really hard to use the data if you haven't looked at it.  And, luckily, I'm an expert at looking at data.  Also - it's really great to start with something that you can be successful with because:
> Success breeds success.

It builds your confidence and, because of your strengthened confidence, you can stick with tasks longer and deal with more frustration.

Anyway, my plan, at first, was just to look at the data and so I did.

```
king_co = pd.read_csv("kc_house_data.csv")
king_co.head()
```

|id|date|price|bedrooms|bathrooms|...|long|sqft_living15|sqft_lot15|
|--|-----|------|------------|------------|--|-----|---------------|------------|
|7129300520|10/13/2014|221900.0|	3|	1.00	|...|	-122.257|	1340|	5650
|6414100192	|12/9/2014|	538000.0|	3	|2.25|...|-122.319|	1690	|7639
|5631500400|	2/25/2015	|180000.0	|2	|1.00|...|	-122.233|	2720|	8062
|2487200875	|12/9/2014|	604000.0|	4|	3.00	|...|-122.393|	1360|	5000
|1954400510|	2/18/2015	|510000.0|3	|2.00|...|-122.045	|1800	|7503

Easy.  What else do I know how to do?  (That's the big question that really drives this forward until I have a better idea of how to get to my goal - I just keep asking, "And what else?" Another good question is: "What does that mean?" because it usually leads to more questions.)

Everything looked alright from the table but I knew that this was a raw dataset so obviously things needed cleaned up.  I just didn't know exactly what cleaning needed to be done so, again, I did the easy things first.  I looked for null values, missing data, all that great stuff.  But once I'd cleaned up the straightforward things, I decided to take a look at the histograms to see what the variables looked like and if anything weird popped up.

![](https://i.imgur.com/zKoJmfW.png)

Those graphs seem fine but there are a number of weird things:
* there are only 19 graphs but 21 variables
* none of the variables are normally distributed
* the axis scales are different by orders of magnitude
* some of the graphs appear to only have one bar

If you want more details about how I dealt with all of those problems, you're welcome to read through the [code for my project](https://github.com/alvacat/dsc-v2-mod1-final-project-online-ds-pt-051319/blob/master/student.ipynb) but for this blog post, I'm going to zoom in one of those issues specifically:  none of the variables are normally distributed.

Normally distributed data can make for better models and so I thought I'd try to transform my variables to make them a bit less skewed.  

I immediately ran into some issues.  First, there were several variables that had entries with a value of 0.  For example, `sqft_basement` was often 0.0 square feet (which is exactly how big the basement is for a basement-less house).

I don't know if you've ever tried to take the log 0 but it's not great.  By which I mean its undefined and impossible.  It's not even a complex/imaginary answer - it's just undefined.  So, for anything that had a potential value of 0, I actually had to take the log (x+1).  The graphs are practically the same (especially as x gets bigger) but it gets rid of the whole issue of impossible answers.

![](https://i.imgur.com/7AkCmZS.png)

The other issue is that some values are negative.  For instance, all of the longitude values are around -122 (which is really 122 degrees West).  Taking the log of negative numbers isn't as impossible as zero, at least.  In fact, log(-122) is equal to 2.08635983 + 1.36437635*i*. 

But, having complex values in a regression model is probably something to avoid (for now, anyway).  The easiest way to deal with that was to just take the absolute value of the longitudes.  It's totally fine to do this because:
* all of the houses are in approximately the same longtitude.  I don't have to worry about getting -122 (122 West) mixed up with 122 (122 East) because none of the houses are anywhere close to 122 degrees East.
* the graph of log(x) is symmetric to the graph of log(-x), just reflected over the y-axis.

Here's my code:
```

maybe_log_columns=king_co_train.drop(['id','date','price','zipcode'],axis=1) #getting a list of the possible predictor columns

maybe_log_columns['long']=abs(maybe_log_columns['long']) #taking the absolute value of the longitude column

for column in maybe_log_columns: #graphing all of the variables with and without taking the log of their values
    fig=plt.figure()
    ax1=fig.add_subplot(121)
    ax2=fig.add_subplot(122)
    maybe_log_columns[column].hist(label=column,ax=ax1)
    column_log=np.log(maybe_log_columns[column]+1)
    column_log.hist(label=column +' log',ax=ax2)
    ax1.set_title(column)
    ax2.set_title("Log of " + column)
```

When I went to take the log of the variables, I realized that it might not be the right decision for every column so I wanted to compare their before/after graphs to see if taking the log actually made them more normal or not.  (Actually, I didn't think about this until I tried taking the log of everything and finding out that my model sucked.  Then I went back and was a little more intentional about my choices.)

These are (some of) the graphs I got from my code.

First, here's an example of one that benefited from the transformation:
![](https://i.imgur.com/2PD7erj.png)

And here's one that didn't benefit:

![](https://i.imgur.com/NmkJ13C.png)

And here's one that was worse off:

![](https://i.imgur.com/s9nS8Wc.png)

The ones that got more normal were `sqft_living`, `sqft_lot`, `sqft_above`, `sqft_living15`, and `sqft_lot15` so I transformed those.  Anything that didn't benefit or actively got worse was not transformed.

Being more intentional with my transformations did end up helping my model and the R-squared value got higher. Funnily enough though, only one of those transformed variables (`sqft_above`) actually ended up in my final model.

* **Square foot of living space**:  This got removed because it was highly correlated (r >0.75) with several other variables in the dataset.  It was highly correlated with the number of bathrooms, the non-basement square footage of the house (`sqft_above`), and the mean square footage of its nearest 15 neighbors (`sqft_living15`).  It was also pretty closely related to the grade.  All of those other variables (aside from `sqft_living15`) ended up in my final model.
* **Square footage of the lot**, of the **nearest 15 neighbors' lots**, of the **nearest 15 neighbors living spaces**:  These were all close to being included in my final model and could actually have been included but the increase of complexity wasn't worth the tiny boost to the adjusted R-squared value.

I realize that most of the variables that ended up in my final model aren't transformed - some of them are standardized but the shape of their distributions are the same.  In future projects, I'd like to figure out more transformations I could use and when it's appropriate and useful to do so.  I think I enjoy thinking about transformations because it's a very math-y part of this whole process and that's where I feel most comfortable right now.  It'll be interesting to see how things change over the next few months.


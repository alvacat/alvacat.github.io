---
layout: post
title:      "The Magic of Collaboration"
date:       2020-06-05 18:10:54 +0000
permalink:  the_magic_of_collaboration
---


For my capstone project, I decided to look at the vast set of Magic: The Gathering cards and build a model to predict their prices.

Side note: Magic is a collectible card game with a thriving side market where players (and investors) can buy, sell, and trade their cards.  Some of them are quite expensive and some of them are essentially free.  As you might expect, cards that are expensive tend to be rare and/or very good to have in a competitive deck.  In my project, I attempted to pin down what exactly makes a card expensive.

I’ve played Magic for a few years but only very casually.  Essentially, I know the basics but I’m nowhere close to being a competitive player.  Compared to my previous projects, however, I can actually say I have some background knowledge in this area.  And, as you might’ve seen in my last blog post, one of my biggest obstacles has been not really having enough knowledge of the field to be able to form good questions and insights about the data.

So, this time I started off the project in a lot better shape but I quickly ran into problems.  Like, almost immediately.  Luckily, I also had something else for this project that I did not have before: an actual expert in the field.  

  ## My Expert

My Magic expert actually lives in the same house as me: my husband has been playing Magic since he was in middle school 26 years ago and it’s safe to say he understands all the intricacies of the game.  He’s even traveled to Italy to act as a judge for a Magic tournament!

I asked him *a lot* of questions during the course of this project.

## The Expert’s Role

### His Thoughts
As a consultant on this project, my experience was utilized to provide relevant details about traits of Magic cards which could influence their market price, as well as questions about how certain mechanics within the game of Magic the Gathering worked. Most of the questions I was asked accomplished those ends. 
 
There were various traits of Magic cards that I brought to your attention that you may not have realized existed, such as double-faced cards, split cards, and Companion cards. *He’s right.  I did not know about split cards or Companion cards.  He also brought my attention to recent rule changes about Companion cards.*
 
I feel like I played an important role, providing the context that was required to make a more robust model.
 
I don't think there was anything I would have changed about our collaboration. I think my best advice for data scientists is to make sure you have a comfortable, trusting relationship with the consultants that you may rely on. It's important that everyone feels at ease enough to ask any questions and raise any concerns without hesitation. You are there to learn from your consultants (and possibly vice versa); leave your ego at the door.

### My Thoughts
I think my questions to my expert fell into two categories: “what does this mean?” and “do you think this is important?” 

#### “What does this mean?” 
These questions were pretty factual.  There’s a lot more to Magic than I realized so it was helpful to be able to ask him things like, “What does ‘Y’ mean in the card’s text?” and “What is a ‘TimeShifted’ card?”  and “What’s a card that costs a lot of different colors to cast?”  Those fact-gathering questions were useful because they saved me a ton of time.  than spending hours searching online.  Sometimes I asked for really specific examples that would’ve been extremely hard to find just by searching online.  I’m sure I could’ve figured out the answers to most of these questions on my own eventually but there are something like 50,000 different cards so it was nice to be able to consult my expert’s encyclopedic knowledge instead.

#### “Do you think this is important?” 
These questions focused more on interpretation and required an expert to make an informed decision. 

One of the first things I did in my project was to map out the SQL database of Magic cards to see what data was available.  Then, I painstakingly went through every table to figure out which columns I thought might possibly affect a card’s price.  Some columns were obvious: the power and toughness of a card will definitely have an effect.  Other columns were much more difficult to figure out.  One example was “hasNoDeckLimit” which indicates whether there can only be a certain number of copies of that card in a deck. (Typically, each card is limited to a maximum of 4 copies in a single deck.) I initially thought it could affect the price - after all, if there’s no limit to how many of them you can have, they’ve got to be pretty special (or pretty bad).  When I asked my expert about it, though, he said that there are so few cards (maybe 5?) that don’t have a limit that it wasn’t worth including that variable at all.   There were also several occasions were I’d ask him about my results to make sure they made sense to an actual Magic expert.  The numbers would seem weird to me (or I’d have no sense of whether they were in the right ballpark or not) and he’d be able to look at them and tell me if they made sense or if they were unexpected (in which case, I’d go back and check my code for errors).  

Having an intuition and deep understanding of Magic was invaluable.  And me having access to his expertise enriched and expanded the work I was able to do.  In future projects, I fully intend to continue collaborating with experts - even if I have to look outside my own house to find them.

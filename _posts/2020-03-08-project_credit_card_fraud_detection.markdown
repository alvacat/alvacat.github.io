---
layout: post
title:      "Project: Credit Card Fraud Detection"
date:       2020-03-09 00:50:16 +0000
permalink:  project_credit_card_fraud_detection
---

Here's my project: https://github.com/alvacat/dsc-mod-5-project-online-ds-pt-071519

It involves looking at a bunch of credit card transactions and classifying them as fraudulent or genuine.

## Evaluating Models

One of the problems I ran across with this project was that the classes were incredibly unbalanced.  The fraud cases only made up 0.17% of the dataset.  It's also really important to catch those fraud cases which meant that false negatives (i.e. missed fraud) needed to be as minimized as possible.

### Aside: Trues and Falses
- True Positive: Fraudulent transaction that's detected <--Perfect
- False Positive: Genuine transaction that's marked as fraud <--Stressful and inconvenient but easy to deal with
- True Negative: Genuine transaction that's marked as genuine <-- Perfect
- False Negative: Fraudulent transaction that's marked as genuine <--Terrible, terrible consequences

### Measurements
There are several choices when it comes to determining how well a classification model does.  Typically, these are the four that are used:
- Accuracy
- Precision
- Recall
- F1

#### Accuracy
It's tempting to use accuracy (I mean, the name itself talks about how accurate something is) but, accuracy doesn't take false negatives into account.)  But accuracy is focused on how many predictions are correct overall.  It doesn't separate out the most important factor for this dataset: false negatives (aka an incorrect prediction).

Here's the formula for accuracy: perfect predictions/total number of predictions.  (Perfect predictions means true positives and true negatives.) 

If we want the majority of our predictions to be correct, accuracy is a great measure to use.  But, in this project, it's more important to minimize false negatives.

#### Precision
Precision focuses on the positive predictions.  Here's the formula:

Precision = true positives/total number of positive predictions.  

Precision answers the question: out of all of the positive predictions that were made, what percentage of them were correct?  Based on that, it's fairly easy to see that false negatives aren't accounted for at all so precision is definitely not the best evaluation metric to use for this project.

#### Recall
Recall has a similar formula to precision but there's an important difference:

Recall = true positives/total number of actual positives

Recall answers the questions: out of all of the actual positives, what percentage of them were labeled as positive?  So, at first glance, it might seem that this doesn't look at false negatives either but let me rephrase that question with the terms "fraud" and "genuine":

Out of all of the actual frauds, what percentage of them were labeled as fraud?

Now, it's a lot clearer that false negatives (i.e. missed frauds) are accounted for by the recall score.  If the recall is high, that means the model labeled most/all of the fraud cases as fraud which is exactly what we want.  Recall is definitely the best metric to use for this project. 

#### F1
F1 is about balancing the false negatives and true positives.  It would be easy enough to catch all the fraud cases by just labeling every single transaction as fraud.  That's not a super useful model though; it would be frustrating for the consumers to have to call the credit card company every time they made a transaction and it would be incredibly time-consuming for the company to have to deal with all of those calls. 

F1 = (precision<sup>-1</sup>+recall<sup>-1</sup>)<sup>-1</sup>  (the harmonic mean of precision and recall)

Because it takes both false positives and true negatives into account, F1 is also an important metric to look at for this project.

### Winners!
Recall is the clear winner followed by F1 in second place.  Accuracy and precision aren't useful on their own for this project so, while I calculated them, they were not an important factor in my decisions.

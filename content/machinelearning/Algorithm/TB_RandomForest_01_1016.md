---
title: "[DataScience][TreeBasedMethod] Random Forests (1)"
date: 2018-10-16T12:59:33+08:00
draft: false
tags:
    ["Algorithm", "TreeBasedMethod"]
categories:
    ["DataScience", "MachineLearning"]
authors: ["bradlee"]
---
# Random Forests explained intuitively
**Original Post**:https://www.datasciencecentral.com/profiles/blogs/random-forests-explained-intuitively

# What is the Random Forest
## Forest
Random forest is a collection of many decision trees. Instead of relying on a single decision tree, you build many decision trees say 100 of them. And you know what a collection of trees is called - forest.

## Random
There are two levels of randomness in this alforithm:

- At **row** level: Each of these decision trees get a random sample of the training data (say 10%) each of these trees will be trained independently on 10% randomlyy chosen rows out of all rows of data.

- At **column** level: Not all the columns are passed into training each of the decision trees. Say we want only 10% of columns to be sent to each tree. If our data set has 30 coulmns, this means a randomly selected 3 columns will be sent to each tree. So for the first decision tree, may be column C1, C2, and C4 were chosen. The next decision tree will have C4, C5, and C10 as chosen columns.

The results from each of the tree are taken and the final result is declared accordingly. Voting and averaginng is used to predict in case of classification and regression respectively.

# Disadvantage
- Random forests don't train well on **smaller datasets** as it fails to pick on the pattern.

- There is a problem of **interpretability** with random forest. You can't see or understand the relationship between the response and the independent variables.

- The **time** taken to train random forests may sometimes be **too huge** as you train multiple decision trees.

- In the case of a regression problem, the range of the values response variable can take is determined by the values already available in the training dataset. Unlike linear regression, decision trees and hence random forest can't take value **outside the training data**.

# Advantage
Since we are using multiple decision trees, the **bias** remains same as that of a single decision tree. However, the **variance** decreases and thus we decrease the chances of overfitting.

When all you care about is the predictions and want a quick and dirty way out, random forest comes to the rescue.

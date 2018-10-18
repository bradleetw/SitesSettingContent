---
title: "[GoogleResoure][ML Concepts] 01 Fundamental Machine Learning Terminology"
date: 2018-10-18T21:43:19+08:00
draft: false
tags:
    ["GoogleMachineLearning"]
categories:
    ["GoogleResource"]
authors: ["bradlee"]
toc: true
mathjax: true
---
Source: https://developers.google.com/machine-learning/crash-course/framing/ml-terminology
# Framing
- How to frame a task as a machine learning problem

## Learning Objectives
- Refresh the fundamental machine learning terms.

- Explore various uses of machine learning.

## ML Terminology
### Label
- **Label**: is the true thing we're predicting: $y$
    - The $y$ variable in basic linear regression

### Features
- **Features**: are input variables describing our data: $x_i$
    - The ${x_1, x_2, ... x_n}$ variables in basic linear regression

### Example
- **Example**: is a particular instance of data, $x$
    - **Labeled example**: has {feature, label}: ($x, y$)
        - Used to **train** the model
    - **Unlabeled example**: has {feature, ?}: ($x$, ?)
        - Used for **making predictions** on new data

### Model
- **Model**: defines the relationship between features and label.
    - **Training phase**: means creating or learning the model. Show the model labeled examples and enable the model to **gradually** learn the relationship between features and label.
    - **Inference phase**: means applying the trained model to unlabeled examples.

### Regression model
- **Regression model**: predicts **continuous** values. For exampl,
    - What is the value of a house in California?
    - What is the probability that a user will click on this ad?

### Classification model
- **Classification model**: predicts **discrete** values. For example,
    - Is a given email message spam or not spam?
    - Is this an image of a dog, a cat, or a hamster?

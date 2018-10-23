---
title: "[GoogleResoure][ML Concepts] 02 Descending Into ML"
date: 2018-10-23T20:32:35+08:00
draft: false
tags:
    ["GoogleMachineLearning"]
categories:
    ["GoogleResource"]
authors: ["bradlee"]
toc: false
mathjax: true
---
Source: https://developers.google.com/machine-learning/crash-course/descending-into-ml/video-lecture

# Descending into ML
**Linear regression** is a method for finding the **straight line** or **hyperplane** that best fits a set of points. This module explores linear regression intuitively before laying the groundwork for a machine learning approach to linear regression.

## Learning Objectives
- Refresh your memory on line fitting.

- Relate weights and biases in machine learning to slope and offset in line fitting.

- Understand "loss" in general and squared loss in particular.

## Descending into ML: Linear Regression
The equation for a linear regression model.

**$y' = b + w_1x_1 $**

where:

- $y'$: The predicted label (a desired output).

- $b$: The **bias**, sometimes referred to as $w_0$.

- $w_1$: The weight of feature 1.

- $x_1$: a feature (a known input).

A more sophisticated model might rely on multiple features, each having a separate weight ($w_1, w_2$, etc.)

**$y' = b + w_1x_1 + w_2x_2 + w_3x_3$**

## Descending into ML: Training and Loss
**Training a model** simply means learning(determining) good values for all the weights and the bias from labeled examples.

In supervised learning, a machine learning algorithm builds a model by examining many examples and attempting to find a model that **minimizes loss**; this is called **empirical risk minimization**.

Loss is the penalty for a bad prediction. That is, **loss is a number indicating how bad the model's prediction was on a single example.** If the model's prediction is **perfect**, the loss is **zero**; otherwise, the loss is greater.

The goal of training a model is to find a set of weights and biases that have **low loss**, on average, across all examples.

### Squared Loss: a popular loss function
The linear regression models we'll examine here use a loss function called **squared loss** (also known as **L$_2$ loss**).

= Square of the difference between prediction and label

= (Observation - prediction($x$))$^2$

= $(y-y')^2$

### Mean square error (MSE)
MSE is the average squared loss per example over the whole dataset.

$$MSE = \frac{1}{N}\sum_{(x,y)\in D}(y-prediction(x))^2$$

where:

- $(x,y)$ is an example in which

    - $x$ is the set of features that the model uses to make predictions.

    - $y$ is the example's label.

- $prediction(x)$ is a function of the weights and bias in combination with the set of features $x$.

- $D$ is a data set containing many labeled examples, which are $(x,y)$ pairs.

- $N$ is the number of examples in $D$

Although MSE is commonly-used in machine learning, it is neither the only practical loss function nor the best loss function for all circumstances.

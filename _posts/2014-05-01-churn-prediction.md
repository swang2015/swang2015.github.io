---
layout: post
title:  "Predicting Customer Churns in Telecom (draft)"
date:   2014-05-01 14:20:00 -0500
categories: business-intelligence
tags: logistic-regression
---

Competition between telecommunication providers is tense. (So are in banking and other industries.) It's usually expensive to acquire a customer. If we can know the leaving customers in advance and try to keep them, it would be much easier. Churn (loss of customers) prediction is an important task in telecom marketing. 

## Business Understanding

We can summarize some subproblem to this project:
- Which customers (especially high value customers) might be leaving?
- What is the feature of these customers?
- How much is the cost to retain these customers?

###### What is churn?

Is it just when customers suddenly stop using the number? Or is it when the account balance is less than 0? When we create the model we should make clear of the definition with some professionals before labeling the data. For example, churn can be defined as when cancelling an account, when debt is overdue for three months, or when the customer did not use the number to make phone calls for a couple of months. 

###### Selecting user features

The data the we use can be categorized into three categories: user's basic information, their behavior records, comments and satisfaction, etc. Sometimes depending on the actual conditions, we are not able to obtain all the data.

###### The time window of data

How to decide the length of time of the data that we use for analysis? If it's too long the data cannot reflect the most recent trends, but if it's too short the random effect might given a large impact. Here we take the data of 6 months long to predict customer churns.

###### Profit

|Expected profit = Expected income from leaving customers - Cost to retain them|

The cost to retain the leaving customers may cover cost for marketing, propaganda and promotions.

## Data Preparation

Usually data understanding and data preparation takes 60-70% the period of the whole project.
Assuming we have cleaned data and combined them into a large wide table, we have:

- customer's basic information: ID, gender, age, length of stay, plans, brand of cellphone
- calls/texts/data: local/national/international usage, day/night/evening usage, usage in total
- details of the plan
- churn labels

Make sure that the data are accurate and within a reasonable range. Be creative and we can derive some new variables such as trends, peak useage, ratios from the data. 

## Model Building and Evaluation

We choose logistic regression which is fit for predicting binary response in this project.


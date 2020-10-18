---
title: 'Covariate Shift and dataset shift'
date: 2019-03-18
permalink: /posts/2019/03/covaritaAndDatasetShift/
tags:
  - Machine Learning
---

If you have productionized a new machine learning model, most probably you have faced the situation after a while the performance of your model has degraded. Let’s say train a model with 90% precision and you are happy with it. You ship the model into production and check the model performance over time. In a month, you see that the model precision has been decreasing over time and has reached 70% precision. Now you may wonder why this is happening. The chances are you the distribution of new data in production is significantly different than the distribution of the data you used for training. This phenomenon is known as the covariate shift or dataset shift.

## Covariate shift: 
This phenomenon happens when the distribution of inputs used as predictors (covariates) changes between the training and production stage, i.e. P<sub>train</sub>(X) != P<sub>production</sub>(X)

## Dataset shift: 
when the joint distribution of inputs and the outputs (the target being predicted) also changes, i.e. P<sub>train</sub>(X, y) != P<sub>production</sub>(X, y)



### Causes of covariate and dataset shift: 
The covariate and dataset shift happen due to two major factors 
- sample selection bias 
- non-stationary environments (when the predictions distribution changes due to different factors such as seasonality, new users, change of entities/products).

### How to detect/treat covariate and dataser shift
In the real-world, the models are retrained with fresh data on a regular basis to resolved this issue this process can be automated with (Airflow)[https://airflow.apache.org/]).
In case, it is expensive to retraining the model regularly, you can check for a covariate shift in your data and when the distribution of data has changed dramatically, you can start the process of retraining the model with fresh data. 

We can detect covariate shift by using data from the training stage and label it with “train” and get a sample from new data/fresh and label it “fresh”. We can train any ML model on this data and if the model predicts the label better than random, there is a covariate shift happening in the data (You can check if your model is doing better than random chance by checking [Matthews correlation coefficient (MCC) or phi coefficient](https://en.wikipedia.org/wiki/Matthews_correlation_coefficient))

Read more here:
(DATASET SHIFT IN MACHINE LEARNING)[http://www.acad.bg/ebook/ml/The.MIT.Press.Dataset.Shift.in.Machine.Learning.Feb.2009.eBook-DDU.pdf]

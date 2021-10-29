---
title: 'Chapter 1'
date: 2021-07-19
permalink: /posts/2020/07/MLDLChapater1/
tags:
  - Machine Learning
  - Deep Learning
  - Interview
---


Cost function: squared of difference, convex
Algorithm: Gradient Descent (each time taking the derivative of the cost function with respect to one of the parameters) or numerically (via normal equation and matrix inverse). theta= (XTX)-1 XTy (here inverse O(n3)). However, if the number of features is larger than the number of data points, the matrix XXT is not invertible and we should get the pseudo inverse.  When we add regularization, we are sure that the matrix is invertible     Is the regularization added here (lambda identity matrix) is L2


If XTX is positive semi-definite it’s not invertible (smallest eigenvalue 0), when we add regularization, we make it positive definite and hence invertible. We are seeing regularization is adding diagonal elements in XTX then, XTX is the full rank matrix. Full rank is an invertible matrix (remember 𝜆𝐼 is positive definite).
A matrix is positive definite if and only if all of its eigenvalues are positive. 
An  symmetric real matrix M is said to be positive-definite if for all non-zero x in .
XTX is PSD because (let’s call the vector v) vT XTX v = (Xv)(Xv)=(Xv)2 which is always >= 0

Collinearity 
In the presence of collinearity, standard coefficient errors increase and the calculated t-statistics are underestimated. Indicators of multicollinearity:
High R2 and negligible odds.
Strong pair correlation of predictors.
Strong partial correlations of predictors.
High VIF - variance inflation factor   (VIF(xj) = 1 / (1- R Squared xj|x-j)   If VIF(xj)>10 multicollinearity is high, a cut of 5 is also commonly used. 

Assumption of Linear regressions

1. Linear Relationship: The relationship between the independent and the dependent variables should be linear.
2. Multivariate Normality: All the variables should be multivariate normal.
3. No or Little Multicollinearity: There should be little or no multicollinearity in the data.
4. No Auto-Correlation: There should be little or no Autocorrelation in the data. When the residual data are not independent of each other, Autocorrelation takes place.
5. Homoscedasticity: The residuals should be equal across the regression line


Where t is the actual value (y)

Metrics for evaluation:
Mean Squared Error (MSE) :        1/n  sumi  (yi - fi) 2 
Root mean squared error:            1/n sqrt(sumi  (yi - fi) 2 )

R squared:                 1 - ( sumi  (yi - fi) 2 /  sumi (yi - mean(y))2 )              i.e.    1 - (RSS/TSS)
adjusted R squared:              1 - ( (sumi  (yi - fi) 2  / (n + p - 1  ) /  ( sumi (yi - mean(y))2   / (n - 1 ))

RSE: Residual standard error:           sqrt (RSS / (n - p - 1) )    i.e.    (residual error/ degree of freedom)

Collinearity link
here are two main problems that arise with collinearity:
The parameter estimates have high variance ( and have large standard errors, which makes the individual variables nonsignificant)
Tiny changes to the input data can have huge effects on the parameter estimates, even reversing their signs (and being significant both times, in opposite directions).

There are many ways to deal with collinearity (to detect collinearity you can use VIF).
Get more data
Drop variables
Do principal component regression
Do partial least squares regression

Logistic regression:
Cost function: Cost(h(x) , y) = -y log h(x)  - (1 - y) log(1 - h(x))    convex
 remember the cost function of linear regression is not convex for logistic (because of 1/1+e-x)
Algorithm: gradient descent. There is no closed form solution for logistic regression here.

The loss function for logistic regression is Log Loss, which is defined as follows with regularization (explanation on how we have obtain log loss from likelihood of theta)


The regularization term is divided by 1/2m for a couple of reasons: 1) to make the cost function comparable in different batch sizes. 2) to scale down regularization as the size of training examples grows, basically, we need less regularization as the number of data points grows. 3) Making λ comparable across different datasets and less hyperparameter tuning when the size of data changes. 

Multi-class classifier: for k classes, we trained k classifiers (one versus all) and assigned the data point to the class with the highest probability. Then we can use the log loss function (equivalent to the above cost function for only two classes).

where N is the number of samples or instances, M is the number of possible labels, yij is a binary indicator of whether or not label j is the correct classification, for instance, i, and pij is the model probability of assigning label j to instance i.
An ROC curve plots TPR vs. FPR at different classification thresholds.
Recall for multi-class LR we have:

Assumption of Logistic regressions
the independent variables do not need to be multivariate normal – although multivariate normality yields a more stable solution 
homoscedasticity isn’t needed (residuals don't need to be equal across the regression line)
assumes that there is minimal or no multicollinearity among the independent variables
the independent variables are linearly related to the log of odds
LR fits a single line to divide the space, hence the space should be linearly separable
Maximum likelihood and log loss
Link, also this one
Basically we want to find the 𝜃 to maximum likelihood of data in each class. Basically, it means how likely the data could be assigned to each class or label.
where f is the density function.




 where y^ is the probability of y being predicted as 1
Density function of binary classification problem (or the mean)



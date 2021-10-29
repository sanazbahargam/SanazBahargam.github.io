---
title: 'Chapter 1'
date: 2021-07-19
permalink: /posts/2020/07/MLDLChapater1/
tags:
  - Machine Learning
  - Deep Learning
  - Interview
---


Linear Regression:
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


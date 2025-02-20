# Week 3

## 1 Regression Metrics

+ MSE, RMSE, R-squared
+ MAE
+ (R)MSPE, MAPE
+ (R)MSLE

### 1.1 MSE, RMSE, R-squared

#### 1.1.1 MSE and RMSE
<p align="center">
  <img src="../res/img/img118.png" width="600"/>
</p>

+ RMSE and MSE are very similar, but they can not be immediately interchangeable for gradient based methods (need to adjust parameters, like learning rate)
+ RMSE or MSE cannot use to evaluate a model only by looking at its value -> use R2

<p align="center">
  <img src="../res/img/img119.png" width="500"/>
</p>

#### 1.1.2 R2

+ Optimizing MSE is equivalent to optimizing R2
+ R2 is MSE score divided by a constant and substracted another constant

<p align="center">
  <img src="../res/img/img120.png" width="600"/>
</p>

### 1.2 MAE

+ Not that sensetive compared to MSE
+ Widely used in financial area ($10 error is usually exactly two times worse than $5 error)

<p align="center">
  <img src="../res/img/img121.png" width="600"/>
</p>

### 1.3 MSE vs. MAE

<p align="center">
  <img src="../res/img/img122.png" width="600"/>
</p>

### 1.4 MSPE and MAPE

+ MSE and MAE can not reflect the data well in this case
+ MAPE and MSPE are basically MAE and MSE with weighted
+ Curve become more flat

<p align="center">
  <img src="../res/img/img123.png" width="500"/>
  <img src="../res/img/img124.png" width="500"/>
</p>

### 1.5 (R)MSLE

+ (R)MSLE - MSE in log space
+ Use same as MSPE and MAPE
+ Relative errors more compared the absolute errors
+ Assymetry error curve: better to predict more than target value

<p align="center">
  <img src="../res/img/img125.png" width="600"/>
</p>

### 1.6 Summary

+ RMSLE > MAPE / MSPE
+ MAPE and MSPE have strong bias to smaller values

<p align="center">
  <img src="../res/img/img126.png" width="600"/>
</p>

## 2 Classification Metrics

### 2.1 Notations

<p align="center">
  <img src="../res/img/img127.png" width="600"/>
</p>

### 2.2 Accuracy score

+ Need hard predictions
+ Baseline could be very high

<p align="center">
  <img src="../res/img/img128.png" width="600"/>
</p>

### 2.3 Logloss

For multi-classes, if the number of classes is two -> binary case

<p align="center">
  <img src="../res/img/img129.png" width="600"/>
</p>

### 2.4 AUC, ROC

+ How to calculate area:
  1. Start with the bottom left one
  2. Go right when meets a red dot
  3. Go left when meets a green dot
+ Does not depend on the abosluate values, but ordering of objects
+ Transfer soft to hard labels -> removes the dependence of the score on threshold

<p align="center">
  <img src="../res/img/img130.png" width="600"/>
</p>

+ Dot line: how is the curve if our predictions are randomly generated
+ Basicline: 0.5

<p align="center">
  <img src="../res/img/img131.png" width="500"/>
  <img src="../res/img/img132.png" width="500"/>
</p>

### 2.5 Cohen's Kappa

Baseline: if we have 20 cat labels and 80 dog labels, baseline would be 0.2\*0.1 + 0.8\*0.9 = 0.74

<p align="center">
  <img src="../res/img/img133.png" width="600"/>
</p>

+ Weighted error -> Quadratic and Linear Weighted Kappa
+ Usually be used as: how much the predictions of the model agree with ground-truth raters -> how much does the model agree with professional doctors

<p align="center">
  <img src="../res/img/img134.png" width="500"/>
  <img src="../res/img/img135.png" width="500"/>
</p>

## 3 Metrics Optimization

### 3.1 Introduction

+ Target metric: what we want to optimize
+ Optimization loss: what model optimizes

<p align="center">
  <img src="../res/img/img136.png" width="600"/>
</p>

### 3.2 Approaches

1. Just run the right model! -> MSE, logloss
  + Find the best model by setting the loss function to be these metrics
2. Preprocess train and optimize another metric -> MSPE, MAPE, RMSLE, ...
  + Cannot be used directly -> preprocess the data to fit the model which can use these metrics: XGBoost can not optimize MSPE, but we can change the train set to make XGBoost optimize MSE
3. Optimize another metric -> Accuracy, Kappa
  + Postprocess predictions
4. Optimize other metrics
  + Early stopping
4. Write custom loss function
  + Example:

<p align="center">
  <img src="../res/img/img137.png" width="500"/>
  <img src="../res/img/img136.png" width="500"/>
</p>

### 3.3 Regression Metrics

#### 3.3.1 RMSE, MSE, R2

+ Left: libraries that support **MSE** optimization
+ Right: libraries that support **MAE** optimization

<p align="center">
  <img src="../res/img/img138.png" width="500"/>
  <img src="../res/img/img139.png" width="500"/>
</p>

Optimize MSE, MAE: write own functions -> hubor loss

<p align="center">
  <img src="../res/img/img140.png" width="600"/>
</p>

#### 3.3.2 MSPE, MAPE

1. Customize loss in NN or XGBoost
2. Different metics and do early stopping

<p align="center">
  <img src="../res/img/img141.png" width="600"/>
</p>

#### 3.3.3 RMSLE

Transform the dataset to log scale

<p align="center">
  <img src="../res/img/img142.png" width="600"/>
</p>

### 3.4 Classification Metrics

#### 3.4.1 Logloss

+ Random forest preidiction tends to have bad logloss performance
+ Solve above: probability calibration (modify prediction)

<p align="center">
  <img src="../res/img/img143.png" width="500"/>
  <img src="../res/img/img144.png" width="500"/>
</p>

#### 3.4.2 Accuracy

Tune the threshold (simply with for loop)

<p align="center">
  <img src="../res/img/img145.png" width="500"/>
  <img src="../res/img/img146.png" width="500"/>
</p>

#### 3.4.3 AUC (ROC)

Preferred pairwise loss -> implement logloss to AUC

<p align="center">
  <img src="../res/img/img147.png" width="500"/>
  <img src="../res/img/img148.png" width="500"/>
</p>

XGBoost learned logloss can give comparable AUC score to the one learned with pairwise loss

<p align="center">
  <img src="../res/img/img149.png" width="500"/>
  <img src="../res/img/img150.png" width="500"/>
</p>

#### 3.4.4 (Quatic weighted) Kappa

How do you otpimize it?
+ Optimize MSE and find right thresholds - simple
+ Customize smooth lost for GBDT or neural nets - hard

Find proper threshold: can be easily done by grid search

<p align="center">
  <img src="../res/img/img151.png" width="600"/>
</p>

### 3.5 Target Eoncoding

Using target to generate features

#### 3.5.1 Simple example

Generate feature mean (group by feature and calculate target mean)

<p align="center">
  <img src="../res/img/img152.png" width="600"/>
</p>

#### 3.5.2 Why does it work

+ Left: label encoding -> random groups, no apprent groups
+ Right: mean encoding -> more apprent groups of features

<p align="center">
  <img src="../res/img/img153.png" width="600"/>
</p>

Performances

<p align="center">
  <img src="../res/img/img154.png" width="600"/>
</p>

#### 3.5.3 Ways to calculate encodings

<p align="center">
  <img src="../res/img/img155.png" width="600"/>
</p>

#### 3.5.4 Springleaf example

Right: clear sign of overfitting -> if we use target mean encoding before train and test splits, we can easily get such a result

<p align="center">
  <img src="../res/img/img156.png" width="500"/>
  <img src="../res/img/img157.png" width="500"/>
</p>

Reasons of overfitting: target 1 in train and target 0 in validation

<p align="center">
  <img src="../res/img/img158.png" width="600"/>
</p>

#### 3.5.5 Regularization

Pipeline

<p align="center">
  <img src="../res/img/img159.png" width="600"/>
</p>

Code

<p align="center">
  <img src="../res/img/img160.png" width="600"/>
</p>

##### 3.5.5.1 CV Loop

<p align="center">
  <img src="../res/img/img161.png" width="600"/>
</p>

##### 3.5.5.2 Smoothing

<p align="center">
  <img src="../res/img/img162.png" width="600"/>
</p>

##### 3.5.5.3 Noise

<p align="center">
  <img src="../res/img/img163.png" width="600"/>
</p>

##### 3.5.5.4 Expanding mean

Use only rows from zero to n minus one to calculate encoding for row n

<p align="center">
  <img src="../res/img/img164.png" width="600"/>
</p>

#### 3.5.6 Generalization and extensions

##### 3.5.6.1 Regression and multiclass

<p align="center">
  <img src="../res/img/img165.png" width="600"/>
</p>

##### 3.5.6.2 Many-to-many relations

<p align="center">
  <img src="../res/img/img166.png" width="600"/>
</p>

##### 3.5.6.3 Time series

<p align="center">
  <img src="../res/img/img167.png" width="600"/>
</p>

##### 3.5.6.4 Interactions and numerical features

Mean encoding interactions: mean cencode on interaction variables

<p align="center">
  <img src="../res/img/img168.png" width="600"/>
</p>

##### 3.5.6.5 Correct validation reminder

<p align="center">
  <img src="../res/img/img169.png" width="600"/>
</p>

#### 3.5.7 Summary

<p align="center">
  <img src="../res/img/img170.png" width="600"/>
</p>
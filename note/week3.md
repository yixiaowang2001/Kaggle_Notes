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
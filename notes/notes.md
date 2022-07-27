# How to Win a Data Science: Learn from Top Kagglers

# Week 1

## 1.1 Course Overview

### 1.1.1 Week 1

+ Intro to competitions & Recap
+ Feature preprocessing & extraction

### 1.1.2 Week 2

+ EDA
+ Validation
+ Data leaks

### 1.1.3 Week 3

+ Metrics
+ Mean-encoding

### 1.1.4 Week 4

+ Advanced features
+ Hpyerparameter optimization
+ Ensembles

### 1.1.5 Week 5

+ Final project
+ Winning solutions

## 1.2 Competitions Mechanics

+ Data
+ Model
+ Submission
+ Evaluation
+ Leaderboard

### 1.2.1 Data
仔细阅读官方提供的数据，判断是否进行特征筛选

### 1.2.2 Model
不是一个特定的算法，而是一个将数据转化为答案的过程。Model最好需要具有两个特性：
+ produce best possible prediction
+ Be reproducible

### 1.2.3 Submission
提交预测结果，注意最后提交文件格式

### 1.2.4 Evaluation
评估模型结果：通过不同的evaluation function（比如Accuracy，Logistic Loss，AUC，RMSE，MAE）

### 1.2.5 Leaderboard
分为Public Test Set和Private Test Set，后者用于比赛后的最终评价

### 1.2.6 总体比赛流程
<p align="center">
  <img src="../res/img/img1.png" width="500"/>
</p>

## 1.3 Real World ML Pipeline
1. Understanding of business problem
2. Problem formalization
3. Data collecting
4. ***Data preprocessing***
5. ***Modelling***
6. Way to evaluate model in real life
7. Way to deploy model

## 1.4 Recap of ML Approach

Families of ML algorithms
+ Linear
+ Tree-based
+ KNN
+ Neural Networks

### 1.4.1 Linear model
本质思想：通过一条线划分空间为两个部分，对数据点进行分类（比如logistic regression和SVM）
+ 优点：
  + Linear model对于稀疏高维数据（sparse high dimensional data）特别好
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
  1. Linear model对于稀疏高维数据（sparse high dimensional data）特别好
+ 缺点：
  1. 线性模型的普适性弱，大多数情况下点的分布会比较复杂
+ 实现：
  1. scikit-learn
  2. Vowpal Wabbit（专门用来处理大型数据）


### 1.4.2 Tree-based
模型：Decision Tree，Random Forest，GBDT
本质思想：通过不同标准分类点
+ 实现：
  1. scikit-learn
  2. XGBoost和LightGBM提高速度和准确性

### 1.4.3 KNN
本质思想：假设一点，然后找最近距离的几个点，然后修改假设点
+ 缺陷：
  1. 需要考虑到距离的计算公式，比如square distance不能捕捉语义
+ 实现：
  1. scikit-learn（包含所有距离函数，并且可以使用自己的距离公式）

### 1.4.4 Neural Networks
+ 实现：
  1. TensorFlow
  2. mxnet
  3. Pytorch
  4. Lasagne

### 1.4.5 Conclusion
1. There is no "silver bullet" algorithm
2. Linear models split space into 2 subspaces
3. Tree-based methods splits space into boxes
4. k-NN methods heavy rely on how to measure points "closeness"
5. Feed-forward NNs produce smooth non-linear decision boundary
6. The most powerful methods are ***Gradient Boosted Decision Trees*** and ***Neural Networks***

## 1.5 Hardware/Software requirement
+ Laptop（RAM、Cores、Storage）
+ Cloud resources（Amazon AWS、Microsoft Azure、Google Cloud）
+ Software（Language）：Python
+ Basic Stack：Numpy、Pandas、scikit-learn、matplotlib
+ IDE：IPython、Jupyter notebook
+ Special packages：XGBoost（提升决策树速度）、Microsoft/LightGBM（提升决策树速度）、Keras（用户友好的神经网络框架）、danielfrg/tsne
+ External tools：Vowpal Wabbit（大型数据计算）、srendle/libfm（优化器，适用于稀疏数据比如点击率预测）、guestwalk/libffm（同上）、baidu/fast_rgf

## 1.6 Featrue preprocessing and generation with respect to models

Main topics:
1. Feature preprocessing
2. Feature generation
3. Their dependence on a model type

Features: numeric, categorical, ordinal, datetime, coordinates

### 1.6.1 具体过程
**以[Titanic的数据集](https://www.kaggle.com/competitions/titanic/data)为例**

<p align="center">
  <img src="../res/img/img2.png" width="500"/>
</p>

#### 判断数据类型

+ Survived: binary
+ Pclass: categorical
+ Name: text
+ Sex: categorical
+ Age: numerical
+ SibSp: categorical
+ Parch: categorical
+ Ticket: ID
+ Fare: numerical
+ Cabin: cateborical
+ Embarked: categorical

为什么要这么做？
1. 模型和预处理高度相关
2. common feature generation methods

#### Feature preprocessing
假设一种情况：

<p align="center">
  <img src="../res/img/img3.png" width="500"/>
</p>

pclass和目标之间很明显不是线性的情况，但如果我们要使用线性模型（随机森林在这种情况下会更好），就需要在某种程度上预处理pclass的数据，如下图：

<p align="center">
  <img src="../res/img/img4.png" width="500"/>
</p>

#### Feature generation
假设对于一个苹果的销售，我们已经拥有过去两周的销售数据和一个大致的趋势。

<p align="center">
  <img src="../res/img/img5.png" width="500"/>
</p>

如果我们决定使用线性模型，并且想要告诉模型这样的趋势，就需要添加一个feature来说明已经过去的周数（number of weeks passed）来让模型很好的找到linear dependency。

另一方面，如果考虑使用决策树，那么我们需要用到mean target value for each week这个特征。

<p align="center">
  <img src="../res/img/img6.png" width="500"/>
  <img src="../res/img/img7.png" width="500"/>
</p>

**所以总结来说，无论是feature preprocessing还是generation，都是和所使用的模型高度相关（从模型到feature preprocessing的方式）。**

## 1.7 Numeric features
+ Preprocessing
  + Tree-based models
  + Non-tree-based models
+ Feature generation


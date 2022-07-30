# How to Win a Data Science: Learn from Top Kagglers

## 1 Course Overview

### 1.1 Week 1

+ Intro to competitions & Recap
+ Feature preprocessing & extraction

### 1.2 Week 2

+ EDA
+ Validation
+ Data leaks

### 1.3 Week 3

+ Metrics
+ Mean-encoding

### 1.4 Week 4

+ Advanced features
+ Hpyerparameter optimization
+ Ensembles

### 1.5 Week 5

+ Final project
+ Winning solutions

## 2 Competitions Mechanics

+ Data
+ Model
+ Submission
+ Evaluation
+ Leaderboard

### 2.1 Data
仔细阅读官方提供的数据，判断是否进行特征筛选

### 2.2 Model
不是一个特定的算法，而是一个将数据转化为答案的过程。Model最好需要具有两个特性：
+ produce best possible prediction
+ Be reproducible

### 2.3 Submission
提交预测结果，注意最后提交文件格式

### 2.4 Evaluation
评估模型结果：通过不同的evaluation function（比如Accuracy，Logistic Loss，AUC，RMSE，MAE）

### 2.5 Leaderboard
分为Public Test Set和Private Test Set，后者用于比赛后的最终评价

### 2.6 总体比赛流程
<p align="center">
  <img src="../res/img/week1/img1.png" width="500"/>
</p>

## 3 Real World ML Pipeline
1. Understanding of business problem
2. Problem formalization
3. Data collecting
4. ***Data preprocessing***
5. ***Modelling***
6. Way to evaluate model in real life
7. Way to deploy model

## 4 Recap of ML Approach

Families of ML algorithms
+ Linear
+ Tree-based
+ KNN
+ Neural Networks

### 4.1 Linear model
本质思想：通过一条线划分空间为两个部分，对数据点进行分类（比如logistic regression和SVM）
+ 优点：
  1. Linear model对于稀疏高维数据（sparse high dimensional data）特别好
+ 缺点：
  1. 线性模型的普适性弱，大多数情况下点的分布会比较复杂
+ 实现：
  1. scikit-learn
  2. Vowpal Wabbit（专门用来处理大型数据）


### 4.2 Tree-based
模型：Decision Tree，Random Forest，GBDT
本质思想：通过不同标准分类点
+ 实现：
  1. scikit-learn
  2. XGBoost和LightGBM提高速度和准确性

### 4.3 KNN
本质思想：假设一点，然后找最近距离的几个点，然后修改假设点
+ 缺陷：
  1. 需要考虑到距离的计算公式，比如square distance不能捕捉语义
+ 实现：
  1. scikit-learn（包含所有距离函数，并且可以使用自己的距离公式）

### 4.4 Neural Networks
+ 实现：
  1. TensorFlow
  2. mxnet
  3. Pytorch
  4. Lasagne

### 4.5 Conclusion
1. There is no "silver bullet" algorithm
2. Linear models split space into 2 subspaces
3. Tree-based methods splits space into boxes
4. k-NN methods heavy rely on how to measure points "closeness"
5. Feed-forward NNs produce smooth non-linear decision boundary
6. The most powerful methods are ***Gradient Boosted Decision Trees*** and ***Neural Networks***

## 5 Hardware/Software requirement
+ Laptop（RAM、Cores、Storage）
+ Cloud resources（Amazon AWS、Microsoft Azure、Google Cloud）
+ Software（Language）：Python
+ Basic Stack：Numpy、Pandas、scikit-learn、matplotlib
+ IDE：IPython、Jupyter notebook
+ Special packages：XGBoost（提升决策树速度）、Microsoft/LightGBM（提升决策树速度）、Keras（用户友好的神经网络框架）、danielfrg/tsne
+ External tools：Vowpal Wabbit（大型数据计算）、srendle/libfm（优化器，适用于稀疏数据比如点击率预测）、guestwalk/libffm（同上）、baidu/fast_rgf

## 6 Featrue preprocessing and generation with respect to models

Main topics:
1. Feature preprocessing
2. Feature generation
3. Their dependence on a model type

Features: numeric, categorical, ordinal, datetime, coordinates

### 6.1 具体过程
**以[Titanic的数据集](https://www.kaggle.com/competitions/titanic/data)为例**

<p align="center">
  <img src="../res/img/week1/img2.png" width="500"/>
</p>

#### a. 判断数据类型
+ Survived: binary
+ Pclass: ordinal
+ Name: text
+ Sex: categorical
+ Age: numerical
+ SibSp: counts
+ Parch: counts
+ Ticket: ID
+ Fare: numerical
+ Cabin: cateborical
+ Embarked: categorical

比如Pclass，如果它是numerical，我们可以说第一类和第二类之间的差异等于第二类和第三类之间的差异，但是Pclass实际上是ordinal的，因为我们并不清楚两个差异是否相等。

为什么要这么做？
1. 模型和预处理高度相关
2. common feature generation methods

#### b. Feature preprocessing
假设一种情况：

<p align="center">
  <img src="../res/img/week1/img3.png" width="500"/>
</p>

pclass和目标之间很明显不是线性的情况，但如果我们要使用线性模型（随机森林在这种情况下会更好），就需要在某种程度上预处理pclass的数据，如下图：

<p align="center">
  <img src="../res/img/week1/img4.png" width="500"/>
</p>

#### c. Feature generation
假设对于一个苹果的销售，我们已经拥有过去两周的销售数据和一个大致的趋势。

<p align="center">
  <img src="../res/img/week1/img5.png" width="500"/>
</p>

如果我们决定使用线性模型，并且想要告诉模型这样的趋势，就需要添加一个feature来说明已经过去的周数（number of weeks passed）来让模型很好的找到linear dependency。

另一方面，如果考虑使用决策树，那么我们需要用到mean target value for each week这个特征。

<p align="center">
  <img src="../res/img/week1/img6.png" width="500"/>
  <img src="../res/img/week1/img7.png" width="500"/>
</p>

### 6.2 结论
所以总结来说，无论是feature preprocessing还是generation，都是和所使用的模型高度相关（从模型到feature preprocessing的方式）。

## 7 Numeric features
+ Preprocessing
  + Tree-based models
  + Non-tree-based models
+ Feature generation

<p align="center">
  <img src="../res/img/week1/img8.png" width="500"/>
</p>

### 7.1 Feature Preprocessing
#### a. Scaling
+ scaling对于KNN和linear都会造成影响；regularization和feature scaling是成正比的
+ gradient descent会受scaling的巨大影响
+ KNN中很重要

总结来说，不同模型所适用的scaling方法是不同的，或者可以说，选择scaling方法本身就是一个parameter needed to be optimized。

1. To [0,1]：distribution并没有变化

<p align="center">
  <img src="../res/img/week1/img9.png" width="500"/>
  <img src="../res/img/week1/img10.png" width="500"/>
</p>

2. To mean = 0, std = 1

<p align="center">
  <img src="../res/img/week1/img11.png" width="500"/>
</p>

#### b. Outliers
对于线性模型来说，outlier是影响结果的重要因素

<p align="center">
  <img src="../res/img/week1/img12.png" width="500"/>
</p>

解决方式：设定upper bound和lower bound（比如1%和99%），被称为winsorization（极值调整）

#### c. Rank
基本思路：sets spaces between proper assorted values to be equal。对于有outlier的情况，rank的处理方式可能会好于MinMaxScaler，因为rank transformation可以将异常值更接近其他对象而不是忽略他们。

<p align="center">
  <img src="../res/img/week1/img13.png" width="500"/>
</p>

#### d. Other
<p align="center">
  <img src="../res/img/week1/img14.png" width="500"/>
</p>

### 7.2 Feature generation
Ways to proceed:
1. prior knowledge
2. EDA (Exploratory Data Analysis)

比如，根据面积和价格创建变量价格每平方米：
<p align="center">
  <img src="../res/img/week1/img15.png" width="500"/>
</p>
比如，根据纵向距离和横向距离创建直接距离：
<p align="center">
  <img src="../res/img/week1/img16.png" width="500"/>
</p>
比如，根据价格创建小数价格和整数价格：
<p align="center">
  <img src="../res/img/week1/img17.png" width="500"/>
</p>

### 7.3 结论
<p align="center">
  <img src="../res/img/week1/img18.png" width="500"/>
</p>

## 8 Categorical and ordinal features

Ordinal features:
ordinal（有顺序的categorical）：
<p align="center">
  <img src="../res/img/week1/img19.png" width="500"/>
</p>

### 8.1 Encoding

#### a. Label encoding
以embarked为例：
<p align="center">
  <img src="../res/img/week1/img20.png" width="500"/>
</p>

#### b. Frequency encoding
但如果出现频率相同，那么这个encoding方式将无法区别他们
<p align="center">
  <img src="../res/img/week1/img21.png" width="500"/>
</p>

#### c. One-hot encoding
特点：already sclaed；会减慢tree的速度并且并不会提升它的表现；如果类别较多，那么会有很多充满零的列
<p align="center">
  <img src="../res/img/week1/img22.png" width="500"/>
</p>

**稀疏矩阵：**在RAM中只存储非零的element，节省空间并且提高运算速度。
<br>可以通过将两个variable并行来进行one-hot encoding：
<p align="center">
  <img src="../res/img/week1/img23.png" width="500"/>
</p>

## 8.2 总结
<p align="center">
  <img src="../res/img/week1/img24.png" width="500"/>
</p>

## 9 Datetime and coordinates
### 9.1 Date and time

#### a. Time moments in a period（当前时间）

Day number in week, month, season, year, second, minute, hour

#### b. Time passed since particular event

<p align="center">
  <img src="../res/img/week1/img25.png" width="500"/>
</p>

比如，对于销售量和Date来说，我们可以进行如下的feature generation：
<p align="center">
  <img src="../res/img/week1/img26.png" width="500"/>
</p>

#### c. Difference between date
datetime_feature_1 - datetime_feature_2
<p align="center">
  <img src="../res/img/week1/img27.png" width="500"/>
  <img src="../res/img/week1/img28.png" width="500"/>
</p>

### 9.2 Coordinates

知道一个地点的坐标后，就可以得知其他相关地址或距离的信息，比如最近的医院、最近的超市、最近的车站：
<p align="center">
  <img src="../res/img/week1/img29.png" width="500"/>
</p>

如果是训练决策树的话，可以略微rotate coordinates as new features
<p align="center">
  <img src="../res/img/week1/img30.png" width="500"/>
</p>

### 9.2 总结
<p align="center">
  <img src="../res/img/week1/img31.png" width="500"/>
</p>

## 10 Handling missing values
### 10.1 寻找missing value
missing value可能不是一个数字，可能是一个空字符串、-1、99等等。通过构建histogram来查找missing value（比如左边的histogram，-1很明显有很多重复值，所以-1可能为missing value）：
<p align="center">
  <img src="../res/img/week1/img32.png" width="500"/>
</p>

### 10.2 Fill NA approaches
1. -999, -1, etc
  + 优点：决策树可能会将其归为单独的类别
  + 缺点：linear model和神经网络会被影响
2. Mean, median
  + 优点：有利于linear model和神经网络
  + 缺点：决策树可能会很难选择有缺失值的observation
3. Reconstruct value
  + 构建"isNull"特征：
<p align="center">
  <img src="../res/img/week1/img33.png" width="500"/>
</p>

  + 如果是连续数据（比如日期），则直接重构（不怎么出现这种情况）
  <p align="center">
    <img src="../res/img/week1/img34.png" width="500"/>
  </p>

  + 如果要基于缺失值生成新的数据，那么在重构缺失值的时候就需要非常小心，很多情况下我们选择直接删除缺失值
  <p align="center">
    <img src="../res/img/week1/img35.png" width="500"/>
  </p>

### 10.3 Missing value related
我们可以把outliers当成缺失值来处理；对于出现在test data里但并没有出现在train data中的类别，outliers被划分的类别就会作为test data新出现的类别的参照。

比如，A、B、C是三个火车站，我们根据其出现次数来进行encoding：在训练数据集中，A为6，B为3，D为1。当测试数据集中出现了新的类别C，C由于也只出现了一次，所以被encoding为1，那么模型就会对待D一样去对待C。这样得到的最终结果就是可以成功被可视化的。
<p align="center">
  <img src="../res/img/week1/img36.png" width="500"/>
</p>

### 10.4 总结
<p align="center">
  <img src="../res/img/week1/img37.png" width="500"/>
</p>

## 11 Feature extraction from texts and images
对于单一文字或图像：
+ 文字：Use search engines in order to find similar text
+ 图像：神经网络（CNN）

但当图像属于附加信息：
比如Titanic中的name，就属于附加信息，我们要从中找到有用信息。同时还有根据text和image来判断广告是否重复的竞赛。

### 11.1 Text

#### a. Bag of words
创建特征：把每个单词作为一列（忽略大小写），然后记录每句话内单词出现的频率。

<p align="center">
  <img src="../res/img/week1/img38.png" width="500"/>
</p>

对于上述特征记录，我们还要对其进行缩放：
1. 目的：增加样本的可比较性；方式：Term frequency（比如，一段话有100个词，“你好”出现过三次，那么TF就是3/100=0.03）
2. 目的：强化更重要特征的权重，削弱无用的特征的权重；方式：Inverse document frequency（比如现在有10000段话，而其中100段话都有“你好”，那么IDF就是lg(10000/100)=2）

<p align="center">
  <img src="../res/img/week1/img39.png" width="500"/>
</p>

以上图的数据为例：
1. 进行Term frequency的处理（对每行进行处理）
<p align="center">
  <img src="../res/img/week1/img40.png" width="500"/>
</p>

2. 再进行Inverse document frequency的处理
<p align="center">
  <img src="../res/img/week1/img41.png" width="500"/>
</p>

与TF和IDF一样有效的方法还有**N-grams**：
<p align="center">
  <img src="../res/img/week1/img42.png" width="500"/>
</p>

将word按照N的大小分开，然后为每个组合创建一个column。有些时候处理按照character处理会比按照word处理要来的出色。Char N-grams还可以帮助模型处理看不见的字（比如，rare forms of already used words）。

实现方面（char N-gram要添加analyzer）：
<p align="center">
  <img src="../res/img/img43.png" width="500"/>
</p>

#### b. Embeddings(~word2vec)

# Week 1

## 1 Competition Overview

### 1.1 Competition Mechanics

+ Data
+ Model
+ Submission
+ Evaluation
+ Leaderboard

<p align="center">
  <img src="../res/img/img1.png" width="600"/>
</p>

### 1.2 ML Pipelines

#### 1.2.1 Real world ML pipeline

<p align="center">
  <img src="../res/img/img2.png" width="600"/>
</p>

#### 1.2.2 Competition ML pipeline

<p align="center">
  <img src="../res/img/img3.png" width="600"/>
</p>

#### 1.2.2 Things we need to care about

<p align="center">
  <img src="../res/img/img4.png" width="600"/>
</p>

## 2 ML Recap

### 2.1 Linear

+ **Examples**: Logistic regession / SVM (linear models with different loss functions)
+ **Good**: Sparse high dimensional data
+ **Limitation**: Too simple
+ **Libraries**: sklearn, vowpal wabbit

<p align="center">
  <img src="../res/img/img5.png" width="500"/>
  <img src="../res/img/img6.png" width="500"/>
</p>

### 2.2 Tree-based

+ **Idea**: Divide and conquer
+ **Examples**: Random forst and gradient boosted decision trees
+ **Good**: Tabular data
+ **Limitation**: Linear dependencies (requires a lot of splits)
+ **Libraries**: sklearn, XGBoost, LightGBM(Github)

<p align="center">
  <img src="../res/img/img7.png" width="500"/>
  <img src="../res/img/img8.png" width="500"/>
</p>

### 2.3 kNN

+ **Idea**: Closer objects are likely to have same labels (square distances)
+ **Good**: Informative
+ **Libraries**: sklearn

<p align="center">
  <img src="../res/img/img9.png" width="600"/>
</p>

### 2.4 Neural Network

+ **Idea**: Produce a smooth separating curve in constrast to decision trees
+ **Good**: Images, sounds, texts, and sequences
+ **Libraries**: TensorFlow, mxnet, PyTorch, Lasagne

<p align="center">
  <img src="../res/img/img10.png" width="600"/>
</p>

## 3 Hardware & Software

### 3.1 Hardware

<p align="center">
  <img src="../res/img/img11.png" width="600"/>
</p>

### 3.2 Software

#### 3.2.1 Basic stack

+ NumPy: Linear algebra library to work with **dimensional arrays**
+ NumPy: Provide fast and flexible way to work with a **relational table of data**
+ Scikit-learn: Classic machine learning algorithms
+ Matplotlib: **Visualizations**

#### 3.2.2 Special pakcages

+ XGBoost, LightGBM(Github): gradient-boosted decision trees
+ Keras: Neural nets
+ TSNE

#### 3.2.3 External tools

+ Vowpal wabbit: Provide blazing speed when handling really large datasets
+ Libfm(Github), libffm(Github): Implement different types of optimization machines; often used for sparse data like click-through rate prediction
+ Fast_rgf(Github): alternative based method to use in ensembles

## 4 Feature Engineering

### 4.1 Feature Preprocessing

Example: Titanic dataset

<p align="center">
  <img src="../res/img/img12.png" width="600"/>
</p>

**Look closer to one predictor and outcome:** Pclass vs. Survival

+ Data is not linear -> if implementing linear model, we need to preprocess Pclass -> Example: one-hot encoding
+ However, random forst can not use obe-hot encoding

<p align="center">
  <img src="../res/img/img13.png" width="600"/>
</p>

### 4.2 Feature Generation

+ If we have know linear relationship and want to inform the model, we can create a feature called "number of weeks passed."
+ However, it is still not working for decision tree
+ **Preprocessing and generation pipelines depend on a model type**

<p align="center">
  <img src="../res/img/img14.png" width="500"/>
  <img src="../res/img/img15.png" width="500"/>
</p>

### 4.3 Numeric Features

#### 4.3.1 Preprocessing

Based on whether the model depends on **scaling**, we can divide models into two parts: decision trees
+ Tree-based models (do not need scaling)
  + try to find the most useful split for each feature
  + won't change its behavior and predictions
+  Non-tree-based models: kNN, neural network (desperately need scaling)
  + Be affected by transformations

<p align="center">
  <img src="../res/img/img16.png" width="600"/>
</p>

**Scaling is important for:** kNN, linear model
+ Regularization impact turns out to be proprtional to feature scale
+ Gradient methood can go crazy without scaling

<p align="center">
  <img src="../res/img/img17.png" width="600"/>
</p>

#### 4.3.2 Scaling

##### 4.3.2.1 Min-max scaler

+ Effect: To [0, 1]
+ Note: Distribution won't change

```Python
sklearn.preprocessing.MinMaxScaler()
```

<p align="center">
  <img src="../res/img/img18.png" width="600"/>
</p>

##### 4.3.2.2 Standard scaler

+ Effect: To mean = 0, std = 1

```Python
sklearn.preprocessing.StandardScaler()
```

#### 4.3.3 Preprocessing: outliers

Affect **linear model** the most: both target and train

<p align="center">
  <img src="../res/img/img19.png" width="600"/>
</p>

**Winsorization**: (common in financial data) We can clip feature values between two chosen values: lower bound and upper bound -> choose some percentiles (1% & 99%)

<p align="center">
  <img src="../res/img/img20.png" width="600"/>
</p>

#### 4.3.4 Preprocessing: rank

+ Rank transformation: can be better than min-max scaler if we have outliers -> make outliers closer to other objects
+ **Benifit:** Linear model, kNN, neural networks

<p align="center">
  <img src="../res/img/img21.png" width="600"/>
</p>

#### 4.3.5 Other preprocessing methods

+ **Benifit:** neural networks
+ Also, try to preprocessing data differently -> benifit: linear model, kNN, neural networks

<p align="center">
  <img src="../res/img/img22.png" width="600"/>
</p>

#### 4.3.6 Feature generation

+ Creativity
+ Data understanding

<p align="center">
  <img src="../res/img/img23.png" width="500"/>
  <img src="../res/img/img24.png" width="500"/>
</p>

### 4.4 Categorical and Ordinal Features

+ Categorical -> order categorical (ordinal) for red box
+ Ordinal:
  + Categorical varaibles ordered in some meaningful ways
  + We don't know which difference is bigger

<p align="center">
  <img src="../res/img/img25.png" width="500"/>
  <img src="../res/img/img26.png" width="500"/>
</p>

#### 4.4.1 Label encoding

+ Map unique values to different numbers
+ Only work with tree models (tree models can treat numbers differently)

<p align="center">
  <img src="../res/img/img27.png" width="500"/>
  <img src="../res/img/img28.png" width="500"/>
</p>

#### 4.4.2 Freqency encoding

+ Store information about distributions
+ **Benifit:** Linear and tree models
+ Useful:
  + If value frequency is related to it's target value
  + Less number of splits
+ Note: multiple variables can not be distinguished if they both use frequency encoding

<p align="center">
  <img src="../res/img/img29.png" width="600"/>
</p>

#### 4.4.3 Other encodings

##### 4.4.3.1 One-hot encodings

**Benifit:** Non-tree based models -> linear, kNN

<p align="center">
  <img src="../res/img/img30.png" width="600"/>
</p>

##### 4.4.3.2 Concatenation features

**Benifit:** Non-tree based models -> linear, kNN

<p align="center">
  <img src="../res/img/img31.png" width="600"/>
</p>

### 4.5 Datetime and Coordinate Features

<p align="center">
  <img src="../res/img/img32.png" width="600"/>
</p>

#### 4.5.1 Time since

Example: sales data -> time from last campaign / time until next campaign

<p align="center">
  <img src="../res/img/img33.png" width="500"/>
  <img src="../res/img/img34.png" width="500"/>
</p>

#### 4.5.2 Time differences

Example: sales data -> time between two purchase dates

<p align="center">
  <img src="../res/img/img35.png" width="500"/>
  <img src="../res/img/img36.png" width="500"/>
</p>

#### 4.5.3 Coordinates

+ Gain information from the surrounding area
  + Divide the map into squares, get the most expensive flat in each square, add the distances
  + Use the center of each cluster as important points, add distances
  + Find special areas (e.g. really old buildings), add distances
+ Calculate aggregated distances from objects in the surrounding area
  + Caluclate the number of flats in that area (areas of polarity)
  + Add mean realty price

<p align="center">
  <img src="../res/img/img37.png" width="600"/>
</p>

+ Rotate coordinates

<p align="center">
  <img src="../res/img/img38.png" width="600"/>
</p>

## 5 Missing Values

### 5.1 Types of Missing Values
+ N/A values
+ Empty strings
+ -1
+ Very large numbers
+ -99999 less)
+ 999
+ 99

Example: matrix of samples and features

<p align="center">
  <img src="../res/img/img39.png" width="600"/>
</p>

#### 5.1.1 Hidden NaNs
+ Left: missing values are replaced by -1
+ Right: missing values are replaced by the average (right plot is on log scale)

<p align="center">
  <img src="../res/img/img40.png" width="600"/>
</p>

### 5.2 Fillna Approach

1. -999, 1, etc.
  + Pros: can possibly treat missing values as a separate category
  + Cons: linear models and neural networks might be suffered
2. Mean / median
  + Pros: works for linear models and neural networks
  + Cons: hard to select objects with missing values in the first place
3. Reconstract value

#### 5.2.1 "Is null" feature

+ Pros: solve problems with trees and neural netorks (with meanmedian)
+ Cons: double the number of columns in the dataset

<p align="center">
  <img src="../res/img/img41.png" width="600"/>
</p>

#### 5.2.2 Reconstract value

For series data only (continuous, like date)

<p align="center">
  <img src="../res/img/img42.png" width="600"/>
</p>

**Be careful**
+ Avoid replacing missing values before feature generation
+ Left: difference will be very large
+ Right: if the data is grouped by a categorical data and we are calculating mean / median, missing values with numbers will affect the result

<p align="center">
  <img src="../res/img/img43.png" width="500"/>
  <img src="../res/img/img44.png" width="500"/>
</p>

**What should we do**
+ Categorical encoding (feature generation) -> ignore missing values
+ Classification task -> treat missing values as outliers
  + Useful: when there is a new group of data in the test set

<p align="center">
  <img src="../res/img/img45.png" width="600"/>
</p>

### 5.3 Summary 

<p align="center">
  <img src="../res/img/img46.png" width="600"/>
</p>

## 6 Texts & Images

### 6.1 Texts

#### 6.1.1 Text to vectors

<p align="center">
  <img src="../res/img/img47.png" width="600"/>
</p>

##### 6.1.1.1 Bag of Words

Create a matrix and count the number of appearance for each word in those sentences

<p align="center">
  <img src="../res/img/img48.png" width="600"/>
</p>

**TFiDF**
+ Decrease the significance of widespread words
+ Require future scaling

<p align="center">
  <img src="../res/img/img49.png" width="600"/>
</p>

Example

<p align="center">
  <img src="../res/img/img50.png" width="500"/>
  <img src="../res/img/img51.png" width="500"/>
</p>

**N-grams**

<p align="center">
  <img src="../res/img/img52.png" width="600"/>
</p>

#### 6.1.2 Text processing

##### 6.1.2.1 Lowercase

<p align="center">
  <img src="../res/img/img53.png" width="600"/>
</p>

##### 6.1.2.2 Lemmatization and stemming

<p align="center">
  <img src="../res/img/img54.png" width="600"/>
</p>

##### 6.1.2.3 Stopwords

<p align="center">
  <img src="../res/img/img55.png" width="600"/>
</p>

### 6.2 Summary

<p align="center">
  <img src="../res/img/img56.png" width="600"/>
</p>
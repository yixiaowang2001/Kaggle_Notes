# Week 2

## 1 EDA

**Purpose**
+ Get comfortable with the data
+ Find magic features

### 1.1 Procedure

Example: Predict advertiser's cost

#### 1.1.1 Getting domain Knowledge

<p align="center">
  <img src="../res/img/img62.png" width="600"/>
</p>

#### 1.1.2 Checking if the data is intuitive

+ Left: Typo -> It might be 36, so we just manually correct that
+ RightL Algorithm? -> Might be a algorithm problem (algorithmn that generates the dataset), and need to be investigated further -> Create a new feature called `is_incorrect`

<p align="center">
  <img src="../res/img/img63.png" width="500"/>
  <img src="../res/img/img64.png" width="500"/>
</p>

#### 1.1.3 Understanding how the data is generated

Plot both train and test sets -> Match train set to test set

<p align="center">
  <img src="../res/img/img65.png" width="600"/>
</p>

### 1.2 Exploring Anonymized Data

#### 1.2.1 Explore individual features

+ Columns -> Meaning / Types
+ Example: x1 & x6 might hash values

<p align="center">
  <img src="../res/img/img66.png" width="600"/>
</p>

#### 1.2.2 Try to decode the features

Example

[Notebook link](https://github.com/yixiaowang2001/Kaggle_Notes/blob/main/res/notebooks/EDA_anonymous.ipynb)

<p align="center">
  <img src="../res/img/img67.png" width="600"/>
</p>

#### 1.2.3 Types of features

<p align="center">
  <img src="../res/img/img68.png" width="600"/>
</p>

### 1.3 Visualization

#### 1.3.1 Explore individual features

+ Histograms
+ Plots
+ Statistics

##### 1.3.1.1 Histogram

+ Left: without log; right: with log -> never make conclusions based on one plot
+ Right: Peak: might be missing value

<p align="center">
  <img src="../res/img/img69.png" width="500"/>
  <img src="../res/img/img70.png" width="500"/>
</p>

##### 1.3.1.2 Plots

+ Left: horizontal line -> repeated values
+ Left: horizontal line but no vertical line -> values are all randomly shuffled
+ Right: by group(color) -> data is not fully shuffled here, sorted by class label

<p align="center">
  <img src="../res/img/img71.png" width="500"/>
  <img src="../res/img/img72.png" width="500"/>
</p>

##### 1.3.1.3 Feature Statistics

+ Right: help find missing values

<p align="center">
  <img src="../res/img/img73.png" width="500"/>
  <img src="../res/img/img74.png" width="500"/>
</p>

#### 1.3.2 Explore feature relations

+ Scatter plot
+ Correlation plot
+ Plot (index vs. feature statistics)

##### 1.3.2.1 Scatter plot

+ Left: relationship between two features -> classification task, colors of points are the groups; regressiion task, heat map light coloring / values can be reflected by point sizes
+ Right: distributions of train and test sets data —> if you see some kind of discrepancy between colored and gray points distribution -> bug/overfitting (not healthy)

<p align="center">
  <img src="../res/img/img75.png" width="500"/>
  <img src="../res/img/img76.png" width="500"/>
</p>

##### 1.3.2.2 Plot (index vs. feature statistics)

+ Left: relationship between x2 and x1? -> x2 <= 1 - x1
+ Right: goal is feature generation -> make a feature to each triangle in given points belong

<p align="center">
  <img src="../res/img/img77.png" width="500"/>
  <img src="../res/img/img78.png" width="500"/>
</p>

Small data: 

<p align="center">
  <img src="../res/img/img79.png" width="600"/>
</p>

##### 1.3.2.3 Correlation plot

+ Left: before clustering: if the plot look like a mess here, we can run some kind of clustering like K-means clustering on the rows and columns of this matrix and reorder the features
+ Right: after clustering

<p align="center">
  <img src="../res/img/img80.png" width="500"/>
  <img src="../res/img/img81.png" width="500"/>
</p>

##### 1.3.2.4 Other plots

+ Left: plot (feature index vs. feature mean)
+ Right: plot after sorting feature mean

<p align="center">
  <img src="../res/img/img82.png" width="600"/>
</p>
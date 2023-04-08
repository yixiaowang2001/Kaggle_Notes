# Week 5

## 1 Crowdflower Competition Analysis

### 1.1 Problem Formulation

- Measure the accuracy of search results
- Predict the relevance score of a given query and problem description

<p align="center">
  <img src="../res/img/img281.png" width="600"/>
</p>

### 1.2 Data

<p align="center">
  <img src="../res/img/img282.png" width="600"/>
</p>

### 1.3 Metric

- Measure the agreement between two outcomes
- 0 (totally disagree) ~ 1 (totally agree); below 0 (less agreement between the raters than expected by random)

<p align="center">
  <img src="../res/img/img283.png" width="600"/>
</p>

- How to calculate Quadratic Weighted Kappa?

<p align="center">
  <img src="../res/img/img284.png" width="500"/>
  <img src="../res/img/img285.png" width="500"/>
</p>

<p align="center">
  <img src="../res/img/img286.png" width="500"/>
  <img src="../res/img/img287.png" width="500"/>
</p>

### 1.4 Solutions

- Text feature
- Extending of queries
- Per-query models
- Sample weighting
- Bumper features
- Ensemble
- Kappa optimization

#### 1.4.1 Text features: similarities

- Standard measurements

<p align="center">
  <img src="../res/img/img288.png" width="600"/>
</p>

- Symbolic n-grams

<p align="center">
  <img src="../res/img/img289.png" width="600"/>
</p>

#### 1.4.2 Extending of queries

- Observe 3 important points about data
  - Queries are very short
  - Number of unique queries is 261
  - Queries are the same in train and test
- Extend queries
  1. For each query, we get the most relevant corresponding items
  2. Join the words form the title of the relevant items and ten popular words

#### 1.4.3 Per-query model

- Train and test sets are the same -> opportunity to split the problem into many small subtasks
- For each query, we can build a separate model -> only predict relevance of corresponding items
- Fit 261 random forest classifiers

<p align="center">
  <img src="../res/img/img290.png" width="600"/>
</p>

#### 1.4.4 Sample weighting

- Larger variance -> lower confidence -> lower weight
- The first approach is good; the second approach is time wasting and does not show a better performance

<p align="center">
  <img src="../res/img/img291.png" width="600"/>
</p>

#### 1.4.5 Bumper features

- Predict multiple classes -> predict binary classes

<p align="center">
  <img src="../res/img/img292.png" width="600"/>
</p>

#### 1.4.6 Ensemble

<p align="center">
  <img src="../res/img/img293.png" width="500"/>
  <img src="../res/img/img294.png" width="500"/>
</p>

#### 1.4.7 Kappa optimization

<p align="center">
  <img src="../res/img/img295.png" width="600"/>
</p>

### 1.5 Conclusion

<p align="center">
  <img src="../res/img/img296.png" width="600"/>
</p>

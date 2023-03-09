# Week 4

## 1 Hyperparameters Tuning

### 1.1 In General

1. Find out what parameters we should tune at first
2. How will the training and vlidation curves change after we increase or decrease the parameter
3. Manually / Automatically

<p align="center">
  <img src="../res/img/img171.png" width="600"/>
</p>

### 1.2 How to Use The Libararies?

+ Define a function that will run our model
+ Specify a serach space

<p align="center">
  <img src="../res/img/img172.png" width="500"/>
  <img src="../res/img/img173.png" width="500"/>
</p>

### 1.3 Color Coding Legend

1. Underfitting (Red)
2. Good fit and generalization
3. Overfitting (Green)

<p align="center">
  <img src="../res/img/img174.png" width="600"/>
</p>

## 2. Hyperparameter Tuning

### 2.1 Tree-based Models

<p align="center">
  <img src="../res/img/img175.png" width="600"/>
</p>

#### 2.1.1 GBDT

1. ***Max depth***: max depth of the tree
    + Deeper, better fit
    + If we get deeper and the model is not overfitting, the model will become better and better for validation set if we increase the depth
    + Alo implies that there might be a lot of important interactions to extract from the data -> stop tuning and doing some feature generations
    + Recommended value: 7
2. ***Subsample***: controls a fraction of objects to use when feeding a tree
    + Prevent from overfitting
3. ***colsample_bytree***, ***colsample_bylevel***: controls a fraction of features
    + Prevent from overfitting
4. ***min_child_weight***, ***lambda***, ***alpha***: regularization parameters
    + min_child_weight: increase it, the model will be more conservative; decrease it, the model will be less constrained
    + Recommend values: 0, 5, 15, 300
5. ***eta***: (not for tree, but for training): a learning weight, like in graident descent
    + Higher learning rate: not converge -> small enough learning rate -> better generalization
    + Too small learning rate: will learn nothing
6. ***num round***: (not for tree, but for training): how many learning steps we want to perform (how many trees we want to build)
    + More steps, better fit
    + Early stopping
    + When we find the right number of round: multiply the number of rounds by alpha, and devide eta by alpha
7. ***seed*** (other)

<p align="center">
  <img src="../res/img/img176.png" width="600"/>
</p>

#### 2.1.2 Radnom forest and extra trees
1. ***n_estimator***:
    + Recommended: 10
    + Higher, better
2. ***max_depth***: Can be set to None (unlimited)
    + Recommended value: 7 (but RF usually have higher depths than XGBoost)
3. ***max_features***: Similar to colsample in XGBoost
4. ***min_samples_leaf***: Similar to min_child_weight in XGBoost
5. ***criterion***: Standard for split
    + Gini or Entropy: try both and choose the better one
6. ***random_state*** (not for tree, but for training)
7. ***n_jobs***: (not for tree, but for training) number of cores you have

<p align="center">
  <img src="../res/img/img177.png" width="600"/>
</p>

### 2.2 Neural Networks

### 2.3 Linear Models
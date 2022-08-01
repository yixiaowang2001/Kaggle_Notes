# How to Win a Data Science: Learn from Top Kagglers
Week 2

## 1 Exploratory Data Analysis

EDA最好的方式：visualization

### 1.1 Understand the data
  + Get domain knowledge:
  <br>理解列名称、列之间的关系
  + Check if the data is intuitive:
  <br>比如在下图的数据中，如果有click但没有impression其实是有问题，所以就创建一个新的column来判断数据是否正确
<p align="center">
<img src="../res/img/week2/img1.png" width="500"/>
</p>

  + Understand how the data was generated:
  <br>It is crucial to undersatnd the generation process to set up a proper validation scheme


### 1.2 Anonymized data
比如，text和encoded text的对比：
<p align="center">
<img src="../res/img/week2/img2.png" width="500"/>
<img src="../res/img/week2/img3.png" width="500"/>
</p>

+ Explore individual features
  + Guess the meaning of the columns
  + Guess the types of the column
+ Explore feature relations
    + Find relaations between pairs
    + Find feature groups

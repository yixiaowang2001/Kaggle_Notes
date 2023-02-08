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

#### 1.2.2 Example

[Notebook link]()


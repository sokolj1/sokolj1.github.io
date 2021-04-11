---
title: Titanic Kaggle Competition
date:   2019-01-15
tags:
  - python
  - machine learning
author_profile: false
excerpt: Predicting Titanic passenger survival
toc: true
mathjax: true
published: true
---

With deep learning taking the data science community by storm, people tend to look down at relatively simple machine learning algorithms. Although deep learning can tackle problems that require complex input-output mappings, these deep learning models lack adequate interpretability. Enter logistic regression, which provides interpretable reasoning for the predictive outputs of this type of statistical model. The purpose of this post is to provide an example application of logistic regression and how to interpret the model outcome.

## Background

### Assumptions

Before logistic regression can be considered a valid algorithm for the data, check these seven assumptions to confirm logistic regression is the best algorithm for the job: 

1. Logistic regression requires the dependent variable to be binary.

2. For binary regression, 1 should represent the desired outcome, and 0 should represent the undesirable outcome.

3. Assume linear relationship between continuous independent variables and logit function.

4. No mulitcollinearity. The independent variables can not be correlated with one another. This leads to difficulty interpreting the variance explained in the dependent variable. 

5. No significant outliers.

6. Only meaningful variables should be included

7. Logistic regression requires large sample sizes 

As mentioned above, logistic regression is used to predict dichotomous (binary) variables. Here are a few classification examples: 

* Presence of disease? (yes/no)
* Death? (yes/no)
* Loan default? (yes/no)

Predictions can be derived from simple (one independent variable) or multivariate (two or more independent variables). The following is the data modeling process for the Titanic dataset. The data contains metadata on over 800 Titanic passengers. The goal is to predict passenger survival based off of this information. 

## Titanic: Machine Learning from Disaster

The first step of building any machine learning model is investigating the dataset to understand the characteristics of each feature to determine if it contains telling predictive information.

### Exploratory data analysis

Import the necessary Python libraries:

```python
import pandas as pd
import scipy as scpy
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn import model_selection
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
from sklearn.naive_bayes import GaussianNB
from sklearn.svm import SVC

%matplotlib inline

```

Import the csv file with Pandas:

Import the necessary Python libraries and peek into the first 8 rows of data:
```python

train = pd.read_csv('titanic_train.csv')
train.head(8)

```

<img src="/assets/titanic_regression/train_head_1.png" >

Next, use Pandas DataFrame methods .describe and .info to obtain feature distribution and data types.

<img src="/assets/titanic_regression/train_describe.png" >

<img src="/assets/titanic_regression/train_info.png" >

From the results above, we know the dataset contains 12 features (PassengerId, Survived, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked)

Here are preliminary thoughts for each feature: 

* Passenger ID: Unique identifier for each passenger; contains no important information for ML model

* Survived: **USEFUL** Target variable we want to predict; binary consisting of 1 (surived) and 0 (died).
* Pclass: **USEFUL** Social status of each passenger; 3 categories of upper (3), middle (2) and lower (1) class.
* Name: last, first name, and salutation of each passenger; string variable but no important information.
* Sex: **USEFUL** Gender of each passenger.
* Age: **USEFUL** Min age of newborn infant ( < 1 year old) and max age of 80 years old.
* SibSp: **USEFUL** Numeric data, max number of siblings / spouses aboard is 8. 
* Parch: **USEFUL** max number of parents / children aboard is 6, useful.
* Ticket: Categorical data, potential to be useful, but values may be too distinct. 
* Fare: Numeric data, preliminary assumption of higher fare correlates to higher social class, which may predict survival. 
* Cabin: Categorical data, potential to be useful.
* Embarked: **USEFUL** Categorical data, with 3 categories, C = Cherbourg, Q = Queenstown, S = Southampton, it contains few nulls (can be imputed), useful.

Drop PassengerID, Name, Cabin, and Ticket, as these features will not contribute to our model.

```python
# default is axis = 0 for rows index; axis = 1 to drop columns
train_id = train['PassengerId']
train = train.drop(['PassengerId','Name', 'Cabin', 'Ticket'], axis = 1)
```

### Missing data

Next, check for missing data values in each column:

```python
train.apply(lambda x: x.isnull().any())
```

<img src="/assets/titanic_regression/train_apply.png" >

Calculate the percentage of records that are null for features that have null values:

```python
pd.DataFrame({'Percent Missing': train.isnull().sum() * 100 / len(train)})
```

<img src="/assets/titanic_regression/train_percent_missing.png" >

Considering the Cabin feature has 77% of rows are null values, we decide to drop this column.
Now let's resolve the missing data issue with Age and Embarked features. 

#### Age

Calculate the overall average age of all Titanic passengers:

```python
avg_age = train['Age'].mean()
print(avg_age)

# 29.69911764705882
```

We could use this average for imputation of all missing values, however, we can logically surmise that age is not evenly distributed across the three Titanic social classes. Let's confirm this thinking: 

```python
sns.boxplot(x = 'Pclass', y = 'Age', data = train, hue = 'Survived')
```

<img src="/assets/titanic_regression/age_group_class.png" >

Observing the above boxplot, the age of each passenger is not evenly distributed across the three social classes. We can investigate further by calculating the average age by Pclass grouping: 

```python
print(train.groupby(['Pclass']).get_group(1).Age.mean())
# Upper class: 38.233440860215055

print(train.groupby(['Pclass']).get_group(2).Age.mean())
# Middle class: 29.87763005780347

print(train.groupby(['Pclass']).get_group(3).Age.mean())
# Lower class: 25.14061971830986

```

Since age distribution is uneven, it would not be appropriate to input the overall average of 29.70 into each null value without considering the Pclass value:

```python
train['Age'] = train.groupby(['Pclass','Survived'])['Age'].transform(lambda x:x.fillna(x.mean()))
```

Check again for percentage of missing values: 

```python
pd.DataFrame({'Percent Missing': train.isnull().sum() * 100 / len(train)})
```

<img src="/assets/titanic_regression/missing_value_age.png" >

#### Embarked

The percentage of records that are null is very small, only 0.22%. Let's find the characteristics of these records to see if there are traits in common. C = Cherbourg, Q = Queenstown, S = Southampton.

```python
train[train.Embarked.isnull()]
```

<img src="/assets/titanic_regression/embarked_null.png" >

Two passengers of very similar characteristics and circumstances: Same Pclass, Sex and Fare.

```python
train.groupby(['Pclass', 'Sex']).get_group((1,'female')).Embarked.value_counts()
```

<img src="/assets/titanic_regression/embarked_group.png" >

The most likely departure location is Southampton, so this value in imputed for the two null value records: 

```python
train.Embarked.fillna('S', inplace = True)
```

Confirm no remaining features have missing data:

<img src="/assets/titanic_regression/percent_missing_embarked.png" >


#### Fare

For investigative purposes, check to determine the difference in fare price by social class and survival category: 

```python
train.groupby(['Pclass', 'Survived'])['Fare'].mean()
```

<img src="/assets/titanic_regression/fare_social_survival.png" >

### Feature uniqueness

Check for percent uniqueness of each feature:

```python
# unique().size counts the distinct values in each column; .size counts all records in each column
pd.DataFrame({'percent_unique': train.apply(lambda x: x.unique().size / x.size*100)})
```

<img src="/assets/titanic_regression/percent_uniqueness.png" >

### Categorical to Dummy

```python
train = pd.get_dummies(train)
train.head(10)
```

<img src="/assets/titanic_regression/train_dummy.png" >

Store the survived predictor feature in a series variable and drop the feature in the main dataset to prepare for train_test_split compartmentalization:

```python
train_label = train['Survived']
train = train.drop(['Survived'], axis = 1)

from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(train, train_label, test_size = 0.25, random_state = 3)
```

The data must be scaled in order to compensate for unequal distributions and intervals of each feature:
```python
from sklearn.preprocessing import StandardScaler

scaled_trn = StandardScaler().fit_transform(X_train)
train_scaled = pd.DataFrame(scaled_trn, index = X_train.index, columns = X_train.columns)
train_scaled.head()
```

<img src="/assets/titanic_regression/train_scaled.png" >

Now we can train the logistic regression model:

```python

logreg = LogisticRegression()
logreg.fit(train_scaled, Y_train)

```

<img src="/assets/titanic_regression/logistic_regression_output.png" >

```python

predictions = logreg.predict_proba(X_test)[:,1]

from sklearn.metrics import roc_auc_score
auc = roc_auc_score(Y_test, predictions)

# auc = 0.6945764725852995
```

This logistic regression model can successfully predict the survival outcome of a Titanic passenger with approximately 70% accuracy. 




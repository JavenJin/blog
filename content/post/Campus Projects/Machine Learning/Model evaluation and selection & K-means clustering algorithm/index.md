---
title: Machine Learning - Model evaluation and selection & K-means clustering algorithm
description: 机器学习 - 模型评估与选择 & K-means聚类算法实验
date: '2020-08-15'
categories:
    - Machine Learning
tags:
    - Machine Learning
    - Python
math: true
---

## Machine Learning - Model evaluation and selection & K-means clustering algorithm

Note: The code is for reference only, according to the actual situation to make the appropriate changes, can not be completely copied, otherwise it will not work!
### 1.Importing Class Libraries
```python
from pandas import read_csv  #Use pandas to import data and perform descriptive statistical analysis on the data
from matplotlib import pyplot  #Plotting with matplotlib, data visualization
```
### 2.Importing Data Sets
```python
#Using the sample dataset that comes with sklearn
from  sklearn import datasets 
iris=datasets.load_iris()
#The dataset has two files, iris.data, which stores feature data, and iris.target, which stores category data.
#View and visualize the two datasets by yourself. Use functions such as describe(), info(), hist(), scatter(), etc.
```
### 3.Separate data sets
```python
from sklearn.model_selection import train_test_split
# The train_test_split function is used to randomly divide the matrix into a training subset and a test subset, and return the divided training set test set samples and training set test set labels.
validation_size = 0.2   #Separate data, 80% training dataset, 20% evaluation dataset
seed = 7
X_train, X_validation, Y_train, Y_validation = train_test_split(iris.data,iris.target, test_size=validation_size, random_state=seed)
```
### 4.Algorithm performance is evaluated using two algorithms, logistic regression and Bayesian classifier, and validated on a test set.
```python
from sklearn.linear_model import LogisticRegression  #Logistic regression
from sklearn.metrics import accuracy_score
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix
from sklearn.naive_bayes import GaussianNB  #Plain Bayesian
from sklearn.model_selection import KFold
from sklearn.model_selection import cross_val_score

# Algorithm review (note that before using a particular algorithm, import it yourself from the skleran class library)
models = {}
models['LR'] = LogisticRegression()
models['LDA'] = LinearDiscriminantAnalysis()
models['KNN'] = KNeighborsClassifier()
models['CART'] = DecisionTreeClassifier()
models['NB'] = GaussianNB()
models['SVM'] = SVC()
# Evaluation algorithm using ten-fold cross-validation
results = []
for key in models:
kfold = KFold(n_splits=10, random_state=seed)
cv_results = cross_val_score(models[key], X_train, Y_train, cv=kfold, scoring='accuracy')	results.append(cv_results)
print('%s: %f (%f)' %(key, cv_results.mean(), cv_results.std()))

#Validate and compare the classification effect of the two algorithms on the test set
lr=LogisticRegression()
lr.fit(X=X_train, y=Y_train)
predictions = lr.predict(X_validation)
print(accuracy_score(Y_validation, predictions))  #Prediction Accuracy
print(confusion_matrix(Y_validation, predictions)) #Conflict Matrix
print(classification_report(Y_validation, predictions))  #Data Report

nb = GaussianNB()
nb.fit(X=X_train, y=Y_train)
predictions = nb.predict(X_validation)
print(accuracy_score(Y_validation, predictions))
print(confusion_matrix(Y_validation, predictions))
print(classification_report(Y_validation, predictions))
```
What should I do if an erase warning message appears? How do I get rid of it?
```
Method 1: Specify the two default parameters of the LogisticsRegression function
      lr=LogisticRegression(solver='liblinear',multi_class='auto') 
Method 2: Import warnings
      warnings.filterwarnings("ignore")
```
### Sklearn implementation of K-means clustering:
![sklearn implementation of k-means clustering](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Model%20evaluation%20and%20selection%20%26%20K-means%20clustering%20algorithm/sklearn-implementation-of-k-means-clustering.png)
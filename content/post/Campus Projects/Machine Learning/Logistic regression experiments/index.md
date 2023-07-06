---
title: Machine Learning - Logistic regression experiments
description: 机器学习 - 逻辑回归实验
date: '2020-08-15'
categories:
    - Machine Learning
tags:
    - Machine Learning
    - Python
math: true
---

## Machine Learning - Logistic regression experiments

### Learning Logistic Regression with scikit-learn and pandas

#### 1. Get the data, define the problem

The sinking of the Titanic is one of the most infamous shipwrecks in history.On April 15, 1912, during its first voyage, the Titanic sank after hitting an iceberg, killing 1,502 of the 2,224 passengers and crew. One of the reasons for the loss of life was that there were not enough lifeboats for the passengers and crew. While there were factors that contributed to the luck of surviving, some people were more likely to survive than others, such as women, children and the upper class.

The Titanic dataset is divided into two parts:

Training dataset-contains feature information and labels for survival and non-survival, train.csv

Test dataset - contains only feature information, test.csv

The dataset can be downloaded from kaggle in csv format.

You can also download it from my csdn resources at [Click to download](https://download.csdn.net/download/weixin_42718701/12715609)

We are going to use the tools of machine learning to predict which passengers are more likely to survive the disaster.

In this lesson's challenge, we are going to use a logistic regression algorithm to complete an analysis of which people are more likely to survive.

In scikit-learn, logistic regression is implemented through the linear_model.LogisticRegression class.

```
LogisticRegression(penalty='l2', dual=False, 
    tol=0.0001, C=1.0, fit_intercept=True, 
    intercept_scaling=1, class_weight=None, 
    random_state=None, solver='warn', max_iter=100,
    multi_class='warn', verbose=0, 
    warm_start=False, n_jobs=None)
```

Reference: [https://www.cnblogs.com/wjq-Law/p/9779657.html](https://www.cnblogs.com/wjq-Law/p/9779657.html)

```
Properties: coef_,  intercept_,  n_iter
Methods:    fit(X_train,y_train)
            score(X_test,y_test)
            predict(X)
            predict_proba(X)
```

#### 2. View Data

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments1.png)

Data columns (total 12 columns):
|||
|--|--|
|PassengerId| 891 non-null int64|
|Pclass|891 non-null int64|
|Name|891 non-null object|
|Sex|891 non-null object|
|Age|714 non-null float64|
|SibSp|891 non-null int64|
|Parch|891 non-null int64|
|Ticket|891 non-null object|
|Fare|891 non-null float64|
|Cabin| 204 non-null object|
|Embarked|      889 non-null object|

It can be seen that the training set contains a total of 891 samples with 12 features each, of which Age, Cabin and Embarked have missing values. In particular, the Carbin feature has values for only 204 samples.

Similarly: observe the missing values in the test set.

Additional functions to view the data:

```python
data_trian.describe() #Description data
data_trian.head() #View the first 5 rows of data
data_trian.tail()  #View the dimensions of the data
data_trian.shape
data_trian.hist() #Data visualization, histogram display. Note that you have to import the matplotlib class library first.
```

#### 3. Handling of missing values

Age features are very important (ladies and children are usually preferred when fleeing for their lives), so we need to fill them.

The methods of filling missing values are: fixed value filling, mean/median filling, adjacent value filling, and model prediction filling.

Here we use mean fill. fillna() function.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments2.png)

Cabin has more missing values, and we directly discard them to avoid introducing larger noise. (Delete a feature, column)
with the drop() function.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments3.png)

Embarked features have only 2 samples with missing values in the training set, so the samples with missing values can be removed directly. (Delete a sample, line)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments4.png)

Similarly, the missing values of the test set are processed.

#### 4. Feature Processing

There are still some problems with the current data, such as the Name feature is text-based, which is not conducive to subsequent processing, so we temporarily discard it when training the model, and the Ticket feature is messy, so we also ignore it temporarily.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments5.png)

Pclass features, Sex features, and Embarked features are all category types, which generally need to be one-hot encoded.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments6.png)

Age features, SibSp features, Parch features and Fare features are numerical and have a wide range of values, so they are generally normalized or normalized first.

The standardization uses the fit() function and fit_transform() function in the preprocessing.StandardScaler class library.

fit() is used to calculate the mean and variance of the training data, which are later used to transform the training data.

fit_transform() not only calculates the mean and variance of the training data, but also transforms the training data based on the calculated mean and variance, thus converting the data into a standard orthogonal distribution.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments7.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments8.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments9.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments10.png)

#### 5. Model Training

(1) Import the required classification algorithm class library.

```python
from sklearn import linear_model.LogisticRegression()
```

The parameters of the logistic regression function are as follows:

```python
LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
          intercept_scaling=1, max_iter=100, multi_class='warn',
          n_jobs=None, penalty='l2', random_state=None, solver='lbfgs',
          tol=1e-06, verbose=0, warm_start=False)
```

(2) Extract the feature values and labels in the training set separately.

(3) Divide the training set and the validation set.

```train_test_split() Function```

(4) Training model.

```fit() Function```

(5) Verify on the validation set and evaluate the performance.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments11.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments12.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments13.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments14.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments15.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments16.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments17.png)

The model has been trained and is performing well enough to be used for prediction.

#### 6. Complete python code

```python
import pandas as pd
import matplotlib

data_train = pd.read_csv("D:/titanic/train.csv")
data_train.info()


data_train.describe()


data_train.head()


data_train.tail()


data_train.shape


data_train.hist()


data_train['Age'].fillna(data_train['Age'].mean(),inplace = True)
data_train.info()


data_train = data_train.drop(['Cabin'],axis=1)
data_train.info()


data_train = data_train.dropna(axis=0)
data_train.info()


data_train.head()


data_train = data_train.drop(['Name','Ticket'],axis=1)
data_train.head()


cate_df = data_train[['Pclass','Sex','Embarked']]
cate_onehot_df = pd.get_dummies(cate_df)
cate_onehot_df.head()


cont_df = data_train[['Age','Fare','SibSp','Parch']]
cont_df.head()


import sklearn.preprocessing as pr

scaler = pr.StandardScaler()
age_scale = scaler.fit(cont_df['Age'].values.reshape(-1,1))

print(age_scale)

cont_df['Age_scaled']=scaler.fit_transform(cont_df['Age'].values.
                                           reshape(-1,1),age_scale)


fare_scale = scaler.fit(cont_df['Fare'].values.reshape(-1,1))
cont_df['Fare_scaled']=scaler.fit_transform(cont_df['Fare'].values.reshape(-1,1),fare_scale)


sibsp_scale=scaler.fit(cont_df['SibSp'].values.reshape(-1,1))
cont_df['SibSp_scaled']=scaler.fit_transform(cont_df['SibSp'].values.reshape(-1,1),sibsp_scale)


parch_scale=scaler.fit(cont_df['Parch'].values.reshape(-1,1))
cont_df['Parch_scaled']=scaler.fit_transform(cont_df['Parch'].values.reshape(-1,1),parch_scale)


cont_df.drop(['Age','Fare','SibSp','Parch'],axis=1,inplace=True)
cont_df.head(3)


cont_df.hist


df_train=pd.concat([data_train['Survived'],cate_onehot_df,cont_df],axis=1)
df_train.head(3)from sklearn import linear_model
y=df_train['Survived']
X=df_train.drop(['Survived'],axis=1)


from sklearn.model_selection import train_test_split
X_train,X_validation,Y_train,Y_validation = \
train_test_split(X,y,test_size=0.3,random_state=1)


LR=linear_model.LogisticRegression(C=1.0,penalty='l2',tol=1e-6,solver='lbfgs')
LR.fit(X_train,Y_train)


y_predict=LR.predict(X_validation)
y_predict_prob=LR.predict_proba(X_validation)[:,1]

from sklearn.metrics import classification_report
print('Check accuracy rate, check completeness rate, F1 value:')
print(classification_report(Y_validation,y_predict,target_names=None))


from sklearn.metrics import accuracy_score
print('Prediction accuracy:')
print(accuracy_score(Y_validation,y_predict))
print('Accurate to 4 decimal places: {:.4f}'.format(accuracy_score(Y_validation,y_predict)))


from sklearn.metrics import roc_auc_score
print('AUC values:')
print((roc_auc_score(Y_validation,y_predict_prob)))
print('Accurate to 6 decimal places: {:.6f}'.format(roc_auc_score(Y_validation,y_predict_prob)))


from sklearn.metrics import confusion_matrix
print('Confusion Matrix')
print(confusion_matrix(Y_validation,y_predict,labels=None))


feature=list(df_train.columns[1:])
weight=LR.coef_[0]
df=pd.DataFrame({'feature':feature,'weight':weight})
print(df)
```
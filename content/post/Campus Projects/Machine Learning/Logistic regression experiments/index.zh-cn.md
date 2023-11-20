---
title: 机器学习 - 逻辑回归实验
description: Machine Learning - Logistic regression experiments
date: '2020-08-15'
categories:
    - Machine Learning
tags:
    - Machine Learning
    - Python
math: true
---

## 机器学习 - 逻辑回归实验

### 用scikit-learn和pandas学习Logistic回归

#### 1. 获取数据，定义问题

泰坦尼克号的沉没是历史上最臭名昭著的沉船事件之一。1912年4月15日，在首次航行期间，泰坦尼克号撞上冰山后沉没，2224名乘客和机组人员中有1502人遇难。导致生命损失的原因之一是没有足够的救生艇给乘客和机组人员。虽然幸存下来的运气有一些因素，但一些人比其他人更有可能生存，比如妇女，儿童和上层阶级。

Titanic数据集分为两部分：

训练数据集-包含特征信息和存活与否的标签，train.csv

测试数据集-只包含特征信息，test.csv

数据集可以从kaggle上下载，格式为csv。

也可以在我的csdn资源里面下载：[点击下载](https://download.csdn.net/download/weixin_42718701/12715609)

我们要运用机器学习的工具来预测哪些乘客更可能幸免于难。

在这本次课的挑战中，我们要用逻辑回归算法，完成对哪些人更有可能生存的分析。

在scikit-learn中，Logistics回归通过linear_model.LogisticRegression类进行实现。

```
LogisticRegression(penalty='l2', dual=False, 
    tol=0.0001, C=1.0, fit_intercept=True, 
    intercept_scaling=1, class_weight=None, 
    random_state=None, solver='warn', max_iter=100,
    multi_class='warn', verbose=0, 
    warm_start=False, n_jobs=None)
```

参考[https://www.cnblogs.com/wjq-Law/p/9779657.html](https://www.cnblogs.com/wjq-Law/p/9779657.html)

```
属性：coef_,  intercept_,  n_iter
方法：fit(X_train,y_train)
     score(X_test,y_test)
     predict(X)
     predict_proba(X)
```

#### 2. 查看数据

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

可以看到，训练集一共包含891个样本，每个样本有12个特征，其中Age、Cabin和Embarked有缺失值。特别是Carbin特征，只有204个样本有值。

同理：观察测试集中的缺失值。

查看数据的其他函数：

```python
data_trian.describe() #描述数据
data_trian.head() #查看数据的前5行
data_trian.tail()  #查看数据的维度
data_trian.shape
data_trian.hist() #数据可视化，直方图显示。注意要先import matplotlib类库。
```

#### 3. 缺失值的处理

Age特征非常重要（逃命时通常女士和小孩优先），因此我们需要对其填充。

缺失值的填充方法有:固定值填充、均值/中位数填充、相邻值填充、模型预测填充。

此处我们使用均值填充。fillna()函数。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments2.png)

Cabin缺失值较多，我们直接将其舍弃，以免引入较大的噪声。（删某一特征，列）
用drop()函数。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments3.png)

Embarked特征在训练集中只有2个样本有缺失值，因此可以直接将有缺失的样本删除。（删某一样本，行）

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments4.png)

同理，对测试集的缺失值进行处理。

#### 4. 特征处理

现在的数据还存在一些问题，如Name特征是文本型，不利于后续处理，我们训练模型时暂时将其舍弃。Ticket特征比较乱，也将其暂时忽略。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments5.png)

Pclass特征、Sex特征、Embarked特征都是类别型，一般需要将其进行one-hot编码。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments6.png)

Age特征、SibSp特征、Parch特征和Fare特征为数值型，取值变化范围较大，一般先将其标准化或归一化。

标准化使用preprocessing.StandardScaler类库中的fit()函数和fit_transform()函数。

fit()用于计算训练数据的均值和方差， 后面就会用均值和方差来转换训练数据。

fit_transform()不仅计算训练数据的均值和方差，还会基于计算出来的均值和方差来转换训练数据，从而把数据转换成标准的正太分布。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments7.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments8.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments9.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments10.png)

#### 5. 模型训练

（1）导入需要的分类算法类库。

```python
from sklearn import linear_model.LogisticRegression()
```

逻辑回归函数的参数如下：

```python
LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
          intercept_scaling=1, max_iter=100, multi_class='warn',
          n_jobs=None, penalty='l2', random_state=None, solver='lbfgs',
          tol=1e-06, verbose=0, warm_start=False)
```

（2）将训练集中的特征值和标签分开提取。

（3）划分训练集和验证集。

```train_test_split()函数```

（4）训练模型。

```fit()函数。```

（5）在验证集上验证，评估性能。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments11.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments12.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments13.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments14.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments15.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments16.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Logistic%20regression%20experiments/logistic-regression-experiments17.png)

模型已经训练好，并且性能还不错，可以拿来进行预测了。

#### 6. 完整python代码

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
print('查准率、查全率、F1值：')
print(classification_report(Y_validation,y_predict,target_names=None))


from sklearn.metrics import accuracy_score
print('预测准确率：')
print(accuracy_score(Y_validation,y_predict))
print('精确到小数点后4位：{:.4f}'.format(accuracy_score(Y_validation,y_predict)))


from sklearn.metrics import roc_auc_score
print('AUC值：')
print((roc_auc_score(Y_validation,y_predict_prob)))
print('精确到小数点后6位：{:.6f}'.format(roc_auc_score(Y_validation,y_predict_prob)))


from sklearn.metrics import confusion_matrix
print('混淆矩阵')
print(confusion_matrix(Y_validation,y_predict,labels=None))


feature=list(df_train.columns[1:])
weight=LR.coef_[0]
df=pd.DataFrame({'feature':feature,'weight':weight})
print(df)
```
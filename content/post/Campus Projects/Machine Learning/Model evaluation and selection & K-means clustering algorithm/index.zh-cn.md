---
title: 机器学习 - 模型评估与选择 & K-means聚类算法实验
description: Machine Learning - Model evaluation and selection & K-means clustering algorithm
date: '2020-08-15'
categories:
    - Machine Learning
tags:
    - Machine Learning
    - Python
math: true
---

## 机器学习 - 模型评估与选择 & K-means聚类算法实验

Note: 代码仅供参考，根据实际情况做相应的修改，不能完全照搬，否则运行不通！
### 1.导入类库
```python
from pandas import read_csv  #使用pandas来导入数据和对数据进行描述性统计分析
from matplotlib import pyplot  #使用matplotlib进行绘图，数据可视化
```
### 2.导入数据集
```python
#使用sklearn自带的示例数据集
from  sklearn import datasets 
iris=datasets.load_iris()
#数据集有两个文件，分别为iris.data，存放特征数据；iris.target，存放类别数据。
#自行对两个数据集进行查看、可视化显示。使用describe(),info(),hist(),scatter()等函数。
```
### 3.分离数据集
```python
from sklearn.model_selection import train_test_split
# train_test_split函数用于将矩阵随机划分为训练子集和测试子集，并返回划分好的训练集测试集样本和训练集测试集标签。
validation_size = 0.2   #分离数据，80%训练数据集，20%评估数据集
seed = 7
X_train, X_validation, Y_train, Y_validation = train_test_split(iris.data,iris.target, test_size=validation_size, random_state=seed)
```
### 4.使用逻辑回归和贝叶斯分类器两种算法进行算法性能评估，并在测试集上进行验证。
```python
from sklearn.linear_model import LogisticRegression  #逻辑回归
from sklearn.metrics import accuracy_score
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix
from sklearn.naive_bayes import GaussianNB  #朴素贝叶斯
from sklearn.model_selection import KFold
from sklearn.model_selection import cross_val_score

# 算法审查（注意，使用某个算法前，要自己先从skleran类库中导入）
models = {}
models['LR'] = LogisticRegression()
models['LDA'] = LinearDiscriminantAnalysis()
models['KNN'] = KNeighborsClassifier()
models['CART'] = DecisionTreeClassifier()
models['NB'] = GaussianNB()
models['SVM'] = SVC()
# 评估算法，使用十折交叉验证法
results = []
for key in models:
kfold = KFold(n_splits=10, random_state=seed)
cv_results = cross_val_score(models[key], X_train, Y_train, cv=kfold, scoring='accuracy')	results.append(cv_results)
print('%s: %f (%f)' %(key, cv_results.mean(), cv_results.std()))

#测试集上验证、比较两种算法分类效果
lr=LogisticRegression()
lr.fit(X=X_train, y=Y_train)
predictions = lr.predict(X_validation)
print(accuracy_score(Y_validation, predictions))  #预测准确率
print(confusion_matrix(Y_validation, predictions)) #冲突矩阵
print(classification_report(Y_validation, predictions))  #数据报告

nb = GaussianNB()
nb.fit(X=X_train, y=Y_train)
predictions = nb.predict(X_validation)
print(accuracy_score(Y_validation, predictions))
print(confusion_matrix(Y_validation, predictions))
print(classification_report(Y_validation, predictions))
```
出现消除警告信息怎么办？怎么消除？
```
方法1：指定LogisticsRegression函数的两个默认参数
      lr=LogisticRegression(solver='liblinear',multi_class='auto') 
方法2：import warnings
      warnings.filterwarnings("ignore")
```
### K-means聚类的sklearn实现：
![sklearn implementation of k-means clustering](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Model%20evaluation%20and%20selection%20%26%20K-means%20clustering%20algorithm/sklearn-implementation-of-k-means-clustering.png)
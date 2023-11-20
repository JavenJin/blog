---
title: 机器学习 - 贝叶斯分类实验
description: Machine Learning - Bayesian classification experiments
date: '2019-11-04'
categories:
    - Machine Learning
tags:
    - Machine Learning
    - Python
math: true
---

## 机器学习 - 贝叶斯分类实验

### 1. 中文文本分类介绍

文本挖掘是指从大量的文本数据中抽取事先未知的、可理解的、最终可用的知识的过程，同时运用这些知识更好的组织信息以便将来参考。

主要有以下几个方面的应用：

搜索和信息检索（IR）：存储和文本文档的检索，包括搜索引擎个关键字搜索。

文本聚类：使用聚类方法，对词汇、片段、段落或文件进行分组和归类。

文本分类：对片段、段落或文件进行分组和归类，在使用数据挖掘分类方法的基础上，经过训练的标记示例模型。

Web挖掘：在互联网上进行数据和文本的挖掘，并特别关注网络的规模和相互的联系。

信息抽取（IE）：从非结构化文本中识别与提取有关的事实和关系：从非结构化或半结构化文本中抽取结构化数据的过程。

自然语言处理（NLP）：将语言作为一种有意义、有规则的符号系统，从底层解析和理解语言的任务（例如词性的标注）；目前的技术方法主要从语法、语义的角度发现语言最本质的结构和所表达的意义。

概念的提取：把单词和短语按语义分成意义相似的组。

### 2. 文本分类的一般步骤：

（1）预处理：去除文本的噪声信息，例如HTML标签、文本的格式转换、检测句子边界等。

（2）中文分词：什么是分词？分词有什么用？怎样分词？

例如一句话：“2019年底部队友谊篮球赛结束”，分词结果为2019/年底/部队/友谊/篮球赛/结束。如果分出的词是底部、队友呢？

使用中文分词器为文本分词，并去除停用词。

中文分词和英文分词对比，中文分词难点：没有形式上的分界符。（英文用空格区分单词）

（3）构建词向量空间：统计文本词频，生成文本的词向量空间。

词映射到向量空间。余弦相似度。“快乐”、“高兴”、“悲伤”三个向量的余弦？

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments1.png)

余弦相似度用向量空间中两个向量夹角的余弦值作为衡量两个个体间差异的大小。余弦值越接近1，就表明夹角越接近0度，也就是两个向量越相似，这就叫"余弦相似性"。

（4）权重策略—TF-IDF方法：使用TF-IDF发现特征词，并抽取为反映文档主题的特征。

TF：词频。

IDF：逆向文档频率。

衡量词语重要性的程度。

（5）分类器：使用朴素贝叶斯算法训练分类器。scikit-learn网站介绍。Naive Bayes

（6）评价分类结果：分类器的测试结果分析。

### 3. 具体操作

（1）下载并安装“结巴”jieba类库。https://pypi.org/project/jieba/

学习在python中安装外部类库的方法。

（2）文本语料库的获取和预处理。

常用的语料库：复旦大学谭松波中文文本分类语料库，搜狐新闻文本分类语料库。

停用词的清理。什么是停用词？停用词库的获取。hlt_stop_words.txt

jieba中文分词。安装、使用，自行把一段话用三种模式进行分词。

（3）将分词向量化，TF_IDF方法。

from sklearn.feature_extraction.text import CountVectorizer

from sklearn.feature_extraction.text import TfidfVectorizer

（4）使用朴素贝叶斯分类模块。scikit-learn网站查看、学习Naive Bayes分类算法。

（5）分类结果评估。

from sklearn.metrics import classification_report

from sklearn.metrics import classification accuracy_score

### 4. 实验步骤

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments2.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments3.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments4.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments5.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments6.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments7.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments8.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments9.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments10.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments11.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments12.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments13.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments14.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments15.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments16.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments17.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments18.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments19.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments20.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments21.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments22.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments23.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments24.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments25.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments26.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Machine%20Learning/Bayesian%20classification%20experiments/bayesian-classification-experiments27.png)

### 5. 实验完整代码python

```python
import jieba #需要先安装结巴类库，再引入，否则报错

seg_list=jieba.cut("西京网讯：10月31日晚，“庆祝中华人民共和国成立70周年暨西京学院建校25周年教职工竹竿舞比赛”举行。",cut_all=True)
print("Full Mode全切分模式:","/".join(seg_list))

seg_list=jieba.cut("教师五分会的《欢乐西京团》与教师二分会的《跳起来》伴随着活泼的音乐和轻盈的舞蹈，把“欢乐”表现的淋淋尽致。")
print("搜索引擎分词模式:","/".join(seg_list))

seg_list=jieba.cut("2019年底部队友谊篮球赛结束",cut_all=False)
print("默认切分模式:","/".join(seg_list))

seg_list=jieba.cut("西京网讯：10月31日晚，“庆祝中华人民共和国成立70周年暨西京学院建校25周年教职工竹竿舞比赛”举行。",cut_all=False)
print("Full Mode全切分模式:","/".join(seg_list))

import os

#定义读取文件内容的函数
def readfile(path):
    #注意文本文件的编码格式，使用自己语料库和测试集txt文件的编码格式。
    fp=open(path,'r',encoding='ANSI',errors='ignore')
    content=fp.read()
    fp.close()
    return content

#定义保存到文件的函数
def savefile(savepath,content):
    fp=open(savepath,'w',encoding='ANSI',errors='ignore')
    fp.write(content)
    fp.close()

#定义一个存放训练集分词后各文档内容的列表
train_corpus=[]

#定义一个存放训练集各文档类别标签的列表
train_label=[]

#未分词的训练集语料库路径，替换为自己电脑保存的路径。train_corpus文件夹。
corpus_path="E:/program/train_corpus/"

#训练集分词以后存放路径，自己提前建立好名字为seg_train_corpus的空文件夹
save_path="E:/program/seg_train_corpus/"

#获取未分词的语料库下所有子目录列表
cate_list=os.listdir(corpus_path)

print("努力分词中，请稍等.........")
#获取每个子目录下的所有文件
for mydir in cate_list:
    class_path=corpus_path+mydir+'/'  #语料集中的某个子目录路径
    seg_dir=save_path+mydir+'/'  #分类后的子目录路径
    file_list=os.listdir(class_path)  #获取具体的文件名称列表
    for file_path in file_list:
        fullname=class_path + file_path
        content=readfile(fullname).strip()  #str.strip()就是把字符串(str)的头和尾的空格，以及位于头尾的\n \t之类给删掉
        content=content.replace("\r\n","").strip()  #删除换行和多余的空格
       
        content_seg=jieba.cut(content)
        
        savefile(seg_dir+file_path," ".join(content_seg))
        train_label.append(mydir)
                        
print("训练集语料库文本分词结束！")

oldpath=r"e:/program/seg_train_corpus/"
newpath=r"e:/program/seg_val_corpus/"
import random  #随机排序文件
import shutil
#从训练集中随机取出20%的文件，保存为验证集。
catelist=os.listdir(oldpath)
for eachlist in catelist:
    fullpath=oldpath+eachlist
    newvalpath=newpath+eachlist+"/"
    isExists=os.path.exists(newvalpath)   #判断路径是否存在，若存在，报错。不存在，创建。
    if isExists==True:
            
        print(newvalpath+"目录已存在，将不再保存新的文件！请确认是否已划分好。")
        
    else:
        os.makedirs(newvalpath,exist_ok=True)
        filename=os.listdir(fullpath)
        filenumber=len(filename)
        random.shuffle(filename) #将文件随机排序
        splitfile=int(filenumber*0.2)
        for i in range(splitfile):  #将随机抽取出的20%文件保存到验证集目录下。
            src=fullpath+"/"+filename[i]
            shutil.move(src,newvalpath)
        print("目录"+newvalpath+"创建成功！")
print("训练集和验证集划分完毕")

newvalpath
     
#对测试集文档进行分词。注意，测试集中直接保存的文档，没有子目录。
test_corpus_path="E:/program/test_corpus/"
save_test_path="E:/program/seg_test_corpus/"  #自行建立该文件夹
test_file_list=os.listdir(test_corpus_path)  #获取具体的文件名称列表
print("努力分词中，请稍等.........")
for file_path in test_file_list:
        fullname=test_corpus_path + file_path
        content=readfile(fullname).strip()  #str.strip()就是把字符串(str)的头和尾的空格，以及位于头尾的\n \t之类给删掉
        content=content.replace("\r\n","").strip()  #删除换行和多余的空格
       
        content_seg=jieba.cut(content)
        
        savefile(save_test_path+file_path," ".join(content_seg))
        
                        
print("测试集语料库文本分词结束！")

from sklearn.datasets.base import Bunch
bunch = Bunch(target_name=[],label=[],filenames=[],contents=[]) 

#先对训练集进行操作
wordbag_path="E:/program/train_word_bag/train_set.dat"#train_word_bag文件夹已经自己创建
seg_path="E:/program/seg_train_corpus/"
cate_list=os.listdir(seg_path)
bunch.target_name.extend(cate_list)#将类别信息保存到Bunch对象

for mydir in cate_list:
    class_path=seg_path+mydir+"/"
    file_list=os.listdir(class_path)
    for file_path in file_list:
        fullname=class_path+file_path
        bunch.label.append(mydir)#保存当前文件的分类标签
        bunch.filenames.append(fullname)#保存当前文件的文件路径
        bunch.contents.append(readfile(fullname).strip())#保存文件词向量

#Bunch对象持久化
import pickle
file_obj=open(wordbag_path,"wb")
pickle.dump(bunch,file_obj)
file_obj.close()
print("训练集构建文本对象结束")

from sklearn import feature_extraction
from sklearn.feature_extraction.text import TfidfTransformer#TF-IDF向量转换类
from sklearn.feature_extraction.text import TfidfVectorizer#TF-IDF向量生成类

def readbunchobj(path):
    file_obj=open(path,"rb")
    bunch=pickle.load(file_obj)
    file_obj.close()
    return bunch
def writebunchobj(path,bunchobj):
    file_obj=open(path,"wb")
    pickle.dump(bunchobj,file_obj)
    file_obj.close()

def readfile(path):
    fp = open(path,"r",encoding='ANSI',errors='ignore')
    content = fp.read()
    fp.close()
    return content


path="E:/program/train_word_bag/train_set.dat"
bunch=readbunchobj(path)

#停用词
stopword_path="E:/program/hlt_stop_words.txt"
stpwrdlst=readfile(stopword_path).splitlines()
#构建TF-IDF词向量空间对象
tfidfspace=Bunch(target_name=bunch.target_name,label=bunch.label,filenames=bunch.filenames,tdm=[],vocabulary={})
#使用TfidVectorizer初始化向量空间模型
vectorizer=TfidfVectorizer(stop_words=stpwrdlst,sublinear_tf=True,max_df=0.5)
#transformer=TfidfTransformer()#该类会统计每个词语的TF-IDF权值

#文本转为词频矩阵，单独保存字典文件
tfidfspace.tdm=vectorizer.fit_transform(bunch.contents)
tfidfspace.vocabulary=vectorizer.vocabulary_

#创建词袋的持久化
space_path="E:/program/train_word_bag/tfidfspace.dat"
writebunchobj(space_path,tfidfspace)
tfidfspace.tdm.shape

bunch = Bunch(target_name=[],label=[],filenames=[],contents=[]) 
wordbag_path="E:/program/val_word_bag/val_set.dat"#train_word_bag文件夹已经自己创建
seg_path="E:/program/seg_val_corpus/"
cate_list=os.listdir(seg_path)
bunch.target_name.extend(cate_list)#将类别信息保存到Bunch对象
for mydir in cate_list:
    class_path=seg_path+mydir+"/"
    file_list=os.listdir(class_path)
    for file_path in file_list:
        fullname=class_path+file_path
        bunch.label.append(mydir)#保存当前文件的分类标签
        bunch.filenames.append(fullname)#保存当前文件的文件路径
        bunch.contents.append(readfile(fullname).strip())#保存文件词向量

#Bunch对象持久化
import pickle
file_obj=open(wordbag_path,"wb")
pickle.dump(bunch,file_obj)
file_obj.close()
print("验证集构建文本对象结束")

#对于验证集生成向量空间，在训练词向量模型时需要加载训练集词袋，将验证集产生的词向量映射到训练集词袋的词典中，生成向量空间模型
path="E:/program/val_word_bag/val_set.dat"
bunch=readbunchobj(path)

#停用词
stopword_path="E:/program/hlt_stop_words.txt"
stpwrdlst=readfile(stopword_path).splitlines()
#构建TF-IDF词向量空间对象
tfidfspace=Bunch(target_name=bunch.target_name,label=bunch.label,filenames=bunch.filenames,tdm=[],vocabulary={})

#导入训练集词袋
train_path="E:/program/train_word_bag/tfidfspace.dat"
trainbunch=readbunchobj(train_path)


#使用TfidVectorizer初始化向量空间模型
vectorizer=TfidfVectorizer(stop_words=stpwrdlst,sublinear_tf=True,max_df=0.5,vocabulary=trainbunch.vocabulary)
#transformer=TfidfTransformer()#该类会统计每个词语的TF-IDF权值

#文本转为词频矩阵，单独保存字典文件
tfidfspace.tdm=vectorizer.fit_transform(bunch.contents)
tfidfspace.vocabulary=trainbunch.vocabulary

#创建词袋的持久化
space_path="E:/program/val_word_bag/tfidfspace.dat"
writebunchobj(space_path,tfidfspace)
type(tfidfspace.tdm)
tfidfspace.tdm.shape

bunch = Bunch(target_name=[],label=[],filenames=[],contents=[]) 
wordbag_path="E:/program/test_word_bag/test_set.dat"#test_word_bag文件夹已经自己创建
seg_path="E:/program/seg_test_corpus/"
file_list=os.listdir(seg_path)
for file_path in file_list:
        fullname=seg_path+file_path
        bunch.filenames.append(fullname)#保存当前文件的文件路径
        bunch.contents.append(readfile(fullname).strip())#保存文件词向量

#Bunch对象持久化

file_obj=open(wordbag_path,"wb")
pickle.dump(bunch,file_obj)
file_obj.close()
print("测试集构建文本对象结束")

path="E:/program/test_word_bag/test_set.dat"
bunch=readbunchobj(path)

#停用词
stopword_path="E:/program/hlt_stop_words.txt"
stpwrdlst=readfile(stopword_path).splitlines()
#构建TF-IDF词向量空间对象
tfidfspace=Bunch(target_name=bunch.target_name,label=bunch.label,filenames=bunch.filenames,tdm=[],vocabulary={})
#使用TfidVectorizer初始化向量空间模型
vectorizer=TfidfVectorizer(stop_words=stpwrdlst,sublinear_tf=True,max_df=0.5)
transfoemer=TfidfTransformer()#该类会统计每个词语的TF-IDF权值

#文本转为词频矩阵，单独保存字典文件
tfidfspace.tdm=vectorizer.fit_transform(bunch.contents)
#tfidfspace.vocabulary=vectorizer.vocabulary

#创建词袋的持久化
space_path="E:/program/test_word_bag/tfidfspace.dat"
writebunchobj(space_path,tfidfspace)

from sklearn.naive_bayes import MultinomialNB# 导入多项式贝叶斯算法包
# 导入训练集向量空间
trainpath = "E:/program/train_word_bag/tfidfspace.dat"
train_set = readbunchobj(trainpath)
# 导入验证集向量空间
valpath = "E:/program/val_word_bag/tfidfspace.dat"
val_set = readbunchobj(valpath)


# 应用贝叶斯算法
# alpha:0.001 alpha 越小，迭代次数越多，精度越高
clf = MultinomialNB(alpha=0.001).fit(train_set.tdm, train_set.label)

# 预测分类结果
predicted = clf.predict(val_set.tdm)
total = len(predicted)
rate = 0
for flabel, file_name, expct_cate in zip(val_set.label, val_set.filenames, predicted):
    if flabel != expct_cate:
        rate += 1
        print(file_name,": 实际类别：", flabel,"-->预测分类：", expct_cate)
# 精度
print("error_rate:",float(rate) *100 /float(total),"%")

from sklearn import metrics

def metrics_result(actual,predict):
    print("精度：{0:.3f}".format(metrics.precision_score(actual,predict,average='weighted')))
    print("召回：{0:0.3f}".format(metrics.recall_score(actual,predict,average='weighted')))
    print("f1-score:{0:.3f}".format(metrics.f1_score(actual,predict,average='weighted')))
metrics_result(test_set.label, predicted)
```
---
title: 题目 1427 [2013年第四届真题]买不到的数目 (C语言)
description: Q 1427 [2013 4th exam questions] The number that cannot be bought (C Language)
date: '2020-02-09'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1427: \[2013年第四届真题\]买不到的数目
时间限制: 1Sec 内存限制: 128MB
## 题目描述
小明开了一家糖果店。他别出心裁：把水果糖包成4颗一包和7颗一包的两种。糖果不能拆包卖。
小朋友来买糖的时候，他就用这两种包装来组合。当然有些糖果数目是无法组合出来的，比如要买  10  颗糖。
你可以用计算机测试一下，在这种包装情况下，最大不能买到的数量是17。大于17的任何数字都可以用4和7组合出来。
本题的要求就是在已知两个包装的数量时，求最大不能组合出的数字。
## 输入
两个正整数，表示每种包装中糖的颗数(都不多于1000) 
## 输出
一个正整数，表示最大不能买到的糖数 
## 样例输入
```
4  7 
```
## 样例输出
```
17
```
## C代码
```c
# include<stdio.h>
int main(){
	int a,b;
	scanf("%d%d",&a,&b);
	printf("%d\n",a*b-a-b);
	return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行
---
title: Q 1632 [Algorithm Improvement VIP]Number of pairs (C Language)
description: 题目 1632 [算法提高VIP]数对 (C语言)
date: '2020-03-21'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1632: \[算法训练VIP\]数对
时间限制: 1Sec 内存限制: 128MB
## 题目描述
编写一个程序，该程序从用户读入一个整数，然后列出所有的数对，每个数对的乘积即为该数。
## 输入
输入只有一行，即一个整数。 
## 输出
输出有若干行，每一行是一个乘法式子。（注意：运算符号与数字之间有一个空格）
## 样例输入
```
32 
```
## 样例输出
```
1 * 32 = 32
2 * 16 = 32
4 * 8 = 32
8 * 4 = 32
16 * 2 = 32
32 * 1 = 32
```
## C代码
```c
#include<stdio.h>
int main(){
    int i,n;
    scanf("%d",&n);
    for(i=1;i<=n;i++){
        if(n%i==0)printf("%d * %d = %d\n",i,n/i,n);
    }
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行
---
title: 题目 1616 [算法提高VIP]反置数 (C语言)
description: Q 1616 [Algorithm Improvement VIP]Inverted number (C Language)
date: '2020-04-11'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# 题目 1616: \[算法训练VIP\]反置数
时间限制: 1Sec 内存限制: 128MB
## 题目描述
一个整数的“反置数”指的是把该整数的每一位  数字的顺序颠倒过来所得到的另一个整数。如果一个整数的末尾是以0结尾，那么在它的反置数当中，这些0就被省略掉了。比如说，1245的反置数是  5421，而1200的反置数是21。请编写一个程序，输入两个整数，然后计算这两个整数的反置数之和sum，然后再把sum的反置数打印出来。要求：由  于在本题中需要多次去计算一个整数的反置数，因此必须把这部分代码抽象为一个函数的形式。
## 输入
输入只有一行，包括两个整数，中间用空格隔开。
## 输出
输出只有一行，即相应的结果。
## 样例输入
```
435 754
```
## 样例输出
```
199 
```
## C代码
#### 解法A
先将整数转换为字符串，再倒置，再转换为整数。
```c
#include <stdio.h> 
#include <string.h>
int fun(int n)
{
    char s[20],t;
    int len,m;
    sprintf(s,"%d",n);
    len=strlen(s);
    for(int i=0;i<len/2;i++)
    {
        t=s[i];s[i]=s[len-1-i];s[len-1-i]=t;   
    }
    sscanf(s,"%d",&m);
    return m; 
}
int main()
{
    int x,y,sum;
    scanf("%d%d",&x,&y);
    sum=fun(x)+fun(y);
    printf("%d\n",fun(sum));
    return 0;
}
```
#### 解法B
是先删除整数后面的0，然后倒置形成新的整数。
```c
#include <stdio.h> 
int fun(int n)
{  
    int m=0;
    while(n%10==0)
        n=n/10;
    while(n!=0)
    {
        m=m*10+n%10;
        n=n/10;
    } 
    return m; 
}
int main()
{
    int x,y,sum;
    scanf("%d%d",&x,&y);
    sum=fun(x)+fun(y);
    printf("%d\n",fun(sum));
    return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行
---
title: 题目 1115 DNA (C语言)
description: Q 1115 DNA (C Language)
date: '2020-02-04'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# 题目 1115: DNA
时间限制: 1Sec 内存限制: 128MB
## 题目描述
小强从小就喜欢生命科学，他总是好奇花草鸟兽从哪里来的。终于， 小强上中学了，接触到了神圣的名词--DNA.它有一个双螺旋的结构。这让一根筋的小强抓破头皮，“要是能画出来就好了” 小强喊道。现在就请你帮助他吧
## 输入
输入包含多组测试数据。第一个整数N（N<=15）,N表示组数，每组数据包含两个整数a,b。a表示一个单位的DNA串的行数，a为奇数且 3<=a<=39。b表示重复度(1<=b<=20)。
## 输出
输出DNA的形状，每组输出间有一空行。
## 样例输入
```
2
3 1
5 4
```
## 样例输出
```
X X
 X
X X

X   X
 X X
  X
 X X
X   X
 X X
  X
 X X
X   X
 X X
  X
 X X
X   X
 X X
  X
 X X
X   X
```
## C代码
```c
#include<stdio.h>
int main()
{
    int N,a[20],b[20],i,j,k,p;
    scanf("%d",&N);
    i = 1;
    while(i<=N)
    {
        scanf("%d%d",&a[i],&b[i]);
        i++;
    }
    for(i=1;i<=N;i++)
    {
        for(j=1;j<=b[i];j++)
        {
            for(k=1;k<a[i];k++)
            {
                for(p=1;p<=a[i];p++)
                {
                    if(p == k || p+k == a[i]+1)
                        printf("X");
                    else
                        printf(" ");
                }
                printf("\n");                
            }
        }
        for(j=1;j<=a[i];j++)
        {
            if(j == k || j+k == a[i]+1)
                printf("X");
            else
                printf(" ");
        }
        printf("\n");
        if(i != N)
        printf("\n");
    }
    return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行
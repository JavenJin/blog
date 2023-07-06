---
title: Q 1648 [Algorithm Training VIP]Order of precedence (C Language)
description: 题目 1648 [算法训练VIP]求先序排列 (C语言)
date: '2020-03-21'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1648: \[算法训练VIP\]求先序排列
时间限制: 1Sec 内存限制: 128MB
## 题目描述
给出一棵二叉树的中序与后序排列。求出它的先序排列。（约定树结点用不同的大写字母表示，长度< =8）。
## 输入
两行，每行一个字符串，分别表示中序和后序排列 
## 输出
一个字符串，表示所求先序排列 
## 样例输入
```
BADC 
BDCA 
```
## 样例输出
```
ABCD
```
## C代码
```c
#include<stdio.h>
#include<string.h>
#define Max(x,y) x>y?x:y 
char s[100],s1[100];
void Pd(char *x,char *x1)
{
    int i,j,k,l,p;
    char c;
    char x3[100],x4[100];//X3:x的左  X4:x的右 
    char x6[100],x7[100];//X6:x1的左  X7:x1的右 
    int t=strlen(x1)-1;
    c=x1[t];//输出后序序列的最后一位 (根节点)
    printf("%c",c);
    p=strlen(x);
    for(i=0;x[i];i++)
    {    
        if(c==x[i])
        {
            break;
        } 
        x3[i]=x[i];//把X的前i个放入左节点的中序 X1的前i个放入右节点的中序 
        x6[i]=x1[i];
    }
    x3[i]='\0';//别忘了 
    x6[i]='\0';
    k=0;
    for(l=i+1;l<p;l++)//把X i后边(i是根节点)的数放入x4 
    {
        x4[k++]=x[l];
    } 
    x4[k]='\0';
    k=0;
    for(l=i;l<p-1;l++)//把X1 的i---（最后-1）放入x7中(因为最后是根节点) 
    {
        x7[k++]=x1[l];
    }
    x7[k]='\0';
    if(x3[0])
        Pd(x3,x6);
    if(x4[0])
        Pd(x4,x7);
}
int main()
{
    int i,j;
    scanf("%s",s);
    scanf("%s",s1);
    Pd(s,s1);
    return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行
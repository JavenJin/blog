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

# Q 1648: [Algorithm Training VIP]Order of precedence
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Give the middle-order and post-order arrangement of a binary tree. Find its prior-order arrangement. (Agreed tree nodes are denoted by different capital letters, length < = 8).
## Input
Two lines, one string per line, representing the middle-order and back-order arrangement respectively 
## Output
A string indicating the desired order of precedence 
## Sample Input
```
BADC 
BDCA 
```
## Sample Output
```
ABCD
```
## C Code
```c
#include<stdio.h>
#include<string.h>
#define Max(x,y) x>y?x:y 
char s[100],s1[100];
void Pd(char *x,char *x1)
{
    int i,j,k,l,p;
    char c;
    char x3[100],x4[100];//X3:left of x X4:right of x 
    char x6[100],x7[100];//X6:x1's left X7:x1's right 
    int t=strlen(x1)-1;
    c=x1[t];//Output the last bit of the subsequence (root node)
    printf("%c",c);
    p=strlen(x);
    for(i=0;x[i];i++)
    {    
        if(c==x[i])
        {
            break;
        } 
        x3[i]=x[i];//Put the first i of X into the middle order of the left node The first i of X1 into the middle order of the right node 
        x6[i]=x1[i];
    }
    x3[i]='\0';//Don't forget 
    x6[i]='\0';
    k=0;
    for(l=i+1;l<p;l++)//Put the number after X i (i is the root node) into x4 
    {
        x4[k++]=x[l];
    } 
    x4[k]='\0';
    k=0;
    for(l=i;l<p-1;l++)//Put i --- (last-1) of X1 into x7 (because last is the root node) 
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
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
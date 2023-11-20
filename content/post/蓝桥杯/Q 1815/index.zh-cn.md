---
title: 题目 1815 [2014年第五届真题]排列序数 (C语言)
description: Q 1815 [2014 5th exam questions]Ranking order (C Language)
date: '2020-04-11'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1815: \[2014年第五届真题\]排列序数
时间限制: 1Sec 内存限制: 128MB
## 题目描述
如果用a b c d这4个字母组成一个串，有4!=24种，如果把它们排个序，每个串都对应一个序号：
  abcd  0
  abdc  1
  acbd  2
  acdb  3
  adbc  4
  adcb  5
  bacd  6
  badc  7
  bcad  8
  bcda  9
  bdac  10
  bdca  11
  cabd  12
  cadb  13
  cbad  14
  cbda  15
  cdab  16
  cdba  17
  ...
现在有不多于10个两两不同的小写字母，给出它们组成的串，你能求出该串在所有排列中的序号吗？
## 输入
一行，一个串。
## 输出
一行，一个整数，表示该串在其字母所有排列生成的串中的序号。注意：最小的序号是0。
## 样例输入
```
bdca
```
## 样例输出
```
11
```
## C代码
```c
#include<stdio.h>
#include<string.h>
char s[11],p[11],d[11],c;        //p用来存放s数组(不变的)  d用来记录s数组(变的) 
int cd,num=0,b[11];              //b用来标记；   cd记录数组的长度； num计数 
void dfs(int x)
{
    int i,j;
    if(x==cd)                    //如果x的长度和cd长度一样 num++ 
    {
        num++;
        if(strcmp(p,d)==0)       //如果当前数组与s数组一样 就输出（num-1）因为abcd是1 
    {
        printf("%d",num-1);
    }
        return ;
    }
    for(i=0;i<cd;i++)
    {
        if(!b[i])
        {
            d[x]=s[i];            //记录 
            b[i]=1;               //标记 
            dfs(x+1);             //dfs 
            b[i]=0;               //回溯 
        }
    }
}
int main()
{
    int i,j,n=0;
    scanf("%s",s);                    //输入 
    strcpy(p,s);                      //复制到p数组 
    cd=strlen(s);                     //记录长度 
     for(i=0;i<strlen(s)-1;i++)       //冒泡法排序 
     {
         for(j=0;j<strlen(s)-1-i;j++)
         {
             if(s[j]>s[j+1])
             {
                 c=s[j];
                 s[j]=s[j+1];
                 s[j+1]=c;
             }
         }
     }
     memset(b,0,sizeof(b));            //把b置零  把一开始的置零也行
     dfs(0);                           //dfs 
    return 0;
 }
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行
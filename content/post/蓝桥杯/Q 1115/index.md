---
title: Q 1115 DNA (C Language)
description: 题目 1115 DNA (C语言)
date: '2020-02-04'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1115: DNA
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Since he was a child, Qiang has always loved life science and was always curious about where flowers, plants, birds and animals came from. Finally, when Qiang went to middle school, he was introduced to the sacred term, DNA. This made the one-track minded Qiang scratch his head, "If only I could draw it," Qiang shouted. Help him now!
## Input
The input contains multiple sets of test data. The first integer N (N<=15), N denotes the number of groups and each group contains two integers a,b. a denotes the number of rows of a unit DNA string, a is odd and 3<=a<=39. b denotes the degree of repetition (1<=b<=20).
## Output
The shape of the output DNA, with a blank line between each set of outputs.
## Sample Input
```
2
3 1
5 4
```
## Sample Output
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
## C Code
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
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
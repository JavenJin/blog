---
title: Q 1616 [Algorithm Improvement VIP]Inverted number (C Language)
description: 题目 1616 [算法提高VIP]反置数 (C语言)
date: '2020-04-11'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1616: [Algorithm Improvement VIP]Inverted number
Time limit: 1Sec Memory Limit: 128MB
## Title Description
The "inverse" of an integer is another integer obtained by reversing the order of each digit of that integer. If an integer ends in zeros, then those zeros are omitted from its inverse. For example, the inverse of 1245 is 5421 and the inverse of 1200 is 21. Write a program that enters two integers, calculates the sum of the inverse of these two integers, and then prints the inverse of sum. Requirement: Since you need to calculate the inverse of an integer more than once in this problem, you must abstract this part of the code to a function.
## Input
The input has only one line, including two integers, separated by a space.
## Output
The output has only one line, the corresponding result.
## Sample Input
```
435 754
```
## Sample Output
```
199 
```
## C Code
#### Solution A
Convert an integer to a string first, then invert it, then convert it to an integer.
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
#### Solution B
Is to first delete the zeros after the integer and then invert it to form a new integer.
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
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
---
title: Q 1609 [Algorithm Improvement VIP]Black Friday (C Language)
description: 题目 1609 [算法提高VIP]黑色星期五 (C语言)
date: '2020-03-21'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1609: [Algorithm Improvement VIP]Black Friday
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Some Westerners are superstitious, and if the 13th of a month falls on a Friday, they feel that it is not auspicious, or in ancient times, "bad for everything". Write a program to find out how many times in a given year the 13th falls on a Friday, to help your superstitious friend solve his problem.
Note: (1) There are 365 days in a year, and 366 days in a leap year. A leap year is a year that is divisible by 4 and not by 100, or a year that is divisible by both 100 and 400; (2) January 1, 1998 is known to be a Thursday, and the year entered by the user must be greater than or equal to 1998.
## Input
The input has only one line, i.e. a specific year (greater than or equal to 1998). 
## Output
The output has only one line, i.e. how many times in the year it occurred that it was both the 13th and a Friday. 
## Sample Input
```
1998
```
## Sample Output
```
3
```
## C Code
```c
#include<stdio.h>
int day[14];
int month[2][20]={{31,28,31,30,31,30,31,31,30,31,30,31},{31,29,31,30,31,30,31,31,30,31,30,31}};
int leap(int year)
{
    if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0)
    {
        //It's a leap year
        return 1;
    }else{
        //Not a leap year
        return 0;
    }
}
void f(int n)
{
    int i,j;
    long sum=0;
    int count = 0;
    for(i=1998;i<n;i++)
    {
        if(leap(i))
        {
            sum += 366;
        }else{
            sum += 365;
        }
    }
    //Count how many days from January 1, 1998 to the 13th of each month
    if(leap(n))
    {
        for(i=1;i<13;i++)
        {
            day[i]=12+sum;
            for(j=0;j<i-1;j++)
            {
                day[i] +=month[1][j];
            }
        }
    }else{
        for(i=1;i<13;i++)
        {
            day[i]=12+sum;
            for(j=0;j<i-1;j++)
            {
                day[i] += month[0][j];
            }
        }
    }
    //Count the number of occurrences of week 5
    for(i=1;i<=12;i++)
    {
        if((day[i]-3)%7==5)
        {
            count ++;
        }  
    }
    printf("%d\n",count);
}
int main()
{
    int year;
    scanf("%d",&year);
    f(year);
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
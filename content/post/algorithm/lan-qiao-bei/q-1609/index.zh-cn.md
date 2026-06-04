---
title: 题目 1609 [算法提高VIP]黑色星期五 (C语言)
description: Q 1609 [Algorithm Improvement VIP]Black Friday (C Language)
date: '2020-03-21'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# 题目 1609: \[算法训练VIP\]黑色星期五
时间限制: 1Sec 内存限制: 128MB
## 题目描述
有些西方人比较迷信，如果某个月的13号正好是星期五，他们就会觉得不太吉利，用古人的说法，就是“诸事不宜”。请你编写一个程序，统计出在某个特定的年份中，出现了多少次既是13号又是星期五的情形，以帮助你的迷信朋友解决难题。
说明：（1）一年有365天，闰年有366天，所谓闰年，即能被4整除且不能被100整除的年份，或是既能被100整除也能被400整除的年份；（2）已知1998年1月1日是星期四，用户输入的年份肯定大于或等于1998年。
## 输入
输入只有一行，即某个特定的年份（大于或等于1998年）。 
## 输出
输出只有一行，即在这一年中，出现了多少次既是13号又是星期五的情形。 
## 样例输入
```
1998
```
## 样例输出
```
3
```
## C代码
```c
#include<stdio.h>
int day[14];
int month[2][20]={{31,28,31,30,31,30,31,31,30,31,30,31},{31,29,31,30,31,30,31,31,30,31,30,31}};
int leap(int year)
{
    if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0)
    {
        //是闰年
        return 1;
    }else{
        //不是闰年
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
    //统计每个月的13号距1998年1月1日有几天
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
    //统计星期5出现的次数
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
#### 通过[C语言网](https://www.dotcpp.com/)编译运行
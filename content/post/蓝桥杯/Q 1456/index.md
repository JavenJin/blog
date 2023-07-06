---
title: Q 1456 [Past Test Questions]Number of consecutive number intervals (C Language)
description: 题目 1456 [历届试题]连号区间数 (C语言)
date: '2019-04-01'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1456: \[历届试题\]连号区间数
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Xiao Ming has been thinking about this strange and interesting question these days:
How many consecutive number intervals are there in a certain full permutation of 1 to N? The definition of a contiguous interval here is:
If all the elements in the interval [L, R] (i.e., the Lth to the Rth elements of the arrangement) are sorted incrementally to obtain a "consecutive" series of length R-L+1, then the interval is called a consecutive interval.
When N is small, Xiao Ming can quickly figure out the answer, but when N becomes large, the problem is not so simple, and now Xiao Ming needs your help.
## input
The first row is a positive integer N (1 < = N < = 50000), representing the size of the full permutation. 
The second line is N different numbers Pi (1 < = Pi < = N), representing some full permutation of these N numbers.
## Output
Output an integer indicating the number of different concatenated intervals.
## Sample Input
```
5
3 4 2 5 1
```
## Sample Output
```
9
```
## C Code
```c
#include<stdio.h>
int main()
{
	long int n,i,j,max,min,sum=0;
	scanf("%ld",&n);
	long int a[n+1];    
	for(i=1;i<=n;i++)
		scanf("%ld",&a[i]);
	for(i=1;i<n;i++)//denotes the interval starting from the ith position 
	{
		min=max=a[i];
		for(j=i+1;j<=n;j++)//Indicates to end at j bit
		{    
    		if(a[j]<min){min=a[j];}
    		if(a[j]>max){max=a[j];}
			if(max-min==j-i) sum++; 
			//If the difference between the maximum and minimum values of an interval is equal to the current number of intervals j-i, then the interval must be continuous after necessarily rearranging 
		}
	}
	printf("%ld\n",sum+n);
	return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
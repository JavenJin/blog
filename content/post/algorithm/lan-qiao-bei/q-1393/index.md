---
title: Q 1393 Bell God Racing (C Language)
description: 题目 1393 钟神赛车 (C语言)
date: '2020-07-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1393: Bell God Racing
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Bell God recently coded tired, want to ride a bicycle scenery, so find a certain gentleman to ride a bicycle race. The speed of each bicycle of a certain gentleman and Bell God is known, Bell God wins one game to get 50 silver taels of silver, loses one game to lose 50 silver taels, and does not earn or lose in a tie. Bell God can arrange the number of high school and low grade bicycle appearances in any order, assuming that Bell God's physical strength is unlimited without loss seek Bell God can earn up to how much money
## Input
Multiple rows of test data, each row contains an integer n and 2n 32-bit positive integers, the first n indicates the number of bicycles, the next n 32-bit integers indicate the speed of a certain gentleman's bicycle, and the last n 32-bit integers indicate the speed of Bell God's bicycle
## Output
The clock god can arrange the number sequence of bicycle appearances at will. Output the maximum amount of money the clock god can earn, the result must be in the range of 32-bit integers
## Sample Input
```
3 2 1 3 2 2 3
3 2 1 3 1 1 3
```
## Sample Output
```
50
0
```
## C Code
```c
#include<stdio.h>  
void pai(int  *a,int n)
{
	int i,j,x;
	for(i=1;i<=n;i++)
	{
		for(j=0;j<n-1;j++)
		{
			if(a[j]<a[j+1])
			{
				x=a[j];a[j]=a[j+1];a[j+1]=x;
			}
		}
	} 
}

int main()  
{  
	int t[1000+22],q[1000+22]; 
    int n,i,j,k,s,win,lose;  
    while(scanf("%d",&n)!=EOF)  
    {  
		k=0;win=0,lose=0;  
        for(i=0;i<n;i++)
			scanf("%d",&q[i]);
        for(i=0;i<n;i++)
			scanf("%d",&t[i]);  
        pai(q,n);pai(t,n);
		while(k<n)
		{
			for(i=0;i<n-k;i++)
			{
				if(t[0]>q[i])
				{
					for(s=0;s<n-k-1;s++)
						t[s]=t[s+1];
					for(s=i;s<n-k-1;s++)
						q[s]=q[s+1];
					k++;
					win++;
					break;
				}
				else if((i==n-k-1)&&t[0]==q[i])
				{
					for(s=0;s<n-k-1;s++)
						t[s]=t[s+1];
					k++;
					break;
				}
				else if((i==n-k-1)&&t[0]<q[i])
				{
					lose=i+1;
					k=n;
					break;
				}
			}
		}
		printf("%d\n",50*(win-lose));  
    }
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
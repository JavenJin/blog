---
title: Q 1462 [Basic Exercise VIP]Huffuman Tree (C Language)
description: 题目 1462 [基础练习VIP]Huffuman树 (C语言)
date: '2019-03-01'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1462: [Basic Exercise VIP]Huffuman Tree
Time limit: 1Sec Memory Limit: 128MB
## Title Description
```
Huffman trees have a wide range of applications in coding. Here, we are only concerned with the process of constructing Huffman trees.

Given a column of numbers {pi} = {p0, p1, ..., pn-1}, the process of constructing a Huffman tree from this column is as follows:

1. find the two smallest numbers in {pi}, set to pa and pb, remove pa and pb from {pi}, and add their sum to {pi}. The cost of this process is noted as pa + pb.

2. Repeat step 1 until there is only one number left in {pi}.

The total cost of constructing the Huffman tree is obtained by adding up all the costs during the above operation.

The task: For a given series, you are now asked to find the total cost of constructing a Huffman tree using that series.



For example, for the series {pi} = {5, 3, 8, 2, 9}, the Huffman tree is constructed as follows:

1. Find the two smallest numbers in {5, 3, 8, 2, 9}, which are 2 and 3 respectively, remove them from {pi} and add the sum 5 to get {5, 8, 9, 5} with cost 5.

2. Find the two smallest numbers in {5, 8, 9, 5}, which are 5 and 5, remove them from {pi} and add the sum 10 to get {8, 9, 10} at a cost of 10.

3. Find the two smallest numbers in {8, 9, 10}, which are 8 and 9, remove them from {pi} and add the sum 17 to get {10, 17} at a cost of 17.

4. Find the two smallest numbers in {10, 17}, which are 10 and 17 respectively, remove them from {pi} and add the sum 27 to get {27} at a cost of 27.

5. Now, there is only one number left in the series, 27, and the construction process is finished, and the total cost is 5+10+17+27=59.
```
## Input
The first line of the input contains a positive integer n (n< =100). 

Next are n positive integers, denoted p0, p1, ..., pn-1, each number not exceeding 1000. 
## Output
Output the total cost of constructing a Huffman tree with these numbers. 
## Sample Input
```
5 
5 3 8 2 9
```
## Sample Output
```
59
```
## C Code
```c
#include<stdio.h>
#define AUM(x,y) {int t;t=x;x=y;y=t;}   //Macro definition, exchange of values.
int main()
{
	int n,i,sz[100],j,sum=0,t;
	scanf("%d",&n);
	for(i=0;i<n;i++)
		scanf("%d",&sz[i]);
	for(t=n-1;t>=1;t--)
	{
		for(i=0;i<n;i++)   //Each calculation is preceded by a sort and then the two numbers in the corresponding positions are added together.
			for(j=0;j<n-1;j++)
				if(sz[j+1]>sz[j])
					AUM(sz[j+1],sz[j]);
		sz[t-1] = sz[t-1]+sz[t];
		sum+=sz[t-1];
	}
	printf("%d",sum);
	return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
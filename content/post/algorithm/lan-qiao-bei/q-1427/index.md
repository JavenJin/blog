---
title: Q 1427 [2013 4th exam questions] The number that cannot be bought (C Language)
description: 题目 1427 [2013年第四届真题]买不到的数目 (C语言)
date: '2020-02-09'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1427: [2013 4th exam questions] The number that cannot be bought
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Xiao Ming opened a candy store. He has an original idea: he packs fruit candies into two kinds: 4 pieces in a packet and 7 pieces in a packet. The candy can't be opened and sold in packages.
When children come to buy candy, he uses these two kinds of packaging to combine. Of course there are some numbers of candies that cannot be combined, for example, to buy 10 candies.
You can use a computer to test that the maximum number that cannot be bought in this packaging case is 17. Any number greater than 17 can be combined with 4 and 7.
The requirement of this problem is to find the maximum number that cannot be combined out when the number of two packages is known.
## Input
Two positive integers, indicating the number of sugars in each package (neither more than 1000) 
## Output
A positive integer indicating the maximum number of sugars that cannot be bought 
## Sample Input
```
4  7 
```
## Sample Output
```
17
```
## C Code
```c
# include<stdio.h>
int main(){
	int a,b;
	scanf("%d%d",&a,&b);
	printf("%d\n",a*b-a-b);
	return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
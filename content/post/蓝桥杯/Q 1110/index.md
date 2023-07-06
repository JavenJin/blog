---
title: Q 1110 2^k decimal numbers (C Language)
description: 题目 1110 2^k进制数 (C语言)
date: '2020-02-04'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1110: 2^k decimal numbers (C Language)
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Let r be a 2^k progressive number and satisfy the following conditions:
(1) r is a 2^k progressive number with at least 2 digits.
(2) As a 2^k progressive number, each bit of r is strictly less than the adjacent bit to its right, except for the last bit.
(3) After converting r to a binary number q, the total number of bits of q does not exceed w.
Here, the positive integers k (1 ≤ k ≤ 9) and w (k < w ≤ 30,000) are given in advance.

Q: How many different r's are there to satisfy the above condition?
Let S be a string of length w (i.e., the string S consists of w "0s" or "1s"), and S corresponds to q in condition (3) above. If S can be divided into at least 2 segments, the binary number corresponding to S can be converted into the above 2^k number r.
Example: Let k=3 and w=7. Then r is an octal number (2^3=8). Since w=7, the 01 string of length 7 is divided into 3 segments (i.e. 1, 3, 3, the first segment on the left has only one binary bit), the octal numbers that satisfy the condition are
2 digits: the high bit is 1: 6 (i.e., 12, 13, 14, 15, 16, 17), the high bit is 2: 5, ..., the high bit is 6: 1 (i.e., 67). Total 6+5+...+1=21.
3 digits: The high digit can only be 1, the 2nd digit is 2:5 (i.e. 123, 124, 125, 126, 127), the 2nd digit is 3:4, ..., and the 2nd digit is 6:1 (i.e. 167). In total, 5 + 4 + ... + 1 = 15.
Therefore, there are 36 r's that satisfy the requirement.
## Input
Only 1 line for two positive integers, separated by a space:
k w
## Output
1 line, a positive integer, is the result of the requested calculation, i.e., the number of different r's that satisfy the condition (expressed as a decimal number), requiring that the highest digit must not be 0, and that no character other than a number (e.g., space, newline, comma, etc.) be inserted between the digits.
(Hint: the positive integer as a result may be large, but will not exceed 200 bits)
## Sample Input
3  7
## Sample Output
36
## C Code
```c
#include<stdio.h>
#include<math.h>

long C(int n,int m)
{
	long sum = 1;
	int i;
	for(i=1;i<=m;i++)
	{
		sum *= (n-i);
		sum /= i;
	}
	return sum;
}
int main()
{
	long sum=0;
    int k,w,max,wei,high,i;
    scanf("%d%d",&k,&w);
    max = pow(2,k);
    wei = w/k+1;
    high = pow(2,w%k)-1;
    if(max-wei < high)
    	high = max-wei;
    for(i=2;i<wei;i++)
    	sum += C(max,i);
    if(high != 0)
    	sum += (C(max,wei)-C(max-high,wei));
    printf("%d",sum);
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
---
title: Q 1255 [Algorithm Improvement]Energy Necklace (C Language)
description: 题目 1115 [算法提高]能量项链 (C语言)
date: '2020-02-06'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1255 [Algorithm Improvement]Energy Necklace
Time limit: 1Sec Memory Limit: 128MB
## Title Description
On the planet Mars, each Mars person wears a string of energy necklace. On the necklace are N energy beads. An energy bead is a bead with a head marker and a tail marker, and these markers correspond to a positive integer. Also, for two adjacent beads, the tail mark of the first bead must be equal to the head mark of the second bead. This is because only then, through the action of the suction cups (suction cups are an organ of the Mars people that absorb energy), the two beads can coalesce into one bead and release energy that can be absorbed by the suction cups. If the first energy bead has a head mark of m and a tail mark of r, and the second energy bead has a head mark of r and a tail mark of n, the energy released after aggregation is m*r*n (Mars units), and the newly created bead has a head mark of m and a tail mark of n.
When needed, the Mars person clips the two adjacent beads with a suction cup and gets energy by aggregation until only one bead is left on the necklace. Obviously, the total energy obtained by different aggregation sequences is different. Please design an aggregation sequence that maximizes the total energy released from a string of necklaces.
For example, let N=4, the head mark and tail mark of 4 beads are (2, 3) (3, 5) (5, 10) (10, 2) in order. We use the notation ◎ to denote the aggregation operation of two beads, and (j ◎ k) to denote the energy released by the aggregation of the jth and kth beads. Then the energy released after the aggregation of the fourth and first two beads is
(4◎1)=10*2*3=60。
The total energy released by this string of necklaces to obtain the optimal value of one aggregation sequence is
((4◎1)◎2)◎3）=10*2*3+10*3*5+10*5*10=710。
## Input
The first row is a positive integer N (4 ≤ N ≤ 100), which indicates the number of beads on the necklace. The second row is a space-separated set of N positive integers, all of which should not exceed 1000. i is the head mark of the i-th bead (1 ≤ i ≤ N), and when i < N, the tail mark of the i-th bead should be equal to the head mark of the i+1-th bead. The tail mark of the Nth bead should be equal to the head mark of the 1st bead.
As for the order of the beads, you can determine it like this: place the necklace on the table without crosses, designate the first bead at random, and then determine the order of the other beads in a clockwise direction.
## Output
There is only one row, a positive integer E (E ≤ 2.1*10^9), for the total energy released by an optimal aggregation sequence
## Sample Input
```
4
2 3 5 10
```
## Sample Output
```
710
```
## C Code
```c
#include<stdio.h>
#include<string.h>
#define Max(a,b) a>b?a:b
int main()
{
	long long int dp[202][202];
	long long int s[202];
	memset(dp,0,sizeof(dp));
	long long int sum=0;
	int n,i,j,k,len;
	scanf("%d",&n);
	for(i=1;i<=n;i++)
        scanf("%lld",&s[i]),s[i+n]=s[i];
    for(len=2;len<=n;len++)
        for(i=1;i+len-1<2*n;i++)
        {
            j=i+len-1;
      	    for(k=i;k<j;k++)
      	        dp[i][j]=Max(dp[i][j],dp[i][k]+dp[k+1][j]+s[i]*s[k+1]*s[j+1]);
        }
	for(i=1;i<=n;i++)
	    if(sum<dp[i][i+n-1])sum=dp[i][i+n-1];
	printf("%lld\n",sum);
	return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.
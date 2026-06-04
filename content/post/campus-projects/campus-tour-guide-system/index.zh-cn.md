---
title: 校园导游系统（纯C语言实现）最短路径 - Dijkstra算法
description: Campus tour guide system (pure C implementation) Shortest path - Dijkstra algorithm
date: '2019-11-27'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Dijkstra
---
### 西京学院导游系统

学习数据结构+C语言实现

```c
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#include <graphics.h>

      
#define MaxViewNum 50      /*景点个数最大50*/
#define MaxRoad 10000      /*定义路径为无穷大*/

typedef int dist[MaxViewNum];
typedef int path[MaxViewNum];

//定义三个结构体表示图中内容 
typedef struct
{
    char name[30];          /*景点名称*/
    char introduce[200];    /*景点介绍*/	
    int  x,y;               /*景点坐标*/ 
}JDXX;                      /*景点信息*/

typedef struct
{
    JDXX jd[MaxViewNum];                 /*存放顶点的一维数组，数组第零单元没有用上*/
    int length[MaxViewNum][MaxViewNum];  /*存放路径长度*/
}MGraph;

MGraph M;                               /*全局变量,定义M为MGraph类型*/
int N=0;                                /*全局变量，目前景点个数*/ 
path p;
dist d;

void init()
{
    int i,j;
    strcpy(M.jd[1].name,"北门");
    strcpy(M.jd[1].introduce,"坐落于西京路，毗邻生活区，购物方便，交通便利");
	strcpy(M.jd[2].name,"艺舫");
    strcpy(M.jd[2].introduce,"坐落于桂湖上，通往艺术的天堂");
    strcpy(M.jd[3].name,"花街");
    strcpy(M.jd[3].introduce,"以s形花坛作为背景，一年四季花常开");
    strcpy(M.jd[4].name,"科苑");
    strcpy(M.jd[4].introduce,"为学生英语听力，计算机等课程提供场所"); 
    strcpy(M.jd[5].name,"广场");
    strcpy(M.jd[5].introduce,"包括博能国旗时代广场，为学生提供娱乐活动场地");
    strcpy(M.jd[6].name,"教学楼");
    strcpy(M.jd[6].introduce,"学生日常上课的地方，通往知识的殿堂");
    strcpy(M.jd[7].name,"工程舫");
    strcpy(M.jd[7].introduce,"为学生提供实验，实训，学习的场地");
    strcpy(M.jd[8].name,"图书馆");
    strcpy(M.jd[8].introduce,"具有浓厚的文化积淀，供同学安静读书学习的环境");
    strcpy(M.jd[9].name,"公寓楼");
    strcpy(M.jd[9].introduce,"11——18号公寓楼");
    strcpy(M.jd[10].name,"大学生发展与服务中心");
    strcpy(M.jd[10].introduce,"各书院办公地点，为学生提供一站式服务");
    strcpy(M.jd[11].name,"璞玉餐厅");
    strcpy(M.jd[11].introduce,"四层餐厅，为学生提供一日三餐");
    strcpy(M.jd[12].name,"京华大礼堂");
    strcpy(M.jd[12].introduce,"学校最大的礼堂");
    strcpy(M.jd[13].name,"体育馆");
    strcpy(M.jd[13].introduce,"为学生室内运动提供场所");
    strcpy(M.jd[14].name,"科研楼");
    strcpy(M.jd[14].introduce,"进行科学研究的场所");
    strcpy(M.jd[15].name,"南操场");
    strcpy(M.jd[15].introduce,"同学们傍晚刷运动软件");
    strcpy(M.jd[16].name,"南湖");
    strcpy(M.jd[16].introduce,"又名含笑湖，夜晚灯光非常美丽");
    strcpy(M.jd[17].name,"南门");
    strcpy(M.jd[17].introduce,"坐落于神禾二路，交通方便");
    for(i=1;i<=MaxViewNum;i++)
	{
		for(j=1;j<=MaxViewNum;j++)
        {
			M.length[i][j]=MaxRoad;
        }
    }
    for(i=1;i<=MaxViewNum;i++)
    M.length[i][i]=0;
    M.length[1][2]=M.length[2][1]=30;
    M.length[1][3]=M.length[3][1]=30;
    M.length[2][3]=M.length[3][2]=30;
    M.length[2][4]=M.length[4][2]=70;
    M.length[3][5]=M.length[5][3]=30;
    M.length[3][6]=M.length[6][3]=50;
    M.length[4][5]=M.length[5][4]=50;
    M.length[4][7]=M.length[7][4]=100;
    M.length[5][6]=M.length[6][5]=30;
    M.length[6][7]=M.length[7][6]=100;
    M.length[6][10]=M.length[10][6]=20;
    M.length[7][8]=M.length[8][7]=30;
    M.length[7][9]=M.length[9][7]=30;
    M.length[7][10]=M.length[10][7]=30;
    M.length[8][9]=M.length[9][8]=30;
    M.length[9][10]=M.length[10][9]=50;
    M.length[9][11]=M.length[11][9]=30;
    M.length[10][11]=M.length[11][10]=30;
    M.length[11][12]=M.length[12][11]=100;
    M.length[11][13]=M.length[13][11]=50;
    M.length[12][13]=M.length[13][12]=50;
    M.length[12][15]=M.length[15][12]=30;
    M.length[12][17]=M.length[17][12]=150;
    M.length[13][14]=M.length[14][13]=70;
    M.length[13][15]=M.length[15][13]=30;
    M.length[13][16]=M.length[16][13]=50;
    M.length[14][16]=M.length[16][14]=50;
    M.length[15][16]=M.length[16][15]=20;
    M.length[16][17]=M.length[17][16]=30;
    N=17;
    M.jd[1].x=50;
    M.jd[1].y=25;
    M.jd[2].x=150;
    M.jd[2].y=125;
    M.jd[3].x=250;
    M.jd[3].y=25;
    M.jd[4].x=150;
    M.jd[4].y=475;
    M.jd[5].x=350;
    M.jd[5].y=175;
    M.jd[6].x=475;
    M.jd[6].y=50;
    M.jd[7].x=475;
    M.jd[7].y=475;
    M.jd[8].x=575;
    M.jd[8].y=650;
    M.jd[9].x=675;
    M.jd[9].y=525;
    M.jd[10].x=575;
    M.jd[10].y=150;
    M.jd[11].x=750;
    M.jd[11].y=225;
    M.jd[12].x=575;
    M.jd[12].y=525;
    M.jd[13].x=575;
    M.jd[13].y=225;
    M.jd[14].x=1075;
    M.jd[14].y=25;
    M.jd[15].x=1000;
    M.jd[15].y=375;
    M.jd[16].x=1100;
    M.jd[16].y=225;
    M.jd[17].x=1175;
    M.jd[17].y=325;
}

void scsyjd()
{
	int t;
	printf("所有景点如下：\n"); 
	for(t=1;t<=N;t++)
	{
		printf("编号：%d\n   景点：%s\n   介绍：%s\n",t,M.jd[t].name,M.jd[t].introduce);
	}
	printf("\n按任意键返回！");
	getch();
}

void zengj()
{  char s1[30],s2[200];    //景点名称；景点介绍 
   int t,i,q,p,x,y;        //t为与该景点共有几个景点相连；i为应第几个景点与之相连；
                           //q为与之相连的景点；p为这个景点和新景点的距离 
                           //x为此景点位置的x值；y为此景点位置的y值 
   N++;  
   printf("请输入该景点的名称：");                 
   scanf("%s",&s1);
   printf("请输入该景点的介绍：");
   scanf("%s",&s2);
   printf("请输入该景点的位置的x值：");
   scanf("%d",&x); 
   printf("请输入该景点的位置的y值：");
   scanf("%d",&y);
   strcpy(M.jd[N].name,s1);
   strcpy(M.jd[N].introduce,s2);
   M.jd[N].x=x;
   M.jd[N].y=y;
   printf("请输入共有几个景点与此景点相通：");
   scanf("%d",&t);
   for(i=1;i<=t;i++)
   {  printf("第%d个景点与之相通；",i);
      scanf("%d",&q);
      printf("他们之间的距离为：");
      scanf("%d",&p);
      M.length[N][q]=M.length[q][N]=p;
	}
	printf("\n按任意键返回！");
	getch();
}

void scjd()
{
	printf("请输入要删除的景点序号数");
	int t,p,Q;
	scanf("%d",&p);
	Q=p;
	if(p<=N)
	{
	for(t=1;t<=N;t++)
	for(p=p;p<=N;p++)
		{
		M.length[t][p]=M.length[t][p+1];
		M.length[p][t]=M.length[p+1][t];		 
		}
	for(Q;Q<N;Q++)
	M.jd[Q]=M.jd[Q+1];
	printf("删除成功O(∩_∩)O");
	}
else
printf("删除失败←_←");
N--;
printf("\n按任意键返回！");	
getch();
}

void gxjd()
{
	int t;
	char s1[30],s2[200];
	printf("请输入要更新的景点编号：");
	scanf("%d",&t);
	if(t>N)
	printf("此景点不存在，更新失败");
	else
	{
		printf("请输入景点名称：");
		scanf("%s",&s1);
		printf("请输入景点介绍：");
		scanf("%s",&s2);
		strcpy(M.jd[t].name,s1);
		strcpy(M.jd[t].introduce,s2);
		printf("更新完成！"); 
	}
	printf("\n按任意键返回！");
	getch();
}

void zengjl()
{
	int a,b,c; 
	printf("请问要在那两个景点之间增加一条路\n");
	printf("请输入第一个景点编号：");
	scanf("%d",&a);
	printf("请输入第二个景点编号：");
	scanf("%d",&b);
	printf("请输入这条路的长度：");
	scanf("%d",&c);
	if(a>N||b>N)
	printf("景点超出了已有景点范围，路径增加失败！");
	else
	{
		M.length[a][b]=M.length[b][a]=c;
		printf("路径增加成功！"); 
	} 
	printf("\n按任意键返回！");
	getch();
}

void scl()
{
	int a,b; 
	printf("请问要删除那两个景点之间的路\n");
	printf("请输入第一个景点编号：");
	scanf("%d",&a);
	printf("请输入第二个景点编号：");
	scanf("%d",&b);
	if(a>N||b>N)
	printf("景点超出了已有景点范围，路径删除失败！");
	else
	{
		M.length[a][b]=M.length[b][a]=MaxRoad;
		printf("路径删除成功！"); 
	} 
	printf("\n按任意键返回！");
	getch();
}

void gxl()
{
	int a,b,c; 
	printf("请问要更新那两个景点之间的路\n");
	printf("请输入第一个景点编号：");
	scanf("%d",&a);
	printf("请输入第二个景点编号：");
	scanf("%d",&b);
	printf("请输入更新后的长度：");
	scanf("%d",&c);
	if(a>N||b>N)
	printf("这条路不存在，路径更新失败！");
	else
	{
		M.length[a][b]=M.length[b][a]=c;
		printf("路径更新成功！"); 
	} 
	printf("\n按任意键返回！");
	getch();
}

void cxjd()
{
	int a;
	printf("请问您要查询的景点编号是：");
	scanf("%d",&a);
	if(a>N)
	printf("查询的景点不存在，查询失败！"); 
	else
	printf("编号：%d\n   景点：%s\n   介绍：%s\n",a,M.jd[a].name,M.jd[a].introduce);
	printf("\n按任意键返回！"); 
	getch();
}

void dijkstra_syjd()
{
	int v0;
	printf("请输入查询的景点：");
	scanf("%d",&v0);
	boolean final[MaxViewNum];
	int i,k,j,v,min,x;
	for(v=1;v<=N;v++)
	{
	final[v]=FALSE;
	d[v]=M.length[v0][v];
	if(d[v]<MaxRoad&&d[v]!=0)
	p[v]=v0;
	else
	p[v]=-1;
	}
	final[v0]=TRUE;
	d[v0]=0;
	for(i=2;i<=N;i++)
	{
		min=MaxRoad;
		for(k=1;k<=N;++k)
		if(!final[k]&&d[k]<min)
		{
			v=k;
			min=d[k];
		}
	
		if(min==MaxRoad)
		return;
		final[v]=TRUE;
		for(k=1;k<=N;++k)
		if(!final[k]&&(min+M.length[v][k]<d[k]))
		{
			d[k]=min+M.length[v][k];
			p[k]=v;
		}
	}
}

void printsyjd()
{
	int st[MaxViewNum],i,pre,top=-1;
	for(i=1;i<=N;i++)
	{
		printf("\n到达景点%2d的总距离是: %5d , 所经过路径:",i,d[i]);
		st[++top]=i;
		pre=p[i];
		while(pre!=-1)
		{
			st[++top]=pre;
			pre=p[pre];
		}
	while(top>0)
	{
	printf("%d",st[top--]);
	if(top>0)
	printf("---");
	}
	}
	getch();
}

void dijkstra_ygjd()
{
	int v0;
	printf("请输入出发景点：");
	scanf("%d",&v0);
	boolean final[MaxViewNum];
	int i,k,j,v,min,x;
	for(v=1;v<=N;v++)
	{
	final[v]=FALSE;
	d[v]=M.length[v0][v];
	if(d[v]<MaxRoad&&d[v]!=0)
	p[v]=v0;
	else
	p[v]=-1;
	}
	final[v0]=TRUE;
	d[v0]=0;
	for(i=2;i<=N;i++)
	{
		min=MaxRoad;
		for(k=1;k<=N;++k)
		if(!final[k]&&d[k]<min)
		{
			v=k;
			min=d[k];
		}
	
		if(min==MaxRoad)
		return;
		final[v]=TRUE;
		for(k=1;k<=N;++k)
		if(!final[k]&&(min+M.length[v][k]<d[k]))
		{
			d[k]=min+M.length[v][k];
			p[k]=v;
		}
	}
}

void printygjd()
{
	int y;
	printf("\n请输入到达景点：");
	scanf("%d",&y);
	int st[MaxViewNum],i,pre,top=-1;
	for(i=1;i<=N;i++)
	{
		if(i==y) 
		printf("\n总距离是: %5d , 所经过路径:",d[i]);
		st[++top]=i;
		pre=p[i];
		while(pre!=-1)
		{
			st[++top]=pre;
			pre=p[pre];
		}
	while(top>0)
	{
	if(i==y)
	{
	printf("%d",st[top--]);
	if(top>0)
	printf("---");
	}
	else
	top--;
	}
	}
	getch();
}

void scdt()
{
	int i,j;
	char s[100];
	strcpy(s,"西京学院地图");
	initgraph(1200,800); 
	for(i=1;i<=N;i++)
	{
		setfillcolor(RGB(225,236,0));
		fillcircle(M.jd[i].x,M.jd[i].y,20);
		outtextxy(M.jd[i].x,M.jd[i].y,M.jd[i].name);
	}
	for(i=1;i<=N;i++)
		for(j=1;j<=N;j++)
		{
			if(M.length[i][j]>0&&M.length[i][j]<1000)
				line(M.jd[i].x,M.jd[i].y,M.jd[j].x,M.jd[j].y);
		}
	outtextxy(900,650,s);
	getch();
	closegraph();
}



main()
{
	init(); 
	int x;
	while(1)
	{
		printf("**********************************************************************\n");
		printf("*         =.=                                          =.=           *\n");
		printf("*    `                                                        `      *\n");
		printf("*     `              主人，欢迎来到西京哟~  喵~              `       *\n");
		printf("*      `              ^-^                  ^-^              `        *\n");
		printf("*       `                       ^-^                        `         *\n");
		printf("**********************************************************************\n");
    	printf("\n                    西京导游系统（输入0退出程序）：");
		printf("\n                     1、输出所有景点及其介绍");
		printf("\n                     2、查询某一个景点及其介绍");
		printf("\n                     3、增加一个景点");
		printf("\n                     4、删除一个景点");
		printf("\n                     5、更新一个景点");
		printf("\n                     6、增加一条路");
		printf("\n                     7、删除一条路");
		printf("\n                     8、更新一条路");
		printf("\n                     9、查询某一景点到其他所有景点的最短路径");
		printf("\n                    10、查询某两个景点之间的最短路径   ");
		printf("\n                    11、输出地图                       已有景点：%d个\n",N);
		printf("请输入选项："); 
		scanf("%d",&x);
		if(x==0)
		break;
		else
			switch(x)
			{
				case 1:scsyjd();break;
				case 2:cxjd();break;
				case 3:zengj();break;
				case 4:scjd();break;
				case 5:gxjd();break;
				case 6:zengjl();break;
				case 7:scl();break;
				case 8:gxl();break;
				case 9:dijkstra_syjd();printsyjd();break;
				case 10:dijkstra_ygjd();printygjd();break;
				case 11:scdt();break;
			} 
			system("cls");
	}
}
```
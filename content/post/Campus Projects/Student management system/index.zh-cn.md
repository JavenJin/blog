---
title: Student management system (pure C implementation)
description: 学生管理系统（纯C语言实现）
date: '2018-12-20'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
---
### 学生管理系统（纯C语言实现）

```c
#include "stdio.h"
#include"string.h"
#include"stdlib.h" 

struct Student
{
     char ID[20];
     char Name[20];
     float Mark1;
     float Mark2;
     float Mark3;
     float Average;
};
 
struct Student students[1000];
int num=0;
 
float Avg(struct Student stu)
{
     return (stu.Mark1+stu.Mark2+stu.Mark3)/3;
}

int Student_SearchByIndex(char id[])
 
{
 
     int i;
     for (i=0;i<num;i++)
     {
         if (strcmp(students[i].ID,id)==0)
         {
              return i;
         }
     }
     return -1;
}

/*通过姓名返回数组下标*/
int Student_SearchByName(char name[])
{
     int i;
     for (i=0;i<num;i++)
     {
         if (strcmp(students[i].Name,name)==0)
         {
              return i;
         }
     }
     return -1;
}

/*显示单条学生记录*/ 
void Student_DisplaySingle(int index)
{
     printf("%10s%10s%8s%8s%8s%10s\n","学号","姓名","高数成绩","c语言成绩","计算机成绩","平均成绩");
     printf("-------------------------------------------------------------\n");
     printf("%10s%10s%8.2f%8.2f%8.2f%10.2f\n",students[index].ID,students[index].Name,students[index].Mark1,students[index].Mark2,students[index].Mark3,students[index].Average);
}

/*插入学生信息*/ 
void Student_Insert()
{
     while(1)
     {
         printf("请输入学号:");
         scanf("%s",&students[num].ID);
         getchar();
         printf("请输入姓名:");
         scanf("%s",&students[num].Name);
         getchar();
         printf("请输入高数成绩:");
         scanf("%f",&students[num].Mark1);
         getchar();
         printf("请输入c语言成绩:");
         scanf("%f",&students[num].Mark2);
         getchar();
         printf("请输入计算机成绩:");
         scanf("%f",&students[num].Mark3);
         getchar();
         students[num].Average=Avg(students[num]);
         num++;
         printf("是否继续?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*修改学生信息*/
void Student_Modify()
{
     //float mark1,mark2,mark3;
     while(1)
     {
         char id[20];
         int index;
         printf("请输入要修改的学生的学号:");
         scanf("%s",&id);
         getchar();
         index=Student_SearchByIndex(id);
         if (index==-1)
         {
              printf("学生不存在!\n");
         }
         else
         {
              printf("你要修改的学生信息为:\n");
              Student_DisplaySingle(index);
              printf("-- 请输入新值--\n");
              printf("请输入学号:");
              scanf("%s",&students[index].ID);
              getchar();
              printf("请输入姓名:");
              scanf("%s",&students[index].Name);
              getchar();
              printf("请输入高数成绩:");
              scanf("%f",&students[index].Mark1);
              getchar();
              printf("请输入c语言成绩:");
              scanf("%f",&students[index].Mark2);
              getchar();
              printf("请输入计算机成绩:");
              scanf("%f",&students[index].Mark3);
              getchar();
              students[index].Average=Avg(students[index]);
         }
         printf("是否继续?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*删除学生信息*/
void Student_Delete()
{
     int i;
     while(1)
     {
         char id[20];
         int index;
         printf("请输入要删除的学生的学号:");
         scanf("%s",&id);
         getchar();
         index=Student_SearchByIndex(id);
         if (index==-1)
         {
              printf("学生不存在!\n");
         }
         else
         {
              printf("你要删除的学生信息为:\n");
              Student_DisplaySingle(index);
              printf("是否真的要删除?(y/n)");
              if (getchar()=='y')
              {
                   for (i=index;i<num-1;i++)
                   {
                       students[i]=students[i+1];//把后边的对象都向前移动
                   }
                   num--;
              }
              getchar();
         }
         printf("是否继续?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*按姓名查询*/
void Student_Select()
{
     while(1)
     {
         char name[20];
         int index;
         printf("请输入要查询的学生的姓名:");
         scanf("%s",&name);
         getchar();
         index=Student_SearchByName(name);
         if (index==-1)
         {
              printf("学生不存在!\n");
         }
         else
         {
              printf("你要查询的学生信息为:\n");
              Student_DisplaySingle(index);
         }
         printf("是否继续?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*按平均值排序*/
void Student_SortByAverage()
{
     int i,j;
     struct Student tmp;
     for (i=0;i<num;i++)
     {
         for (j=1;j<num-i;j++)
         {
              if (students[j-1].Average<students[j].Average)
              {
                   tmp=students[j-1];
                   students[j-1]=students[j];
                   students[j]=tmp;
              }
         }
     }
}
 
/*显示学生信息*/
void Student_Display()
{
     int i;
     printf("%10s%10s%8s%8s%8s%10s\n","学号","姓名","高数成绩","c语言成绩","计算机成绩","平均成绩");
     printf("-------------------------------------------------------------\n");
     for (i=0;i<num;i++)
     {
         printf("%10s%10s%8.2f%8.2f%8.2f%10.2f\n",students[i].ID,students[i].Name,students[i].Mark1,students[i].Mark2,students[i].Mark3,students[i].Average);
     }
}
 
/*将学生信息从文件读出*/
void IO_ReadInfo()
{
     FILE *fp;
     int i;
     if ((fp=fopen("Database.txt","rb"))==NULL)
     {
         printf("不能打开文件!\n");
         return;
     }
     if (fread(&num,sizeof(int),1,fp)!=1)
     {
         num=-1;
     }
     else
     {
         for(i=0;i<num;i++)
         {
              fread(&students[i],sizeof(struct Student),1,fp);
         }
     }
     fclose(fp);
}
 
/*将学生信息写入文件*/
void IO_WriteInfo()
{
     FILE *fp;
     int i;
     if ((fp=fopen("Database.txt","wb"))==NULL)
     {
         printf("不能打开文件!\n");
         return;
     }
     if (fwrite(&num,sizeof(int),1,fp)!=1)
     {
         printf("写入文件错误!\n");
     }
     for (i=0;i<num;i++)
     {
         if (fwrite(&students[i],sizeof(struct Student),1,fp)!=1)
         {
              printf("写入文件错误!\n");
         }
     }    
     fclose(fp);
}
 
/*主程序*/
void main()
{
     int choice;
     IO_ReadInfo();
     while(1)
     {
         /*主菜单*/
         printf("\n------ 学生管理系统------\n");
         printf("1. 增加学生记录\n");
         printf("2. 修改学生记录\n");
         printf("3. 删除学生记录\n");
         printf("4. 按姓名查询学生记录\n");
         printf("5. 按平均成绩排序\n");
         printf("6. 退出\n");
         printf("请选择(1-6):");
         scanf("%d",&choice);
         getchar();
         switch(choice)
         {
         case 1:
              Student_Insert();
              break;
         case 2:
              Student_Modify();
              break;
         case 3:
              Student_Delete();
              break;
         case 4:
              Student_Select();
              break;
         case 5:
              Student_SortByAverage();
              Student_Display();
              break;
         case 6:
              exit(0);
              break;
         }
         IO_WriteInfo();
     }
}
```
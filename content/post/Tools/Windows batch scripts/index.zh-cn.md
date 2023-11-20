---
title: Windows批处理脚本（.bat）
description: Windows batch scripts(.bat)
date: '2022-05-17'
categories:
    - Tools
tags:
    - Tools
---

# Windows批处理脚本（.bat）

## 常用文件操作DOS命令

- dir	列文件名
- cd	改变当前目录
- ren	改变文件名
- copy	拷贝文件
- del	删除文件
- md	建立子目录
- rd	删除目录
- deltree	删除目录树
- format	格式化磁盘
- edit	文本编辑
- type	显示文件内容
- mem	查看内存状况
- help	显示帮助提示
- cls	清屏
- move	移动文件，改目录名
- more	分屏显示
- xcopy	拷贝目录和文件
- echo	显示输入内容
- echo on	打开命令回显
- echo off	关闭命令回显
- @	加上@的命令不会显示
- pause	将程序挂起，按下任意键继续
- \>	将显示的内容输出到某处
- \>\>	将显示内容追加到某处
- \>nul	命令后加上\>nul表示输出到空设备
- mode	设置窗口尺寸：mode con cols=32 lines=8
- color	设置背景颜色：color 3a（背景(暗靛色)和文字(亮绿色)）
- title	改变当前命令提示符的标题名称
- rem	注释（属于命令会显示出来）
- ::	注释（不会显示出来）
- prompt	修改当前路径为根路径并重命名
- goto	命令跟上标签可以跳转
- :	命令后面写标签名（不区分大小写），特殊标签:EOF或:eof不需要定义
- call	调用批处理或者标签
- start	启动应用程序

## 变量

| 命令                            | 解释                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| set var=1                       | 定义变量var并将1复制给a                                      |
| set var                         | 查看变量var的值                                              |
| set v                           | 查看所有v开头的变量值                                        |
| set                             | 查看所有变量的值                                             |
| %var%                           | var变量的值（内容）                                          |
| set /a var=48                   | 将数字48赋给变量var，32位的整数型数值，占用4个字节           |
| set /p var                      | 用户手动输入值给var                                          |
| set /p var=请输入一些文字       | 用户手动输入值给var，并显示提示文字：“请输入一些文字”        |
| set var=Hello world!            |                                                              |
| echo %var:o=z%                  | 输出Hello world!不改变var值                                  |
| set var2=%var:ld=ms and bugs%   | 将Hello worms and bugs!赋值给var2不改变var值                 |
| %var:~m%                        | 数字m为正数表示取变量var中从左侧第m个字符以后的内容 数字m为负数表示取变量var中从右侧数第-m个字符以及其右侧所有字符 |
| %var:~m,n%                      | 从m开始，n为正数取n个字符，n为负数取到剩-n个字符为止         |
| set /a num=48                   | 将数值48赋值给变量num                                        |
| set /a result=%num%+12          | 变量num与12相加的结果赋给变量result                          |
| echo %result%                   | 显示变量result的值                                           |
| setlocal EnableDelayedExpansion | 延迟变量扩充使!var!有意义                                    |

## 传递参数

使用%接收参数 在call或者start或者在cmd中运行批处理文件时后面直接加上参数来传递参数

```bat
接收参数：
echo 您输入的第1条参数为 %1
echo 您输入的第2条参数为 %2

传递参数：
call 被调用.bat hello world!
start 被调用.bat hello world!
./被调用.bat hello world!
```

## 条件IF

| 符号 | 意义     |
| ---- | -------- |
| EQU  | 相等     |
| NEQ  | 不相等   |
| LSS  | 小于     |
| LEQ  | 小于等于 |
| GTR  | 大于     |
| GEQ  | 大于等于 |
| NOT  | 非       |

- if exist	判断文件是否存在
- if defined	判断环境变量是否被定义

## 循环FOR

for循环的一般使用格式：for %i in (\*.\*) do @echo %i

```bat
:::::::批量修改文件名.bat:::::::
@echo off
setlocal EnableDelayedExpansion
set /a num=1
for %%i in (D:\test\*.txt) do (
ren "%%i" !num!.txt
set /a num+=1
)
::::::::::::::::::::::::::::::::
```

for循环使用数字循环的一般格式：for /l %i in (5,3,16) do echo %i

数值型变量i依次成为：5、8、11、14。从5开始，每次增加3到16为止。

```bat
::::::::::圆圈方阵.bat::::::::::
@echo off
setlocal EnableDelayedExpansion

set var=○
for /l %%i in (1,1,7) do set var=%var%!var!
:: 此时变量 var 已经变成一行连续的8个圆圈了

for /l %%i in (1,1,8) do (
echo 这是第 %%i 份>输出结果%%i.txt
for /l %%j in (1,1,8) do echo %var%>>输出结果%%i.txt
)

echo 8 X 8 的 ○ 矩阵已经画好，并保存到8份文本文件里了
pause
::::::::::::::::::::::::::::::::
```

## 组合命令

1. &

   ```bat
   echo Checking what executable files we have in WINDOWS... & dir C:\WINDOWS\*.exe & echo And we got lots of stuff here.
   ```

   &在多个命令之间起连接作用。

   不论三者中每一条命令的结果如何，后面的一条命令总能被得到执行。

2. &&

   和&类似，并列多条命令并将其按顺序执行。

   如果多命令中的某一条命令执行出错，后面的命令将不会再被执行；如果一直没有出错，就会一直执行完所有并列命令。

3. ||

   ||的用途和&&恰好相反。

   当遇到执行正确的命令后将不再执行后面的命令。

   如果没有出现正确的命令则一直执行完所有命令。

## 管道命令

1. \>和\>\>

   输入重定向命令。将一条命令或某个程序输出结果的重定向到特定文件中。

   \>会清除掉原文件中的内容后写入指定文件，而\>\>只会追加内容到指定文件中。

2. |

   它可以将它左边命令的输出结果放到它右边的命令里作为参数。

3. 管道命令还有\<、\<&和\>&，它们并不常见，暂不讨论。

## 学习地址

[Windows 批处理脚本学习教程](http://docs.30c.org/dosbat/index.html)
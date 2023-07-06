---
title: Gluttony Game (Java GUI)
description: 贪吃蛇游戏（Java GUI）
date: '2020-12-24'
categories:
    - Java (Programming Language)
tags:
    - Java (Programming Language)
---

# Gluttony Game (Java GUI)

## GUI Overview

### GUI Overview

&emsp;&emsp;In the early days, computers offered users a monotonous, boring, character-only state of the "Command Line Interface (CLI)". It is to this day that we can still vaguely see them: open a DOS window in Windows and you can see the footprint of history. Later, Apple took the lead in the computer's operating system to achieve a graphical user interface (Graphical User Interface, or GUI), but due to Apple's closed market strategy to complete their own computer hardware, operating system, application software a one-stop product, and other PC incompatible. This makes Apple miss a good opportunity to unify the global PC.

&emsp;&emsp;Later, Microsoft launched the popular Windows operating system, which established the status of the operating system standard with its excellent graphical user interface. This also created the world's richest man --- Bill. Gates and the titan of the IT industry, Microsoft Corporation.

&emsp;&emsp;In today's world of graphical user interfaces, an application is not acceptable to users without a good GUI. And the Java language understands the importance of this, and it provides a set of tools that make it easy to build GUIs. In this and the next chapter, we will demonstrate this to you in full.

&emsp;&emsp;A Graphical User Interface (GUI, also known as a graphical user interface) is a user interface for computer operations that uses a graphical display.

&emsp;&emsp; GUI is an interface display format for human-computer communication that allows users to manipulate on-screen icons or menu options using input devices such as a mouse to select commands, invoke files, start programs, or perform some other everyday task. The GUI has many advantages over a character interface where routine tasks are performed by entering text or character commands from the keyboard. The GUI consists of windows, drop-down menus, dialog boxes, and their corresponding control mechanisms that are standardized across a variety of newer applications, i.e., the same operations are always performed in the same way. In the GUI, the user sees and manipulates graphical objects and applies the techniques of computer graphics.

### Packages for GUI development in Java

&emsp;&emsp;java.awt package - mainly provides font/layout manager

&emsp;&emsp;javax.swing package [common for commercial development] - mainly provides various components (windows/buttons/textboxes)

&emsp;&emsp;java.awt.event package - event handling, implementation of backend functions.

## Game screenshots

![Gluttony Game 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Gluttony%20game%20(Java%20GUI)/gluttony-game1.jpeg)

![Gluttony Game 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Gluttony%20game%20(Java%20GUI)/gluttony-game2.jpeg)

![Gluttony Game 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Gluttony%20game%20(Java%20GUI)/gluttony-game3.jpeg)

## Code display

### The main launch class of the game

```java
package com.study.snake;

import javax.swing.*;

//游戏的主启动类
public class StartGame {
    public static void main(String[] args) {
        JFrame frame = new JFrame("贪吃蛇");

        frame.setBounds(10,10,915,720);
        frame.setResizable(false);//窗口大小不可变
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        //正常游戏界面都应该在面板上！
        frame.add(new GamePanel());

        frame.setVisible(true);
    }
}
```

### The game's panel

```java
package com.study.snake;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.util.Random;

//游戏的面板
public class GamePanel extends JPanel implements KeyListener, ActionListener {

    //定义蛇的数据结构
    int length; //蛇的长度
    int[] snakeX = new int[600]; //蛇的x坐标 25*25
    int[] snakeY = new int[500]; //蛇的坐标 25*25
    String fx;//初始方向

    //食物的坐标
    int foodX;
    int foodY;
    Random random = new Random();

    int score;//成绩

    //游戏当前的状态： 开始  or  停止
    boolean isStart = false; //默认是停止
    boolean isFail = false; //游戏失败


    //定时器 以ms为单位 1000ms = 1s
    Timer timer = new Timer(100,this); //100毫秒执行一次！

    //构造器
    public GamePanel() {
        init();
        //获得焦点和键盘事件
        this.setFocusable(true); //获得焦点事件
        this.addKeyListener(this); //获得键盘监听事件
        timer.start(); //游戏一开始定时器就启动
    }

    //初始化方法
    public void init(){
        length = 3;
        snakeX[0] = 100;        snakeY[0] = 100; //脑袋的坐标
        snakeX[1] = 75 ;        snakeY[1] = 100; //第一个身体的坐标
        snakeX[2] = 50 ;        snakeY[2] = 100; //第二个身体的坐标
        fx = "R"; //初始方向向右
        foodX = 25 + 25*random.nextInt(34);
        foodY = 75 + 25*random.nextInt(24);

        score = 0;//初始0分
    }

    //绘制面板，游戏中的所有东西，都使用这个画笔来画
    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this,g,25,11);//头部广告栏画上去
        g.fillRect(25,75,850,600);//默认的游戏界面

        //画积分
        g.setColor(Color.WHITE);
        g.setFont(new Font("微软雅黑",Font.BOLD,18));
        g.drawString("长度"+length,750,40);
        g.drawString("分数"+score,750,60);

        //画食物
        Data.food.paintIcon(this,g,foodX,foodY);

        //把小蛇画上去
        if (fx.equals("R")){
            Data.right.paintIcon(this,g,snakeX[0],snakeY[0]);
        }else if (fx.equals("L")){
            Data.left.paintIcon(this,g,snakeX[0],snakeY[0]);
        }else if (fx.equals("U")){
            Data.up.paintIcon(this,g,snakeX[0],snakeY[0]);
        }else if (fx.equals("D")){
            Data.down.paintIcon(this,g,snakeX[0],snakeY[0]);
        }

//        Data.right.paintIcon(this,g,snakeX[0],snakeY[0]);//蛇头初始化向右

        for (int i = 1; i < length ; i++){
            Data.body.paintIcon(this,g,snakeX[i],snakeY[i]);//身体坐标
        }

//        Data.body.paintIcon(this,g,snakeX[1],snakeY[1]);//第一个身体坐标
//        Data.body.paintIcon(this,g,snakeX[2],snakeY[2]);//第二个身体坐标


        //游戏状态
        if (isStart == false){
            g.setColor(Color.WHITE);
            //设置字体
            g.setFont(new Font("微软雅黑",Font.BOLD,40));
            g.drawString("按下空格开始游戏！",300,300);
        }

        if (isFail){
            g.setColor(Color.RED);
            //设置字体
            g.setFont(new Font("微软雅黑",Font.BOLD,40));
            g.drawString("失败，按下空格重新开始！",300,300);
        }

    }

    //键盘监听事件
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode(); //获得键盘按键是哪一个
        if (keyCode == KeyEvent.VK_SPACE){ //如果按下的是空格键
            if (isFail){
                isFail = false; //重新开始
                init();
            }else{
                isStart = !isStart; //取反
            }
            repaint();
        }
        //小蛇移动
        if (keyCode == KeyEvent.VK_UP){
            fx = "U";
        }else if (keyCode == KeyEvent.VK_DOWN){
            fx = "D";
        }else if (keyCode == KeyEvent.VK_LEFT){
            fx = "L";
        }else if (keyCode == KeyEvent.VK_RIGHT){
            fx = "R";
        }
    }

    //事件监听--需要通过固定时间来刷新，1s=10次
    @Override
    public void actionPerformed(ActionEvent e) {
        if (isStart && isFail == false){ //如果游戏是开始状态并且没有失败，就让小蛇动起来

            //吃食物
            if (snakeX[0] == foodX && snakeY[0] == foodY){
                length++; //长度 + 1
                //分数加10
                score += 10;
                //再次随机食物
                foodX = 25 + 25*random.nextInt(34);
                foodY = 75 + 25*random.nextInt(24);
            }

            //移动
            for (int i = length-1; i > 0; i--){ //后一节移动到前一节的位置snakeX[1] = snakeX[0];
                snakeX[i] = snakeX[i-1];
                snakeY[i] = snakeY[i-1];
            }
            //走向
            if (fx.equals("R")){
                snakeX[0] = snakeX[0]+25;
                if (snakeX[0] > 850){
                    snakeX[0] = 25;
                } //边界判断
            }else if (fx.equals("L")){
                snakeX[0] = snakeX[0]-25;
                if (snakeX[0] < 25){
                    snakeX[0] = 850;
                } //边界判断
            }else if (fx.equals("U")){
                snakeY[0] = snakeY[0]-25;
                if (snakeY[0] < 75){
                    snakeY[0] = 650;
                } //边界判断
            }else if (fx.equals("D")){
                snakeY[0] = snakeY[0]+25;
                if (snakeY[0] > 650){
                    snakeY[0] = 75;
                } //边界判断
            }

            //失败判断，撞到自己就算失败
            for (int i = 1; i < length; i++) {
                if (snakeX[0] == snakeX[i] && snakeY[0] == snakeY[i]){
                    isFail = true;
                }
            }

            repaint(); //重画页面

        }
        timer.start(); //定时器开启！

    }

    @Override
    public void keyTyped(KeyEvent e) {

    }

    @Override
    public void keyReleased(KeyEvent e) {

    }
}
```

### Games for the data center

```java
package com.study.snake;

import javax.swing.*;
import java.net.URL;

//数据中心
public class Data {

    //相对路径  相对于当前类的路径
    //绝对路径  相对于当前项目的根目录
    public static URL headerURL = Data.class.getResource("statics/header.png");
    public static ImageIcon header = new ImageIcon(headerURL);

    public static URL upURL = Data.class.getResource("statics/up.png");
    public static ImageIcon up = new ImageIcon(upURL);

    public static URL downURL = Data.class.getResource("statics/down.png");
    public static ImageIcon down = new ImageIcon(downURL);

    public static URL leftURL = Data.class.getResource("statics/left.png");
    public static ImageIcon left = new ImageIcon(leftURL);

    public static URL rightURL = Data.class.getResource("statics/right.png");
    public static ImageIcon right = new ImageIcon(rightURL);

    public static URL foodURL = Data.class.getResource("statics/food.png");
    public static ImageIcon food = new ImageIcon(foodURL);

    public static URL bodyURL = Data.class.getResource("statics/body.png");
    public static ImageIcon body = new ImageIcon(bodyURL);
}
```

## Code Download

Source code download link: [Gluttony Game](https://download.csdn.net/download/weixin_42718701/13770943)
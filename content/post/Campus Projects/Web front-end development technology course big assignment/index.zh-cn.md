---
title: Web前端开发技术课程大作业
description: Web front-end development technology course big assignment
date: '2020-07-27'
categories:
    - Front End
tags:
    - Front End
    - Html
    - CSS
    - JavaScript
---

## Web前端开发技术课程大作业
### 作业要求

网站前端程序不仅要能够把用户要求的内容呈现出来，还要满足布局良好、界面美观、配色优雅、表现形式多样等要求。
为此，本次作业的要求主要有：

（1）登录功能。登陆是对用户的验证，防止非法用户登陆和使用。

（2）注册功能。注册是对新用户的加入设定的，可以增加游戏用户。

（3）导航功能。提供完整的系统导航功能，帮助用户快速定位到需要浏览的区域。

（4）广告轮播。广告轮播实现了重要客户的主要产品核心位置展示功能。

（5）搜索入口。搜索功能提供客户搜索定位功能，可以帮助客户快速找到需要的产品。

### 最终界面

![homework1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Web%20front-end%20development%20technology%20course%20big%20assignment/homework1.jpeg)

![homework2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Web%20front-end%20development%20technology%20course%20big%20assignment/homework2.jpeg)

![homework3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Web%20front-end%20development%20technology%20course%20big%20assignment/homework3.jpeg)

![homework4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Web%20front-end%20development%20technology%20course%20big%20assignment/homework4.jpeg)

![homework5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Web%20front-end%20development%20technology%20course%20big%20assignment/homework5.jpeg)

![homework6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Web%20front-end%20development%20technology%20course%20big%20assignment/homework6.jpeg)

### 代码

#### index.html

```html
<!doctype html>
<html lang="en">

<head>
    <title>英雄联盟</title>
    <meta charset="UTF-8">
    <meta name="keywords" content="LOL,腾讯游戏,英雄联盟" />
    <meta name="description" content="LOL,腾讯游戏,英雄联盟" />

    <link href="css/index.css" rel="stylesheet" type="text/css" />
    <script type="text/javascript" src="js/qiehuan.js"></script>
    <script type="text/javascript" src="js/switchpic.js"></script>
</head>

<body onload="init();">
    <div id="topNavBar">
        <input type="text" value="">
        <input type="button" value="搜索" id="where">
        <a href="logon.html" class="nav_on">注册</a> &nbsp;
        <a href="login.html" class="nav_on">登录</a>
    </div>
    <div id="container" class="">
        <div id="header" class="">
            <img src="img/lol_logo.jpg" alt="">
        </div>
        <div id="menu_out">
            <div id="menu_in">
                <div id="menu">
                    <ul id="nav">
                        <li><a class="nav_on" id="mynav0" onmouseover="javascript:qiehuan(0)" href="#" target="framebody"><span>游戏资料</span></a></li>
                        <li class="menu_line"></li>
                        <li><a href="#" onmouseover="javascript:qiehuan(1)" id="mynav1" class="nav_off"><span>游戏商城</span></a></li>
                        <li class="menu_line"></li>
                        <li><a href="#" onmouseover="javascript:qiehuan(2)" id="mynav2" class="nav_off"><span>游戏合作</span></a></li>
                        <li class="menu_line"></li>
                        <li><a href="#" onmouseover="javascript:qiehuan(3)" id="mynav3" class="nav_off"><span>社区互动</span></a></li>
                        <li class="menu_line"></li>
                        <li><a href="#" onmouseover="javascript:qiehuan(4)" id="mynav4" class="nav_off"><span>赛事官网</span></a></li>
                        <li class="menu_line"></li>
                        <li><a href="#" onmouseover="javascript:qiehuan(5)" id="mynav5" class="nav_off"><span>自助系统</span></a></li>
                        <li class="menu_line"></li>
                        <li><a href="#" onmouseover="javascript:qiehuan(6)" id="mynav6" class="nav_off"><span>游戏视频</span></a></li>
                        <li class="menu_line"></li>
                        <li><a href="#" onmouseover="javascript:qiehuan(7)" id="mynav7" class="nav_off"><span>填写问卷</span></a></li>
                        <li class="menu_line"></li>
                        <li><a class="nav_off" id="mynav8" onmouseover="javascript:qiehuan(8)" href="#"><span>关于网站</span></a></li>
                    </ul>
                    <div id="menu_con">
                        <div id="qh_con0" style="display: block">
                            <ul>
                                <li><a href="#"><span>游戏下载</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>游戏指引</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="./web_first.html" target="block"><span>资料库</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>云顶之弈</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>攻略中心</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con1" style="display: none">
                            <ul>
                                <li><a href="#"><span>点卷充值</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>道具城</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>周边商城</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con2" style="display: none">
                            <ul>
                                <li><a href="#"><span>LOL桌游</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>LOL信用卡</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>网吧特权</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>电竞小说</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con3" style="display: none">
                            <ul>
                                <li><a href="#"><span>官方社区</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>视频中心</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>官方论坛</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>官方微信</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>官方微博</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con4" style="display: none">
                            <ul>
                                <li><a href="#"><span>LPL职业联赛</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>LDL发展联赛</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>全球总决赛</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>全明星赛</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>季中杯</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>德玛西亚杯</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>全国高校联赛</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con5" style="display: none">
                            <ul>
                                <li><a href="#"><span>转区系统</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>封号查询</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>账号注销</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>信誉分系统</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con6" style="display: none">
                            <ul>
                                <li><a href="#"><span>推荐视频</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>官方视频</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>娱乐视频</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>赛事视频</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>云顶之弈视频</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>教学视频</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con7" style="display: none">
                            <ul>
                                <li><a href="web_question.html" target="block"><span>填写问卷</span></a></li>
                            </ul>
                        </div>
                        <div id="qh_con8" style="display: none">
                            <ul>
                                <li><a href="#"><span>联系客服</span></a></li>
                                <li class="menu_line2"></li>
                                <li><a href="#"><span>网站作者</span></a></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div id="main">
            <div id="top" class="">
                <a href="#"><img id="pic" src="img/example1.jpg" border="0" alt="" onmouseover="pause();" onmouseout="reStart();"></a>
            </div>

            <div id="down" class="">
                <iframe name="framebody" src="web_first.html"></iframe>
            </div>
        </div>
        <div class="bottom">
            <ul>
                <li><strong>友情链接：</strong>
                    <select size="1" name="d1" onchange="window.open(this.options[this.selectedindex].value)">
                        <option>
                            知名游戏厂家&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                        </option>
                        <option value="https://game.qq.com/portal2010/about.htm">腾讯游戏</option>
                        <option value="https://www.activisionblizzard.com/">动视暴雪</option>
                        <option value="https://www.microsoft.com/zh-cn/">微软游戏工作室</option>
                        <option value="https://www.apple.com.cn/">苹果</option>
                        <option value="https://www.sony.com.cn/">索尼</option>
                    </select>
                    <select size="1" name="d1" onchange="window.open(this.options[this.selectedindex].value)">
                        <option>
                            优秀游戏连接&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                        </option>
                        <option value="https://pubg.qq.com/">绝地求生</option>
                        <option value="https://dnf.qq.com/">地下城与勇士</option>
                        <option value="http://www.m3guo.com/v2/">梦三国</option>
                        <option value="https://wow.blizzard.cn/landing">魔兽世界</option>
                        <option value="https://xyq.163.com/">梦幻西游</option>
                        <option value="https://wuxia.qq.com/">天涯明月刀</option>
                    </select>
                </li>
                <li>
                    腾讯游戏&nbsp;·&nbsp;英雄联盟&nbsp;&nbsp;LOL 1998-2020&copy;保留所有权利，未经允许不得复制、镜像</li>
            </ul>
        </div>
    </div>
</body>

</html>
```

#### login.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>登陆界面</title>
    <link href="css/login.css" rel="stylesheet" type="text/css" />
</head>

<body>
    <div class="dowebok">
        <div class="logo"></div>
        <div class="form-item">
            <input id="username" type="text" autocomplete="off" placeholder="账号">
        </div>
        <div class="form-item">
            <input id="password" type="password" autocomplete="off" placeholder="登录密码">
        </div>
        <div class="form-item">
            <a href="index.html"><button id="submit">登 录</button></a>
        </div>
    </div>
</body>

</html>
```

#### index.css

```css
            @charset "utf-8";
            * {
                font-size: 12px;
                font-family: Arial, Helvetica, sans-serif;
            }
            
            body {
                margin: 0px auto;
                padding: 0px;
                text-align: center;
                position: relative;
            }
            
            #topNavBar {
                position: absolute;
                margin-left: 290px;
                font-size: 20px;
            }
            
            #topNavBar a {
                font-size: 12px;
            }
            
            #topNavBar a:link {
                color: white;
                text-decoration: none;
            }
            
            #topNavBar a:visited {
                color: white;
                text-decoration: none;
            }
            
            #topNavBar a:hover {
                color: white;
                text-decoration: none;
            }
            
            #topNavBar a:active {
                color: white;
                text-decoration: none;
            }
            
            #where {
                margin-right: 660px;
            }
            
            #container {
                width: 960px;
                padding: 0 auto;
                margin: 0 auto;
            }
            
            img {
                width: 960px;
                height: auto;
            }
            
            #menu ul {
                padding: 0;
                border: 0;
                list-style: none;
                line-height: 150%;
                margin-top: 0;
                margin-right: 0;
                margin-bottom: 0;
                margin-left: 40px;
            }
            
            #menu li {
                color: white;
            }
            
            #menu_out {
                width: 960px;
                padding-left: 4px;
                margin-left: auto;
                margin-right: auto;
                background: url("../img/menu_left.gif") no-repeat left top;
                overflow: hidden;
                /* ����������� */
            }
            
            #menu_in {
                background: url("../img/menu_right.gif") no-repeat right top;
                padding-right: 4px;
            }
            
            #menu {
                background: url("../img/menu_bg.gif") repeat-x;
                height: 73px;
                width: 960px;
            }
            
            .menu_line {
                background: url("../img/menu_line.gif") no-repeat center top;
                width: 8px;
            }
            
            .menu_line2 {
                background: url("../img/menu_line2.gif") no-repeat center top;
                width: 15px;
            }
            
            #nav {
                padding-left: 20px;
                width: 960px;
            }
            
            #nav li {
                float: left;
                height: 35px;
            }
            
            #nav li a {
                float: left;
                display: block;
                padding-left: 6px;
                height: 35px;
                background: url("../img/menu_on_left.gif") no-repeat left top;
                cursor: pointer;
                text-decoration: none;
            }
            
            #nav li a span {
                float: left;
                padding: 11px 14px 10px 10px;
                line-height: 14px;
                background: url("../img/menu_on_right.gif") no-repeat right top;
                font-size: 14px;
                font-weight: bold;
                color: #FFFFFF;
                text-decoration: none;
            }
            
            #nav li .nav_on {
                background-position: left 100%;
            }
            
            #nav li .nav_on span {
                background-position: right 100%;
                color: #333333;
                text-decoration: none;
                padding: 14px 14px 7px 10px;
            }
            
            #menu_con {
                text-align: left;
                padding-left: 20px;
                clear: both;
            }
            
            #menu_con li {
                float: left;
                height: 22px;
                margin-top: 8px;
            }
            
            #menu_con li a {
                display: block;
                float: left;
                background: url("../img/menu_on_left2.gif") no-repeat left top;
                cursor: pointer;
                padding-left: 3px;
            }
            
            #menu_con li a span {
                float: left;
                padding: 6px 10px 4px 10px;
                line-height: 12px;
                background: url("../img/menu_on_right2.gif") no-repeat right top;
                color: black;
            }
            
            #menu_con li a:hover {
                text-decoration: none;
                background: url("../img/menu_on_left2.gif") no-repeat left bottom;
            }
            
            #menu_con li a:hover span {
                background: url("../img/menu_on_right2.gif") no-repeat right bottom;
            }
            
            #main {
                width: 960px;
                height: 300px;
            }
            
            #top {
                width: 960px;
                height: auto;
                border: 1px solid white;
            }
            
            #top img {
                width: 960px;
                height: 489px;
            }
            
            #down {
                width: 960px;
                height: 500px;
                margin: 0 auto;
            }
            
            #down iframe {
                width: 960px;
                height: 500px;
                border: 0px;
                padding: 0px;
                margin: 0px;
            }
            
            .bottom {
                clear: both;
                height: 80px;
                background: #000000;
                text-align: center;
                padding-top: 20px;
                color: white;
                font-size: 18px;
                width: 960px;
                margin-top: 694px;
                /* please */
            }
            
            .bottom ul {
                list-style: none;
                color: white;
            }
```

#### login.css

```css
* {
    margin: 0;
    padding: 0;
}

html {
    height: 100%;
}

body {
    height: 100%;
    background: #fff url(../img/example1.jpg) 50% 50% no-repeat;
    background-size: cover;
}

.dowebok {
    position: absolute;
    left: 50%;
    top: 50%;
    width: 430px;
    height: 550px;
    margin: -300px 0 0 -215px;
    border: 1px solid #fff;
    border-radius: 20px;
    overflow: hidden;
}

.logo {
    width: 200px;
    height: 100px;
    margin-top: 130px;
    margin-bottom: 70px;
    margin-left: 130px;
    background: url(../img/logo-public.png) 0 0 no-repeat;
}

.form-item {
    position: relative;
    width: 360px;
    margin: 0 auto;
    padding-bottom: 30px;
}

.form-item input {
    width: 288px;
    height: 48px;
    padding-left: 70px;
    border: 1px solid #fff;
    border-radius: 25px;
    font-size: 18px;
    color: #fff;
    background-color: transparent;
    outline: none;
}

.form-item button {
    width: 360px;
    height: 50px;
    border: 0;
    border-radius: 25px;
    font-size: 18px;
    color: #1f6f4a;
    outline: none;
    cursor: pointer;
    background-color: #fff;
}

.tip {
    display: none;
    position: absolute;
    left: 20px;
    top: 52px;
    font-size: 14px;
    color: #f50;
}

.reg-bar {
    width: 360px;
    margin: 20px auto 0;
    font-size: 14px;
    overflow: hidden;
}

.reg-bar a {
    color: #fff;
    text-decoration: none;
}

.reg-bar a:hover {
    text-decoration: underline;
}

.reg-bar .reg {
    float: left;
}

.reg-bar .forget {
    float: right;
}

.dowebok ::-webkit-input-placeholder {
    font-size: 18px;
    line-height: 1.4;
    color: #fff;
}

.dowebok :-moz-placeholder {
    font-size: 18px;
    line-height: 1.4;
    color: #fff;
}

.dowebok ::-moz-placeholder {
    font-size: 18px;
    line-height: 1.4;
    color: #fff;
}

.dowebok :-ms-input-placeholder {
    font-size: 18px;
    line-height: 1.4;
    color: #fff;
}

@media screen and (max-width: 500px) {
    * {
        box-sizing: border-box;
    }
    .dowebok {
        position: static;
        width: auto;
        height: auto;
        margin: 0 30px;
        border: 0;
        border-radius: 0;
    }
    .logo {
        margin: 50px auto;
    }
    .form-item {
        width: auto;
    }
    .form-item input,
    .form-item button,
    .reg-bar {
        width: 100%;
    }
}
```

#### swithpic.js

```javascript
 /* switchpic.js */
 var CurScreen = 1;
 var MaxScreen = 7;
 var timer = null;

 function $(id) { return document.getElementById(id); }

 function switchPic() {
     if (CurScreen == MaxScreen) { CurScreen = 1; } else { CurScreen++; }
     $("pic").src = "img/example" + CurScreen + ".jpg";
 }

 function reStart() {
     switchPic();
     init();
 }

 function pause() {
     clearInterval(timer);
 }

 function init() {
     timer = setInterval('switchPic();', 1000);
 }
```

### csdn 链接
[Web前端开发技术课程大作业](https://blog.csdn.net/weixin_42718701/article/details/107619050)
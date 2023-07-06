---
title: Front End - Personal Resume Exercise
description: 前端 - 个人Resume练习
date: '2020-04-23'
categories:
    - Front End
tags:
    - Front End
    - Html
    - CSS
---

### Personal Resume Exercise

#### Final page effect

##### Reference page
[https://rscard.px-lab.com/startuper/](https://rscard.px-lab.com/startuper/)

##### Personal Works

![Personal Works](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Front%20End%20-%20Personal%20Resume%20Exercise/personal-works.jpeg)

### Code

#### index.html
```html
<!DOCTYPE html>
<html>

<head>
    <title>Me的个人简历</title>
    <link rel="stylesheet" href="./a.css">
</head>

<body>
    <div class="topNavBar">
        <div class="topNavBar-inner clearfix">
            <a href="#" class="logo" alt="logo">
                <span class="rs">RS</span><span class="card">card</span>
            </a>
            <nav>
                <ul class="clearfix">
                    <li>
                        <a href="#">关于</a>
                    </li>
                    <li>
                        <a href="#jineng">技能</a>
                    </li>
                    <li>
                        <a href="#zuopin">作品</a>
                    </li>
                    <li>
                        <a href="#">博客</a>
                    </li>
                    <li>
                        <a href="#">日历</a>
                    </li>
                    <li>
                        <a href="#">联系方式</a>
                    </li>
                    <li>
                        <a href="#">其他</a>
                    </li>
                </ul>
            </nav>
        </div>
    </div>
    <div class="banner">
        <div class="mask"></div>
    </div>
    <main>
        <div class="userCard">
            <div class="pictureAndText clearfix">
                <div class="picture">
                    <img src="./img/avatar.jpg" width="299" height="347" alt="头像">
                </div>
                <div class="text">
                    <span class="welcome">Hello
                        <span class="triangle"></span>
                    </span>
                    <h1>靳文杰</h1>
                    <p>前端开发工程师</p>
                    <hr>
                    <dl>
                        <dt>年龄</dt>
                        <dd>21</dd>
                        <dt>所在城市</dt>
                        <dd>西安</dd>
                        <dt>邮箱</dt>
                        <dd>j_861142@163.com</dd>
                        <dt>手机</dt>
                        <dd>15502979297</dd>
                    </dl>
                </div>
            </div>
            <footer class="media">
                <a href="#">
                    <img src="./png/github.png" class="icon" alt="#">
                </a>
                <a href="#">
                    <img src="./png/ins.png" class="icon" alt="#">
                </a>
                <a href="#">
                    <img src="./png/qq.png" class="icon" alt="#">
                </a>
                <a href="#">
                    <img src="./png/weibo.png" class="icon" alt="#">
                </a>
                <a href="#">
                    <img src="./png/weixin.png" class="icon" alt="#">
                </a>
            </footer>
        </div>
        <p class="downloadResume-wrapper">
            <a href="./resume.pdf" class="downloadResume" target="_blank" download>下载 PDF 简历</a>
        </p>
        <p class="selfIntroduction">
            靳文杰，计算机科学与技术1701班，1998年9月，共青团员。<br> 大一学年成绩在专业排名第8名，大二学年成绩在专业排名第1名。
            <br> 荣获2017-2018学年国家励志奖学金、2018-2019学年国家奖学金等。
        </p>
    </main>
    <section class="skills">
        <a name="jineng"></a>
        <h2>技能</h2>
        <ol class="clearfix">
            <li>
                <h3>
                    HTML 5 &amp; CSS 3
                </h3>
                <div class="progressBar">
                    <div class="progress" style="width: 10%;"></div>
                </div>
            </li>
            <li>
                <h3>
                    JavaScript
                </h3>
                <div class="progressBar">
                    <div class="progress" style="width: 40%;"></div>
                </div>
            </li>
            <li>
                <h3>
                    jQuery
                </h3>
                <div class="progressBar">
                    <div class="progress" style="width: 60%;"></div>
                </div>
            </li>
            <li>
                <h3>
                    Vue
                </h3>
                <div class="progressBar">
                    <div class="progress" style="width: 90%;"></div>
                </div>
            </li>
            <li>
                <h3>
                    React
                </h3>
                <div class="progressBar">
                    <div class="progress" style="width: 20%;"></div>
                </div>
            </li>
            <li>
                <h3>
                    HTTP
                </h3>
                <div class="progressBar">
                    <div class="progress" style="width: 40%;"></div>
                </div>
            </li>
        </ol>
    </section>
    <section class="portfolio">
        <a name="zuopin"></a>
        <h2>作品集</h2>
        <nav>
            <ol class="clearfix">
                <li id="portfolio1">所有</li>
                <li id="portfolio2">框架</li>
                <li id="portfolio3">原生 JS &amp; CSS</li>
            </ol>
            <div id="portfolioBar" class="bar state-1">
                <div class="bar-inner"></div>
            </div>
        </nav>
        <script>
            portfolio1.onclick = function () {
                portfolioBar.className = 'bar state-1'
            }
            portfolio2.onclick = function () {
                portfolioBar.className = 'bar state-2'
            }
            portfolio3.onclick = function () {
                portfolioBar.className = 'bar state-3'
            }
        </script>
        <div class="works" style="height: 576px;">
            <div class="big" style="top: 0px; left: 0px;">
                <img src="./jpg/111.JPG" alt="作品1">
            </div>
            <div class="small" style="top: 0px; left: 644px;">
                <img src="./jpg/222.JPG" alt="作品2">
            </div>
            <div class="small" style="top: 298px; left: 644px;">
                <img src="./jpg/333.JPG" alt="作品3">
            </div>
        </div>
    </section>
</body>

</html>
```
#### a.css
```css
body {
    background: #EFEFEF;
    margin: 0;
}

a {
    color: inherit;
    text-decoration: none;
}

* {
    margin: 0;
    padding: 0;
}

hr {
    height: 0;
    border: none;
    border-top: 1px solid #DEDEDE;
}

ul,
ol {
    list-style: none;
}

h1,
h2,
h3,
h4,
h5,
h6 {
    font-weight: normal;
}

.clearfix::after {
    content: '';
    display: block;
    clear: both;
}

.topNavBar nav>ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

.topNavBar {
    /*
    padding-top: 20px;
    padding-bottom: 20px;
    padding-left: 16px;
    padding-right: 16px;
    padding:上 右 下 左
    */
    padding: 20px 0 20px 0;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
}

.topNavBar-inner {
    padding: 0 16px;
}

.topNavBar nav {
    padding-top: 7px;
    padding-bottom: 2.19px;
}

.topNavBar nav>ul>li {
    float: left;
    margin-left: 17px;
    margin-right: 17px;
}

.topNavBar nav>ul>li>a {
    font-size: 12px;
    color: #B7B7B7;
    font-weight: bold;
    border-top: 3px solid transparent;
    border-bottom: 3px solid transparent;
    padding-top: 5px;
    padding-bottom: 5px;
    display: block;
}

.topNavBar nav>ul>li>a:hover {
    border-bottom: 3px solid #e06567;
}

.topNavBar a {
    float: left;
}

.topNavBar nav {
    float: right;
}

.topNavBar .logo {
    font-size: 24px;
    font-family: "Arial Black";
    padding-top: 3px;
    padding-bottom: 4px;
}

.topNavBar .logo .rs {
    margin-right: 4px;
    color: #E6696A;
}

.topNavBar .logo .card {
    color: #9A9DA2;
}

.banner {
    height: 515px;
    background-image: url(./img/rs-cover.jpg);
    background-position: center center;
    background-size: cover;
}

.banner .mask {
    height: 515px;
    background-color: rgba(0, 0, 0, 0.8);
}

.userCard {
    max-width: 940px;
    margin-left: auto;
    margin-right: auto;
    background-color: #FFFFFF;
    box-shadow: 0px 1px 5px 0px rgba(0, 0, 0, 0.5);
}

.userCard .welcome {
    background: #E6686A;
    color: white;
    display: inline-block;
    /*
    width: 70px;
    height: 29px;
    line-height: 29px;
    text-align: center;
    */
    padding: 3.5px 16.5px;
    line-height: 22px;
    position: relative;
    margin-bottom: 10px;
}

.userCard .welcome .triangle {
    display: block;
    border: 10px solid transparent;
    width: 0px;
    border-left-color: #E6686A;
    border-top-width: 0px;
    position: absolute;
    left: 4px;
    top: 100%;
}

.userCard .picture {
    float: left;
}

.userCard .text {
    float: left;
    margin-left: 65px;
    width: 470px;
}

.userCard .text h1 {
    margin-top: 18px;
}

.userCard .text hr {
    margin: 20px 0;
}

.userCard .pictureAndText {
    padding: 50px;
}

.userCard dl dt,
.userCard dl dd {
    float: left;
    padding: 5px 0;
}

.userCard dl dt {
    width: 30%;
    font-weight: bold;
}

.userCard dl dd {
    width: 70%;
    color: #9da0a7;
}

.userCard>footer.media {
    background: #E6686A;
    text-align: center;
}

.userCard>footer.media>a {
    display: inline-block;
    width: 60px;
    line-height: 30px;
    padding: 15px 0;
    border-radius: 50%;
    margin: 8px;
}

.userCard>footer.media>a:hover {
    background: #CF5D5F;
}

.icon {
    width: 30px;
    height: 30px;
    overflow: hidden;
    vertical-align: top;
}

body>main {
    margin-top: -340px;
}

body>main .downloadResume-wrapper {
    text-align: center;
}

body>main .downloadResume {
    font-size: 14px;
    line-height: 16px;
    padding: 21px 55px;
    border: 1px solid #CDCFD1;
    background: #EFEFEF;
    display: inline-block;
    border-radius: 5px;
    color: #3d4451;
    font-weight: bold;
    margin: 32px 0;
    transition: box-shadow 0.2s;
}

body>main .downloadResume:hover {
    box-shadow: 0px 4px 13px 0px rgba(0, 0, 0, 0.2);
}

.selfIntroduction {
    max-width: 940px;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    font-family: cursive;
    line-height: 1.8;
    font-size: 18px;
    font-weight: 900;
}

section.skills,
section.portfolio {
    max-width: 940px;
    margin-left: auto;
    margin-right: auto;
    margin-top: 60px;
}

section.skills>h2,
section.portfolio>h2 {
    text-align: center;
    color: #3d4451;
    font-size: 34px;
    line-height: 1.2;
    font-weight: 600;
}

section.skills h3 {
    font-size: 14px;
    line-height: 1.1;
    padding-right: 40px;
}

section.skills>ol {
    background: white;
    box-shadow: 0px 1px 5px 0px rgba(0, 0, 0, 0.5);
    padding: 42px 50px 0;
    margin-top: 30px;
}

section.skills>ol>li {
    float: left;
    width: 48%;
    box-sizing: border-box;
}

section.skills>ol>li:nth-child(even) {
    float: right;
}

section.skills .progressBar {
    height: 5px;
    background: #fae1e1;
    border-radius: 9px;
    margin: 4px 0 40px;
}

section.skills .progressBar>.progress {
    height: 100%;
    background: #e6686a;
    width: 70%;
    border-radius: 9px;
}

section.portfolio {
    text-align: center;
    margin-bottom: 100px;
}

section.portfolio>nav {
    text-align: center;
}

section.portfolio>nav>ol {
    margin: 0 auto;
    display: inline-block;
    vertical-align: top;
}

section.portfolio>nav>ol>li {
    float: left;
    margin-left: 40px;
    cursor: pointer;
}

section.portfolio>nav>ol>li:nth-child(1) {
    margin-left: 0;
}

section.portfolio>nav {
    display: inline-block;
    vertical-align: top;
    margin-top: 32px;
}

section.portfolio>nav .bar {
    height: 5px;
    background: white;
    margin-top: 5px;
    margin-bottom: 28px;
    border-radius: 9px;
}

section.portfolio>nav .bar-inner {
    height: 100%;
    background: #E6686A;
    width: 10%;
    border-radius: 9px;
    transition: all 0.3s;
}

section.portfolio>nav .bar.state-1 .bar-inner {
    margin-left: 0px;
    width: 33px;
}

section.portfolio>nav .bar.state-2 .bar-inner {
    margin-left: 73px;
    width: 33px;
}

section.portfolio>nav .bar.state-3 .bar-inner {
    margin-left: 143px;
    width: 107px;
}

section.portfolio .works {
    position: relative;
}

section.portfolio .works>.big,
section.portfolio .works>.small {
    position: absolute;
}
```

### csdn link
[Front End - Personal Resume Exercise](https://blog.csdn.net/weixin_42718701/article/details/107618705)
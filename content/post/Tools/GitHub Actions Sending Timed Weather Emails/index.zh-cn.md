---
title: GitHub Actions：定时发送天气邮件
description: GitHub Actions (Sending Timed Weather Emails)
date: '2023-11-28'
categories:
    - Tools
tags:
    - Tools
---

# GitHub Actions：定时发送天气邮件

2019年底的时候，GitHub正式开放了[GitHub Actions](https://github.com/features/actions)这个功能，可以免费使用。

GitHub Actions 是一个 CI/CD（持续集成/持续部署）工具，但也可用作代码运行环境。功能非常强大，能够玩出许多花样。

这里使用GitHub Actions完成一个实例：每天定时运行一次脚本，获取天气预报，发送电子邮件。

完整代码可以从[GitHub](https://github.com/JavenJin/weather-action)仓库获取。

## 获取天气预报

网站[wttr.in](wttr.in)支持使用命令行请求天气预报。

```bash
curl wttr.in
```

上面的命令会返回，当前IP地址的天气。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails1.png)

我们可以在URL中指定城市。

```bash
curl wttr.in/Xian
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails2.png)

返回的数据可以通过`curl`命令的`-o`参数，保存成文件，以便后面发送。

```bash
curl -o result.html wttr.in/Xian
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails3.png)

wttr.in允许定制天气预报的格式和内容，详见[https://github.com/chubin/wttr.in](https://github.com/chubin/wttr.in)，这里就不展开了。最后封装好的脚本[weather.sh](https://github.com/JavenJin/weather-action/blob/main/weather.sh)，完整代码如下：

```bash
#!/bin/sh

set -eux

CITY=Xian
LANGUAGE="zh-CN"
UNIT=m

curl \
  -H "Accept-Language: $LANGUAGE" \
  -o result.html \
  wttr.in/$CITY?format=4\&$UNIT
```

## 配置发送邮件账户

我使用的是网易163邮箱的免费发送服务，也可以使用其他邮箱。

需要首先在网易163邮箱中生成授权码。

1. 登录网易163邮箱（[https://mail.163.com/](https://mail.163.com/)）

2. 点击设置，选择设置POP3/SMTP/IMAP

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails4.png)

3. 点击新增授权密码，保存好该授权密码。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails5.png)

## 配置GitHub Actions

触发GitHub Actions需要在项目仓库新建一个`.github/workflows`子目录，里面是YAML格式配置文件，文件名可以随便取。GitHub只要发现配置文件，就会运行Actions。

配置文件的第一部分是触发条件。

```yaml
name: 'GitHub Action Weather Bot'

on:
  push:
  schedule:
    - cron: '0 0 * * *'
```

上面代码中，`name`字段是配置文件的描述，`on`字段是触发条件。我们指定两种情况下触发，第一种是代码Push进仓库，第二种是定时任务，每天在国际标准时间0点（北京时间早上8点）运行。

接着，就是运行流程。

```yaml
    runs-on: ubuntu-latest
    steps:
      - name: 'Checkout codes'
        uses: actions/checkout@v1
```

上面代码中，运行环境指定为最新版的 Ubuntu。流程的第一步是从代码仓库获取代码。

拿到代码以后，就可以获取天气预报了。

```yaml
      - name: 'Get Weather'
        run: bash ./weather.sh
```

上面代码中，`run`字段就是所要运行的命令。

最后，发送邮件。

```yaml
      - name: 'Send mail'
        uses: dawidd6/action-send-mail@master
        with:
          server_address: smtp.163.com
          server_port: 465
          username: ${{ secrets.MAIL_USERNAME }}
          password: ${{ secrets.MAIL_PASSWORD }}
          subject: Xian Weather Report (${{env.REPORT_DATE}})
          body: file://result.html
          to: ${{ secrets.TO_EMAIL_ADDRESS }}
          from: GitHub Actions
          content_type: text/html
```

上面代码中，发送邮件使用的是一个已经写好的action，只要配几个参数就可以用。参数之中，邮件SMTP服务器的用户名和密码，使用的是加密变量，需要在项目的`settings/secrets`菜单里面设置。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails6.png)

[完整的配置文件](https://github.com/JavenJin/weather-action/blob/main/.github/workflows/weather.yml)如下：

```yaml
name: 'GitHub Action Weather Bot'

on:
  push:
  schedule:
    - cron: '0 0 * * *'

jobs:
  bot:
    runs-on: ubuntu-latest
    steps:
      - name: 'Checkout codes'
        uses: actions/checkout@v1
      - name: 'Get Weather'
        run: bash ./weather.sh
      - name: 'Get Date'
        run: echo "REPORT_DATE=$(TZ=':Asia/Xian' date '+%Y-%m-%d %T')" >> $GITHUB_ENV
      - name: 'Send mail'
        uses: dawidd6/action-send-mail@master
        with:
          server_address: smtp.163.com
          server_port: 465
          username: ${{ secrets.MAIL_USERNAME }}
          password: ${{ secrets.MAIL_PASSWORD }}
          subject: Xian Weather Report (${{env.REPORT_DATE}})
          body: file://result.html
          to: ${{ secrets.TO_EMAIL_ADDRESS }}
          from: GitHub Actions
          content_type: text/html
```

写好配置，推送到仓库以后，就可以每天清早收到一封天气预报邮件了。在这个基础上不难扩展，可以定时执行各种脚本（比如每5分钟检查一次某个网站是否在线），然后将结果发到指定的渠道等等。

## 成功发送

配置成功后，每天固定时间都会接收到当天的天气邮件。

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails7.png)
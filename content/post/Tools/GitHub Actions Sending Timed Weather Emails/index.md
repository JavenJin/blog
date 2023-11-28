---
title: GitHub Actions (Sending Timed Weather Emails)
description: GitHub Actions：定时发送天气邮件
date: '2023-11-28'
categories:
    - Tools
tags:
    - Tools
---

# GitHub Actions: Sending Timed Weather Emails

Toward the end of 2019, GitHub officially opened up [GitHub Actions](https://github.com/features/actions), a feature that can be used for free.

GitHub Actions is a CI/CD (Continuous Integration/Continuous Deployment) tool, but it can also be used as a code runtime environment. It's very powerful and can do a lot of tricks.

Here's an example of what you can do with GitHub Actions: run a script once a day to get the weather forecast and send an email.

The full code is available from the [GitHub](https://github.com/JavenJin/weather-action) repository.

## Get the weather forecast

The website [wttr.in](wttr.in) supports requesting weather forecasts using the command line.

```bash
curl wttr.in
```

The above command will return, the weather for the current IP address.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails1.png)

We can specify the city in the URL.

```bash
curl wttr.in/Xian
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails2.png)

The returned data can be saved to a file to be sent later, using the `-o` parameter of the `curl` command.

```bash
curl -o result.html wttr.in/Xian
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails3.png)

wttr.in allows customization of the format and content of the weather forecast, as detailed in [https://github.com/chubin/wttr.in](https://github.com/chubin/wttr.in), which will not be expanded upon here. The final encapsulated script [weather.sh](https://github.com/JavenJin/weather-action/blob/main/weather.sh), complete with code, is as follows:

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

## Configuring an Outgoing Mail Account

I use the free sending service of NetEase 163 mailbox, or you can use other mailboxes.

You need to first generate an authorization code in your Netflix 163 email.

1. Login to Netease 163 mailbox（[https://mail.163.com/](https://mail.163.com/)）

2. Click on Settings and choose to set POP3/SMTP/IMAP

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails4.png)

3. Click Add Authorization Password to save that authorization password

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails5.png)

## Configuring GitHub Actions

Triggering GitHub Actions requires that you create a new `.github/workflows` subdirectory in your project repository with a YAML-formatted configuration file with any filename you want.GitHub will run the Actions as soon as it finds the configuration file.

The first part of the configuration file is the trigger condition.

```yaml
name: 'GitHub Action Weather Bot'

on:
  push:
  schedule:
    - cron: '0 0 * * *'
```

In the above code, the `name` field is the description of the configuration file and the `on` field is the trigger condition. We specify two conditions for triggering, the first is code Push into the repository, the second is a timed task that runs every day at 0:00 international standard time (8:00 am Beijing time).

Next, there is the running process.

```yaml
    runs-on: ubuntu-latest
    steps:
      - name: 'Checkout codes'
        uses: actions/checkout@v1
```

In the above code, the runtime environment is specified to be the latest version of Ubuntu. the first step in the process is to get the code from the code repository.

Once you have the code, you can get the weather forecast.

```yaml
      - name: 'Get Weather'
        run: bash ./weather.sh
```

In the above code, the `run` field is the command to be run.

Finally, send an email.

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

In the above code, the email is sent using an action that has already been written and can be used with just a few parameters. Among the parameters, the username and password of the mail SMTP server are encrypted variables, which need to be set in the `settings/secrets` menu of the project.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails6.png)

The [complete configuration file](https://github.com/JavenJin/weather-action/blob/main/.github/workflows/weather.yml) is below:

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

After writing the configuration and pushing it to the repository, you can receive a weather forecast email early in the morning every day. It's not hard to expand on this by executing various scripts at regular intervals (e.g., checking whether a site is online every 5 minutes) and then sending the results to a specified channel, etc.

## Successfully sent

After successful configuration, you will receive the day's weather email at a fixed time every day.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails/GitHub%20Actions%20Sending%20Timed%20Weather%20Emails7.png)
---
title: 使用 Cloudflare 部署 edgetunnel 免费节点（永久可用 + 免费域名）
description: Deploy an edgetunnel free node with Cloudflare (permanent availability + free domain)
date: '2026-06-04'
slug: deploy-edgetunnel-free-node-with-cloudflare
categories:
    - Tools
tags:
    - Tools
---

# 使用 Cloudflare 部署 edgetunnel 免费节点（永久可用 + 免费域名）

如果你需要“长期可用”的免费节点方案，那么使用这套基于 Cloudflare 的搭建方式是你的不二选择。

它最大的特点只有三个：免费、稳定、速度极快！不需要服务器、不需要额外成本，甚至连域名都可以免费获取；整个搭建过程从零开始，大约 10 分钟就能完成。同时，由于依托 Cloudflare 本身的网络基础，这套方案在稳定性和可用性方面，也远远优于传统的临时节点或不稳定方案。

相比过去那些复杂、容易失效、需要频繁维护的方式，这种方案更像是一种“轻量级长期解决方案”：一次搭建，持续可用，几乎不需要额外折腾，非常适合个人用户或轻度使用场景。

## 域名注册

注册一个永久免费的域名。

访问这个链接：[https://www.dnshe.com/](https://my.dnshe.com/aff.php?aff=180471)

![](images/image01.png)

选择右上角的 `Sign Up`。

![](images/image02.png)

填写所有信息，点击立即注册。

注册成功后进入免费域名。

![](images/image03.png)

使用 GitHub 进行验证。

验证完成后选择注册新域名，填写信息，点击确认注册。

![](images/image04.png)

注册后保留该网页不要关闭。

## 注册并登录 Cloudflare 平台

注册并登录 Cloudflare 平台。

访问这个链接：[https://www.cloudflare.com/](https://www.cloudflare.com/)

![](images/image05.png)

选择 `Login`，然后点击 `Sign up`，输入 `Email` 和 `Password` 信息后点击 `Sign up`。

![](images/image06.png)

点 `Skip` 跳过前面的步骤即可。

## 在 Cloudflare 平台托管域名

登录后，选择左边的 `Domains`，点击右上方的 `Add domain`。

![](images/image07.png)

选择 `Connect a domain`。

![](images/image08.png)

输入第一步注册的域名，点击 `Continue`。

![](images/image09.png)

选择 `Free Plan`。

![](images/image10.png)

直接点击 `Continue to activation`，然后 `Confirm`。

![](images/image11.png)

将下面的两个地址，填写到域名注册网站的 `DNS服务器` 配置上，然后点击 `保存设置`。

![](images/image12.png)

![](images/image13.png)

保存成功后在 `Cloudflare` 站点上点击 `I updated my nameservers`。

![](images/image14.png)

## 部署 edgetunnel 程序到 Cloudflare 站点

点击 [edgetunnel-main.zip](https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip) 下载由 [CMliu](https://github.com/cmliu/edgetunnel) 开源的程序备用。

进入 `Workers & Pages` 页面，选择 `Create application`，这一步可能需要验证邮箱，验证即可。

![](images/image15.png)

选择 `Pages`，点击 `Get started`。

![](images/image16.png)

选择 `Drag and drop your files`。

![](images/image17.png)

设置项目名称，并点击 `Create project`。

![](images/image18.png)

上传开始下载的 [edgetunnel-main.zip](https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip) 文件。

![](images/image19.png)

上传完成后点击 `Deploy site`。

![](images/image20.png)

成功后点击 `Continue to project`。

![](images/image21.png)

然后进入到项目后，选择 `Settings`，然后选择 `Variables and Secrets`，点击 `Add` 来添加一个变量。

![](images/image22.png)

类型选择 `Text`，变量名为 `ADMIN`，`Value` 为登录密码，建议设置复杂，完成后点 `Save`。

![](images/image23.png)

再点击 `Storage & databases`，选择 `Workers KV`，点击右上角的 `Create Instance`。

![](images/image24.png)

设置 `KV` 空间名称后点击 `Create`。

![](images/image25.png)

返回项目设置页面（在 `Compute` 下的 `Workers & Pages` 里找）。然后选择 `Bindings`，点击 `Add`。

![](images/image26.png)

选择 `KV` 命名空间。

![](images/image27.png)

变量名称添加 `KV`，选择刚才创建的命名空间后点 `Save`。

![](images/image28.png)

再次点击右上角的 `Create deployment`。

![](images/image29.png)

再次上传文件后点击 `Save and deploy`。

![](images/image30.png)

至此，部署完成。

![](images/image31.png)

访问显示的站点会显示 `nginx`。

![](images/image32.png)

需要在地址后面加上 `admin` 即可访问，输入设置的管理员密码。

![](images/image33.png)

复制订阅信息即可使用。

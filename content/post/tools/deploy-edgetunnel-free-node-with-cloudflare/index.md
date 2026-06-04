---
title: Deploy an edgetunnel Free Node with Cloudflare (Permanent Availability + Free Domain)
description: 使用 Cloudflare 部署 edgetunnel 免费节点（永久可用 + 免费域名）
date: '2026-06-04'
slug: deploy-edgetunnel-free-node-with-cloudflare
categories:
    - Tools
tags:
    - Tools
---

# Deploy an edgetunnel Free Node with Cloudflare (Permanent Availability + Free Domain)

If you need a free node solution that can stay available for the long term, this Cloudflare-based setup is a great choice.

Its biggest advantages are simple: it is free, stable, and fast. You do not need to rent a server, pay extra costs, or even buy a domain name. The whole setup can be completed from scratch in about 10 minutes. Because it is built on Cloudflare's network infrastructure, this solution is also much more stable and reliable than temporary or unstable node setups.

Compared with older methods that are complicated, easy to break, and require frequent maintenance, this approach feels more like a lightweight long-term solution: set it up once, keep using it, and avoid most of the extra maintenance work. It is especially suitable for personal users and light usage scenarios.

## Register a Domain

Register a permanently free domain name.

Open this link: [https://www.dnshe.com/](https://my.dnshe.com/aff.php?aff=180471)

![](images/image01.png)

Select `Sign Up` in the upper-right corner.

![](images/image02.png)

Fill in all the required information, then click the registration button.

After registration succeeds, go to the free domain section.

![](images/image03.png)

Use GitHub to complete the verification.

After verification is complete, choose to register a new domain, fill in the required information, and confirm the registration.

![](images/image04.png)

After the domain is registered, keep this page open.

## Register and Log In to Cloudflare

Register and log in to the Cloudflare platform.

Open this link: [https://www.cloudflare.com/](https://www.cloudflare.com/)

![](images/image05.png)

Select `Login`, then click `Sign up`. Enter your `Email` and `Password`, then click `Sign up`.

![](images/image06.png)

Click `Skip` to skip the initial setup steps.

## Host the Domain on Cloudflare

After logging in, select `Domains` on the left, then click `Add domain` in the upper-right corner.

![](images/image07.png)

Select `Connect a domain`.

![](images/image08.png)

Enter the domain name registered in the first step, then click `Continue`.

![](images/image09.png)

Select the `Free Plan`.

![](images/image10.png)

Click `Continue to activation`, then click `Confirm`.

![](images/image11.png)

Copy the two nameserver addresses shown by Cloudflare, paste them into the `DNS服务器` configuration on the domain registration website, then click `保存设置`.

![](images/image12.png)

![](images/image13.png)

After saving the settings successfully, return to Cloudflare and click `I updated my nameservers`.

![](images/image14.png)

## Deploy edgetunnel to Cloudflare

Click [edgetunnel-main.zip](https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip) to download the open-source project by [CMliu](https://github.com/cmliu/edgetunnel).

Go to `Workers & Pages`, then select `Create application`. Cloudflare may ask you to verify your email at this step; complete the verification if prompted.

![](images/image15.png)

Select `Pages`, then click `Get started`.

![](images/image16.png)

Select `Drag and drop your files`.

![](images/image17.png)

Set a project name, then click `Create project`.

![](images/image18.png)

Upload the [edgetunnel-main.zip](https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip) file downloaded earlier.

![](images/image19.png)

After the upload completes, click `Deploy site`.

![](images/image20.png)

After deployment succeeds, click `Continue to project`.

![](images/image21.png)

After entering the project, open `Settings`, select `Variables and Secrets`, and click `Add` to add a variable.

![](images/image22.png)

Set the type to `Text`. Set the variable name to `ADMIN`, and set `Value` to your login password. It is recommended to use a strong password. Click `Save` when finished.

![](images/image23.png)

Next, click `Storage & databases`, select `Workers KV`, and click `Create Instance` in the upper-right corner.

![](images/image24.png)

Enter a name for the `KV` namespace, then click `Create`.

![](images/image25.png)

Return to the project settings page. You can find it under `Compute` -> `Workers & Pages`. Select `Bindings`, then click `Add`.

![](images/image26.png)

Select the `KV` namespace.

![](images/image27.png)

Set the variable name to `KV`, select the namespace you just created, then click `Save`.

![](images/image28.png)

Click `Create deployment` again in the upper-right corner.

![](images/image29.png)

Upload the file again, then click `Save and deploy`.

![](images/image30.png)

At this point, the deployment is complete.

![](images/image31.png)

When you visit the displayed site, it will show `nginx`.

![](images/image32.png)

Append `admin` to the URL to open the admin page, then enter the administrator password you configured earlier.

![](images/image33.png)

Copy the subscription information and use it as needed.

---
title: 完美解决无Internet但能正常上网的问题（转载整合）
tags: Computer Internet
categories:
  - study
  - Internet
toc: true
abbrlink: 42651546
date: 2025-08-10 00:00:00
comment: 'valine'
---

2025.8.10有效
今日打开电脑发现电脑显示无法访问到Internet，ipv6和ipv4全部无网络，以太网显示无法连接到网络
但是依旧可以上网

<!--more-->

上网搜发现是个老生常谈的问题，最后靠的是[这篇文章-来自b站](https://www.bilibili.com/opus/370927441707295830)解决

文章不够全面，我结合了评论区几个才搞好，总结一下。

## 方法

注册表打开`\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NlaSvc\Parameters\Internet`
有问题的注册表长这样：

![有问题的注册表](42651546/1.png)

修改后的注册表：

![修改后的注册表](42651546/2.png)

> 注：与原文章相比多修改了一个CaptivePortalTimer（从0到1）
> 来自@布熹瘦在下方的评论
> ![评论](42651546/3.png)

还没完，我重启之后依旧失效，继续修改

根据@御石同行的评论，修改`\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityStatusIndicator`下noactiveprobe的值，从1改为0
![评论](42651546/5.png)

修改后长这样：
![修改后](42651546/4.png)

重启后正常

## 原因

总结：微软通过向一个服务器发送请求来检验你是否联网，更新后换了一个服务器，但由于国内运营商重定向所以失败了，出现可以上网但显示无Internet的情况。

如果大家也出现以上状况，尤其是**win10 18362（即1903）版以后的新版本**，则取消上网验证通常不能解决问题。

原因分析：经注册表选项比对，发现问题出在连网返回值功能有了变化。原理是每当**连网后，系统会自动向微软的dns.msftncsi.com发出请求，然后返回一个NCSI.txt的值**，这一值如果正确时，则确认为已连网。而Win10最近的版本中，这个返回服务器和值有了新变化并反映为6个注册表项中。**这些变化因国内部分运行商的网络重定向，不能得到正确的反馈，因此出现实际能上网却显示为无internet的问题。**

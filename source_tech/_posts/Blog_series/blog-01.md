---
title: 零基础搭建个人博客（壹）
tags:
  - Computer Network
  - blog
categories: 
- study
- blog-building
category_bar: true
toc: true
comment: 'valine'
abbrlink: 9828
date: 2023-09-29 19:51:05
---

# 前言

> 学习做一个博客网站并不需要很多程序知识，更多的是一颗敢做敢坚持的心
<!--more-->
但是必要的基础知识还是必要的，假如你已经是对Github、HTML有所了解的老油条，请直接跳转至下一章。
o(〃＾▽＾〃)o

- 原理
GitHub是世界上最大的代码托管平台，通过将网页代码放在github上访问就可以实现一个简单且免费的博客网站。虽说如此，因Github的服务器架设在国外，导致访问速度可谓出名的慢。对于这些问题，我们会在后续尽力优化，而现在，我们最有效的方式便是——

**等吧。**

（最好不要晚上搞，别问我为什么）

# 注册登录Github账号

打开官网：[GITHUB官网](https://github.com "GITHUB官网")
点击右上角“sign in”注册
动画很牛逼，但是不用管，输入邮箱再设定密码
{% asset_img /9828/1.png 注册 %}
接下来输入昵称，回答是否要收产品更新的邮件，再输入奇奇怪怪的机器人验证。。。输入邮箱的验证码后，账户便创建成功了。
Github这时会问你团队的信息，但是怎么回答都无所谓，最后Github询问你是否参与付费服务，GitHub 的仓库分为两种，一种是公开免费版，一种是私有付费版。其中，免费版完全公开的，而私有版一般是由企业或者不愿公开仓库的个人用户购买。在这里选择Free即可。
{% asset_img 2.png 反正选免费 %}
注册与登陆的过程并不难，凭借一些网上冲浪的经验以及翻译器应该可以轻轻松松完成的啦。

# 创建Github库

*(是的图片被吞掉了，很简单不懂还是看看百度吧)*
前头就提到库这东西了，其实说白了他就是储存你的程序文件的地方。英文叫repository，在主页找到repositories选项卡：
<!-- ![repositories](https://blog.windeling.com/202309295207cddc/image-20230930111610185.png "找到repositories单词即可") -->
找到那个绿油油的new按钮进行创建，进入创建仓库的页面
在这个页面按着英文提示 *（请自行使用翻译器）*填入仓库名、仓库描述，**勾选Add a README file**，其他的设置保留原样即可，点击Create。终于，你有了你的第一个项目！
接下来，你将安装创建博客最重要的软件——Git，并将其与你的Github链接以上传文件。再接再厉哟！

<a href="https://blog.windeling.com/202309295207cddc/" class="linking" target="_self">➢下一站：零基础搭建个人博客（贰） | Windeling</a>
<style>
    .linking{
        color: rgb(4, 45, 92);;
    }
    .linking:hover{
        color: rgb(4, 33, 66);
    }
</style>

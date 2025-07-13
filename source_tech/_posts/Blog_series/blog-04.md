---
title: 零基础搭建个人博客（肆）
tags:
  - Computer Network
  - blog
categories: 
- study
- blog-building
category_bar: true
toc: true
comment: 'valine'
abbrlink: 10453
date: 2023-09-30 10:15:05
---
话说上回咱选好了域名（我这个穷B必定是跳过的啦），这篇就来教大家提交库并搭建起基本的网页框架！！
<!--more-->
# 安装并配置Node.js

## 安装Node.js

Node.js® 是一个开源、跨平台的JavaScript运行时的环境。
对于安装，干了好几次了应该会了吧。。。
先打开官网：[Node.js官网](https://nodejs.org/zh-cn "Node.js官网")
将一个msi文件下载下来，点击安装，一路照着翻译即可安装成功。详细过程参见[这里](https://blog.csdn.net/antma/article/details/86104068 "点喂")
安装后可以打开cmd检验是否成功，用以下命令检查文本：
`node -v`
`npm -v`

<!-- {% asset_img 4.png 检查 %} -->
![检查](10453/4.png "检查")

出现版本号即为安装成功。

## 设置npm安装路径

我们将用npm命令安装模块，但是由于它的默认安装路径在C盘，可能会导致C盘遭占用甚至影响hexo使用，于是我们更改一下安装路径。
打开之前安装node.js的文件夹，新建node_cache、node_global两个空的文件夹
![新建俩文件夹](10453/5.png "新建")
创建后打开cmd输入命令更改路径
`npm config set prefix "I:\node\node_global"`
`npm config set cache "I:\node\node_cache"`
**其中I:\node是你安装node的位置**，具体可以打开刚刚创建的node_cache、node_global文件夹，直接使用它的位置即可。
![自个找文件夹看去](10453/6.png "文件夹路径")

## 配置npm环境变量

这还不够，得为它配置一个环境变量。
什么？你问我环境变量是啥？
其实就是软件在这个环境运行所需的配置，但这不重要。
以win10系统为例，打开**设置 → 系统 → 关于 → 高级系统设置 → 环境变量**
![环境变量就搁这下面我还看半天没找到](10453/7.png "找到环境变量")
新建一个环境变量，变量名为“NODE_PATH”，值为“I:\node\node_global\node_modules” **（你刚刚新建的文件夹node_global里的node_modules）**
![新建，虽然我已经建好了](10453/8.png "新建环境变量")
再编辑用户变量的path，将npm的路径改为I:\node\node_global **（就是你刚刚新建的文件夹node_global的位置）**
![更改，虽然我已经改好了（这里好像有些人有问题那就自己问度娘吧](10453/9.png "Path更改")
确定保存即可。

## 测试

在 cmd 命令下执行`npm install webpack -g`
有Warn不要紧，打开刚刚的node_global里的node_modules文件夹，发现出现了webpack便顺利配置完成(～￣▽￣)～
当然，出现超时等错误就换个时段吧，Github嘛，你懂的。

# 安装hexo

hexo就是我们网站的框架啦，安装前我们先在Github上新建一个仓库作为网站储存位置。

## 新建网站仓库

新建仓库在第一章讲过，此处不再赘述。
![看到加号还不懂啥意思吗](10453/10.png "建仓库")
仓库名称叫“你的用户名.github.io”，勾选README file
创建后选择Settings，滑到底端能看见Github Pages即可。

## 安装hexo

温馨提示：此部分坑多，请配合度娘食用( ‵▽′)ψ

首先，在你的一个盘上新建文件夹blog，打开它，复制文件夹的路径
以**管理员身份**打开cmd，输入`cd /D I:\Blog`(I:\Blog就是文件夹路径)定位到博客文件夹。
![/D不要忘记加啊啊啊啊啊啊别问我为啥](10453/11.png "定位文件夹")
输入以下npm命令安装Hexo。
`npm install -g hexo-cli`
安装完成后，输入`hexo init`命令初始化博客,
然后输入`hexo g`静态部署，在闪过一堆INFO、create的命令后，网页框架就已经部署到了本地，输入`hexo s`命令，再在浏览器输入[http://localhost:4000](http://localhost:4000 "本地查看")就可以查看长什么样。
![乌漆嘛黑的宇宙和大大的hexo以及老生常谈的helloworld](https://pic3.zhimg.com/80/v2-5a8d3a94b1eb5e4e79f2e733ddaed2aa_720w.webp "部署的网页就长这样")
看完按ctrl+C停止吧

## 把hexo部署到Github

网站网站，总得在网上吧。现在就把hexo与Github给它关联上，这样就能让别人也访问了。
现在回到我们的blog文件夹，用笔记本打开 **_config.yml** 文件（当然也可以用VScode一类软件）
在文件底部添加：

```yml
deploy:
  type: git
  repository: git@github.com:BoredLiam/BoredLiam.github.io.git  #你的仓库地址，位置参见下文
  branch: main
```

注意：
①type&repository&branch的冒号后必须带上空格！
②有一些教程的branch写的是master，这是Github过去的默认分支，请改为main
③有些教程仓库地址是`repository: https://github.com/XXX/XXX.github.io.git`，但由于2021年8月之后不支持https访问仓库了，只能ssh，因此请以`repository: git@github.com:XXX/XXX.github.io.git`的形式，其中XXX是你的Github用户名

接下来在刚刚的cmd上输入`npm install hexo-deployer-git --save`
Warn什么的不理他，接下来再依次输入三条命令

```hexo
hexo clean   #清除缓存文件 db.json 和已生成的静态文件 public
hexo g       #生成网站静态文件到默认设置的 public 文件夹(hexo generate 的缩写)
hexo d       #自动生成网站静态文件，并部署到设定的仓库(hexo deploy 的缩写)
```

*（这个命令后面还得用，还可以用`hexo g -f -d`代替）*

完成以后，打开浏览器，输入 <https://xxx.github.io> 就可以打开你的网页了，但这空空如也的网站还待你来添加都属于你的内容。虽说不会网页设计，但是我们有前车之鉴啊！「主题」就是前人们的网页模板，有了它，网页就可以迅速变得成熟啦~
下面我们就来介绍如何添加主题！
<a href="https://blog.windeling.com/2023093017f4661a/" class="linking" target="_self">➢下一站：零基础搭建个人博客（伍） | Windeling</a>
<style>
    .linking{
        color: rgb(4, 45, 92);;
    }
    .linking:hover{
        color: rgb(4, 33, 66);
    }
</style>
{% asset_img a.jpg 提示文字 %}
嗨呀终于写完了累死我咯~_~
有什么问题欢迎评论留言呀~~~
> 我去你的图床全崩完了我放个p的图片
> ——2024.1.31
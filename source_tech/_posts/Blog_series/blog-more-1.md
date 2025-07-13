---
title: yilia博客中“下一页”的美化
tags:
  - Computer Network
  - blog
categories: 
- study
- blog-building
category_bar: true
toc: false
abbrlink: 15695
date: 2024-02-06 22:45:11
comment: 'valine'
---
> 失踪人口找回
> （我真的不知道怎么形容这个标题）

默认的yilia博客主题中，切换页数的按钮显示的是`Next &raquo;`和`&laquo; Prev`，这看起来非常让人不爽
所以我们尝试给他变得好看一点(●'◡'●)
<!-- more -->

## step1 “上一页”“下一页”

我们先打开`\themes\yilia\layout\_partial\archive.ejs`，更改以下内容为“上一页”“下一页”
{% asset_img 1.png 大约8-9行处 %}
（或者你搜索`Next &raquo;`和`&laquo; Prev`也可以）
{% asset_img 2.png 大约36-37行处 %}
接着你会发现在首页与尾页的“下一页”“上一页”都不会消失（加载完成后），令人气愤
改！

## step2 修修bug

我们打开`\themes\yilia\layout\_partial\script.ejs`
> 代码没有格式化估计会有点乱，如果你跟我一样有强迫症的话可以全篇复制到[这个网站](https://tool.chinaz.com/tools/jsformat.aspx)来格式化

`ctrl+F`搜索next或prev
{% asset_img 3.png <a>标签里的内容应该是Next &raquo;，但是我删掉了 %}
这`<a 什么=啊吧啊吧></a>`中间里的内容可能有点不一样，因为我删掉了，你看着前后差不多就行
{% asset_img 4.png <a>标签里的内容应该是&laquo; Prev，但是被我删掉了 %}
直接把`<a 什么=啊吧啊吧></a>`删除即可
（注：只删标签中间的`Next &raquo;`和`&laquo; Prev`也可以，但是会对后面Step3操作有影响）
好的，问题解决了，长这样
{% asset_img 5.png 差不多吧 %}
不过这个下一页跟页码按钮风格不统一，令人恼羞成怒
改！

## step3 变好看点

我们打开`\themes\yilia\source\main.0cf68a.css`
`crtl+F`搜索`#page-nav .extend`，
{% asset_img 6.png 看到没有，删掉它 %}
我们选中并`ctrl+/`注释掉，在后面加上以下代码：

```css
#page-nav .extend{
  width: 50px;/* 注：这里的宽度比较适应“下一页”三个字，假如你想要更多的字符将数字改大即可 */
  height: 25px;
  background: #4d4d4d;
  display: inline-block;
  color: #fff;
  line-height: 25px;
  font-size: 12px;
  margin: 0 5px 30px;
  border-radius: 2px
}

#page-nav .extend:hover {
  background: #5e5e5e
}
```

保存，并把它`hexo g -f -d`推送到仓库
效果如下：
{% asset_img 7.png 好看多了 %}
{% asset_img 8.png 好看多了*2 %}

收工睡觉！

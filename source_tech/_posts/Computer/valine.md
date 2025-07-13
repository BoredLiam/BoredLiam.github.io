---
title: 在Valine 1.5.1版本实现QQ邮箱识别生成头像地址
tags:
  - Computer Network
  - blog
categories:
  - study
  - blog-building
toc: true
hidden: false
abbrlink: 24506
date: 2024-07-11 00:00:00
comment: 'valine'
---
代码原作者：[cungudafa（CSDN）](https://cungudafa.blog.csdn.net/)，Valine 1.2.10至1.4.4的更改办法见[原文](https://blog.csdn.net/cungudafa/article/details/104638730)

## 问题

在升级为Valine1.5.1后，再按文章中方法，在Valine.min.js中加入代码时，出现了评论无法加载的问题（评论区内只显示`{}`）
原代码：
```js
var qq_img = E.cdn+(0,s.default)(t.get("mail"))+E.params;
if (t.get("mail").indexOf("@qq.com") >= 0) {
	var prefix = t.get("mail").replace(/@.*/, "");//前缀
	var pattern = /^\d+$/g;  //正则表达式
	var result = prefix.match(pattern);//match 是匹配的意思
	if (result !== null) {
		qq_img = "//q1.qlogo.cn/g?b=qq&nk=" + prefix + "&s=100";
	}
}
```

<!-- more -->

## 原因

在1.5.1版本的Valine.min.js中的这段代码<sub>（代码框下有滑动条，别改怪我没告诉你）</sub>
```js
f = $.hide ? "" : e.cfg.enableQQ && t.get("QQAvatar") ? (0, C.default)('<img class="vimg" src="' + j(t.get("QQAvatar")) + '" referrerPolicy="no-referrer"/>') : '<img class="vimg" src="' + (E.cdn+(0,s.default)(n.get("mail"))+E.params;) + $.params) + '">',
```
其中`src=`中间部分在更新时
由`E.cdn+(0,s.default)(n.get("mail"))+E.params;`
更改为`$.cdn + (0, u.default)(t.get("mail")) + $.params`，
将代码首句更改为`var qq_img = $.cdn + (0, u.default)(t.get("mail")) + $.params`即可
更改后代码：
```js
var qq_img = $.cdn + (0, u.default)(t.get("mail")) + $.params
    if (t.get("mail").indexOf("@qq.com") >= 0) {
        var prefix = t.get("mail").replace(/@.*/, "");
        var pattern = /^\d+$/g;  //正则表达式
        var result = prefix.match(pattern);`	`
        if (result !== null) {
            qq_img = "//q2.qlogo.cn/g?b=qq&nk=" + prefix + "&s=100";
        }
    }
```
其他方法都与原来相同

## 拓展

假如使用了[Valine博主标签](https://blog.hclonely.com/posts/409d3090/)的修改版Valine.min.js，代码结构会稍有不同

首先还是在Valine.min.js直接搜索`vimg`，找到这段代码
```js
u = (V.hide ? "" : s.cfg.enableQQ && e.get("QQAvatar") ? (0, U.default)('<img class="vimg" src="' + (y(e.get("QQAvatar"))) + '" referrerPolicy="no-referrer"/>') : '<img class="vimg" src="' + (V.cdn + (0, j.default)(e.get("mail")) + V.params) + '">') + '<div class="vh"><div class="vhead">' + a + " " + i + '</div><div class="vmeta"><span class="vtime" >' + (0, R.default)(e.get("insertedAt"), s.i18n) + '</span><span class="vat" data-vm-id="' + (e.get("rid") || e.id) + '" data-self-id="' + e.id + '">' + s.i18n.t("reply") + '</span></div><div class="vcontent" data-expand="' + s.i18n.t("expand") + '">' + (0, N.default)(e.get("comment")) + '</div><div class="vreply-wrapper" data-self-id="' + e.id + '"></div><div class="vquote" data-self-id="' + e.id + '"></div></div>',
```
将本段第二个vimg后的
```js
'<img class="vimg" src="' + (V.cdn + (0, j.default)(e.get("mail")) + V.params) + '">'
```
更改为
```js
'<img class="vimg" src="' + (QQ_img) + '">'
```
同时将原来插入的代码更改为<sub>（不止第一句有更改哦）</sub>
```js
var QQ_img = V.cdn + (0, j.default)(e.get("mail")) + V.params
    if (e.get("mail").indexOf("@qq.com") >= 0) {
        var prefix = e.get("mail").replace(/@.*/, "");
        var pattern = /^\d+$/g; 
        var result = prefix.match(pattern);`    `
        if (result !== null) {
            QQ_img = "//q2.qlogo.cn/g?b=qq&nk=" + prefix + "&s=100";
        }
    }
```
接着找到这段代码（搜索`((0, j.default)(e.get("mail")))),`）
```js
b = function(e, t, n) {
                    var r = (0, L.default)('<div class="vcard" id="' + e.id + '"></div>'),
                        o = (0, U.default)(e.get("ua")),
                        i = "",
                        o = (o && !/ja/.test(s.cfg.lang) && (i = (o = L.default.detect(o)).version ? o.os ? '<span class="vsys"><i class="browser-icon fab fa-' + (["xiaomi"].includes(o.browser.toLowerCase()) ? "mobile-alt fas" : o.browser.toLowerCase()) + '"></i>' + o.browser + " " + o.version + '</span> <span class="vsys"><i class="os-icon fab fa-' + (["mac os", "ios"].includes(o.os.toLowerCase()) ? "apple" : o.os.toLowerCase()) + '"></i>' + o.os + " " + o.osVersion + "</span>" : "" : '<span class="vsys">' + o.browser + "</span>"), "*" === s.cfg.path && (i = '<a href="' + e.get("url") + '" class="vsys">' + e.get("url") + "</a>"), s.cfg.master.includes((0, j.default)(e.get("mail")))),
```
将最后一句`s.cfg.master.includes((0, j.default)(e.get("mail")))),`最后的逗号改为分号，并在其后换行，将代码分为上下两部分
紧接着把后面部分的
```js
a = s.cfg.friends.includes((0, j.default)(e.get("mail").toLowerCase())),
```
前加上`var`，即为
```js
var a = s.cfg.friends.includes((0, j.default)(e.get("mail").toLowerCase())),
```
最后将插入的代码粘贴在刚刚换行的位置，即分开的两段之间
最终代码长这样：
```js
b = function(e, t, n) {
    var r = (0, L.default)('<div class="vcard" id="' + e.id + '"></div>'),
        o = (0, U.default)(e.get("ua")),
        i = "",
        o = (o && !/ja/.test(s.cfg.lang) && (i = (o = L.default.detect(o)).version ? o.os ? '<span class="vsys"><i class="browser-icon fab fa-' + (["xiaomi"].includes(o.browser.toLowerCase()) ? "mobile-alt fas" : o.browser.toLowerCase()) + '"></i>' + o.browser + " " + o.version + '</span> <span class="vsys"><i class="os-icon fab fa-' + (["mac os", "ios"].includes(o.os.toLowerCase()) ? "apple" : o.os.toLowerCase()) + '"></i>' + o.os + " " + o.osVersion + "</span>" : "" : '<span class="vsys">' + o.browser + "</span>"), "*" === s.cfg.path && (i = '<a href="' + e.get("url") + '" class="vsys">' + e.get("url") + "</a>"), s.cfg.master.includes((0, j.default)(e.get("mail"))));
        // 拉取qq
    var QQ_img = V.cdn + (0, j.default)(e.get("mail")) + V.params
        if (e.get("mail").indexOf("@qq.com") >= 0) {
            var prefix = e.get("mail").replace(/@.*/, "");
            var pattern = /^\d+$/g; 
            var result = prefix.match(pattern);`    `
            if (result !== null) {
                QQ_img = "//q2.qlogo.cn/g?b=qq&nk=" + prefix + "&s=100";
            }
        }
        // end
    var a = s.cfg.friends.includes((0, j.default)(e.get("mail").toLowerCase())),
    ...
}
```

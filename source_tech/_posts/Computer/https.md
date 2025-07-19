---
title: 解决yilia和fluid博客中mathjax数学公式和valine无法加载的"Mixed Content"问题
categories:
  - study
  - computer
toc: true
abbrlink: 471936
date: 2025-07-19 21:45:28
tags:
  - Computer Network
---

yilia和fluid博客中mathjax数学公式和valine无法加载，打开控制台出现如下报错：

```text
Mixed Content: The page at 'https://www.boredliam.top/homepage/posts/35201.html' was loaded over HTTPS, but requested an insecure script 'http://cdn.mathjax.org/mathjax/latest/extensions/MathMenu.js?V=2.7.1'. This request has been blocked; the content must be served over HTTPS.
```
<!-- more -->

## 原因

> 当用户访问通过HTTPS提供的页面时，他们与 Web 服务器的连接使用TLS 进行加密，因此可以防止大多数嗅探器和中间人攻击。包含使用明文 HTTP 获取的内容的 HTTPS 页面称为混合内容页面。像这样的页面只是部分加密，使嗅探器和中间人攻击者可以访问未加密的内容。这使页面不安全。

实际上只需要在头部加上meta信息即可：

```html
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
```

## 解决方法

fluid会判断网站是否采用https而选择性假如该meta，但是有时会出现判断失误的情况，所以可以删去判断：
定位`\themes\fluid\layout\_partials\head.ejs`

```html
  <% if (theme.force_https) { %>
    <meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
  <% } %>
```

删去前后只留下`<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">`即可。

对于yilia，似乎没有这个meta
手动加入到`\themes\yilia\layout\_partial\head.ejs`某处即可（注意不要插入`<% if (...) { %>`和`<% } %>`之间）

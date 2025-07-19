---
title: hexo博客中使用多主题并在vercel中自动部署
tags:
  - Computer Network
  - blog
categories: 
- study
- blog-building
abbrlink: 156955
date: 2025-07-19 19:52:11
---

从yilia主题换到fluid主题后，我还是舍不得我在yilia做的美化，所以就想到使用双主题一起走。
结果就是困难总比办法多。。。。

<!-- more -->

{% note info %}
【注】做双主题已经是一段时间之前的事了，当时懒得写文章，现在迁移的时候出了bug才想起来写，所以记忆可能出现某些偏差，请谨慎操作。
(*^▽^*)
{% endnote %}

## 参考文章

[我的Hexo博客多主题同时部署的实现思路（Butterfly+安知鱼） - InsectMk | 2024-07-30](https://insectmk.cn/posts/10d64ca8/)
[Hexo中同时使用多个主题 - Immortalqx | 2022-04-1](https://immortalqx.github.io/2022/04/17/hexo-multi-theme/)

## 实现思路

当我们使用`hexo generate`生成网站html的时候，hexo通常会按照默认主题里面的`_config.yml`来进行生成。
那么我们只要使用不同的config文件分别生成就可以实现多主题了，比如：

假如我们有`_config_homepage.yml`，我们就可以用以下命令来用这个配置生成主题

```hexo
hexo --config _config_homepage.yml g
```

我们可以将生成的另一个主题放在博客的子目录下，这样就不会冲突了

## 操作步骤

- 1.安装需要使用的新主题（正常安装流程即可）

- 2.分离配置，复制一份`_config.yml`，将其命名为另一个名字，我这里命名为`_config_homepage.yml`
接着还得创建新的资源目录`source`，我这里直接在根目录创建了`source_homepage`，

- 3.修改新的配置文件`_config_homepage.yml`，我的修改如下：

```yaml
# Site
# 部分选项置空，防止和采用的theme冲突
title: Homepage
subtitle: 'Homepage'
description:
keywords:
author:
language: EN
timezone: ''

# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://www.boredliam.top/homepage/ # 改到新目录
root: /homepage/ # 改到新目录
permalink: posts/:abbrlink.html
permalink_defaults: :title/
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks

# Directory
# 这个public_dir是最终生成html文件的地方，像我这样就在boredliam.top/homepage这里访问双主题
source_dir: source_homepage # 改到新的资源目录
public_dir: public/homepage # 改到新的资源目录（必须在博客的public文件夹内）
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: yilia # 我使用的副主题是yilia
```

原来的`_config.yml`修改为新的主题即可

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: fluid
```

- 4.写新文章

创建新文章的命令和以前相同，只不过hexo后面要加上配置文件的声明，如在homepage中创建一篇新文章：

```yaml
hexo --config _config_homepage.yml new "xxxxx"
```

- 5.开始部署

```git
hexo cl
hexo --config _config.yml g
hexo --config _config_homepage.yml g
hexo d
```

这里的`hexo --config _config.yml g`也可以写`hexo g`，因为都是按默认配置部署。
由于所有渲染内容都在原博客的public文件夹下，所以这里对应的是同一个github仓库，只需要`hexo d`就能同时把两个主题渲染的页面推送过去。

但是部署完成后可能出现homepage额外渲染blog中的内容，这是因为文章信息储存在db.json中，可以通过`hexo g`后加上`rm db.json`来解决

## vercel部署

我切换到vercel自动部署之后发现，vercel的自动部署不会渲染homepage中的内容，手动部署了之后虽然生成了html文件，但是访问依旧显示404
vercel的自动部署默认只执行`hexo generate`，所以只要想办法加上渲染homepage的命令即可
vercel通过调用`npm run build`指令来进行部署，`build`的内容可以在`package.json`中更改，我的更改如下

```json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "build": "hexo --config _config_homepage.yml generate & hexo clean && hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
 ......
  },
  ......
}
```

将命令改为了先执行`hexo --config _config_homepage.yml generate`，再执行一次`hexo clean`（因为此时不使用db.json），最后再执行`hexo generate`
终于完美实现（终于改好bug）

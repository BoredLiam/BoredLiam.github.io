---
title: 运用云函数实现自动签到（nodejs+serverless云函数）
tags: Computer Network
categories:
  - study
  - computer
toc: true
abbrlink: 32638
comment: 'valine'
date: 2024-02-15 00:00:00
---
前言：本文照抄自[林语琛的稀土掘金文章](https://juejin.cn/post/7124865201442127902 "林语琛的稀土掘金文章")
在此基础上添加了自己发现的一些问题
侵权删
<!--more-->

## 基本流程

- 进入签到页面
- 打开浏览器控制台执行签到请求
- 获取请求的cURL
- 到postman页面生成nodejs代码
- 生成package.json并根据对应平台的云函数格式调整nodejs代码
- 在控制台新建云函数、提交代码并设置固定时间的触发器
- 完成并回去给他点赞！

## 所需工具

- 免费的云函数服务：阿里云、百度云
（好像是取消了，但是使用量小不贵）
- Chrome、FireFox或者一切可以打开控制台的浏览器（用于捕捉请求）
- Postman（用于一键生成请求代码）
[Postman网址](https://web.postman.co/home "Postman")，注册即可
- nodejs（如果不在本地调试而是直接在云函数端调试则无需安装）
[下载链接](https://nodejs.org/en "nodejs")（这个下载应该没啥问题）

## 详情

### Step1 进入签到页面

选择你要自动签到的网页打开，这里使用某论坛的打卡签到（切记先不要点击！否则没法捕捉到请求了）：
![打卡签到](32638/A.webp "切记先不要点击")
打开浏览器控制台（一般就是F12），点netwrok或网络标签：
**这里要注意两点：**

- 勾选上“保留日志”或“preserve log”，避免页面跳转当前页请求消失
- 如果下面列表中已经存在之前的请求的，点击清除按钮清除之前的请求，避免跟要捕捉的签到请求混淆

然后进行签到操作，此时列表里就会出现签到的请求了（一般都是第一个请求，因为加载了图片或跳转页面会出现多个请求，这个就只能自己通过地址名称、响应内容进行甄别了）：
![寻找请求](32638/B.webp "请求")
（一般都是.php的文件，名字里带个sign啥的）

### Step2 获取请求的cURL

在刚才的请求上单击右键，选择`复制-以cURL(bash)copy格式复制`：
（英文版是`copy-Copy as cURL(bash)`）
![复制cURL(bash)](32638/C.webp "cURL")
**这个代码里包含着你账号的cookie等信息，不要泄露给其他人**
大概长这样：

```bash
curl 'https://xxx.cn/home.php?mod=task&id=2&referer=%2F' \
  -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9' \
  -H 'Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6' \
  -H 'Connection: keep-alive' \
  -H 'Cookie: 重要的cookie内容，千万不要随便发给别人'\
  -H 'Referer: https://xxx.cn/' \
  -H 'Sec-Fetch-Dest: document' \
  -H 'Sec-Fetch-Mode: navigate' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'Sec-Fetch-User: ?1' \
  -H 'Upgrade-Insecure-Requests: 1' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
  -H 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  --compressed
```

### step3 到postman页面生成nodejs代码

打开postman（也可以用网站，用软件的话版本尽量新一点，旧的版本没有生成代码的功能）
点击`import`，在蓝色框粘贴刚才的代码就会自动跳转：
![粘贴代码](32638/1.png "粘贴代码")
这时候请求就直接导入到postman中了（你也可以点击send发送请求进行测试）：
![导入成功](32638/D.webp "成功")
点击右侧代码样式的按钮：
![点](32638/E.webp "点")
其中就可以生成各个语言下的签到请求代码，可以随意挑选，这里用他比较熟悉的axios框架为例：
<img src="32638/F.webp" style="display: flex;margin: auto;height: 600px;">

### step4 生成`package.json`并根据对应平台的云函数格式调整nodejs代码

axios需要运行在nodejs下并且需要安装依赖，安装nodejs的步骤就不说了
直接新建文件夹，在cmd中执行下面的代码

```bash
cd /D D:\axios
# 上面D:\axios指的是你新建文件夹的路径
npm init -y
npm install axios@0.19.2 --save
```

> 这里原文章默认下载最新版本，但是后面云函数会报错，所以[参考这里](https://blog.csdn.net/weixin_52153645/article/details/130362110 "参考这里")，安装的是旧版本的axios

在刚刚文件夹里创建index.js文件，粘贴刚才postman中生成的代码，也可以在控制台（或者cmd）输入node index.js发送请求进行测试：
![测试](32638/G.webp "测试")
这时候，签到请求的代码就完成了，但是要放到云函数上的时候还要做一点修改，以百度云函数为例：

```js
exports.handler = (event, context, callback) => {
    // 这里放进去你生成的代码即可
    // 当然如果想查看接口返回信息的话可以把callback方法写在请求的回调中，第二个参数替换成接口的回调：
    // 上面这段我实在看不太懂（没用过axios），但是把下面取消注释也可以查看返回信息
    // axios(config)
    //  .then(function (response) {
    //    callback(null, JSON.stringify(response.data));
    //  })
};
```

（具体的格式一般在各个平台的云函数生成时都会有示例代码，只要按照示例代码正常返回值即可）

### step4 在控制台新建云函数、提交代码并设置固定时间的触发器（以百度云函数为例）

注册登录百度智能云，打开[函数计算CFC](https://console.bce.baidu.com/cfc/functions)，点击函数列表，创建函数：
![创建函数](32638/2.png "创建函数")
什么你说你的是灰的？那你身份认证啊
模板选择空白函数
![选择模板](32638/3.png "选择模板")
![设定基本信息](32638/H.webp "设定基本信息")
![定时触发器](32638/I.webp "设定定时触发器")

> 2025.7.20 似乎百度云把定时任务触发器改成Crontab触发器了。。注意一下即可

时间的填写方式参考下表或[百度云官方文档](https://cloud.baidu.com/doc/CFC/s/ajzmg1mft)：

样例（注意：以下样例均使用UTC时区，Asia/Shangha时区比UTC时区多八个小时）:

| cron表达式(UTC时间) | 解释 |
| ----------- | ----------- |
| `cron(0 10 * * ?)` | 每天上午的 10:00 (UTC) 触发；对应Asia/Shanghai为每天下午18:00执行 |
| `cron(30 10 * * ?)` | 每天上午的 10:30 (UTC) 触发 ；对应Asia/Shanghai为每天下午18:30执行 |
| `cron(10,11,12 * * * ?)` | 每小时的10分，11分，12分(UTC) 触发 |
| `cron(0 8 1 * ?)` | 每月第 1 天的上午 8:00 (UTC) 触发；对应Asia/Shanghai为每月第 1 天的下午16:00执行 |
| `cron(0/10 * * * ?)` | 每10分钟 (UTC) 触发 |
| `cron(0/10 8-10 ? * MON-FRI)` | 每星期一到星期五的上午 8:00 和 10:00 (UTC) 之间，每10分钟触发一次；对应Asia/Shanghai为每星期一到星期五的下午16:00和18:00之间执行，每10分钟触发一次 |

函数创建完毕之后，进入函数代码，选择“上传函数.zip包”，压缩刚才新建的文件夹并上传：
> 注意：压缩文件里包含`node_modules` `package.json` `package-lock.json` `index.js`
> ![上传函数代码](32638/J.webp "上传函数代码")

上传成功后，你也可以点击测试手动触发一次来查看签到是否成功。
（直接点击执行就好了）
![测试](32638/4.png "测试")
到此为止，自动签到就完成了！等着第二天查看成果吧！

### step5 cookie过期后重新上传代码

> 重复步骤重复的是啥？
> 后面我再补( ⓛ ω ⓛ *) --2024.6.10
>
> 我发现我好蠢，只要直接在百度智能云那里更改部分代码就行了。。。。
> --2025.5.11

一段时间后cookie会过期，具体时间看网站而定（一般至少几个月）
过期之后重复的步骤其实差不多，不过写出来方便我回来看

---
打开网站页面，按下F12，选择保留日志，点击签到按钮，找到.php文件
![F12](32638/a.png "F12")
单击右键，选择`复制-以cURL(bash)copy格式复制`
打开[postman](https://web.postman.co/ "https://web.postman.co/")
点击import，在蓝色框粘贴刚才的代码，在跳转页面点击右侧代码样式的按钮，选择`NodeJs - Axios`并复制代码

接下来打开`函数运算CFC`然后选择你的函数代码，`编辑类型→在线编辑`，将需要更改的部分修改为新的代码即可。

{% note info %}
*这些是原来写的更繁琐的方式不用看了*

打开之前安装`axios`的文件夹，修改之前新建的`index.js`文件，以百度云为例

```js
exports.handler = (event, context, callback) => {
    // 替换原来的代码即可
    // axios(config)
    //  .then(function (response) {
    //    callback(null, JSON.stringify(response.data));
    //  })
};
```

修改后将`node_modules` `package.json` `package-lock.json` `index.js`三个文件以.zip格式压缩
打开[百度智能云](https://console.bce.baidu.com/ "百度智能云")并登录，打开函数列表并找到你的云函数
选择`函数代码——上传函数.zip包`并上传刚刚的压缩文件，点击保存
{% endnote %}

点击右上角测试可以查看是否成功
完成！

> 20260805二编
> 这个postman页面似乎改了一大堆，不管怎么样只要找到`My Workspace`，新建一个GET请求然后粘贴cURL就行
> 接下来生成代码，它默认收起右侧边栏我找了好久。。。
> ![点击右上角或右下角展开右侧边栏](32638/note.png "点击右上角或右下角展开右侧边栏")
> 就这样吧（居然还想起来更新 ~~其实是因为太闲了~~）

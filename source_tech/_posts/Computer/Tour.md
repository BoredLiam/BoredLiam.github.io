---
title: 我把英语书上的Online Tour（简单）复刻了：Around the World in Eight Hours
tags: Computer Network
categories:
  - html
  - study
  - computer
toc: false
comment: 'valine'
abbrlink: 53826
date: 2024-04-12 15:56:42
---
已经消失了很久一段时间了，那么我这段时间做了些什么了呢？
就如很多年前起的这个‘bored’名字一样，我还是在干一些很无聊的事情。于是最后就得到了这个———[Online Tour:Around the World in Eight Hours](https://boredliam.github.io/tour)<!-- more -->

## 废话先行

先来说几句废话。
这个鬼东西是是译林版英语书八年级下册Unit3的课文
> <sub>来自<a href="https://edu.yilin.com/index.php/Category/show?nav_id=14&cat_id=31&resid=37f47fc3d91d3cacacb9b3b644881ba1">译林教育网 英语（八年级下册）</a></sub>

功能如你所见，就是给你展示世界各地的美(wén)景(zhāng)
为了让我回忆起曾经的html知识，就试着做了这个（一边学一边写，代码真的很乱）

2025.3.29
废话夹在这里吧，居然有人看并且发现有问题（震惊），不管怎样已经改好了，顺便把失效的链接补上了。。。

## 接下来是简单的介绍（这有什么分开的必要吗）

因为课文里只有纽约，所以我只做了纽约。
弹出的窗口我猜测是点击进入，但是似乎很多人看不出来要点击<sub>（不过我是不会改的）</sub>
课文中标有行数，但是因为是从第一个页面开始计数，不太符合网站本身，所以我没有做（更加重要的是我不会做，哪个大佬教我）
导航栏中的`Camera`其实课本中有介绍，是用来浏览本城市的图片的，但是我实在不会做，故作罢
至于上面的图标.....课本上的太糊了，我也找不到原图，于是就偷了几个xp的图标代替
大概就是这么多，上学的时候脑子完全单开一个线程，以至于回来打代码什么都不会，最后就是磨磨蹭蹭做出来这个鬼东西。
[点我下载垃圾代码](https://boredliam.gz.bcebos.com/Online_Tour.zip)
代码：

### index.html

```html
<html>
    <head>
        <meta charset="UTF-8">
        <title>
            Online Tour-Around the World in Eight Hours
        </title>
        <script type="text/javascript">
            function newyork () {
                window.open(
                'pop_up.html',
                '单独窗口',
                'height=300,width=600,top=300,left=200,toolbar=no,menubar=no,scrollbars=no,resizable=no,location=no,status=no,titlebar=no'
                )
                window.opener=null;
				window.open('','_self');
				window.close();
            }
            function page_print () {
                const printContentHtml = document.getElementById("content").innerHTML;
                const iframe = document.createElement("iframe");
                iframe.setAttribute(
                    "style",
                    "position:absolute;width:0px;height:0px;left:-500px;top:-500px;"
                );
                document.body.appendChild(iframe);
                iframe.contentDocument.write(printContentHtml);
                iframe.contentDocument.close();
                iframe.contentWindow.print();
                document.body.removeChild(iframe);
            }
        </script>
        </head>
    <body style="background-color: #F4F9F7;">
        <div class="guide">
            <div class="item"><img src="https://img2.imgtp.com/2024/04/06/SK2cQvst.ico" style="padding-left: 10px;">
                Tour
                <div class="dropdown-content">
                    <p>Asia</p>
                    <p>Africa</p>
                    <p>Europe</p>
                    <div class="double-content">
                        America
                        <div class="double-dropdown-content">
                            <div class="triple-content">
                                the USA
                                <div class="triple-dropdown-content">
                                    <p>Miami</p>
                                    <a onclick="newyork()">New York</a>
                                    <p>San Francisco</p>
                                    <p>Seattle</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <p>Others</p>
                </div>
            </div>
            <div class="item"><img src="https://img2.imgtp.com/2024/04/06/MVKTfLg9.ico"><button onclick="alert('Please Choose a city first!')">Camera</button></div>
            <div class="item" style="border-right: 0;"><img src="https://img2.imgtp.com/2024/04/06/q25eyVyE.ico"><button onclick="page_print()">Print</button></div>
        </div>
        <div class="content" id="content">
            <img src="https://img2.imgtp.com/2024/04/06/IZdIDqxc.png" id="earth">
            <p>
                Welcome to "Around the World in Eight Hours". I'm your tour guide, Robin. Have you noticed the "Tour" icon at the top of the page? Just click on it,and you can visit Asia, Africa, Europe, America and more in only eight hours!
            </p>
            <br>
            <!-- <a id="enter" href="new_york.html"></a> -->
        </div>
        <style>
            .guide{
                position: sticky;
                font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
                font-size: 25px;
                background-color: #e1e3d6;
                top: 0;
                z-index: 1000;
            }
            .item img{
                height: 30px;
                vertical-align: middle;
                padding-right: 2px;
            }
            .item{
                /* width: 10%; */
                display: inline-block;
                text-align: center;
                border-right: 2px solid #ccc8c4;
                margin: 10px;
                align-items: center;
                padding-right: 20px;
                margin-right: 0;
                margin-left: 20px;
            }
            .item button{
                border: 0;
                background-color: unset;
                display: inline-block;
                text-align: center;
                align-items: center;
                font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
                font-size: 25px;
            }
            .content p{
                font-family:'Times New Roman';
                font-size: 30px;
                position: relative;
                margin: auto;
                padding: 70px;
                top: 70px;
                line-height: 1.8em;
            }
            #earth{
                position: relative;
                width: 40%;
                margin: auto;
                left: 55%;
                top: 60px;
            }
            .dropdown-content {
                display: none;
                position: absolute;
                left: 0px;
                background-color: #f9f9f9;
                min-width: 160px;
                border: 2px #000000 solid;
                /* padding: 2px 16px; */
                font-size: 20px;
                font-style: initial;
                z-index: 1;
            }
            .double-dropdown-content{
                display: none;
                position: absolute;
                left: 160px;
                margin-top: -30px;
                background-color: #f9f9f9;
                min-width: 160px;
                border: 2px #000000 solid;
                font-size: 20px;
                font-style: initial;
                padding: 10px;
            }
            .triple-dropdown-content{
                display: none;
                position: absolute;
                left: 145px;
                margin-top: -36px;
                background-color: #f9f9f9;
                min-width: 160px;
                border: 2px #000000 solid;
                font-size: 20px;
                font-style: initial;
            }
            .item:hover .dropdown-content {
                display: block;
            }
            .double-content:hover .double-dropdown-content{
                display: block;
            }
            .triple-content:hover .triple-dropdown-content{
                display: block;
            }
            #enter img{
                position: relative;
                margin: auto;
                width: 90%;
                display: block;
            }
        </style>
    </body>
</html>
```

### new_york.html

```html
<html>
    <head>
        <meta charset="UTF-8">
        <title>
            New York-Online Tour-Around the World in Eight Hours
        </title>
        <script type="text/javascript">
            function newyork () {
                window.open(
                'pop_up.html',
                '单独窗口',
                'height=300,width=600,top=300,left=200,toolbar=no,menubar=no,scrollbars=no,resizable=no,location=no,status=no,titlebar=no'
                )
                window.opener=null;
				window.open('','_self');
				window.close();
            }
            function page_print () {
                const printContentHtml = document.getElementById("content").innerHTML;
                const iframe = document.createElement("iframe");
                iframe.setAttribute(
                    "style",
                    "position:absolute;width:0px;height:0px;left:-500px;top:-500px;"
                );
                document.body.appendChild(iframe);
                iframe.contentDocument.write(printContentHtml);
                iframe.contentDocument.close();
                iframe.contentWindow.print();
                document.body.removeChild(iframe);
            }
        </script>
        </head>
    <body style="background-color: #F4F9F7;">
        <div class="guide">
            <div class="item"><img src="https://img2.imgtp.com/2024/04/06/SK2cQvst.ico" style="padding-left: 10px;">
                Tour
                <div class="dropdown-content">
                    <p>Asia</p>
                    <p>Africa</p>
                    <p>Europe</p>
                    <div class="double-content">
                        America
                        <div class="double-dropdown-content">
                            <div class="triple-content">
                                the USA
                                <div class="triple-dropdown-content">
                                    <p>Miami</p>
                                    <a onclick="newyork()">New York</a>
                                    <p>San Francisco</p>
                                    <p>Seattle</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <p>Others</p>
                </div>
            </div>
            <div class="item"><img src="https://img2.imgtp.com/2024/04/06/MVKTfLg9.ico"><button onclick="">Camera</button></div>
            <div class="item" style="border-right: 0;"><img src="https://img2.imgtp.com/2024/04/06/q25eyVyE.ico"><button onclick="page_print()">Print</button></div>
        </div>
        <div class="content" id="content">
            <div class="text">
                <p>Here we are in "the Big Apple"—New York, the biggest city in the USA. </p>
                <br>
                <p>Wall Street, the world-famous trade centre, is here at the southern end of Manhattan Island. There are many big companies and international banks here.</p>
            </div>
            <div class="pic">
                <img src="https://img2.imgtp.com/2024/04/06/c0jhnEN4.png" style="right: 30px;">
            </div>
            <div>
                <br>
                <p>Further on is Times Square. Every year, thousands of people gather here on New Year's Eve. It's exciting to see the huge glass ball falling through the darkness! </p>
                <br>
                <p>In the centre of the island is Central Park. With several lakes, hills and a large green lawn, it's a good place to relax after a hard day's work. </p>
            </div>
            <div class="pic">
                <img src="https://img2.imgtp.com/2024/04/06/vv3Q7c5O.png" style="left: 30px;">
            </div>
            <div class="text">
                <br>
                <p>When you visit New York, don't miss Broadway. It has been famous for its theatres since the early twentieth century. Have you ever heard of the song "Memory"? It comes from the famous Broadway musical <em>Cats</em>. </p>
                <br>
                <p>OK, so much for New York. There's a "Back" icon at the bottom of the page. Click on it, pick another city and then start your new tour!</p>
            </div>
        </div>
        <div id="pictures"></div>
        <div class="back">
            <a href="index.html"><img src="https://img2.imgtp.com/2024/04/06/U7rJlMaS.png"> Back</a>
        </div>
        <style>
            .guide{
                position: sticky;
                font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
                font-size: 25px;
                background-color: #e1e3d6;
                top: 0;
                z-index: 1000;
            }
            .item img{
                height: 30px;
                vertical-align: middle;
                padding-right: 2px;
            }
            .item{
                /* width: 10%; */
                display: inline-block;
                text-align: center;
                border-right: 2px solid #ccc8c4;
                margin: 10px;
                align-items: center;
                padding-right: 20px;
                margin-right: 0;
                margin-left: 20px;
            }
            .item button{
                border: 0;
                background-color: unset;
                display: inline-block;
                text-align: center;
                align-items: center;
                font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
                font-size: 25px;
            }
            .dropdown-content {
                display: none;
                position: absolute;
                left: 0px;
                background-color: #f9f9f9;
                min-width: 160px;
                border: 2px #000000 solid;
                /* padding: 2px 16px; */
                font-size: 20px;
                font-style: initial;
                z-index: 1;
            }
            .double-dropdown-content{
                display: none;
                position: absolute;
                left: 160px;
                margin-top: -30px;
                background-color: #f9f9f9;
                min-width: 160px;
                border: 2px #000000 solid;
                font-size: 20px;
                font-style: initial;
                padding: 10px;
            }
            .triple-dropdown-content{
                display: none;
                position: absolute;
                left: 145px;
                margin-top: -36px;
                background-color: #f9f9f9;
                min-width: 160px;
                border: 2px #000000 solid;
                font-size: 20px;
                font-style: initial;
            }
            .item:hover .dropdown-content {
                display: block;
            }
            .double-content:hover .double-dropdown-content{
                display: block;
            }
            .triple-content:hover .triple-dropdown-content{
                display: block;
            }
            #enter img{
                position: relative;
                margin: auto;
                width: 90%;
                display: block;
            }
            .content::after{
                content:"";
                display: block;
                clear: both;
            }
            .content p{
                font-family:'Times New Roman';
                font-size: 30px;
                position: relative;
                margin: auto;
                padding-left: 70px;
                padding-right: 70px;
                top: 20px;
                line-height: 1.8em;
            }
            .content div{
                float: left;
                margin: auto;
            }
            .pic img{
                width: 90%;
                top: 80px;
                position: relative;
                margin-bottom: 20px;
            }
            .text{
                width: 70%;
            }
            .pic{
                width: 30%;
            }
            .back{
                font-size: 20px;
                font-family: Arial, Helvetica, sans-serif;
                font-weight: bold;
                margin: 40px;
                padding-bottom: 20px;
                position: initial;
            }
            .back img{
                width: 30px;
            }
            .back a{
                position: absolute;
                right: 5%;
                color: #000000;
                text-decoration: none;
            }
            #pictures img{
                width: 90%;
                top: 80px;
                position: relative;
                margin-bottom: 50px;
            }
        </style>
        <script>
            function show_picture () {
                var newyork = document.createElement("img");
                newyork.src = "https://cdn.pixabay.com/photo/2023/04/16/11/23/bridge-7929999_1280.jpg";
                var enter = document.getElementById('pictures');
                enter.appendChild(newyork);
                // var arr=[
                //     'https://cdn.pixabay.com/photo/2023/04/16/11/23/bridge-7929999_1280.jpg',
                //     'https://cdn.pixabay.com/photo/2016/11/23/15/32/pedestrians-1853552_960_720.jpg'
                // ];
                // var imgs=''
                // for(var i=0;i<arr.length;i++){
                //     imgs+='<img src="'+arr[i]+'" />';
                // }
                // document.getElementById("img").innerHTML=imgs;
            }
        </script>
    </body>
</html>
```

### pop_up.html

```html
<html>
    <head>
        <meta charset="UTF-8">
    </head>
    <body style="background-color: #F2F3EE;margin: 0;">
            <a id="enter" onclick="window.opener=null;window.open('','_self');window.close();" target="_blank" href="new_york.html"><img src="https://img2.imgtp.com/2024/04/06/vO7q13N8.png"></a>
        <style>
            #enter img{
                position: relative;
                margin: 0;
                width: 100%;
                display: block;
            }
        </style>
    </body>
</html>
```


> <div style="font-size: xx-small;transform: rotate(180deg);">一些完全无关的话：最近真的好忙准备考一模但是甚至一轮复习还没过完三月三放假完就很久之后才能长假了虽然我还是在浪费时间以及我的语文成绩真的好烂怎么基础都错这么多更何况还有几万首前面的古诗文没背背完后面的又忘记了回去还得考每天想摆烂又不敢摆卷又没力气卷每天也不知道在干什么玩也玩不好学也没学到简直是人生输家现在回想今天一天似乎还是啥也没干假期就已经过去一半了前面定下的目标完全忘记完美的脱轨今天还看到某人自己一个在教室学习估计这次他又考的不错那他进尖子班应该稳了吧至于我我也不知道但是已经开始做最坏的打算了算了不理了还是休息一下先吧等会又要看书虽然不知道看什么再见当然这段话我不太想让某些人看到所以我要把它旋转九十度啊不对是一百八十度我的心算能力到底该怎么提高我的计算题写的好慢对了说点正常的我今早看了啥啥水母的番似乎挺不错的.....</div>

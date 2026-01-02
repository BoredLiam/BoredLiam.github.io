---
layout: false
comments: false
---
<html>
    <head>
        <meta charset="UTF-8">
            <script type="text/javascript">
            function notfound() {
                var img = event.srcElement;
                img.src = "pic/New York.png";
                img.onerror = null; //解绑onerror事件
            }
        </script>
    </head>
    <body style="background-color: #F2F3EE;margin: 0;">
            <a id="enter" onclick="window.opener=null;window.open('','_self');window.close();" target="_blank" href="new_york.html"><img src="https://s21.ax1x.com/2024/06/16/pkwYpQK.png" onerror="notfound();" style="height: 100vh;"></a>
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
<!-- pkwYpQK.png -->
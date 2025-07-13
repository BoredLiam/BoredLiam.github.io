---
layout: false
comments: false
---

<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>生日快乐！</title>
    <style>
body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            overflow: hidden;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }
        
        body::before {
            content: "";
            position: absolute;
            top: -100%;
            left: -100%;
            right: -100%;
            bottom: -100%;
            background-image: url('https://boredliam.gz.bcebos.com/retouch_2025051023335518.jpg');
            background-size: 20% auto;
            background-repeat: repeat;
            transform: rotate(25deg);
            z-index: -2; /* 置于最底层 */
        }
        
        body::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ffebee;
            opacity: 0.9; /* 调整透明度以获得理想的滤镜效果 */
            z-index: -1; /* 位于背景图片上方，内容下方 */
        }
        
        .card {
            position: relative;
            width: 350px;
            height: 450px;
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
            padding: 30px;
            text-align: center;
            color: #fff;
            transform-style: preserve-3d;
            transition: transform 0.5s;
        }
        
        .card:hover {
            transform: translateY(-10px) rotateX(5deg);
        }
        
        h1 {
            font-size: 28px;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        p {
            font-size: 18px;
            line-height: 1.6;
            margin-bottom: 25px;
        }
        
        .name {
            font-weight: bold;
            font-size: 24px;
            color: #d81b60;
            text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.5);
            font-family: sans-serif;
        }
        
        .balloon {
            position: absolute;
            font-size: 40px;
            opacity: 0.9;
            animation: float 3s infinite ease-in-out;
        }
        
        .balloon:nth-child(1) {
            top: 50px;
            left: 30px;
            animation-delay: 0s;
        }
        
        .balloon:nth-child(2) {
            top: 80px;
            right: 40px;
            animation-delay: 0.5s;
            filter: hue-rotate(240deg) saturate(1.5); /* 紫色效果 */
        }
        
        .balloon:nth-child(3) {
            bottom: 100px;
            left: 50px;
            animation-delay: 1s;
            filter: hue-rotate(180deg) saturate(1.2) brightness(1.1); /* 天蓝色效果 */
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(-5deg); }
            50% { transform: translateY(-20px) rotate(5deg); }
        }
        
        .cake {
            font-size: 50px;
            margin: 20px 0;
        }
        
        .signature {
            font-style: italic;
            margin-top: 30px;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <div class="card">
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        
        <h1>生日快乐！</h1>
        <div class="cake">🎂</div>
        <p>亲爱的 <span class="name">Windeling</span>，</p>
        <p>在这个特别的日子里，祝你生日快乐！愿你的每一天都充满欢笑和幸福，学业进步，心想事成！</p>
        
        <p class="signature">Yours<br>BoredLiam</p>
    </div>
</body>
</html>
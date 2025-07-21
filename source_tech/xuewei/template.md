---
layout: false
comments: false
---
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>视频播放</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
        }
        .video-container {
            text-align: center;
        }
        video {
            max-width: 90%;
            max-height: 90vh;
            border: 1px solid #ddd;
        }
    </style>
</head>
<body>
    <div class="video-container">
        <video controls>
            <!-- 视频源链接留空 -->
            <source src="" type="video/mp4">
            您的浏览器不支持HTML5视频标签。
        </video>
    </div>
</body>
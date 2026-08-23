---
layout: false
comments: false
---
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <link rel="icon" type="image/gif" href="coin-flip/icon.gif">
    <title>抛硬币</title>
    <style>
        :root {
            --coin-size: clamp(140px, 38vw, 220px);
            --coin-thickness: clamp(8px, 2vw, 12px);
            --gold-light: #FFF5B0;
            --gold-main: #FFD700;
            --gold-dark: #B8860B;
            --gold-deep: #8B6914;
            --silver-light: #FFFFFF;
            --silver-main: #E8E8E8;
            --silver-dark: #A0A0A0;
            --silver-deep: #707070;
            --bg-color: #f5f0eb;
            --text-color: #333;
            --shadow-color: rgba(0, 0, 0, 0.25);
            --transition-speed: 1.6s;
            --ease-curve: cubic-bezier(0.3, 0.1, 0.2, 1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            min-height: 100vh;
            min-height: 100dvh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: var(--bg-color);
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC',
                'Hiragino Sans GB', 'Microsoft YaHei', 'Noto Sans SC', sans-serif;
            color: var(--text-color);
            user-select: none;
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            overflow: hidden;
            padding: 16px;
            background-image: radial-gradient(ellipse at center, #faf7f2 0%, #f0ebe4 60%, #e8e0d8 100%);
        }

        .title {
            font-size: clamp(1.8rem, 6vw, 2.8rem);
            font-weight: 700;
            letter-spacing: 0.08em;
            margin-bottom: clamp(20px, 4vh, 40px);
            color: #4a3f35;
            text-align: center;
            position: relative;
            text-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
        }
        .title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 60px;
            height: 3px;
            border-radius: 3px;
            background: linear-gradient(90deg, transparent, #c9b99a, transparent);
        }

        .coin-area {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            flex: 1;
            min-height: 0;
            position: relative;
            width: 100%;
        }

        .perspective-container {
            perspective: 1200px;
            -webkit-perspective: 1200px;
            perspective-origin: 50% 50%;
            -webkit-perspective-origin: 50% 50%;
            cursor: pointer;
            position: relative;
            touch-action: manipulation;
        }

        .coin {
            width: var(--coin-size);
            height: var(--coin-size);
            position: relative;
            transform-style: preserve-3d;
            -webkit-transform-style: preserve-3d;
            transition: transform var(--transition-speed) var(--ease-curve);
            will-change: transform;
            border-radius: 50%;
            cursor: pointer;
            touch-action: manipulation;
        }

        .coin.flipping {
            animation: coin-toss-bounce var(--transition-speed) var(--ease-curve);
        }

        @keyframes coin-toss-bounce {
            0% {
                translate: 0 0;
            }
            20% {
                translate: 0 calc(var(--coin-size) * -0.25);
            }
            50% {
                translate: 0 calc(var(--coin-size) * -0.4);
            }
            80% {
                translate: 0 calc(var(--coin-size) * -0.15);
            }
            100% {
                translate: 0 0;
            }
        }

        .coin-face {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
            -moz-backface-visibility: hidden;
            overflow: hidden;
            box-sizing: border-box;
        }

        /* 正面 - 金色 */
        .coin-face.front {
            background: radial-gradient(ellipse at 32% 28%,
                    var(--gold-light) 0%,
                    var(--gold-main) 35%,
                    #e6b800 55%,
                    var(--gold-dark) 75%,
                    var(--gold-deep) 100%);
            border: 3px solid #7a5c10;
            box-shadow:
                inset 0 0 30px rgba(255, 255, 200, 0.5),
                inset 0 0 8px rgba(120, 80, 10, 0.3),
                0 4px 24px var(--shadow-color),
                0 2px 6px rgba(0, 0, 0, 0.15);
            z-index: 2;
        }
        .coin-face.front::before {
            content: '';
            position: absolute;
            top: 6%;
            left: 6%;
            width: 88%;
            height: 88%;
            border-radius: 50%;
            border: 2px solid rgba(180, 140, 20, 0.55);
            box-shadow: inset 0 0 20px rgba(180, 140, 20, 0.2);
            pointer-events: none;
        }
        .coin-face.front::after {
            content: '';
            position: absolute;
            top: 12%;
            left: 12%;
            width: 76%;
            height: 76%;
            border-radius: 50%;
            border: 1px dashed rgba(160, 120, 15, 0.4);
            pointer-events: none;
        }
        .coin-face.front .coin-text {
            color: #5a3e08;
            font-weight: 800;
            font-size: clamp(1.1rem, 4.5vw, 1.7rem);
            letter-spacing: 0.12em;
            text-shadow:
                0 1px 2px rgba(255, 240, 160, 0.7),
                0 0 10px rgba(255, 220, 100, 0.3);
            z-index: 1;
            position: relative;
        }

        /* 反面 - 银色 */
        .coin-face.back {
            background: radial-gradient(ellipse at 32% 28%,
                    var(--silver-light) 0%,
                    var(--silver-main) 30%,
                    #d0d0d0 55%,
                    var(--silver-dark) 78%,
                    var(--silver-deep) 100%);
            border: 3px solid #5a5a5a;
            box-shadow:
                inset 0 0 30px rgba(255, 255, 255, 0.6),
                inset 0 0 8px rgba(80, 80, 80, 0.25),
                0 4px 24px var(--shadow-color),
                0 2px 6px rgba(0, 0, 0, 0.15);
            transform: rotateY(180deg);
            -webkit-transform: rotateY(180deg);
            z-index: 1;
        }
        .coin-face.back::before {
            content: '';
            position: absolute;
            top: 6%;
            left: 6%;
            width: 88%;
            height: 88%;
            border-radius: 50%;
            border: 2px solid rgba(130, 130, 130, 0.5);
            box-shadow: inset 0 0 20px rgba(130, 130, 130, 0.15);
            pointer-events: none;
        }
        .coin-face.back::after {
            content: '';
            position: absolute;
            top: 12%;
            left: 12%;
            width: 76%;
            height: 76%;
            border-radius: 50%;
            border: 1px dashed rgba(120, 120, 120, 0.4);
            pointer-events: none;
        }
        .coin-face.back .coin-text {
            color: #4a4a4a;
            font-weight: 800;
            font-size: clamp(1.1rem, 4.5vw, 1.7rem);
            letter-spacing: 0.12em;
            text-shadow:
                0 1px 2px rgba(255, 255, 255, 0.8),
                0 0 10px rgba(220, 220, 220, 0.4);
            z-index: 1;
            position: relative;
        }

        /* 硬币边缘厚度模拟 */
        .coin-edge {
            position: absolute;
            top: 50%;
            left: 50%;
            width: calc(var(--coin-size) - 2px);
            height: calc(var(--coin-size) - 2px);
            transform: translate(-50%, -50%) translateZ(calc(var(--coin-thickness) * -1));
            border-radius: 50%;
            background: linear-gradient(180deg, #c9a84c, #8a6d20, #c9a84c);
            z-index: 0;
            pointer-events: none;
            box-shadow: 0 0 4px rgba(0, 0, 0, 0.3);
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
        }
        .coin-edge-ring {
            position: absolute;
            top: 50%;
            left: 50%;
            width: var(--coin-size);
            height: var(--coin-size);
            transform: translate(-50%, -50%);
            border-radius: 50%;
            background: transparent;
            border: 4px solid #8a6d20;
            z-index: 0;
            pointer-events: none;
            box-shadow:
                0 0 0 1px rgba(0, 0, 0, 0.2),
                inset 0 0 0 1px rgba(255, 255, 255, 0.1);
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
        }

        .coin-shadow {
            position: absolute;
            bottom: calc(var(--coin-size) * -0.35);
            left: 50%;
            transform: translateX(-50%);
            width: calc(var(--coin-size) * 0.85);
            height: calc(var(--coin-size) * 0.18);
            border-radius: 50%;
            background: radial-gradient(ellipse at center, rgba(0, 0, 0, 0.35) 0%, rgba(0, 0, 0, 0.12) 50%, transparent 75%);
            transition: all var(--transition-speed) var(--ease-curve);
            pointer-events: none;
            z-index: -1;
        }
        .coin-shadow.active {
            width: calc(var(--coin-size) * 0.55);
            height: calc(var(--coin-size) * 0.1);
            opacity: 0.35;
            background: radial-gradient(ellipse at center, rgba(0, 0, 0, 0.25) 0%, rgba(0, 0, 0, 0.08) 60%, transparent 80%);
        }

        .hint-text {
            font-size: clamp(0.85rem, 3vw, 1rem);
            color: #9a8a7a;
            margin-top: clamp(32px, 6vh, 56px);
            letter-spacing: 0.05em;
            text-align: center;
            opacity: 0.8;
            transition: opacity 0.4s ease;
        }
        .hint-text.hidden {
            opacity: 0;
            pointer-events: none;
        }

        .result-text {
            font-size: clamp(1.2rem, 4.5vw, 1.8rem);
            font-weight: 700;
            letter-spacing: 0.1em;
            margin-top: clamp(8px, 2vh, 16px);
            min-height: 2.2em;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: color 0.4s ease, opacity 0.5s ease;
            opacity: 0;
            text-align: center;
        }
        .result-text.visible {
            opacity: 1;
        }
        .result-text.front-result {
            color: #b8860b;
            text-shadow: 0 1px 4px rgba(184, 134, 11, 0.3);
        }
        .result-text.back-result {
            color: #6a6a6a;
            text-shadow: 0 1px 4px rgba(106, 106, 106, 0.3);
        }

        /* 折叠菜单容器 */
        .stats-details {
            margin-top: clamp(8px, 2vh, 16px);
            font-size: clamp(0.9rem, 3vw, 1rem);
            color: #7a6a5a;
            letter-spacing: 0.03em;
            user-select: none;
            -webkit-user-select: none;
        }
        .stats-details summary {
            cursor: pointer;
            font-size: inherit;
            color: inherit;
            display: flex;
            align-items: center;
            gap: 6px;
            list-style: none;
            background: rgba(255, 255, 255, 0.65);
            border-radius: 20px;
            padding: 6px 16px;
            box-shadow: 0 1px 6px rgba(0, 0, 0, 0.06);
            backdrop-filter: blur(6px);
            -webkit-backdrop-filter: blur(6px);
            border: 1px solid rgba(255, 255, 255, 0.7);
            transition: background 0.2s;
            outline: none;
        }
        .stats-details summary::-webkit-details-marker {
            display: none;
        }
        .stats-details summary:hover {
            background: rgba(255, 255, 255, 0.85);
        }
        .stats-details[open] summary {
            margin-bottom: 8px;
        }

        .stats {
            display: flex;
            gap: clamp(16px, 4vw, 32px);
            margin-top: 0;
            font-size: clamp(0.85rem, 3vw, 1rem);
            color: #7a6a5a;
            letter-spacing: 0.03em;
            flex-wrap: wrap;
            justify-content: center;
        }
        .stats .stat-item {
            display: flex;
            align-items: center;
            gap: 6px;
            background: rgba(255, 255, 255, 0.65);
            border-radius: 20px;
            padding: 6px 16px;
            box-shadow: 0 1px 6px rgba(0, 0, 0, 0.06);
            backdrop-filter: blur(6px);
            -webkit-backdrop-filter: blur(6px);
            border: 1px solid rgba(255, 255, 255, 0.7);
        }
        .stats .stat-dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            display: inline-block;
            flex-shrink: 0;
        }
        .stats .stat-dot.front-dot {
            background: linear-gradient(135deg, #ffe566, #daa520);
            box-shadow: 0 0 6px rgba(218, 165, 32, 0.5);
        }
        .stats .stat-dot.back-dot {
            background: linear-gradient(135deg, #f0f0f0, #b0b0b0);
            box-shadow: 0 0 6px rgba(160, 160, 160, 0.5);
        }
        .stats .stat-number {
            font-weight: 700;
            font-size: 1.1em;
            color: #4a3f35;
        }

        /* 重置按钮 */
        .reset-btn {
            display: block;
            margin: 8px auto 0;
            padding: 6px 24px;
            font-size: 0.9rem;
            font-weight: 600;
            color: #6a5a4a;
            background: rgba(255, 255, 255, 0.65);
            border: 1px solid rgba(255, 255, 255, 0.7);
            border-radius: 20px;
            cursor: pointer;
            box-shadow: 0 1px 6px rgba(0, 0, 0, 0.06);
            backdrop-filter: blur(6px);
            -webkit-backdrop-filter: blur(6px);
            transition: background 0.2s, transform 0.1s;
            letter-spacing: 0.05em;
        }
        .reset-btn:hover {
            background: rgba(255, 255, 255, 0.9);
        }
        .reset-btn:active {
            transform: scale(0.96);
        }

        @media (max-width: 480px) {
            :root {
                --coin-size: clamp(110px, 42vw, 160px);
                --coin-thickness: 6px;
            }
            body {
                padding: 8px;
            }
            .title {
                margin-bottom: 16px;
            }
            .hint-text {
                margin-top: 24px;
            }
            .coin-shadow {
                bottom: calc(var(--coin-size) * -0.3);
            }
        }
        @media (min-width: 768px) {
            :root {
                --coin-size: clamp(180px, 22vw, 230px);
                --coin-thickness: 10px;
            }
        }
        @media (min-width: 1200px) {
            :root {
                --coin-size: 220px;
                --coin-thickness: 12px;
            }
        }

        @media (prefers-reduced-motion: reduce) {
            .coin {
                transition-duration: 0.6s;
            }
            .coin.flipping {
                animation-duration: 0.6s;
            }
            .coin-shadow {
                transition-duration: 0.6s;
            }
        }
    </style>
</head>
<body>

    <h1 class="title">抛硬币</h1>
    
        <p>不知道该干啥就抛硬币吧。</p>
    <div class="coin-area">
        <div class="perspective-container" id="perspectiveContainer" role="button" aria-label="抛硬币" tabindex="0">
            <div class="coin" id="coin">
                <div class="coin-face front">
                    <span class="coin-text">正面</span>
                </div>
                <div class="coin-face back">
                    <span class="coin-text">反面</span>
                </div>
            </div>
            <div class="coin-shadow" id="coinShadow"></div>
        </div>

        <div class="result-text" id="resultText"></div>

        <!-- 折叠统计菜单 -->
        <details class="stats-details" id="statsDetails">
            <summary>📊 统计</summary>
            <div class="stats" id="stats">
                <div class="stat-item">
                    <span class="stat-dot front-dot"></span>
                    <span>正面</span>
                    <span class="stat-number" id="frontCount">0</span>
                </div>
                <div class="stat-item">
                    <span class="stat-dot back-dot"></span>
                    <span>反面</span>
                    <span class="stat-number" id="backCount">0</span>
                </div>
            </div>
            <button id="resetBtn" class="reset-btn">重置次数</button>
        </details>

        <div class="hint-text" id="hintText">👆 点击硬币开始抛掷</div>
        <div style="color: #bfbfbf;bottom: 0;position: absolute;text-align: center;font-family: &quot;Times New Roman&quot;;font-size: 0.15em;">Copywrong&nbsp;©&nbsp;6202&nbsp;boredliam.top&nbsp;All Wrongs Reserved</div>
    </div>

    <script>
        (function() {
            // DOM元素
            const coin = document.getElementById('coin');
            const perspectiveContainer = document.getElementById('perspectiveContainer');
            const coinShadow = document.getElementById('coinShadow');
            const resultText = document.getElementById('resultText');
            const frontCountEl = document.getElementById('frontCount');
            const backCountEl = document.getElementById('backCount');
            const hintText = document.getElementById('hintText');
            const resetBtn = document.getElementById('resetBtn');

            // 状态变量
            let currentRotation = 0;
            let isFlipping = false;
            let frontCount = 0;
            let backCount = 0;
            let flipTimeout = null;

            // 音频上下文（延迟初始化）
            let audioCtx = null;

            const EASE_CURVE = 'cubic-bezier(0.3, 0.1, 0.2, 1)';
            const ANIMATION_DURATION = 1600;
            const BASE_ROTATIONS = 1800;

            function updateStats() {
                frontCountEl.textContent = frontCount;
                backCountEl.textContent = backCount;
            }

            function showResult(result) {
                resultText.classList.remove('visible', 'front-result', 'back-result');
                void resultText.offsetWidth;
                if (result === 'front') {
                    resultText.textContent = '🎉 正面！';
                    resultText.classList.add('front-result');
                } else {
                    resultText.textContent = '✨ 反面！';
                    resultText.classList.add('back-result');
                }
                requestAnimationFrame(() => {
                    resultText.classList.add('visible');
                });
            }

            function hideResult() {
                resultText.classList.remove('visible');
            }

            // 播放简单音效
            function playSound(frequency, duration = 0.15, type = 'sine') {
                if (!audioCtx) {
                    try {
                        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                    } catch (e) {
                        return;
                    }
                }
                if (audioCtx.state === 'suspended') {
                    audioCtx.resume().catch(() => {});
                }
                const oscillator = audioCtx.createOscillator();
                const gainNode = audioCtx.createGain();
                oscillator.type = type;
                oscillator.frequency.value = frequency;
                gainNode.gain.setValueAtTime(0.3, audioCtx.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + duration);
                oscillator.connect(gainNode);
                gainNode.connect(audioCtx.destination);
                oscillator.start(audioCtx.currentTime);
                oscillator.stop(audioCtx.currentTime + duration);
            }

            function onFlipComplete(result) {
                isFlipping = false;
                coin.classList.remove('flipping');
                coinShadow.classList.remove('active');

                if (result === 'front') {
                    frontCount++;
                } else {
                    backCount++;
                }
                updateStats();
                showResult(result);

                // 振动反馈
                if (navigator.vibrate) {
                    navigator.vibrate(100);
                }

                // 音效反馈（正面高音，反面低音）
                if (result === 'front') {
                    playSound(880, 0.18, 'sine');
                } else {
                    playSound(440, 0.18, 'sine');
                }

                hintText.classList.remove('hidden');
                hintText.textContent = '👆 再抛一次？';
                perspectiveContainer.style.cursor = 'pointer';
            }

            function flipCoin() {
                if (isFlipping) return;

                isFlipping = true;
                coin.classList.remove('flipping');
                coinShadow.classList.remove('active');
                hideResult();
                hintText.classList.add('hidden');
                perspectiveContainer.style.cursor = 'wait';

                const isFront = Math.random() < 0.5;
                const targetMod = isFront ? 0 : 180;

                let addedRotation = BASE_ROTATIONS;
                const currentMod = ((currentRotation % 360) + 360) % 360;
                const neededAdjustment = ((targetMod - ((currentMod + addedRotation) % 360)) + 360) % 360;
                addedRotation += neededAdjustment;
                const extraRotations = Math.floor(Math.random() * 3) * 360;
                addedRotation += extraRotations;

                const newRotation = currentRotation + addedRotation;
                coin.style.transform = 'rotateY(' + newRotation + 'deg)';
                coin.classList.add('flipping');
                coinShadow.classList.add('active');
                currentRotation = newRotation;

                if (flipTimeout) clearTimeout(flipTimeout);
                flipTimeout = setTimeout(() => {
                    onFlipComplete(isFront ? 'front' : 'back');
                    flipTimeout = null;
                }, ANIMATION_DURATION + 80);
            }

            function resetCounters() {
                if (isFlipping) return; // 翻转中不重置
                frontCount = 0;
                backCount = 0;
                updateStats();
                // 可选：重置结果文字
                hideResult();
                hintText.textContent = '👆 点击硬币开始抛掷';
                hintText.classList.remove('hidden');
            }

            // 事件绑定
            perspectiveContainer.addEventListener('click', function(e) {
                e.preventDefault();
                flipCoin();
            });

            perspectiveContainer.addEventListener('keydown', function(e) {
                if (e.key === 'Enter' || e.key === ' ') {
                    e.preventDefault();
                    flipCoin();
                }
            });

            perspectiveContainer.addEventListener('touchstart', function(e) {
                // 保留触摸反馈
            }, { passive: true });

            perspectiveContainer.addEventListener('dblclick', function(e) {
                e.preventDefault();
                if (!isFlipping) {
                    currentRotation = 0;
                    coin.style.transform = 'rotateY(0deg)';
                    hideResult();
                    hintText.textContent = '👆 点击硬币开始抛掷';
                    hintText.classList.remove('hidden');
                    perspectiveContainer.style.cursor = 'pointer';
                    coinShadow.classList.remove('active');
                }
            });

            resetBtn.addEventListener('click', function(e) {
                e.preventDefault();
                resetCounters();
            });

            // 阻止折叠菜单上的点击事件冒泡到硬币区域（确保summary点击不会误触）
            const statsDetails = document.getElementById('statsDetails');
            statsDetails.addEventListener('click', function(e) {
                e.stopPropagation();
            });

            // 初始化
            function init() {
                coin.style.transform = 'rotateY(0deg)';
                coin.style.transition = 'transform ' + ANIMATION_DURATION + 'ms ' + EASE_CURVE;
                coinShadow.style.transition = 'all ' + ANIMATION_DURATION + 'ms ' + EASE_CURVE;
                resultText.style.transition = 'opacity 0.5s ease, color 0.4s ease';
                hintText.style.transition = 'opacity 0.4s ease';
                updateStats();
                console.log('抛硬币已就绪！点击硬币开始。');
            }

            if (document.readyState === 'loading') {
                document.addEventListener('DOMContentLoaded', init);
            } else {
                init();
            }

            document.addEventListener('visibilitychange', function() {
                if (document.hidden && isFlipping) {
                    if (flipTimeout) {
                        clearTimeout(flipTimeout);
                        flipTimeout = null;
                    }
                    isFlipping = false;
                    coin.classList.remove('flipping');
                    coinShadow.classList.remove('active');
                    perspectiveContainer.style.cursor = 'pointer';
                    hintText.classList.remove('hidden');
                    hintText.textContent = '👆 再抛一次？';
                }
            });

        })();
    </script>
</body>
</html>
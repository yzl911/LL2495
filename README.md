<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LL2495 前端Demo合集</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            width: 100vw;
            min-height: 100vh;
            background: #0f172a;
            font-family: Arial, sans-serif;
            padding: 40px 15px;
        }

        /* ========== 可拖动计算器窗口样式 ========== */
        .calculator-window {
            position: absolute;
            top: 50px;
            left: 50px;
            width: 320px;
            background: #1e293b;
            border-radius: 12px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.4);
            z-index: 1000;
            user-select: none;
            overflow: hidden;
        }
        .calc-header {
            padding: 14px 16px;
            background: #334155;
            color: #fff;
            cursor: move;
            font-weight: bold;
            font-size: 16px;
            text-align: center;
        }
        .calc-display {
            padding: 20px 16px;
            text-align: right;
            font-size: 32px;
            color: #fff;
            background: #0f172a;
            font-family: 'Courier New', monospace;
            word-break: break-all;
            min-height: 70px;
            display: flex;
            align-items: center;
            justify-content: flex-end;
        }
        .calc-buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 8px;
            padding: 12px;
        }
        .calc-btn {
            padding: 16px;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            cursor: pointer;
            transition: all 0.15s ease;
            font-weight: 500;
        }
        .calc-btn:hover {
            opacity: 0.85;
            transform: translateY(-1px);
        }
        .calc-btn:active {
            transform: translateY(0);
        }
        .btn-number {
            background: #475569;
            color: #fff;
        }
        .btn-operator {
            background: #f59e0b;
            color: #fff;
        }
        .btn-clear {
            background: #ef4444;
            color: #fff;
        }
        .btn-backspace {
            background: #64748b;
            color: #fff;
        }
        .btn-equals {
            background: #10b981;
            color: #fff;
        }
        .btn-zero {
            grid-column: span 2;
        }

        /* ========== 数字时钟样式 ========== */
        .clock-section {
            text-align: center;
            margin: 80px 0 60px;
        }
        .clock-date {
            color: #94a3b8;
            font-size: 26px;
            margin-bottom: 15px;
        }
        .clock-time {
            font-size: 80px;
            color: #38bdf8;
            letter-spacing: 6px;
            text-shadow: 0 0 12px #38bdf8;
        }

        /* ========== 第一套相册样式（在线相册） ========== */
        .gallery-section-1 h1 {
            color: #fff;
            text-align: center;
            margin-bottom: 40px;
        }
        .photo-gallery {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(240px,1fr));
            gap: 16px;
        }
        .photo-item {
            border-radius: 10px;
            overflow: hidden;
            cursor: pointer;
            transition: all 0.25s ease;
            background: #1e293b;
            height: 220px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #94a3b8;
        }
        .photo-item:hover {
            transform: scale(1.04);
        }
        .photo-item img {
            width: 100%;
            height: 220px;
            object-fit: cover;
            display: block;
        }
        /* 点击放大弹窗 - 第一套 */
        .preview-box {
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.92);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 999;
            padding: 20px;
        }
        .preview-box img {
            max-width: 95%;
            max-height: 95%;
            border-radius: 6px;
        }
        .preview-box .close {
            position: absolute;
            top: 20px;
            right: 30px;
            color: #fff;
            font-size: 35px;
            cursor: pointer;
        }

        /* ========== 第二套相册样式（本地相册） ========== */
        .gallery-section-2 {
            margin-top: 80px;
        }
        .gallery-section-2 h2 {
            color: #fff;
            text-align: center;
            margin-bottom: 30px;
        }
        .gallery {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 18px;
        }
        .img-item {
            border-radius: 8px;
            overflow: hidden;
            cursor: pointer;
            transition: transform 0.2s ease;
            background: #1e293b;
            height: 200px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #94a3b8;
        }
        .img-item:hover {
            transform: scale(1.05);
        }
        .img-item img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            display: block;
        }
        /* 大图弹窗 - 第二套 */
        .mask {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 999;
        }
        .mask img {
            max-width: 95%;
            max-height: 95vh;
        }
        .close-btn {
            position: absolute;
            top: 20px;
            right: 30px;
            font-size: 40px;
            color: #fff;
            cursor: pointer;
        }

        /* ========== 计时器样式 ========== */
        .timer-section {
            margin: 80px 0;
            text-align: center;
        }
        .timer-text {
            font-size: 80px;
            color: #ff9500;
            letter-spacing: 4px;
            text-shadow: 0 0 12px #ff9500;
            margin-bottom: 30px;
        }
        .btn-group button {
            font-size: 18px;
            padding: 10px 24px;
            margin: 0 8px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            color: #fff;
            transition: opacity 0.2s;
        }
        .btn-group button:hover {
            opacity: 0.9;
        }
        #startBtn {
            background-color: #2ecc71;
        }
        #pauseBtn {
            background-color: #f39c12;
        }
        #resetBtn {
            background-color: #e74c3c;
        }
    </style>
</head>
<body>

    <!-- 可拖动计算器窗口 -->
    <div class="calculator-window" id="calcWin">
        <div class="calc-header" id="calcHeader">🧮 计算器（拖动标题栏移动）</div>
        <div class="calc-display" id="calcDisplay">0</div>
        <div class="calc-buttons">
            <button class="calc-btn btn-clear" onclick="clearCalc()">C</button>
            <button class="calc-btn btn-backspace" onclick="backspace()">←</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('%')">%</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('/')">÷</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('7')">7</button>
            <button class="calc-btn btn-number" onclick="appendNumber('8')">8</button>
            <button class="calc-btn btn-number" onclick="appendNumber('9')">9</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('*')">×</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('4')">4</button>
            <button class="calc-btn btn-number" onclick="appendNumber('5')">5</button>
            <button class="calc-btn btn-number" onclick="appendNumber('6')">6</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('-')">−</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('1')">1</button>
            <button class="calc-btn btn-number" onclick="appendNumber('2')">2</button>
            <button class="calc-btn btn-number" onclick="appendNumber('3')">3</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('+')">+</button>
            
            <button class="calc-btn btn-number btn-zero" onclick="appendNumber('0')">0</button>
            <button class="calc-btn btn-number" onclick="appendNumber('.')">.</button>
            <button class="calc-btn btn-equals" onclick="calculate()">=</button>
        </div>
    </div>

    <!-- 数字时钟 -->
    <div class="clock-section">
        <div class="clock-date" id="dateBox"></div>
        <div class="clock-time" id="timeBox"></div>
    </div>

    <!-- 第一套相册（在线相册） -->
    <div class="gallery-section-1">
        <h1>我的相册</h1>
        <div class="photo-gallery">
            <div class="photo-item" onclick="openPreview(this)">
                <img src="https://picsum.photos/400/300?random=1" alt="图片1">
            </div>
            <div class="photo-item" onclick="openPreview(this)">
                <img src="https://picsum.photos/400/300?random=2" alt="图片2">
            </div>
            <div class="photo-item" onclick="openPreview(this)">
                <img src="https://picsum.photos/400/300?random=3" alt="图片3">
            </div>
            <div class="photo-item" onclick="openPreview(this)">
                <img src="https://picsum.photos/400/300?random=4" alt="图片4">
            </div>
        </div>
    </div>

    <!-- 第一套相册的放大弹窗 -->
    <div class="preview-box" id="preview">
        <span class="close" onclick="closePreview()">×</span>
        <img id="previewImg" alt="大图预览">
    </div>

    <!-- 第二套相册（本地相册） -->
    <div class="gallery-section-2">
        <h2>我的本地相册</h2>
        <div class="gallery">
            <div class="img-item" onclick="openBigImg(this)">
                <img src="1.jpg" alt="本地图片1">
            </div>
            <div class="img-item" onclick="openBigImg(this)">
                <img src="2.jpg" alt="本地图片2">
            </div>
            <div class="img-item" onclick="openBigImg(this)">
                <img src="3.jpg" alt="本地图片3">
            </div>
        </div>
    </div>

    <!-- 第二套相册的放大弹窗 -->
    <div class="mask" id="mask">
        <span class="close-btn" onclick="closeImg()">×</span>
        <img id="bigImage" alt="大图预览">
    </div>

    <!-- 计时器 -->
    <div class="timer-section">
        <div class="timer-text" id="stopTime">00:00:00.00</div>
        <div class="btn-group">
            <button id="startBtn">开始</button>
            <button id="pauseBtn">暂停</button>
            <button id="resetBtn">重置</button>
        </div>
    </div>

    <script>
        // ========== 拖动计算器窗口功能 ==========
        (function() {
            let ox, oy;
            const el = document.getElementById('calcWin');
            const header = document.getElementById('calcHeader');

            header.onmousedown = function(e) {
                ox = e.clientX - el.offsetLeft;
                oy = e.clientY - el.offsetTop;
                document.onmousemove = function(e) {
                    el.style.left = e.clientX - ox + 'px';
                    el.style.top = e.clientY - oy + 'px';
                };
                document.onmouseup = function() {
                    document.onmousemove = null;
                    document.onmouseup = null;
                };
                e.preventDefault(); // 防止拖动时选中文本
            };
        })();

        // ========== 计算器功能 ==========
        let calcExpression = '';
        const calcDisplay = document.getElementById('calcDisplay');

        function updateDisplay() {
            calcDisplay.textContent = calcExpression || '0';
        }

        function appendNumber(num) {
            // 防止多个小数点
            if (num === '.' && calcExpression.split(/[\+\-\*\/\%]/).pop().includes('.')) {
                return;
            }
            // 开头是0的情况，除非是小数点
            if (calcExpression === '0' && num !== '.') {
                calcExpression = num;
            } else {
                calcExpression += num;
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (calcExpression === '') return;
            // 如果最后一个是运算符，直接替换
            const lastChar = calcExpression.slice(-1);
            if (['+', '-', '*', '/', '%'].includes(lastChar)) {
                calcExpression = calcExpression.slice(0, -1) + op;
            } else {
                calcExpression += op;
            }
            updateDisplay();
        }

        function clearCalc() {
            calcExpression = '';
            updateDisplay();
        }

        function backspace() {
            calcExpression = calcExpression.slice(0, -1);
            updateDisplay();
        }

        function calculate() {
            try {
                let result = eval(calcExpression);
                // 处理浮点数精度问题，保留8位有效数字
                result = Math.round(result * 100000000) / 100000000;
                calcExpression = result.toString();
                updateDisplay();
            } catch (e) {
                calcDisplay.textContent = '错误';
                calcExpression = '';
            }
        }

        // ========== 数字时钟功能 ==========
        function syncClock(){
            let now = new Date();
            let year = now.getFullYear();
            let month = String(now.getMonth()+1).padStart(2,"0");
            let day = String(now.getDate()).padStart(2,"0");
            let weekArr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
            let week = weekArr[now.getDay()];

            let h = String(now.getHours()).padStart(2,"0");
            let m = String(now.getMinutes()).padStart(2,"0");
            let s = String(now.getSeconds()).padStart(2,"0");

            document.getElementById("dateBox").innerText = `${year}年${month}月${day}日 ${week}`;
            document.getElementById("timeBox").innerText = `${h}:${m}:${s}`;
        }
        syncClock();
        setInterval(syncClock, 1000);

        // ========== 第一套相册JS ==========
        const preview = document.getElementById("preview");
        const previewImg = document.getElementById("previewImg");
        
        function openPreview(el){
            previewImg.src = el.querySelector('img').src;
            preview.style.display = "flex";
        }
        
        function closePreview(){
            preview.style.display = "none";
        }
        
        preview.addEventListener('click', e => {
            if(e.target === preview) closePreview();
        });

        // ========== 第二套相册JS ==========
        const mask = document.getElementById('mask');
        const bigImg = document.getElementById('bigImage');
        
        function openBigImg(dom) {
            bigImg.src = dom.querySelector('img').src;
            mask.style.display = 'flex';
        }
        
        function closeImg() {
            mask.style.display = 'none';
        }
        
        mask.addEventListener('click', (e) => {
            if (e.target === mask) closeImg();
        });

        // ========== 计时器功能 ==========
        let timer = null;
        let startTime = 0;
        let elapsedTime = 0;
        let running = false;
        const stopDom = document.getElementById('stopTime');
        const startBtn = document.getElementById('startBtn');
        const pauseBtn = document.getElementById('pauseBtn');
        const resetBtn = document.getElementById('resetBtn');

        // 格式化时间 时:分:秒.毫秒
        function formatTime(ms) {
            const totalSec = Math.floor(ms / 1000);
            const hour = String(Math.floor(totalSec / 3600)).padStart(2, '0');
            const min = String(Math.floor((totalSec % 3600) / 60)).padStart(2, '0');
            const sec = String(totalSec % 60).padStart(2, '0');
            const msec = String(Math.floor((ms % 1000) / 10)).padStart(2, '0');
            return `${hour}:${min}:${sec}.${msec}`;
        }

        function updateTimer() {
            elapsedTime = Date.now() - startTime;
            stopDom.textContent = formatTime(elapsedTime);
        }

        startBtn.onclick = () => {
            if (!running) {
                running = true;
                startTime = Date.now() - elapsedTime;
                timer = setInterval(updateTimer, 10);
            }
        }

        pauseBtn.onclick = () => {
            if (running) {
                running = false;
                clearInterval(timer);
            }
        }

        resetBtn.onclick = () => {
            clearInterval(timer);
            running = false;
            elapsedTime = 0;
            stopDom.textContent = "00:00:00.00";
        }
    </script>
</body>
</html>

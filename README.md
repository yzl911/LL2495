<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LL2495 工具合集</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            background: #0f172a;
            font-family: Arial, sans-serif;
            padding: 40px 15px;
        }

        /* ========== 可拖动窗口通用样式 ========== */
        .draggable-window {
            position: absolute;
            background: #1e293b;
            border-radius: 12px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.4);
            z-index: 1000;
            user-select: none;
            overflow: hidden;
        }
        .window-header {
            padding: 14px 16px;
            background: #334155;
            color: #fff;
            cursor: move;
            font-weight: bold;
            font-size: 16px;
            text-align: center;
        }

        /* ========== 计算器 ========== */
        #calcWin {
            top: 50px;
            left: 50px;
            width: 320px;
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
            color: #fff;
        }
        .calc-btn:hover { opacity: 0.85; transform: translateY(-1px); }
        .calc-btn:active { transform: translateY(0); }
        .btn-number { background: #475569; }
        .btn-operator { background: #f59e0b; }
        .btn-clear { background: #ef4444; }
        .btn-backspace { background: #64748b; }
        .btn-equals { background: #10b981; }
        .btn-zero { grid-column: span 2; }

        /* ========== 记事本 ========== */
        #notepadWin {
            top: 50px;
            right: 50px;
            width: 350px;
        }
        .notepad-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .notepad-clear-btn {
            background: #ef4444;
            color: #fff;
            border: none;
            padding: 4px 10px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 12px;
            transition: opacity 0.2s;
        }
        .notepad-clear-btn:hover { opacity: 0.8; }
        .notepad-content { padding: 12px; }
        #notepadText {
            width: 100%;
            height: 280px;
            background: #0f172a;
            color: #e2e8f0;
            border: 1px solid #334155;
            border-radius: 8px;
            padding: 12px;
            font-size: 14px;
            line-height: 1.6;
            resize: none;
            outline: none;
        }
        #notepadText:focus { border-color: #38bdf8; }
        .notepad-status {
            text-align: right;
            font-size: 12px;
            color: #94a3b8;
            margin-top: 8px;
            padding-right: 4px;
        }

        /* ========== 中央搜索框 ========== */
        .search-container {
            max-width: 600px;
            margin: 120px auto 60px;
            text-align: center;
        }
        .search-title {
            color: #fff;
            font-size: 48px;
            margin-bottom: 30px;
            font-weight: 300;
            letter-spacing: 2px;
        }
        .search-form {
            display: flex;
            gap: 10px;
        }
        .search-input {
            flex: 1;
            padding: 14px 20px;
            border: 2px solid #334155;
            border-radius: 30px;
            background: #1e293b;
            color: #fff;
            font-size: 16px;
            outline: none;
            transition: border-color 0.2s;
        }
        .search-input:focus {
            border-color: #38bdf8;
        }
        .search-btn {
            padding: 14px 30px;
            border: none;
            border-radius: 30px;
            background: #38bdf8;
            color: #0f172a;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
        }
        .search-btn:hover {
            background: #0ea5e9;
            transform: translateY(-1px);
        }

        /* ========== 数字时钟 ========== */
        .clock-section {
            text-align: center;
            margin-bottom: 60px;
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

        /* ========== 计时器 ========== */
        .timer-section {
            text-align: center;
            margin-bottom: 40px;
        }
        .timer-text {
            font-size: 60px;
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
        .btn-group button:hover { opacity: 0.9; }
        #startBtn { background-color: #2ecc71; }
        #pauseBtn { background-color: #f39c12; }
        #resetBtn { background-color: #e74c3c; }
    </style>
</head>
<body>

    <!-- 计算器窗口 -->
    <div class="draggable-window" id="calcWin">
        <div class="window-header calc-header">🧮 计算器</div>
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

    <!-- 记事本窗口 -->
    <div class="draggable-window" id="notepadWin">
        <div class="window-header notepad-header">
            <span>📝 便签</span>
            <button class="notepad-clear-btn" onclick="clearNotepad()">清空</button>
        </div>
        <div class="notepad-content">
            <textarea id="notepadText" placeholder="输入内容自动保存..."></textarea>
            <div class="notepad-status" id="notepadStatus">已保存</div>
        </div>
    </div>

    <!-- 中央搜索框 -->
    <div class="search-container">
        <h1 class="search-title">Google 搜索</h1>
        <form class="search-form" onsubmit="googleSearch(event)">
            <input type="text" class="search-input" id="searchInput" placeholder="输入搜索内容..." autofocus>
            <button type="submit" class="search-btn">搜索</button>
        </form>
    </div>

    <!-- 数字时钟 -->
    <div class="clock-section">
        <div class="clock-date" id="dateBox"></div>
        <div class="clock-time" id="timeBox"></div>
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
        // ========== 通用拖动功能 ==========
        function makeDraggable(windowId, headerSelector) {
            const el = document.getElementById(windowId);
            const header = el.querySelector(headerSelector);
            
            header.onmousedown = function(e) {
                // 点击按钮时不触发拖动
                if (e.target.tagName === 'BUTTON') return;
                
                const ox = e.clientX - el.offsetLeft;
                const oy = e.clientY - el.offsetTop;
                
                document.onmousemove = function(e) {
                    el.style.left = e.clientX - ox + 'px';
                    el.style.top = e.clientY - oy + 'px';
                };
                document.onmouseup = function() {
                    document.onmousemove = null;
                    document.onmouseup = null;
                };
                e.preventDefault();
            };
        }
        makeDraggable('calcWin', '.calc-header');
        makeDraggable('notepadWin', '.notepad-header');

        // ========== 计算器功能 ==========
        let calcExpression = '';
        const calcDisplay = document.getElementById('calcDisplay');

        function updateDisplay() {
            calcDisplay.textContent = calcExpression || '0';
        }

        function appendNumber(num) {
            if (num === '.' && calcExpression.split(/[\+\-\*\/\%]/).pop().includes('.')) return;
            if (calcExpression === '0' && num !== '.') {
                calcExpression = num;
            } else {
                calcExpression += num;
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (calcExpression === '') return;
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
                result = Math.round(result * 100000000) / 100000000;
                calcExpression = result.toString();
                updateDisplay();
            } catch (e) {
                calcDisplay.textContent = '错误';
                calcExpression = '';
            }
        }

        // ========== 记事本功能 ==========
        const notepadText = document.getElementById('notepadText');
        const notepadStatus = document.getElementById('notepadStatus');
        let saveTimer = null;

        function loadNotepad() {
            const saved = localStorage.getItem('notepad_content');
            if (saved) notepadText.value = saved;
        }

        function autoSave() {
            notepadStatus.textContent = '保存中...';
            clearTimeout(saveTimer);
            saveTimer = setTimeout(() => {
                localStorage.setItem('notepad_content', notepadText.value);
                notepadStatus.textContent = '已保存';
            }, 500);
        }

        function clearNotepad() {
            if (confirm('确定清空所有内容？')) {
                notepadText.value = '';
                localStorage.removeItem('notepad_content');
                notepadStatus.textContent = '已清空';
            }
        }

        notepadText.addEventListener('input', autoSave);
        loadNotepad();

        // ========== 谷歌搜索功能 ==========
        function googleSearch(e) {
            e.preventDefault();
            const query = document.getElementById('searchInput').value.trim();
            if (query) {
                window.open(`https://www.google.com/search?q=${encodeURIComponent(query)}`, '_blank');
            }
        }

        // ========== 数字时钟功能 ==========
        function syncClock(){
            const now = new Date();
            const year = now.getFullYear();
            const month = String(now.getMonth()+1).padStart(2,"0");
            const day = String(now.getDate()).padStart(2,"0");
            const weekArr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
            const week = weekArr[now.getDay()];
            const h = String(now.getHours()).padStart(2,"0");
            const m = String(now.getMinutes()).padStart(2,"0");
            const s = String(now.getSeconds()).padStart(2,"0");

            document.getElementById("dateBox").innerText = `${year}年${month}月${day}日 ${week}`;
            document.getElementById("timeBox").innerText = `${h}:${m}:${s}`;
        }
        syncClock();
        setInterval(syncClock, 1000);

        // ========== 计时器功能 ==========
        let timer = null;
        let startTime = 0;
        let elapsedTime = 0;
        let running = false;
        const stopDom = document.getElementById('stopTime');
        const startBtn = document.getElementById('startBtn');
        const pauseBtn = document.getElementById('pauseBtn');
        const resetBtn = document.getElementById('resetBtn');

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

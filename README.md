<!DOCTYPE html>
<head><meta charset="UTF-8"><title>可拖动窗口</title></head>
<body>

<!-- ===== 可拖动窗口 ===== -->
<div id="win" style="position:fixed;width:320px;background:#fff;border-radius:10px;box-shadow:0 8px 30px rgba(0,0,0,.25);top:60px;left:60px;font-family:system-ui;overflow:hidden;">
  <!-- 标题栏（拖动手柄） -->
  <div id="bar" style="height:40px;background:linear-gradient(135deg,#667eea,#764ba2);color:#fff;line-height:40px;padding:0 18px;cursor:grab;user-select:none;font-weight:600;letter-spacing:.3px;"
       onmousedown="d(event)">✧ 拖动我</div>
  <!-- 内容 -->
  <div style="padding:24px 20px 28px;color:#333;background:#fafafa;border-top:1px solid #eee;">
    <p style="margin:0 0 8px;font-size:15px;">内容区域 · 点击标题栏拖动</p>
    <p style="margin:0;font-size:13px;color:#888;">松开鼠标停止拖动</p>
  </div>
</div>

<script>
  // —— 最简拖动 ——
  let ox, oy, el = win;
  function d(e) {
    ox = e.clientX - el.offsetLeft;
    oy = e.clientY - el.offsetTop;
    document.onmousemove = function(e) {
      el.style.left = e.clientX - ox + 'px';
      el.style.top = e.clientY - oy + 'px';
    };
    document.onmouseup = function() { document.onmousemove = null; };
  }
</script>

</body>
  <body>
  <h1>yzl</h1>
  <h2>Introduction</h2>
  <p>Hello world！</p>
  <img src="20260706_030040742_iOS.heic"/>
  </body>
  <body>
  (链接)
  <a href="https://aka.ms/AnaheimRW/ad6-douyin-cid116-pid2/Jan26">label</a>
  <p style="color: red">This text is red</p>
  <body style="font-family: Helvetica, Noto Sans, sans-serif">
  <h1 style="margin: 4px;">thomasOS</h1>

<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>居中同步数字时钟</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        body{
            width: 100vw;
            height: 100vh;
            /* flex 实现页面水平+垂直居中 */
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: #0f172a;
            font-family: Arial, sans-serif;
        }
        .clock-date{
            color: #94a3b8;
            font-size: 26px;
            margin-bottom: 15px;
        }
        .clock-time{
            font-size: 80px;
            color: #38bdf8;
            letter-spacing: 6px;
            text-shadow: 0 0 12px #38bdf8;
        }
    </style>
</head>
<body>
    <div class="clock-date" id="dateBox"></div>
    <div class="clock-time" id="timeBox"></div>

    <script>
        function syncClock(){
            let now = new Date();
            // 获取年、月、日、星期
            let year = now.getFullYear();
            let month = String(now.getMonth()+1).padStart(2,"0");
            let day = String(now.getDate()).padStart(2,"0");
            let weekArr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
            let week = weekArr[now.getDay()];

            // 时分秒自动补零
            let h = String(now.getHours()).padStart(2,"0");
            let m = String(now.getMinutes()).padStart(2,"0");
            let s = String(now.getSeconds()).padStart(2,"0");

            // 赋值到页面
            document.getElementById("dateBox").innerText = `${year}年${month}月${day}日 ${week}`;
            document.getElementById("timeBox").innerText = `${h}:${m}:${s}`;
        }

        syncClock(); // 打开页面立刻显示时间
        setInterval(syncClock, 1000); // 每隔1秒自动同步刷新时间
    </script>
</body>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的在线相册</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:system-ui}
        body{background:#121212;padding:30px 15px}
        h1{color:#fff;text-align:center;margin-bottom:40px}
        /* 相册网格 */
        .photo-gallery{
            max-width:1200px;
            margin:0 auto;
            display:grid;
            grid-template-columns: repeat(auto-fill, minmax(240px,1fr));
            gap:16px;
        }
        .photo-item{
            border-radius:10px;
            overflow:hidden;
            cursor:pointer;
            transition:all 0.25s ease;
        }
        .photo-item:hover{transform:scale(1.04)}
        .photo-item img{width:100%;height:220px;object-fit:cover;display:block}
        /* 点击放大弹窗 */
        .preview-box{
            position:fixed;
            inset:0;
            background:rgba(0,0,0,0.92);
            display:none;
            align-items:center;
            justify-content:center;
            z-index:999;
            padding:20px;
        }
        .preview-box img{max-width:95%;max-height:95%;border-radius:6px}
        .preview-box .close{
            position:absolute;
            top:20px;right:30px;
            color:#fff;font-size:35px;cursor:pointer;
        }
    </style>
</head>
<body>
    <h1>我的相册</h1>
    <div class="photo-gallery">
        <!-- 替换成你的图片网络地址，本地图片上线后必须用图片外链 -->
        <div class="photo-item" onclick="openPreview(this)"><img src="https://picsum.photos/id/1015/600/600"></div>
        <div class="photo-item" onclick="openPreview(this)"><img src="https://picsum.photos/id/1018/600/600"></div>
        <div class="photo-item" onclick="openPreview(this)"><img src="https://picsum.photos/id/1036/600/600"></div>
        <div class="photo-item" onclick="openPreview(this)"><img src="https://picsum.photos/id/1039/600/600"></div>
    </div>

    <div class="preview-box" id="preview">
        <span class="close" onclick="closePreview()">×</span>
        <img id="previewImg">
    </div>

    <script>
        const preview = document.getElementById("preview");
        const previewImg = document.getElementById("previewImg");
        function openPreview(el){
            previewImg.src = el.querySelector('img').src;
            preview.style.display = "flex";
        }
        function closePreview(){
            preview.style.display = "none";
        }
        // 点击黑色背景关闭大图
        preview.addEventListener('click',e=>{
            if(e.target===preview) closePreview();
        })
    </script>
</body>
</html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>居中同步数字时钟</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        body{
            width: 100vw;
            min-height: 100vh;
            background: #0f172a;
            font-family: Arial, sans-serif;
            padding: 40px 15px;
        }
        /* 原有时钟样式 */
        .clock-date{
            color: #94a3b8;
            font-size: 26px;
            margin-bottom: 15px;
            text-align: center;
        }
        .clock-time{
            font-size: 80px;
            color: #38bdf8;
            letter-spacing: 6px;
            text-shadow: 0 0 12px #38bdf8;
            text-align: center;
            margin-bottom: 60px;
        }

        /* 新增相册样式 */
        h2{
            color:#fff;
            text-align:center;
            margin-bottom:30px;
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
        /* 大图弹窗 */
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
    </style>
</head>
<body>
    <!-- 原本时钟区域 -->
    <div class="clock-date" id="dateBox"></div>
    <div class="clock-time" id="timeBox"></div>

    <!-- 新增本地相册区域 -->
    <h2>我的本地相册</h2>
    <div class="gallery">
        <div class="img-item" onclick="openBigImg(this)">
            <img src="1.jpg">
        </div>
        <div class="img-item" onclick="openBigImg(this)">
            <img src="2.jpg">
        </div>
        <div class="img-item" onclick="openBigImg(this)">
            <img src="3.jpg">
        </div>
    </div>

    <!-- 图片放大弹窗 -->
    <div class="mask" id="mask">
        <span class="close-btn" onclick="closeImg()">×</span>
        <img id="bigImage">
    </div>

    <script>
        // 原有时钟代码（保持原样）
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

        // 相册功能JS代码
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
        })
    </script>
</body>
<head>
<mead charset="UTF-8>
<meta name=" content="width=device-width,initial-scale=1.0">
<title>计时器</title>
<style>
     * {
        margin:0;
        padding:0;
        box-sizing:bordorder-box;
         }
        body {
            width:100vw;
            height:100vh;
            background:#0f172a;
            display:flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-family: Arial, sans-serif;
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
    <div class="timer-text" id="stopTime">00:00:00.00</div>
    <div class="btn-group">
        <button id="startBtn">开始</button>
        <button id="pauseBtn">暂停</button>
        <button id="resetBtn">重置</button>
    </div>

    <script>
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

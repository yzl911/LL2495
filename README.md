<!DOCTYPE html>
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
</html>

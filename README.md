<html lang="th">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ClassFocus - Focus Timer</title>
  <script src="/_sdk/element_sdk.js"></script>
  <style>
    body {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #E3F2FD 0%, #F5F5F5 100%);
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .app-container {
      width: 100%;
      max-width: 500px;
      padding: 40px 30px;
      text-align: center;
    }

    .header {
      margin-bottom: 30px;
    }

    .app-title {
      font-size: 32px;
      font-weight: 700;
      color: #1976D2;
      margin: 0 0 10px 0;
      letter-spacing: -0.5px;
    }

    .app-subtitle {
      font-size: 14px;
      color: #64B5F6;
      margin: 0;
      font-weight: 500;
    }

    .timer-container {
      position: relative;
      margin: 40px auto;
    }

    .timer-circle {
      width: 280px;
      height: 280px;
      margin: 0 auto;
      background: linear-gradient(145deg, #ffffff, #f0f0f0);
      border-radius: 50%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      box-shadow: 
        0 10px 30px rgba(33, 150, 243, 0.15),
        inset 0 -5px 15px rgba(0, 0, 0, 0.05);
      position: relative;
      overflow: hidden;
    }

    .timer-circle::before {
      content: '';
      position: absolute;
      top: -2px;
      left: -2px;
      right: -2px;
      bottom: -2px;
      background: linear-gradient(135deg, #64B5F6, #90CAF9);
      border-radius: 50%;
      z-index: -1;
      opacity: 0.3;
    }

    .timer-display {
      font-size: 56px;
      font-weight: 700;
      color: #1976D2;
      margin: 0;
      line-height: 1;
      font-variant-numeric: tabular-nums;
    }

    .timer-status {
      font-size: 16px;
      color: #64B5F6;
      margin-top: 12px;
      font-weight: 500;
    }

    .icon-focus {
      font-size: 36px;
      margin-bottom: 8px;
    }

    .controls {
      display: flex;
      gap: 15px;
      justify-content: center;
      margin-top: 30px;
    }

    .btn {
      padding: 14px 32px;
      border: none;
      border-radius: 25px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    .btn-primary {
      background: linear-gradient(135deg, #42A5F5, #2196F3);
      color: white;
    }

    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 16px rgba(33, 150, 243, 0.3);
    }

    .btn-secondary {
      background: white;
      color: #42A5F5;
      border: 2px solid #42A5F5;
    }

    .btn-secondary:hover {
      background: #E3F2FD;
    }

    .stats-container {
      display: flex;
      gap: 20px;
      justify-content: center;
      margin-top: 40px;
    }

    .stat-card {
      background: white;
      padding: 20px 30px;
      border-radius: 20px;
      box-shadow: 0 4px 15px rgba(33, 150, 243, 0.1);
      min-width: 140px;
    }

    .stat-icon {
      font-size: 28px;
      margin-bottom: 8px;
    }

    .stat-value {
      font-size: 28px;
      font-weight: 700;
      color: #1976D2;
      margin: 5px 0;
    }

    .stat-label {
      font-size: 13px;
      color: #90CAF9;
      font-weight: 500;
    }

    .gamification-info {
      background: linear-gradient(135deg, #FFF9C4, #FFF59D);
      padding: 16px 24px;
      border-radius: 20px;
      margin-top: 30px;
      box-shadow: 0 4px 12px rgba(255, 193, 7, 0.2);
      border: 2px solid #FFE082;
    }

    .gamification-info .emoji {
      font-size: 24px;
      margin-right: 8px;
    }

    .gamification-info .text {
      font-size: 15px;
      color: #F57F17;
      font-weight: 600;
    }

    .warning-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 1000;
      animation: fadeIn 0.3s ease;
    }

    .warning-overlay.show {
      display: flex;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-10px); }
      75% { transform: translateX(10px); }
    }

    .warning-modal {
      background: white;
      padding: 40px 50px;
      border-radius: 30px;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
      text-align: center;
      max-width: 400px;
      animation: shake 0.5s ease;
    }

    .warning-icon {
      font-size: 64px;
      margin-bottom: 20px;
    }

    .warning-title {
      font-size: 24px;
      font-weight: 700;
      color: #EF5350;
      margin: 0 0 15px 0;
    }

    .warning-message {
      font-size: 16px;
      color: #666;
      margin: 0 0 25px 0;
      line-height: 1.5;
    }

    .warning-timer {
      font-size: 48px;
      font-weight: 700;
      color: #1976D2;
      margin: 20px 0;
      opacity: 0.5;
    }

    .btn-back {
      background: linear-gradient(135deg, #66BB6A, #4CAF50);
      color: white;
      padding: 14px 40px;
      border: none;
      border-radius: 25px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(76, 175, 80, 0.3);
      transition: all 0.3s ease;
    }

    .btn-back:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 16px rgba(76, 175, 80, 0.4);
    }

    .pulse {
      animation: pulse 2s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }

    @media (max-width: 600px) {
      .app-container {
        padding: 30px 20px;
      }

      .timer-circle {
        width: 240px;
        height: 240px;
      }

      .timer-display {
        font-size: 48px;
      }

      .stats-container {
        flex-direction: column;
        gap: 15px;
      }

      .stat-card {
        min-width: auto;
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div class="app-container">
   <div class="header">
    <h1 class="app-title" id="app-title">ClassFocus</h1>
    <p class="app-subtitle">🎯 Focus Timer สำหรับห้องเรียน</p>
   </div>
   <div class="timer-container">
    <div class="timer-circle" id="timer-circle">
     <div class="icon-focus">
      🎓
     </div>
     <div class="timer-display" id="timer-display">
      00:00
     </div>
     <div class="timer-status" id="timer-status">
      พร้อมเริ่มโฟกัส
     </div>
    </div>
   </div>
   <div class="controls"><button class="btn btn-primary" id="start-btn">เริ่มโฟกัส</button> <button class="btn btn-secondary" id="reset-btn">รีเซ็ต</button>
   </div>
   <div class="stats-container">
    <div class="stat-card">
     <div class="stat-icon">
      ⭐
     </div>
     <div class="stat-value" id="points-display">
      0
     </div>
     <div class="stat-label" id="points-label">
      แต้มโฟกัส
     </div>
    </div>
    <div class="stat-card">
     <div class="stat-icon">
      🔥
     </div>
     <div class="stat-value" id="streak-display">
      0
     </div>
     <div class="stat-label">
      นาทีต่อเนื่อง
     </div>
    </div>
   </div>
   <div class="gamification-info"><span class="emoji">🏆</span> <span class="text" id="streak-message">โฟกัสต่อเนื่อง 5 นาที = +10 pts</span>
   </div>
  </div>
  <div class="warning-overlay" id="warning-overlay">
   <div class="warning-modal">
    <div class="warning-icon">
     ⚠️
    </div>
    <h2 class="warning-title" id="warning-title">⚠️ คุณออกจากหน้าเว็บ</h2>
    <p class="warning-message" id="warning-message">เวลาถูกหยุดแล้ว กรุณากลับมาโฟกัสต่อ</p>
    <div class="warning-timer" id="warning-timer">
     00:00
    </div><button class="btn-back" id="back-btn">กลับมาโฟกัสต่อ</button>
   </div>
  </div>
  <script>
    const defaultConfig = {
      app_title: "ClassFocus",
      focus_message: "กำลังโฟกัสในคาบ",
      points_label: "แต้มโฟกัส",
      streak_message: "โฟกัสต่อเนื่อง 5 นาที = +10 pts",
      warning_title: "⚠️ คุณออกจากหน้าเว็บ",
      warning_message: "เวลาถูกหยุดแล้ว กรุณากลับมาโฟกัสต่อ",
      background_color: "#E3F2FD",
      primary_color: "#42A5F5",
      text_color: "#1976D2",
      accent_color: "#64B5F6",
      warning_color: "#EF5350"
    };

    let config = defaultConfig;
    let timerInterval = null;
    let seconds = 0;
    let points = 0;
    let streak = 0;
    let isRunning = false;
    let wasTabVisible = true;

    const timerDisplay = document.getElementById('timer-display');
    const timerStatus = document.getElementById('timer-status');
    const startBtn = document.getElementById('start-btn');
    const resetBtn = document.getElementById('reset-btn');
    const pointsDisplay = document.getElementById('points-display');
    const streakDisplay = document.getElementById('streak-display');
    const warningOverlay = document.getElementById('warning-overlay');
    const warningTimer = document.getElementById('warning-timer');
    const backBtn = document.getElementById('back-btn');
    const timerCircle = document.getElementById('timer-circle');

    function formatTime(totalSeconds) {
      const mins = Math.floor(totalSeconds / 60);
      const secs = totalSeconds % 60;
      return `${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
    }

    function updateDisplay() {
      timerDisplay.textContent = formatTime(seconds);
      pointsDisplay.textContent = points;
      streakDisplay.textContent = Math.floor(seconds / 60);
    }

    function startTimer() {
      if (isRunning) return;
      
      isRunning = true;
      startBtn.textContent = 'หยุดชั่วคราว';
      timerStatus.textContent = config.focus_message || defaultConfig.focus_message;
      timerCircle.classList.add('pulse');
      
      timerInterval = setInterval(() => {
        seconds++;
        streak = Math.floor(seconds / 60);
        
        if (seconds % 60 === 0 && seconds > 0) {
          points += 2;
        }
        
        if (seconds % 300 === 0 && seconds > 0) {
          points += 10;
        }
        
        updateDisplay();
      }, 1000);
    }

    function pauseTimer() {
      if (!isRunning) return;
      
      isRunning = false;
      clearInterval(timerInterval);
      startBtn.textContent = 'เริ่มต่อ';
      timerStatus.textContent = 'หยุดชั่วคราว';
      timerCircle.classList.remove('pulse');
    }

    function resetTimer() {
      pauseTimer();
      seconds = 0;
      points = 0;
      streak = 0;
      startBtn.textContent = 'เริ่มโฟกัส';
      timerStatus.textContent = 'พร้อมเริ่มโฟกัส';
      updateDisplay();
    }

    function showWarning() {
      warningTimer.textContent = formatTime(seconds);
      warningOverlay.classList.add('show');
    }

    function hideWarning() {
      warningOverlay.classList.remove('show');
    }

    startBtn.addEventListener('click', () => {
      if (isRunning) {
        pauseTimer();
      } else {
        startTimer();
      }
    });

    resetBtn.addEventListener('click', resetTimer);

    backBtn.addEventListener('click', () => {
      hideWarning();
      startTimer();
    });

    document.addEventListener('visibilitychange', () => {
      if (document.hidden) {
        if (isRunning) {
          pauseTimer();
          showWarning();
          wasTabVisible = false;
        }
      } else {
        if (!wasTabVisible && !isRunning) {
          hideWarning();
        }
        wasTabVisible = true;
      }
    });

    window.addEventListener('blur', () => {
      if (isRunning) {
        pauseTimer();
        showWarning();
        wasTabVisible = false;
      }
    });

    async function onConfigChange(newConfig) {
      config = { ...defaultConfig, ...newConfig };
      
      document.getElementById('app-title').textContent = config.app_title || defaultConfig.app_title;
      document.getElementById('points-label').textContent = config.points_label || defaultConfig.points_label;
      document.getElementById('streak-message').textContent = config.streak_message || defaultConfig.streak_message;
      document.getElementById('warning-title').textContent = config.warning_title || defaultConfig.warning_title;
      document.getElementById('warning-message').textContent = config.warning_message || defaultConfig.warning_message;
      
      if (isRunning) {
        timerStatus.textContent = config.focus_message || defaultConfig.focus_message;
      }
      
      document.body.style.background = `linear-gradient(135deg, ${config.background_color || defaultConfig.background_color} 0%, #F5F5F5 100%)`;
      
      const buttons = document.querySelectorAll('.btn-primary');
      buttons.forEach(btn => {
        btn.style.background = `linear-gradient(135deg, ${config.primary_color || defaultConfig.primary_color}, ${config.text_color || defaultConfig.text_color})`;
      });
      
      const timerElements = document.querySelectorAll('.timer-display, .stat-value, .warning-timer');
      timerElements.forEach(el => {
        el.style.color = config.text_color || defaultConfig.text_color;
      });
      
      const accentElements = document.querySelectorAll('.timer-status, .stat-label, .app-subtitle');
      accentElements.forEach(el => {
        el.style.color = config.accent_color || defaultConfig.accent_color;
      });
    }

    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig,
        onConfigChange,
        mapToCapabilities: (cfg) => ({
          recolorables: [
            {
              get: () => cfg.background_color || defaultConfig.background_color,
              set: (value) => {
                cfg.background_color = value;
                window.elementSdk.setConfig({ background_color: value });
              }
            },
            {
              get: () => cfg.primary_color || defaultConfig.primary_color,
              set: (value) => {
                cfg.primary_color = value;
                window.elementSdk.setConfig({ primary_color: value });
              }
            },
            {
              get: () => cfg.text_color || defaultConfig.text_color,
              set: (value) => {
                cfg.text_color = value;
                window.elementSdk.setConfig({ text_color: value });
              }
            },
            {
              get: () => cfg.accent_color || defaultConfig.accent_color,
              set: (value) => {
                cfg.accent_color = value;
                window.elementSdk.setConfig({ accent_color: value });
              }
            }
          ],
          borderables: [],
          fontEditable: undefined,
          fontSizeable: undefined
        }),
        mapToEditPanelValues: (cfg) => new Map([
          ["app_title", cfg.app_title || defaultConfig.app_title],
          ["focus_message", cfg.focus_message || defaultConfig.focus_message],
          ["points_label", cfg.points_label || defaultConfig.points_label],
          ["streak_message", cfg.streak_message || defaultConfig.streak_message],
          ["warning_title", cfg.warning_title || defaultConfig.warning_title],
          ["warning_message", cfg.warning_message || defaultConfig.warning_message]
        ])
      });
    }

    updateDisplay();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a845c64f5de8995',t:'MTc2NDc3ODUwNy4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>

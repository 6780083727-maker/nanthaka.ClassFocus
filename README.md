<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>ClassFocus - Mockup</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- Google Fonts & some basic icons -->
  <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@400;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css">
  <style>
    body {
      font-family: 'Prompt', sans-serif;
      background: linear-gradient(135deg, #E9F5FE 0%, #FAFAFF 100%);
      margin: 0; padding: 0;
      color: #295872;
    }
    header {
      padding: 1.5rem;
      text-align: center;
      background: #B3E5FC;
      border-bottom: 1px solid #e0f7fa;
    }
    h1 {
      font-size: 2rem;
      margin: 0;
      font-weight: 700;
      display: flex; align-items: center; justify-content: center;
      gap: .5em;
    }
    .logo {
      display: inline-block;
      font-size: 1.8rem;
      background: #FFFFFF;
      border-radius: 1em;
      padding: 0.2em 0.5em;
      color: #6EC6FF;
      font-weight: bold;
      box-shadow: 0 2px 8px rgba(84,196,255,0.12);
      margin-right: 0.5em;
    }
    .container {
      max-width: 500px;
      margin: 2rem auto;
      background: #fff;
      border-radius: 24px;
      box-shadow: 0 4px 32px rgba(80,140,200,0.12);
      padding: 2rem 1.5rem 2rem 1.5rem;
    }
    .section-title {
      font-size: 1.2rem;
      margin: 1rem 0 .5rem .5rem;
      color: #3689B1;
      font-weight: bold;
    }
    /* Basic buttons */
    .btn {
      background: #6EC6FF;
      color: #fff;
      border-radius: 12px;
      border: none;
      font-size: 1rem;
      font-weight: 500;
      padding: .8em 2em;
      margin: .5em 0;
      cursor: pointer;
      box-shadow: 0 2px 6px rgba(80,196,255,0.09);
      transition: 0.3s;
    }
    .btn:active {background: #42A5F5;}
    .btn.outline {background: #fff; color: #6EC6FF; border: 2px solid #6EC6FF;}
    .info-card,.score-card,.dashboard-card {
      background: #F3F9FE;
      border-radius: 18px;
      margin: 1em 0;
      padding: 1em;
      box-shadow: 0 2px 8px rgba(80,171,255,.08);
    }
    .icon {
      font-size:2rem; vertical-align:middle;
      color: #64B5F6; margin-right: .5em;
    }
    .points-circle {
      display: inline-block;
      background: #FFF3E0;
      color: #FFA726;
      font-weight: bold;
      border-radius: 50%;
      width: 38px; height: 38px;
      text-align: center; line-height: 38px;
      margin:0 .3em;
      font-size:1.2rem;
    }
    .dashboard-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }
    /* Cute sticker for gamification mockup */
    .sticker {
      display: inline-block;
      font-size:2.3rem;
      margin: .2em;
      transform: rotate(-8deg);
    }
    /* For the focus mode timer */
    .focus-timer {
      font-size: 2.5rem;
      text-align: center;
      font-weight: 700;
      letter-spacing: .07rem;
      margin: 1rem 0 .8rem 0;
      color: #00BCD4;
    }
    /* Responsive */
    @media (max-width:600px){
      .container{max-width:100%;margin:1rem;}
      header{font-size:1.2rem;}
    }
  </style>
</head>
<body>
  <header>
    <h1>
      <span class="logo"><i class="bi bi-lightning"></i>ClassFocus</span>
      แอปเพิ่มสมาธิห้องเรียน
    </h1>
  </header>
  <!-- Tab sections (for example only) -->
  <div style="text-align:center;margin-top:.5em;">
    <button class="btn outline" onclick="showSection('student-main')">นักเรียน</button>
    <button class="btn outline" onclick="showSection('focus')">โฟกัส</button>
    <button class="btn outline" onclick="showSection('score')">คะแนน/รางวัล</button>
    <button class="btn outline" onclick="showSection('teacher-timer')">ครูควบคุมเวลา</button>
    <button class="btn outline" onclick="showSection('dashboard')">Dashboard ครู</button>
  </div>

  <!-- หน้าหลักนักเรียน -->
  <div id="student-main" class="container section">
    <div class="section-title"><i class="bi bi-house-heart icon"></i>หน้าหลักนักเรียน</div>
    <div class="info-card">
      <div style="font-size:1.1rem;">
        สวัสดี <b>นักเรียน!</b> วันนี้คุณโฟกัสได้ <span class="points-circle">63</span> นาที<br>
        คะแนนสะสม <span class="points-circle">120</span>
      </div>
      <hr style="margin:.7em 0;">
      <button class="btn" onclick="showSection('focus')"><i class="bi bi-lightning"></i> เริ่มโฟกัส</button>
      <button class="btn outline" onclick="showSection('score')"><i class="bi bi-gift"></i> รางวัลของฉัน</button>
      <button class="btn outline" onclick="showSection('homework')"><i class="bi bi-card-checklist"></i> งานที่ได้รับมอบหมาย</button>
    </div>
    <div class="info-card">
      <div style="font-size:1em;">
        <b>กิจกรรมกำลังดำเนินอยู่:</b><br>
        - วิทยาศาสตร์ (เหลือเวลาอีก <span style="color:#42A5F5;"><b>28:49 นาที</b></span>)
      </div>
    </div>
  </div>

  <!-- หน้าทำโฟกัส -->
  <div id="focus" class="container section" style="display:none;">
    <div class="section-title"><i class="bi bi-stopwatch icon"></i>โฟกัสคาบเรียน</div>
    <div class="focus-timer" id="focusCount">28:49</div>
    <div style="text-align:center;">
      <button class="btn" style="width:85%;" onclick="alert('Focus Mode Started!')"><i class="bi bi-eye"></i> เริ่มโฟกัส</button>
    </div>
    <div  class="info-card" style="text-align:left;">
      <span class="bi bi-exclamation-circle" style="color:#FF8A65;"></span>
      ถ้าหลุดออกจากหน้าจอ ระบบจะหยุดนับเวลาทันทีและแจ้งเตือน
    </div>
    <div style="text-align:center;margin-top:1em;">
      <img src="https://cdn-icons-png.flaticon.com/128/3602/3602123.png" alt="Study" width="90" style="filter:drop-shadow(0 1px 6px #6ec6ff33)">
      <br>
      <span style="color:#9ad0ed;">ขอให้มีสมาธิเต็มที่!</span>
    </div>
  </div>

  <!-- หน้าคะแนน/รางวัล Gamification -->
  <div id="score" class="container section" style="display:none;">
    <div class="section-title"><i class="bi bi-star icon"></i>คะแนน & รางวัล</div>
    <div class="score-card">
      คะแนนที่โฟกัสในสัปดาห์นี้: <span class="points-circle">120</span>
      <hr>
      <b>แลกรางวัล/สิทธิ์พิเศษในห้องเรียน</b>
      <ul style="list-style:none;padding-left:0;">
        <li><span class="sticker">🌈</span> ธีมสีพาสเทลใหม่ <button class="btn outline" style="font-size:0.9rem;padding:.3em 1.2em;">แลกเลย (100 คะแนน)</button></li>
        <li><span class="sticker">🥇</span> สติ๊กเกอร์ “โฟกัสเทพ” <button class="btn outline" style="font-size:0.9rem;padding:.3em 1.2em;">แลกเลย (50 คะแนน)</button></li>
        <li><span class="sticker">🎙️</span> ขอเป็นผู้นำกิจกรรม <button class="btn outline" style="font-size:0.9rem;padding:.3em 1.2em;">แลกเลย (150 คะแนน)</button></li>
      </ul>
    </div>
  </div>

  <!-- หน้าครูควบคุมเวลา (Class Timer & โพสต์งานใหม่) -->
  <div id="teacher-timer" class="container section" style="display:none;">
    <div class="section-title"><i class="bi bi-clock-history icon"></i>หน้าควบคุมเวลา (ครู)</div>
    <div class="info-card" style="background:#FFF;">
      <label for="class-select"><b>วิชา:</b></label>
      <select id="class-select" style="font-size:1em;padding:.3em;margin-left:.5em;border-radius:8px;">
        <option>วิทยาศาสตร์</option>
        <option>คณิตศาสตร์</option>
        <option>ภาษาอังกฤษ</option>
      </select>
      <br><br>
      <label for="timer-set"><b>ตั้งเวลา:</b></label>
      <input type="number" id="timer-set" value="30" style="width:60px;font-size:1em;padding:.25em;border-radius:8px;"> <span>นาที</span>
      <button class="btn" onclick="alert('Timer Started!')"><i class="bi bi-play-circle"></i> เริ่มนับเวลา</button>
    </div>
    <div class="info-card">
      <b>Task Card</b> <i class="bi bi-card-checklist"></i>
      <form>
        <input type="text" placeholder="ชื่องาน/กิจกรรม" style="width:82%;padding:.3em;border-radius:8px;">
        <button class="btn outline" type="submit"><i class="bi bi-send"></i> โพสต์งาน</button>
      </form>
    </div>
  </div>

  <!-- Dashboard รายงานของครู -->
  <div id="dashboard" class="container section" style="display:none;">
    <div class="section-title"><i class="bi bi-graph-up icon"></i>Class Dashboard รายงาน (ครู)</div>
    <div class="dashboard-card">
      <div class="dashboard-grid">
        <div>
          <span class="bi bi-person-circle" style="font-size:1.5rem;color:#90caf9"></span><br>
          นักเรียนโฟกัส: <b style="color:#388e3c;">18/22</b><br>
          (82%)
        </div>
        <div>
          <span class="bi bi-trophy" style="font-size:1.5rem;color:#ffb74d"></span><br>
          นักเรียนที่โฟกัสครบ 100% <br>
          <b>6 คน</b>
        </div>
      </div>
      <hr>
      <b>สรุปเวลานักเรียนแต่ละคน</b>
      <ul style="list-style:none;padding-left:0;">
        <li>ดิว <span class="points-circle" style="background:#C8E6C9;color:#388e3c;">30</span> นาที</li>
        <li>เมย์ <span class="points-circle">28</span> นาที</li>
        <li>บิว <span class="points-circle">24</span> นาที</li>
        <!-- ... เพิ่มรายชื่อได้ -->
      </ul>
      <hr>
      <button class="btn outline" style="float:right;" onclick="alert('ดาวน์โหลดรายงาน pdf')"><i class="bi bi-file-earmark-pdf"></i> ดาวน์โหลดรายงาน</button>
    </div>
  </div>

  <!-- งานที่ได้รับมอบหมายสำหรับนักเรียน (Task Card) -->
  <div id="homework" class="container section" style="display:none;">
    <div class="section-title"><i class="bi bi-journal-check icon"></i>งานที่ได้รับมอบหมาย</div>
    <div class="info-card">
      <div>โจทย์: แบบฝึกหัดเลขหน้า 34</div>
      <div>ครูโพสต์เมื่อ 10:11 น.</div>
      <button class="btn" onclick="alert('เริ่มจับเวลาทำงาน!')"><i class="bi bi-hourglass-top"></i> เริ่มทำงาน</button>
      <span style="margin-left:1em;">เวลาที่ใช้ล่าสุด: <span style="color:#2196F3;">14 นาที</span></span>
    </div>
    <div class="info-card">
      <div>โจทย์: เขียนสรุปวิทย์</div>
      <div>ครูโพสต์เมื่อ 8:45 น.</div>
      <button class="btn outline" onclick="alert('เริ่มจับเวลาทำงาน!')"><i class="bi bi-hourglass-top"></i> เริ่มทำงาน</button>
    </div>
  </div>

  <script>
    // เปลี่ยน section แต่ละหน้า (mockup toggle)
    function showSection(id){
      document.querySelectorAll('.section').forEach(el => el.style.display='none');
      document.getElementById(id).style.display = 'block';
      window.scrollTo(0,0);
    }
  </script>
</body>
</html>

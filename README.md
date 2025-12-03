<html lang="th">
<head>
  <meta charset="UTF-8" />
  <title>ClassFocus – Classroom Focus & Time Management</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <!-- จุดสำหรับใส่ CSS ภายหลัง -->
  <style>
    /* โครงพื้นฐานเล็กน้อย เพื่อให้ดูออกว่าหน้าแบ่งส่วนยังไง (ลบออกได้) */
    body {
      margin: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Kanit", sans-serif;
      background: #f5f7fb;
    }
    .app-shell {
      max-width: 480px;
      margin: 0 auto;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      background: #ffffff;
    }
    header.app-header {
      padding: 12px 16px;
      border-bottom: 1px solid #e3e6f0;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: #ffffff;
      position: sticky;
      top: 0;
      z-index: 10;
    }
    header .app-title {
      font-size: 18px;
      font-weight: 600;
    }
    header .app-subtitle {
      font-size: 12px;
      color: #6b7280;
    }
    main {
      flex: 1;
      padding: 12px 16px 72px;
      box-sizing: border-box;
    }
    .screen {
      display: none;
    }
    .screen.active {
      display: block;
    }
    .section-title {
      font-size: 16px;
      font-weight: 600;
      margin: 12px 0 8px;
    }
    .card {
      background: #ffffff;
      border-radius: 16px;
      padding: 12px 14px;
      margin-bottom: 10px;
      box-shadow: 0 1px 3px rgba(15, 23, 42, 0.06);
      border: 1px solid #e5e7eb;
    }
    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 6px;
    }
    .card-title {
      font-weight: 600;
      font-size: 14px;
    }
    .card-subtitle {
      font-size: 12px;
      color: #6b7280;
    }
    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      border-radius: 999px;
      padding: 8px 14px;
      font-size: 14px;
      font-weight: 500;
      cursor: pointer;
      border: none;
    }
    .btn-primary {
      background: #4f9fff;
      color: #ffffff;
    }
    .btn-outline {
      background: #ffffff;
      border: 1px solid #4f9fff;
      color: #4f9fff;
    }
    .btn-ghost {
      background: transparent;
      border: none;
      color: #4f9fff;
      padding: 4px 8px;
      font-size: 13px;
    }

    /* bottom nav */
    .bottom-nav {
      position: fixed;
      left: 50%;
      transform: translateX(-50%);
      bottom: 0;
      max-width: 480px;
      width: 100%;
      background: #ffffff;
      border-top: 1px solid #e5e7eb;
      display: flex;
      justify-content: space-around;
      padding: 6px 0 4px;
      z-index: 20;
    }
    .nav-btn {
      flex: 1;
      text-align: center;
      font-size: 11px;
      color: #9ca3af;
      cursor: pointer;
      padding: 4px 0;
    }
    .nav-btn span {
      display: block;
      font-size: 10px;
    }
    .nav-btn.active {
      color: #4f9fff;
      font-weight: 600;
    }
    .nav-btn svg {
      width: 20px;
      height: 20px;
      display: block;
      margin: 0 auto 2px;
    }

    /* ฟอร์ม */
    .form-group {
      margin-bottom: 10px;
    }
    .form-label {
      font-size: 13px;
      font-weight: 500;
      margin-bottom: 4px;
      display: inline-block;
    }
    .form-input,
    .form-select,
    .form-textarea {
      width: 100%;
      border-radius: 999px;
      border: 1px solid #d1d5db;
      padding: 8px 12px;
      font-size: 14px;
      box-sizing: border-box;
    }
    .form-textarea {
      border-radius: 12px;
      min-height: 60px;
      resize: vertical;
    }
    .badge {
      display: inline-flex;
      align-items: center;
      padding: 2px 8px;
      border-radius: 999px;
      font-size: 11px;
      font-weight: 500;
    }
    .badge-green {
      background: #dcfce7;
      color: #166534;
    }
    .badge-yellow {
      background: #fef9c3;
      color: #854d0e;
    }
    .badge-red {
      background: #fee2e2;
      color: #b91c1c;
    }
    .badge-gray {
      background: #e5e7eb;
      color: #374151;
    }
    .progress-bar {
      width: 100%;
      height: 6px;
      border-radius: 999px;
      background: #e5e7eb;
      overflow: hidden;
      margin-top: 4px;
    }
    .progress-fill {
      height: 100%;
      width: 40%;
      background: #4f9fff;
    }

    .timer-circle {
      width: 220px;
      height: 220px;
      border-radius: 50%;
      border: 8px solid #e7f2ff;
      margin: 16px auto;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
    }
    .timer-time {
      font-size: 32px;
      font-weight: 700;
    }
    .timer-sub {
      font-size: 12px;
      color: #6b7280;
    }
    .timer-status {
      text-align: center;
      margin-top: 4px;
      font-size: 12px;
      color: #6b7280;
    }

    .tab-row {
      display: flex;
      gap: 6px;
      margin-bottom: 10px;
    }
    .tab-btn {
      flex: 1;
      border-radius: 999px;
      border: 1px solid #d1d5db;
      background: #f3f4f6;
      font-size: 13px;
      padding: 6px 8px;
      cursor: pointer;
      text-align: center;
    }
    .tab-btn.active {
      border-color: #4f9fff;
      background: #e7f2ff;
      color: #1d4ed8;
      font-weight: 600;
    }

    .table {
      width: 100%;
      border-collapse: collapse;
      font-size: 12px;
      margin-top: 6px;
    }
    .table th,
    .table td {
      border-bottom: 1px solid #e5e7eb;
      padding: 6px 4px;
      text-align: left;
    }
    .table th {
      font-weight: 600;
      color: #4b5563;
    }

    .badge-level {
      font-size: 11px;
      padding: 2px 8px;
      border-radius: 999px;
      background: #e0f2fe;
      color: #1d4ed8;
      margin-left: 4px;
    }

    .pill {
      display: inline-flex;
      align-items: center;
      padding: 4px 10px;
      border-radius: 999px;
      font-size: 12px;
      background: #eff6ff;
      color: #1d4ed8;
      margin-top: 4px;
    }

    .chips-row {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
      margin-top: 6px;
    }
    .chip {
      padding: 4px 10px;
      border-radius: 999px;
      border: 1px solid #d1d5db;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <div class="app-shell">
    <!-- HEADER หลัก -->
    <header class="app-header">
      <div>
        <div class="app-title">ClassFocus</div>
        <div class="app-subtitle" id="appRoleLabel">
          นักเรียน – คาบวิทยาศาสตร์ ม.2/1
        </div>
      </div>
      <button class="btn-ghost" id="btnToggleRole" type="button">
        สลับเป็นครู
      </button>
    </header>

    <!-- เนื้อหาหลัก -->
    <main>
      <!-- ============= LOGIN / ROLE SELECTION (สามารถซ่อนในภายหลังได้) ============= -->
      <section id="screen-login" class="screen">
        <h2 class="section-title">เข้าสู่ระบบ ClassFocus</h2>
        <form id="loginForm">
          <div class="form-group">
            <span class="form-label">บทบาทผู้ใช้</span>
            <div class="chips-row">
              <label class="chip">
                <input type="radio" name="role" value="student" checked /> นักเรียน
              </label>
              <label class="chip">
                <input type="radio" name="role" value="teacher" /> ครู
              </label>
            </div>
          </div>
          <div class="form-group">
            <label class="form-label" for="schoolCode">รหัสโรงเรียน / โค้ดห้องเรียน</label>
            <input
              id="schoolCode"
              name="schoolCode"
              class="form-input"
              placeholder="เช่น SCI-M2-2025"
              required
            />
          </div>
          <div class="form-group">
            <label class="form-label" for="userId">
              รหัสนักเรียน / อีเมลครู
            </label>
            <input
              id="userId"
              name="userId"
              class="form-input"
              placeholder="กรอกรหัสนักเรียนหรืออีเมล"
              required
            />
          </div>
          <div class="form-group">
            <button class="btn btn-primary" type="submit" style="width: 100%;">
              เข้าสู่ระบบ
            </button>
          </div>
        </form>
      </section>

      <!-- ======================= STUDENT HOME ======================= -->
      <section id="screen-student-home" class="screen active">
        <!-- Banner สถานะคาบ -->
        <div class="card" id="studentClassBanner">
          <div class="card-header">
            <div>
              <div class="card-title">คาบกำลังเรียน: วิทยาศาสตร์</div>
              <div class="card-subtitle">
                เหลือเวลาอีก <strong>18:25 นาที</strong>
              </div>
            </div>
            <span class="badge badge-green">⚡ Focus Session</span>
          </div>
          <div style="display: flex; gap: 8px;">
            <button class="btn btn-primary" type="button" data-nav-target="screen-student-focus">
              เริ่มโฟกัส
            </button>
            <button class="btn btn-outline" type="button">
              ดูรายละเอียดคาบ
            </button>
          </div>
        </div>

        <!-- งานในคาบนี้ -->
        <div class="card">
          <div class="card-header">
            <div class="card-title">งานในคาบนี้</div>
            <button class="btn-ghost" type="button">ดูทั้งหมด &gt;</button>
          </div>

          <!-- Task Card 1 -->
          <article class="card" style="margin-bottom: 8px;">
            <div class="card-header">
              <div>
                <div class="card-title">ใบงานที่ 3: แรงและการเคลื่อนที่</div>
                <div class="card-subtitle">
                  กำหนดส่ง: วันนี้ 15:30
                </div>
              </div>
              <span class="badge badge-green">กำลังทำอยู่</span>
            </div>
            <div>
              <div style="font-size: 12px; color: #6b7280;">
                ความคืบหน้าจากเวลาโฟกัส
              </div>
              <div class="progress-bar">
                <div class="progress-fill" style="width: 60%;"></div>
              </div>
            </div>
            <div style="margin-top: 8px;">
              <button
                class="btn btn-primary"
                type="button"
                data-nav-target="screen-student-focus"
              >
                ทำต่อ
              </button>
              <button class="btn-ghost" type="button">
                รายละเอียดงาน
              </button>
            </div>
          </article>

          <!-- Task Card 2 -->
          <article class="card">
            <div class="card-header">
              <div>
                <div class="card-title">อ่านหนังสือเงียบ 10 นาที</div>
                <div class="card-subtitle">
                  ใช้เพื่อเก็บเวลาการอ่านในคาบนี้
                </div>
              </div>
              <span class="badge badge-gray">ยังไม่เริ่ม</span>
            </div>
            <div class="progress-bar">
              <div class="progress-fill" style="width: 0%;"></div>
            </div>
            <div style="margin-top: 8px;">
              <button
                class="btn btn-outline"
                type="button"
                data-nav-target="screen-student-focus"
              >
                เริ่มทำงาน
              </button>
            </div>
          </article>
        </div>

        <!-- สรุปคะแนนวันนี้ -->
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">สรุปโฟกัสวันนี้</div>
              <div class="card-subtitle">
                ข้อมูลเฉพาะในวันนี้เท่านั้น
              </div>
            </div>
          </div>
          <div style="font-size: 14px;">
            วันนี้คุณโฟกัสไปแล้ว:
            <strong>32 นาที</strong><br />
            ได้แต้ม: <strong>+120 Focus Points</strong>
          </div>
          <div style="margin-top: 8px;">
            <button
              class="btn btn-outline"
              type="button"
              data-nav-target="screen-student-rewards"
            >
              ดูคะแนน &amp; ของรางวัล
            </button>
          </div>
        </div>
      </section>

      <!-- ======================= STUDENT FOCUS MODE ======================= -->
      <section id="screen-student-focus" class="screen">
        <h2 class="section-title">โหมดโฟกัส</h2>

        <!-- เลือกงานที่โฟกัส -->
        <div class="card">
          <div class="form-group">
            <label class="form-label" for="focusTaskSelect">
              กำลังโฟกัสกับงาน
            </label>
            <select id="focusTaskSelect" class="form-select" name="focusTask">
              <option value="worksheet3">
                ใบงานที่ 3: แรงและการเคลื่อนที่
              </option>
              <option value="silent-reading">
                อ่านหนังสือเงียบ 10 นาที
              </option>
              <option value="general">
                โฟกัสทั่วไปในคาบเรียน
              </option>
            </select>
          </div>
          <div class="card-subtitle">
            เลือกงานเพื่อให้เวลาที่โฟกัสถูกบันทึกให้ถูกกิจกรรม
          </div>
        </div>

        <!-- Timer -->
        <div class="timer-circle">
          <div class="timer-time" id="focusTimerDisplay">
            18:25
          </div>
          <div class="timer-sub">
            เหลือเวลาคาบเรียน
          </div>
        </div>
        <div class="timer-status">
          <span class="badge badge-green">กำลังโฟกัส</span><br />
          โฟกัสต่อเนื่องอีก 5 นาที จะได้ +10 แต้ม 🎁
        </div>

        <!-- ปุ่มควบคุม -->
        <div style="margin-top: 16px; display: flex; flex-direction: column; gap: 8px;">
          <button
            class="btn btn-primary"
            type="button"
            id="btnPauseFocus"
          >
            หยุดโฟกัสชั่วคราว
          </button>
          <button class="btn btn-outline" type="button" id="btnEndFocus">
            จบโฟกัส
          </button>
        </div>

        <!-- แจ้งเตือนเรื่องการออกจากแอป (ตัวอย่าง UI) -->
        <div class="card" style="margin-top: 16px;">
          <div class="card-title">การแจ้งเตือนเมื่อสลับไปแอปอื่น</div>
          <div class="card-subtitle">
            หากคุณออกจากแอปหรือสลับหน้าจอ เวลาโฟกัสจะถูกหยุดและอาจถูกตัดแต้ม
          </div>
          <ul style="font-size: 12px; padding-left: 18px; margin-top: 6px;">
            <li>ออกจากแอป 1 ครั้ง: หยุดเวลาชั่วคราว</li>
            <li>ออกจากแอปหลายครั้ง: ครูจะเห็นในระบบรายงาน</li>
          </ul>
        </div>
      </section>

      <!-- ======================= STUDENT REWARDS ======================= -->
      <section id="screen-student-rewards" class="screen">
        <h2 class="section-title">คะแนน &amp; ของรางวัล</h2>

        <!-- Summary -->
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">
                คะแนนสะสม: <strong>1,250 pts</strong>
              </div>
              <div class="card-subtitle">
                โฟกัสต่อเนื่องสูงสุด: 27 นาที
              </div>
            </div>
          </div>
          <div>
            เลเวลปัจจุบัน:
            <span class="badge-level">Lv.4 – Focus Explorer</span>
          </div>
        </div>

        <!-- Tabs -->
        <div class="tab-row">
          <button
            class="tab-btn active"
            type="button"
            data-tab-group="rewards"
            data-tab-id="rewards-class"
          >
            รางวัลในห้องเรียน
          </button>
          <button
            class="tab-btn"
            type="button"
            data-tab-group="rewards"
            data-tab-id="rewards-themes"
          >
            ธีม &amp; สติ๊กเกอร์
          </button>
        </div>

        <!-- Tab Content: รางวัลในห้องเรียน -->
        <div id="tab-rewards-class" data-tab-group-panel="rewards">
          <div class="card">
            <!-- Reward Card 1 -->
            <article class="card">
              <div class="card-header">
                <div>
                  <div class="card-title">สิทธิ์เลือกที่นั่งแถวหน้า 🎟️</div>
                  <div class="card-subtitle">
                    ใช้ได้ 1 ครั้ง / สัปดาห์
                  </div>
                </div>
                <span class="badge badge-yellow">400 pts</span>
              </div>
              <div style="margin-top: 6px; font-size: 12px;">
                เมื่อแลกแล้ว ระบบจะส่งคำขอให้ครูอนุมัติในชั้นเรียน
              </div>
              <div style="margin-top: 8px;">
                <button class="btn btn-primary" type="button">
                  ขอแลก
                </button>
              </div>
            </article>

            <!-- Reward Card 2 -->
            <article class="card">
              <div class="card-header">
                <div>
                  <div class="card-title">สิทธิ์ส่งงานช้าพิเศษ 1 วัน ⏰</div>
                  <div class="card-subtitle">
                    ใช้ได้เฉพาะงานการบ้านวิชาวิทยาศาสตร์
                  </div>
                </div>
                <span class="badge badge-yellow">600 pts</span>
              </div>
              <div style="margin-top: 6px; font-size: 12px;">
                การใช้สิทธิ์นี้ขึ้นอยู่กับดุลยพินิจของครูผู้สอน
              </div>
              <div style="margin-top: 8px;">
                <button class="btn btn-outline" type="button">
                  ขอแลก
                </button>
              </div>
            </article>
          </div>
        </div>

        <!-- Tab Content: ธีม & สติ๊กเกอร์ -->
        <div
          id="tab-rewards-themes"
          data-tab-group-panel="rewards"
          style="display: none;"
        >
          <div class="card">
            <!-- Theme 1 -->
            <article class="card">
              <div class="card-header">
                <div>
                  <div class="card-title">ธีมท้องฟ้าพาสเทล ☁️</div>
                  <div class="card-subtitle">
                    เปลี่ยนพื้นหลังและปุ่มแอปเป็นสีฟ้า-ขาวละมุน
                  </div>
                </div>
                <span class="badge badge-yellow">250 pts</span>
              </div>
              <div style="margin-top: 6px; font-size: 12px;">
                สถานะ: <strong>ยังไม่ได้ปลดล็อก</strong>
              </div>
              <div style="margin-top: 8px;">
                <button class="btn btn-primary" type="button">
                  ปลดล็อก
                </button>
              </div>
            </article>

            <!-- Theme 2 -->
            <article class="card">
              <div class="card-header">
                <div>
                  <div class="card-title">แพ็กสติ๊กเกอร์ห้องเรียนเวทมนตร์ ✨</div>
                  <div class="card-subtitle">
                    ใช้สติ๊กเกอร์ในแชต/กระดานประกาศของห้องเรียน
                  </div>
                </div>
                <span class="badge badge-yellow">300 pts</span>
              </div>
              <div style="margin-top: 6px; font-size: 12px;">
                สถานะ: <strong>ปลดล็อกแล้ว</strong>
              </div>
              <div style="margin-top: 8px;">
                <button class="btn btn-outline" type="button">
                  ใช้แพ็กนี้
                </button>
              </div>
            </article>
          </div>
        </div>
      </section>

      <!-- ======================= TEACHER – CLASS TIMER ======================= -->
      <section id="screen-teacher-timer" class="screen">
        <h2 class="section-title">จัดการคาบเรียน – ม.2/1</h2>

        <!-- เลือกกิจกรรม -->
        <div class="card">
          <div class="form-group">
            <label class="form-label" for="teacherActivitySelect">
              กิจกรรมตอนนี้
            </label>
            <select
              id="teacherActivitySelect"
              class="form-select"
              name="teacherActivity"
            >
              <option value="worksheet3">
                ทำใบงานที่ 3 – แรงและการเคลื่อนที่
              </option>
              <option value="silent-reading">
                อ่านหนังสือเงียบ
              </option>
              <option value="quiz">
                ทำแบบทดสอบย่อย
              </option>
            </select>
          </div>
          <button class="btn btn-ghost" type="button">
            สร้างกิจกรรมใหม่ +
          </button>
        </div>

        <!-- Timer สำหรับทั้งห้อง -->
        <div class="card">
          <div class="card-header">
            <div class="card-title">Class Timer</div>
            <span class="badge badge-gray">ซิงค์กับอุปกรณ์นักเรียน</span>
          </div>
          <div style="text-align: center;">
            <div class="timer-time" id="classTimerDisplay">30:00</div>
            <div class="timer-sub">
              เวลาคาบเรียนที่กำหนด
            </div>
            <div style="margin-top: 8px;">
              <button class="btn-ghost" type="button">– 1 นาที</button>
              <button class="btn-ghost" type="button">+ 1 นาที</button>
            </div>
          </div>
          <div style="margin-top: 8px;">
            <label style="font-size: 13px;">
              <input type="checkbox" name="hideTime" />
              ซ่อนเวลาจากจอนักเรียน
            </label>
          </div>
          <div style="margin-top: 10px; display: flex; gap: 8px;">
            <button class="btn btn-primary" type="button">
              เริ่มคาบ
            </button>
            <button class="btn btn-outline" type="button">
              จบคาบ
            </button>
          </div>
        </div>

        <!-- สถานะโฟกัสของนักเรียน -->
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">สถานะนักเรียนตอนนี้</div>
              <div class="card-subtitle">
                นักเรียนที่กำลังโฟกัส: 24 / 30 คน
              </div>
            </div>
          </div>

          <div class="chips-row">
            <span class="chip">กำลังโฟกัส: 68%</span>
            <span class="chip">หยุดชั่วคราว: 20%</span>
            <span class="chip">หลุดจากแอปบ่อย: 12%</span>
          </div>

          <!-- รายชื่อนักเรียน -->
          <article class="card" style="margin-top: 10px;">
            <div class="card-header">
              <div>
                <div class="card-title">นัทธพงศ์</div>
                <div class="card-subtitle">
                  โฟกัสต่อเนื่อง: 12:40 นาที
                </div>
              </div>
              <span class="badge badge-green">กำลังโฟกัส</span>
            </div>
            <div style="font-size: 12px;">
              รวมเวลาทั้งคาบ: 18 นาที<br />
              ออกจากแอป: 1 ครั้ง
            </div>
          </article>

          <article class="card">
            <div class="card-header">
              <div>
                <div class="card-title">อมร</div>
                <div class="card-subtitle">
                  โฟกัสต่อเนื่อง: 04:10 นาที
                </div>
              </div>
              <span class="badge badge-red">ออกจากแอปบ่อย</span>
            </div>
            <div style="font-size: 12px;">
              รวมเวลาทั้งคาบ: 10 นาที<br />
              ออกจากแอป: 4 ครั้ง
            </div>
          </article>
        </div>
      </section>

      <!-- ======================= TEACHER DASHBOARD ======================= -->
      <section id="screen-teacher-dashboard" class="screen">
        <h2 class="section-title">Dashboard รายงานของครู</h2>

        <!-- Tabs รายงาน -->
        <div class="tab-row">
          <button
            class="tab-btn active"
            type="button"
            data-tab-group="dashboard"
            data-tab-id="dashboard-today"
          >
            ภาพรวมวันนี้
          </button>
          <button
            class="tab-btn"
            type="button"
            data-tab-group="dashboard"
            data-tab-id="dashboard-class"
          >
            รายคาบ
          </button>
          <button
            class="tab-btn"
            type="button"
            data-tab-group="dashboard"
            data-tab-id="dashboard-student"
          >
            รายบุคคล
          </button>
        </div>

        <!-- Tab: ภาพรวมวันนี้ -->
        <div id="tab-dashboard-today" data-tab-group-panel="dashboard">
          <div class="card">
            <div class="card-title">ภาพรวมวันนี้</div>
            <div class="chips-row">
              <span class="pill">เวลารวมที่นักเรียนโฟกัส: 12 ชม. 30 นาที</span>
              <span class="pill">เปอร์เซ็นต์โฟกัสเฉลี่ย: 74%</span>
              <span class="pill">โฟกัสเกิน 20 นาที/คาบ: 18 คน</span>
            </div>
          </div>

          <div class="card">
            <div class="card-title">เปอร์เซ็นต์โฟกัสตามคาบเรียน</div>
            <div class="card-subtitle">
              (กราฟแท่ง – ให้ front-end นำไปวาดต่อ)
            </div>
            <table class="table">
              <thead>
                <tr>
                  <th>คาบ</th>
                  <th>วิชา</th>
                  <th>% โฟกัสเฉลี่ย</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>คาบ 1</td>
                  <td>วิทยาศาสตร์ ม.2/1</td>
                  <td>78%</td>
                </tr>
                <tr>
                  <td>คาบ 2</td>
                  <td>คณิตศาสตร์ ม.2/1</td>
                  <td>70%</td>
                </tr>
                <tr>
                  <td>คาบ 3</td>
                  <td>ภาษาไทย ม.2/1</td>
                  <td>74%</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Tab: รายคาบ -->
        <div
          id="tab-dashboard-class"
          data-tab-group-panel="dashboard"
          style="display: none;"
        >
          <div class="card">
            <div class="form-group">
              <label class="form-label" for="dashboardClassSelect">
                เลือกรายวิชา / ห้อง
              </label>
              <select
                id="dashboardClassSelect"
                name="dashboardClass"
                class="form-select"
              >
                <option value="sci-m2-1">วิทยาศาสตร์ ม.2/1 – 3 ธ.ค. 2025</option>
                <option value="math-m2-1">คณิตศาสตร์ ม.2/1 – 3 ธ.ค. 2025</option>
              </select>
            </div>
          </div>

          <div class="card">
            <div class="card-title">สรุปของคาบนี้</div>
            <ul style="font-size: 13px; padding-left: 18px;">
              <li>เวลาโฟกัสเฉลี่ยต่อคน: 17 นาที</li>
              <li>นักเรียนที่โฟกัส ≥ 80% ของเวลาคาบ: 12 / 30 คน</li>
              <li>นักเรียนที่ออกจากแอปเกิน 3 ครั้ง: 4 คน</li>
            </ul>

            <table class="table">
              <thead>
                <tr>
                  <th>ชื่อนักเรียน</th>
                  <th>เวลาโฟกัส (นาที)</th>
                  <th>ออกแอป (ครั้ง)</th>
                  <th>แต้มที่ได้</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>นัทธพงศ์</td>
                  <td>22</td>
                  <td>1</td>
                  <td>+60</td>
                </tr>
                <tr>
                  <td>อมร</td>
                  <td>10</td>
                  <td>4</td>
                  <td>+20</td>
                </tr>
              </tbody>
            </table>

            <div style="margin-top: 10px; display: flex; gap: 8px;">
              <button class="btn btn-outline" type="button">
                ดาวน์โหลดรายงาน PDF
              </button>
              <button class="btn btn-ghost" type="button">
                ส่งออก CSV
              </button>
            </div>
          </div>
        </div>

        <!-- Tab: รายบุคคล -->
        <div
          id="tab-dashboard-student"
          data-tab-group-panel="dashboard"
          style="display: none;"
        >
          <div class="card">
            <div class="form-group">
              <label class="form-label" for="searchStudentInput">
                ค้นหานักเรียน
              </label>
              <input
                id="searchStudentInput"
                name="searchStudent"
                class="form-input"
                placeholder="พิมพ์ชื่อหรือลำดับที่..."
              />
            </div>
          </div>

          <div class="card">
            <div class="card-header">
              <div>
                <div class="card-title">โปรไฟล์นักเรียน – นัทธพงศ์</div>
                <div class="card-subtitle">
                  ห้อง ม.2/1 เลขที่ 12
                </div>
              </div>
            </div>
            <div style="font-size: 13px;">
              เวลาโฟกัสเฉลี่ยต่อคาบ:
              <strong>15 นาที</strong><br />
              โฟกัสสูงสุดในคาบเดียว:
              <strong>26 นาที</strong>
            </div>

            <div style="margin-top: 10px;">
              <div class="card-subtitle">
                แนวโน้มเวลาโฟกัสย้อนหลัง 4 สัปดาห์
                (พื้นที่สำหรับกราฟ)
              </div>
              <div class="chips-row">
                <span class="chip">สัปดาห์ 1: 13 นาที/คาบ</span>
                <span class="chip">สัปดาห์ 2: 14 นาที/คาบ</span>
                <span class="chip">สัปดาห์ 3: 16 นาที/คาบ</span>
                <span class="chip">สัปดาห์ 4: 17 นาที/คาบ</span>
              </div>
            </div>

            <div style="margin-top: 10px;">
              <div class="card-title" style="font-size: 14px;">
                คาบที่โดดเด่น
              </div>
              <ul style="font-size: 13px; padding-left: 18px;">
                <li>วิทยาศาสตร์ – 28 พ.ย. 2025: โฟกัส 25 นาที</li>
                <li>คณิตศาสตร์ – 1 ธ.ค. 2025: โฟกัส 24 นาที</li>
              </ul>

              <div class="card-title" style="font-size: 14px; margin-top: 8px;">
                คาบที่ควรดูแลเป็นพิเศษ
              </div>
              <ul style="font-size: 13px; padding-left: 18px;">
                <li>วิทยาศาสตร์ – 20 พ.ย. 2025: ออกจากแอป 5 ครั้ง</li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <!-- ======================= TEACHER – TASK & REWARD SETUP (ฟอร์มตัวอย่าง) ======================= -->
      <section id="screen-teacher-setup" class="screen">
        <h2 class="section-title">ตั้งค่างาน &amp; รางวัล</h2>

        <div class="card">
          <div class="card-title">สร้างงาน / กิจกรรมใหม่</div>
          <form id="taskCreateForm">
            <div class="form-group">
              <label class="form-label" for="taskName">ชื่อกิจกรรม/งาน *</label>
              <input
                id="taskName"
                name="taskName"
                class="form-input"
                placeholder="เช่น ใบงานที่ 3: แรงและการเคลื่อนที่"
                required
              />
            </div>
            <div class="form-group">
              <label class="form-label" for="taskDescription">
                คำอธิบาย (ตัวเลือก)
              </label>
              <textarea
                id="taskDescription"
                name="taskDescription"
                class="form-textarea"
                placeholder="อธิบายรายละเอียดงานหรือขั้นตอนคร่าว ๆ"
              ></textarea>
            </div>
            <div class="form-group">
              <label class="form-label" for="taskType">ประเภท</label>
              <select id="taskType" name="taskType" class="form-select">
                <option value="homework">การบ้าน</option>
                <option value="in-class">กิจกรรมในคาบ</option>
                <option value="exercise">แบบฝึกหัด</option>
              </select>
            </div>
            <div class="form-group">
              <label class="form-label" for="taskExpectedMinutes">
                เวลาที่คาดว่าจะใช้ (นาที)
              </label>
              <input
                id="taskExpectedMinutes"
                name="taskExpectedMinutes"
                class="form-input"
                type="number"
                min="1"
                placeholder="เช่น 20"
              />
            </div>
            <div class="form-group">
              <label class="form-label" for="taskDueDatetime">
                วัน/เวลาที่กำหนดส่ง (ถ้ามี)
              </label>
              <input
                id="taskDueDatetime"
                name="taskDueDatetime"
                class="form-input"
                type="datetime-local"
              />
            </div>
            <div class="form-group">
              <label class="form-label" for="taskBasePoints">
                คะแนนโฟกัสพื้นฐานสำหรับงานนี้
              </label>
              <input
                id="taskBasePoints"
                name="taskBasePoints"
                class="form-input"
                type="number"
                min="0"
                placeholder="เช่น 50"
              />
            </div>
            <div class="form-group">
              <button class="btn btn-primary" type="submit" style="width: 100%;">
                สร้างกิจกรรม
              </button>
            </div>
          </form>
        </div>

        <div class="card">
          <div class="card-title">ตั้งค่ารางวัลในห้องเรียน</div>
          <form id="rewardCreateForm">
            <div class="form-group">
              <label class="form-label" for="rewardName">ชื่อรางวัล *</label>
              <input
                id="rewardName"
                name="rewardName"
                class="form-input"
                placeholder="เช่น สิทธิ์เลือกที่นั่งแถวหน้า"
                required
              />
            </div>
            <div class="form-group">
              <label class="form-label" for="rewardPoints">คะแนนที่ใช้แลก *</label>
              <input
                id="rewardPoints"
                name="rewardPoints"
                class="form-input"
                type="number"
                min="10"
                step="10"
                placeholder="อย่างน้อย 10 คะแนน"
                required
              />
            </div>
            <div class="form-group">
              <label class="form-label" for="rewardDescription">
                รายละเอียด/เงื่อนไข
              </label>
              <textarea
                id="rewardDescription"
                name="rewardDescription"
                class="form-textarea"
                placeholder="ตัวอย่าง: ใช้ได้ 1 ครั้ง/สัปดาห์ และต้องอยู่ในเกณฑ์มาสายไม่เกิน 1 ครั้ง"
              ></textarea>
            </div>
            <div class="form-group">
              <label class="form-label" for="rewardLimit">
                จำนวนครั้งที่ใช้ได้
              </label>
              <input
                id="rewardLimit"
                name="rewardLimit"
                class="form-input"
                type="number"
                min="0"
                placeholder="0 = ไม่จำกัด"
              />
            </div>
            <div class="form-group">
              <label class="form-label" for="rewardLimitPeriod">
                ช่วงเวลาจำกัดการใช้
              </label>
              <select
                id="rewardLimitPeriod"
                name="rewardLimitPeriod"
                class="form-select"
              >
                <option value="none">ไม่จำกัดช่วงเวลา</option>
                <option value="week">ต่อสัปดาห์</option>
                <option value="term">ต่อภาคเรียน</option>
              </select>
            </div>
            <div class="form-group">
              <label style="font-size: 13px;">
                <input
                  type="checkbox"
                  id="rewardIsActive"
                  name="rewardIsActive"
                  checked
                />
                เปิดให้แลกทันที
              </label>
            </div>
            <div class="form-group">
              <button class="btn btn-primary" type="submit" style="width: 100%;">
                บันทึกรางวัล
              </button>
            </div>
          </form>
        </div>
      </section>
    </main>

    <!-- ======================= BOTTOM NAV (แชร์ทุกโหมด) ======================= -->
    <nav class="bottom-nav">
      <!-- แท็บสำหรับนักเรียน -->
      <div
        class="nav-btn active"
        data-role="student"
        data-nav-target="screen-student-home"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" />
        </svg>
        <span>หน้าหลัก</span>
      </div>
      <div
        class="nav-btn"
        data-role="student"
        data-nav-target="screen-student-focus"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <rect
            x="7"
            y="6"
            width="3"
            height="12"
            fill="none"
            stroke="currentColor"
          />
          <rect
            x="14"
            y="6"
            width="3"
            height="12"
            fill="none"
            stroke="currentColor"
          />
        </svg>
        <span>โฟกัส</span>
      </div>
      <div
        class="nav-btn"
        data-role="student"
        data-nav-target="screen-student-rewards"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <path
            d="M5 10h14l-2 9H7z"
            fill="none"
            stroke="currentColor"
          />
          <path
            d="M9 10V5h6v5"
            fill="none"
            stroke="currentColor"
          />
        </svg>
        <span>รางวัล</span>
      </div>

      <!-- แท็บสำหรับครู -->
      <div
        class="nav-btn"
        data-role="teacher"
        data-nav-target="screen-teacher-timer"
        style="display: none;"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <circle cx="12" cy="12" r="8" fill="none" stroke="currentColor" />
          <path
            d="M12 8v4l3 2"
            fill="none"
            stroke="currentColor"
          />
        </svg>
        <span>Timer</span>
      </div>
      <div
        class="nav-btn"
        data-role="teacher"
        data-nav-target="screen-teacher-dashboard"
        style="display: none;"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <rect
            x="5"
            y="10"
            width="3"
            height="8"
            fill="none"
            stroke="currentColor"
          />
          <rect
            x="10.5"
            y="6"
            width="3"
            height="12"
            fill="none"
            stroke="currentColor"
          />
          <rect
            x="16"
            y="8"
            width="3"
            height="10"
            fill="none"
            stroke="currentColor"
          />
        </svg>
        <span>Dashboard</span>
      </div>
      <div
        class="nav-btn"
        data-role="teacher"
        data-nav-target="screen-teacher-setup"
        style="display: none;"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <circle cx="12" cy="12" r="3" fill="none" stroke="currentColor" />
          <path
            d="M12 5v2M12 17v2M5 12h2M17 12h2M7.8 7.8l1.4 1.4M14.8 14.8l1.4 1.4M16.2 7.8l-1.4 1.4M9.2 14.8l-1.4 1.4"
            fill="none"
            stroke="currentColor"
          />
        </svg>
        <span>ตั้งค่า</span>
      </div>
    </nav>
  </div>

  <!-- สคริปต์เล็ก ๆ สำหรับสลับหน้าภายในหน้าเดียว (ไม่จำเป็นต้องใช้ก็ได้ สามารถลบได้) -->
  <script>
    // helper: สลับหน้าจอ (screen)
    function showScreen(id) {
      document.querySelectorAll(".screen").forEach((el) => {
        el.classList.remove("active");
      });
      const target = document.getElementById(id);
      if (target) target.classList.add("active");
    }

    // nav bottom
    document.querySelectorAll(".nav-btn[data-nav-target]").forEach((btn) => {
      btn.addEventListener("click", () => {
        const targetId = btn.getAttribute("data-nav-target");
        showScreen(targetId);
        const role = btn.getAttribute("data-role");
        document.querySelectorAll(".nav-btn[data-role='" + role + "']").forEach((b) =>
          b.classList.remove("active")
        );
        btn.classList.add("active");
      });
    });

    // ปุ่มในเนื้อหา ที่ใช้ data-nav-target
    document.querySelectorAll("[data-nav-target]").forEach((el) => {
      el.addEventListener("click", (e) => {
        const targetId = el.getAttribute("data-nav-target");
        if (!targetId) return;
        showScreen(targetId);
      });
    });

    // สลับ Tab
    function setupTabs(group) {
      const btnSelector = ".tab-btn[data-tab-group='" + group + "']";
      const panelSelector = "[data-tab-group-panel='" + group + "']";
      document.querySelectorAll(btnSelector).forEach((btn) => {
        btn.addEventListener("click", () => {
          const tabId = btn.getAttribute("data-tab-id");
          document.querySelectorAll(btnSelector).forEach((b) =>
            b.classList.remove("active")
          );
          btn.classList.add("active");
          document.querySelectorAll(panelSelector).forEach((p) => {
            p.style.display = "none";
          });
          const panel = document.getElementById("tab-" + tabId);
          if (panel) panel.style.display = "block";
        });
      });
    }

    setupTabs("rewards");
    setupTabs("dashboard");

    // สลับบทบาท นักเรียน/ครู แบบง่าย (Front-end เท่านั้น)
    const btnToggleRole = document.getElementById("btnToggleRole");
    const appRoleLabel = document.getElementById("appRoleLabel");
    let currentRole = "student";

    function updateRoleUI() {
      if (currentRole === "student") {
        // แสดงหน้านักเรียน
        showScreen("screen-student-home");
        appRoleLabel.textContent = "นักเรียน – คาบวิทยาศาสตร์ ม.2/1";
        btnToggleRole.textContent = "สลับเป็นครู";

        // bottom nav: นักเรียน
        document
          .querySelectorAll(".nav-btn[data-role='student']")
          .forEach((b) => (b.style.display = "block"));
        document
          .querySelectorAll(".nav-btn[data-role='teacher']")
          .forEach((b) => (b.style.display = "none"));
      } else {
        // แสดงหน้าครู
        showScreen("screen-teacher-timer");
        appRoleLabel.textContent = "ครู – คาบวิทยาศาสตร์ ม.2/1";
        btnToggleRole.textContent = "สลับเป็นนักเรียน";

        // bottom nav: ครู
        document
          .querySelectorAll(".nav-btn[data-role='student']")
          .forEach((b) => (b.style.display = "none"));
        document
          .querySelectorAll(".nav-btn[data-role='teacher']")
          .forEach((b) => (b.style.display = "block"));
      }
    }

    btnToggleRole.addEventListener("click", () => {
      currentRole = currentRole === "student" ? "teacher" : "student";
      updateRoleUI();
    });

    // เริ่มต้นเป็นนักเรียน
    updateRoleUI();
  </script>
</body>
</html>

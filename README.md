<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ClassFocus – Focus Timer</title>

<style>
    body {
        font-family: "Prompt", sans-serif;
        background: #eef6ff;
        text-align: center;
        padding: 40px;
        color: #333;
    }

    h1 {
        color: #2b6cb0;
        margin-bottom: 10px;
    }

    .timer {
        font-size: 80px;
        font-weight: bold;
        margin: 30px 0;
        color: #1a365d;
    }

    button {
        padding: 12px 25px;
        font-size: 18px;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        margin: 5px;
    }

    #startBtn {
        background-color: #4299e1;
        color: white;
    }

    #stopBtn {
        background-color: #e53e3e;
        color: white;
    }

    .alert {
        margin-top: 20px;
        color: #e53e3e;
        font-weight: bold;
    }
</style>
</head>

<body>

<h1>ClassFocus – โหมดโฟกัสสำหรับนักเรียน</h1>
<p>ถ้าออกจากแท็บ เวลาโฟกัสจะหยุดอัตโนมัติ</p>

<div class="timer" id="timer">00:00</div>

<button id="startBtn">เริ่มโฟกัส</button>
<button id="stopBtn">หยุด</button>

<div class="alert" id="alertMessage"></div>

<script>
    let seconds = 0;
    let timerInterval;
    let isFocusing = false;

    function updateTimer() {
        let mins = Math.floor(seconds / 60);
        let secs = seconds % 60;
        document.getElementById("timer").textContent =
            `${String(mins).padStart(2, "0")}:${String(secs).padStart(2, "0")}`;
    }

    document.getElementById("startBtn").onclick = function () {
        if (!isFocusing) {
            isFocusing = true;
            timerInterval = setInterval(() => {
                seconds++;
                updateTimer();
            }, 1000);
            document.getElementById("alertMessage").textContent = "";
        }
    };

    document.getElementById("stopBtn").onclick = function () {
        isFocusing = false;
        clearInterval(timerInterval);
    };

    // หยุดเวลาเมื่อออกจากแท็บ
    document.addEventListener("visibilitychange", function () {
        if (document.hidden && isFocusing) {
            clearInterval(timerInterval);
            document.getElementById("alertMessage").textContent =
                "ออกจากแท็บ! เวลาถูกหยุดชั่วคราว";
        }
    });
</script>

</body>
</html>

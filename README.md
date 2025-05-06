<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Timer</title>
  <style>
    body {
      font-family: sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #f5f5f5;
    }

    .timer {
      background: white;
      border-radius: 20px;
      padding: 30px;
      width: 200px;
      text-align: center;
      box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
    }

    .time {
      font-size: 48px;
      font-weight: bold;
      margin-bottom: 10px;
      border-bottom: 2px solid black;
      padding-bottom: 10px;
    }

    .controls {
      display: flex;
      justify-content: space-around;
      margin-top: 10px;
    }

    button {
      padding: 5px 10px;
      font-size: 14px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .start {
      background-color: #d3d3d3;
    }

    .cancel {
      background: none;
      color: grey;
      cursor: default;
    }

    .add, .subtract {
      background-color: #f0f0f0;
    }
  </style>
</head>
<body>
  <div class="timer">
    <div class="time" id="time">03:00</div>
    <div class="controls">
      <button class="subtract" onclick="adjustTime(-60)">-</button>
      <button class="start" onclick="startTimer()">Start</button>
      <button class="add" onclick="adjustTime(60)">+</button>
    </div>
    <div class="cancel">Cancel</div>
  </div>

  <script>
    let totalSeconds = 180;
    let interval = null;

    function updateDisplay() {
      const minutes = String(Math.floor(totalSeconds / 60)).padStart(2, '0');
      const seconds = String(totalSeconds % 60).padStart(2, '0');
      document.getElementById('time').textContent = `${minutes}:${seconds}`;
    }

    function adjustTime(seconds) {
      totalSeconds = Math.max(0, totalSeconds + seconds);
      updateDisplay();
    }

    function startTimer() {
      if (interval !== null) return;
      interval = setInterval(() => {
        if (totalSeconds <= 0) {
          clearInterval(interval);
          interval = null;
        } else {
          totalSeconds--;
          updateDisplay();
        }
      }, 1000);
    }

    updateDisplay();
  </script>
</body>
</html>


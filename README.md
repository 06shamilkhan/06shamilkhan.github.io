<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Timer</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f4;
        }
        .timer-container {
            text-align: center;
            padding: 20px;
            background: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        .timer-display {
            font-size: 48px;
            margin-bottom: 20px;
        }
        .btn {
            padding: 10px 20px;
            margin: 5px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        .btn:disabled {
            background-color: #cccccc;
        }
    </style>
</head>
<body>
    <div class="timer-container">
        <div id="timer" class="timer-display">00:00</div>
        <button id="startStopBtn" class="btn">Start</button>
        <button id="resetBtn" class="btn">Reset</button>
    </div>

    <script>
        let timer;
        let isRunning = false;
        let seconds = 0;

        const timerDisplay = document.getElementById('timer');
        const startStopBtn = document.getElementById('startStopBtn');
        const resetBtn = document.getElementById('resetBtn');

        function updateTimerDisplay() {
            const minutes = Math.floor(seconds / 60);
            const remainingSeconds = seconds % 60;
            timerDisplay.textContent = `${minutes < 10 ? '0' : ''}${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`;
        }

        function startStopTimer() {
            if (isRunning) {
                clearInterval(timer);
                startStopBtn.textContent = "Start";
            } else {
                timer = setInterval(() => {
                    seconds++;
                    updateTimerDisplay();
                }, 1000);
                startStopBtn.textContent = "Stop";
            }
            isRunning = !isRunning;
        }

        function resetTimer() {
            clearInterval(timer);
            seconds = 0;
            isRunning = false;
            updateTimerDisplay();
            startStopBtn.textContent = "Start";
        }

        startStopBtn.addEventListener('click', startStopTimer);
        resetBtn.addEventListener('click', resetTimer);
    </script>
</body>
</html>

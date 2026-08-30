<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>TV Clock - Erbil & GMT</title>
    <style>
        body {
            /* پاشبنەمایەکی بە تەواوی شەفاف */
            background-color: transparent;
            color: #ffffff;
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .clock-box {
            /* لابردنی سندوقی پشتەوە و هێشتنەوەی تەنها دەقەکان بە تارمایی */
            background: transparent;
            padding: 10px 20px;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .time-display {
            font-size: 50px;
            font-weight: bold;
            letter-spacing: 2px;
            font-family: 'Courier New', monospace;
            color: #ffffff; /* سپیی سادە */
            /* تارماییەکی توند بۆ ئەوەی بە ڕوونی لەسەر ڤیدیۆ دیار بێت */
            text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.9), 0 0 15px rgba(0, 0, 0, 0.7);
        }
        .label-display {
            font-size: 24px;
            color: #ffffff; /* سپیی سادە */
            font-weight: bold;
            letter-spacing: 1px;
            text-transform: uppercase;
            /* تارمایی بۆ ناوی شارەکەش */
            text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.9), 0 0 15px rgba(0, 0, 0, 0.7);
            border-left: 2px solid rgba(255, 255, 255, 0.5);
            padding-left: 15px;
        }
    </style>
</head>
<body>

    <div class="clock-box">
        <div id="clockTime" class="time-display">00:00:00</div>
        <div id="clockLabel" class="label-display">Erbil</div>
    </div>

    <script>
        function updateClock() {
            const now = new Date();
            
            const utcHours = now.getUTCHours();
            const utcMinutes = now.getUTCMinutes();
            const utcSeconds = now.getUTCSeconds();

            // کاتی هەولێر (UTC+3)
            const erbilHours = (utcHours + 3) % 24;

            // هەژمارکردنی چرکەکان: ١٠ چرکە هەولێر + ١٠ چرکە گەینویتچ (کۆی گشتی ٢٠ چرکە)
            const totalSeconds = Math.floor(now.getTime() / 1000);
            const cycle = totalSeconds % 20;

            let displayHours, labelText;

            // ئەگەر لە ١٠ چرکەی یەکەم تێپەڕی (واتا لە 10 تا 19)، دەبێتە GMT
            if (cycle >= 10) {
                displayHours = utcHours;
                labelText = "GMT";
            } else {
                // بۆ ماوەی ١٠ چرکەی یەکەم (0 تا 9) دەبێتە Erbil
                displayHours = erbilHours;
                labelText = "Erbil";
            }

            // فۆرماتکردنی کاتەکە
            const formattedTime = 
                String(displayHours).padStart(2, '0') + ':' +
                String(utcMinutes).padStart(2, '0') + ':' +
                String(utcSeconds).padStart(2, '0');

            // نیشاندان لەسەر شاشە
            document.getElementById('clockTime').innerText = formattedTime;
            document.getElementById('clockLabel').innerText = labelText;
        }

        setInterval(updateClock, 1000);
        updateClock();
    </script>

</body>
</html>

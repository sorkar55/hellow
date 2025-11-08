
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>System Breached</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Courier New', monospace;
        }

        body {
            background: #000;
            color: #0f0;
            overflow: hidden;
            position: relative;
            height: 100vh;
        }

        /* Popup Styles */
        .popup-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .popup-content {
            background: #000;
            border: 3px solid #f00;
            border-radius: 15px;
            padding: 40px;
            text-align: center;
            box-shadow: 
                0 0 30px #f00,
                0 0 60px #f00,
                0 0 90px #f00;
            animation: popup-glow 2s infinite alternate;
            max-width: 500px;
            width: 90%;
        }

        .popup-title {
            color: #f00;
            font-size: 2.5rem;
            margin-bottom: 20px;
            text-shadow: 0 0 10px #f00;
            animation: flicker 1.5s infinite;
        }

        .popup-button {
            background: #000;
            color: #0f0;
            border: 2px solid #0f0;
            padding: 15px 30px;
            font-size: 1.2rem;
            cursor: pointer;
            margin-top: 20px;
            border-radius: 8px;
            box-shadow: 0 0 15px #0f0;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .popup-button:hover {
            background: #0f0;
            color: #000;
            box-shadow: 0 0 25px #0f0;
            transform: scale(1.05);
        }

        @keyframes popup-glow {
            from {
                box-shadow: 
                    0 0 30px #f00,
                    0 0 60px #f00,
                    0 0 90px #f00;
            }
            to {
                box-shadow: 
                    0 0 40px #f00,
                    0 0 80px #f00,
                    0 0 120px #f00;
            }
        }

        /* Main Content Styles */
        .background-video {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0.4;
            z-index: -2;
        }

        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: -1;
        }

        .container {
            display: flex;
            height: 100vh;
            padding: 20px;
        }

        .left-panel {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .logo {
            width: 180px;
            height: 180px;
            border-radius: 50%;
            border: 3px solid #0f0;
            margin-bottom: 30px;
            box-shadow: 0 0 20px #0f0;
            z-index: 10;
            position: absolute;
            top: 50px;
            left: 50%;
            transform: translateX(-50%);
        }

        .video-container {
            width: 80%;
            max-width: 500px;
            border: 3px solid #0f0;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 
                0 0 25px #0f0,
                0 0 50px #0f0,
                0 0 75px #0f0;
            animation: border-glow 2s infinite alternate;
            position: relative;
        }

        .video-container::before {
            content: '';
            position: absolute;
            top: -5px;
            left: -5px;
            right: -5px;
            bottom: -5px;
            background: linear-gradient(45deg, #0f0, #00ff88, #00ffff, #0f0);
            border-radius: 20px;
            z-index: -1;
            animation: rotate-border 3s linear infinite;
        }

        .video-container::after {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: #000;
            border-radius: 15px;
            z-index: -1;
        }

        video {
            width: 100%;
            height: auto;
            display: block;
        }

        .right-panel {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .hacked-title {
            font-size: 5rem;
            text-align: center;
            margin-bottom: 30px;
            text-shadow: 0 0 10px #0f0;
            animation: glow 2s infinite alternate;
            letter-spacing: 5px;
        }

        .hacker-name {
            font-size: 3rem;
            color: #ff0;
            margin-bottom: 40px;
            text-shadow: 0 0 10px #ff0;
            animation: flicker 3s infinite;
            letter-spacing: 3px;
        }

        .warning-container {
            background: rgba(0, 0, 0, 0.8);
            border-left: 5px solid #f00;
            border-right: 5px solid #f00;
            padding: 25px;
            width: 95%;
            max-width: 700px;
            margin-bottom: 30px;
            box-shadow: 0 0 30px rgba(255, 0, 0, 0.5);
        }

        .warning-title {
            color: #f00;
            font-size: 2rem;
            margin-bottom: 20px;
            text-align: center;
            text-shadow: 0 0 5px #f00;
            letter-spacing: 2px;
        }

        .warning-message {
            color: #ff6b6b;
            font-size: 1.3rem;
            margin-bottom: 15px;
            line-height: 1.5;
            text-align: center;
            padding: 10px;
            border-bottom: 1px solid rgba(255, 0, 0, 0.3);
        }

        .warning-message:last-child {
            border-bottom: none;
        }

        .terminal {
            background: rgba(0, 0, 0, 0.9);
            border-top: 2px solid #0f0;
            border-bottom: 2px solid #0f0;
            padding: 20px;
            width: 95%;
            max-width: 700px;
            box-shadow: 0 0 20px #0f0;
        }

        .terminal-header {
            color: #0f0;
            margin-bottom: 15px;
            font-size: 1.3rem;
            text-shadow: 0 0 5px #0f0;
        }

        .terminal-line {
            margin-bottom: 8px;
            display: flex;
        }

        .prompt {
            color: #0f0;
            margin-right: 10px;
        }

        .command {
            color: #fff;
        }

        .blink {
            animation: blink 1s infinite;
        }

        @keyframes glow {
            from {
                text-shadow: 0 0 10px #0f0;
            }
            to {
                text-shadow: 0 0 20px #0f0, 0 0 30px #0f0;
            }
        }

        @keyframes flicker {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.7;
            }
        }

        @keyframes blink {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0;
            }
        }

        .scan-line {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: rgba(0, 255, 0, 0.7);
            box-shadow: 0 0 15px #0f0;
            animation: scan 4s linear infinite;
            z-index: 10;
        }

        @keyframes scan {
            0% {
                top: 0;
            }
            100% {
                top: 100%;
            }
        }

        @keyframes border-glow {
            from {
                box-shadow: 
                    0 0 25px #0f0,
                    0 0 50px #0f0,
                    0 0 75px #0f0;
            }
            to {
                box-shadow: 
                    0 0 30px #0f0,
                    0 0 60px #0f0,
                    0 0 90px #0f0;
            }
        }

        @keyframes rotate-border {
            0% {
                filter: hue-rotate(0deg);
            }
            100% {
                filter: hue-rotate(360deg);
            }
        }

        .glitch {
            position: relative;
        }

        .glitch::before, .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .glitch::before {
            left: 2px;
            text-shadow: -2px 0 #ff00ff;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim 5s infinite linear alternate-reverse;
        }

        .glitch::after {
            left: -2px;
            text-shadow: -2px 0 #00ffff;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim2 5s infinite linear alternate-reverse;
        }

        @keyframes glitch-anim {
            0% {
                clip: rect(42px, 9999px, 44px, 0);
            }
            5% {
                clip: rect(12px, 9999px, 59px, 0);
            }
            10% {
                clip: rect(48px, 9999px, 29px, 0);
            }
            15% {
                clip: rect(42px, 9999px, 73px, 0);
            }
            20% {
                clip: rect(63px, 9999px, 27px, 0);
            }
            25% {
                clip: rect(34px, 9999px, 55px, 0);
            }
            30% {
                clip: rect(86px, 9999px, 73px, 0);
            }
            35% {
                clip: rect(20px, 9999px, 20px, 0);
            }
            40% {
                clip: rect(26px, 9999px, 60px, 0);
            }
            45% {
                clip: rect(25px, 9999px, 66px, 0);
            }
            50% {
                clip: rect(57px, 9999px, 98px, 0);
            }
            55% {
                clip: rect(5px, 9999px, 46px, 0);
            }
            60% {
                clip: rect(82px, 9999px, 31px, 0);
            }
            65% {
                clip: rect(54px, 9999px, 27px, 0);
            }
            70% {
                clip: rect(28px, 9999px, 99px, 0);
            }
            75% {
                clip: rect(45px, 9999px, 69px, 0);
            }
            80% {
                clip: rect(23px, 9999px, 85px, 0);
            }
            85% {
                clip: rect(54px, 9999px, 84px, 0);
            }
            90% {
                clip: rect(45px, 9999px, 47px, 0);
            }
            95% {
                clip: rect(37px, 9999px, 20px, 0);
            }
            100% {
                clip: rect(4px, 9999px, 91px, 0);
            }
        }

        @keyframes glitch-anim2 {
            0% {
                clip: rect(65px, 9999px, 100px, 0);
            }
            5% {
                clip: rect(52px, 9999px, 74px, 0);
            }
            10% {
                clip: rect(79px, 9999px, 85px, 0);
            }
            15% {
                clip: rect(75px, 9999px, 5px, 0);
            }
            20% {
                clip: rect(67px, 9999px, 61px, 0);
            }
            25% {
                clip: rect(14px, 9999px, 79px, 0);
            }
            30% {
                clip: rect(1px, 9999px, 66px, 0);
            }
            35% {
                clip: rect(86px, 9999px, 30px, 0);
            }
            40% {
                clip: rect(23px, 9999px, 98px, 0);
            }
            45% {
                clip: rect(85px, 9999px, 72px, 0);
            }
            50% {
                clip: rect(71px, 9999px, 75px, 0);
            }
            55% {
                clip: rect(2px, 9999px, 48px, 0);
            }
            60% {
                clip: rect(30px, 9999px, 16px, 0);
            }
            65% {
                clip: rect(59px, 9999px, 50px, 0);
            }
            70% {
                clip: rect(41px, 9999px, 62px, 0);
            }
            75% {
                clip: rect(2px, 9999px, 82px, 0);
            }
            80% {
                clip: rect(47px, 9999px, 73px, 0);
            }
            85% {
                clip: rect(3px, 9999px, 27px, 0);
            }
            90% {
                clip: rect(26px, 9999px, 55px, 0);
            }
            95% {
                clip: rect(42px, 9999px, 97px, 0);
            }
            100% {
                clip: rect(38px, 9999px, 49px, 0);
            }
        }

        .matrix-rain {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
            opacity: 0.3;
        }

        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>
    <!-- Welcome Popup -->
    <div class="popup-overlay" id="welcomePopup">
        <div class="popup-content">
            <h1 class="popup-title">YOUR Website Hacked</h1>
            <p style="color: #0f0; font-size: 1.2rem; margin-bottom: 20px; text-shadow: 0 0 5px #0f0;">
                System Security Breached
            </p>
            <button class="popup-button" onclick="closePopup()">Click Here</button>
        </div>
    </div>

    <!-- Main Content -->
    <video class="background-video" autoplay loop muted>
        <source src="https://d.top4top.io/m_3571cyeri1.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <div class="overlay"></div>
    <canvas class="matrix-rain"></canvas>
    
    <div class="scan-line"></div>
    
    <div class="container">
        <div class="left-panel">
            <img src="https://i.top4top.io/p_3571o4ygp1.jpg" alt="Team Logo" class="logo">
            <div class="video-container">
                <video autoplay loop muted>
                    <source src="https://h.top4top.io/m_3571yrc2r1.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </div>
        </div>
        
        <div class="right-panel">
            <h1 class="hacked-title glitch" data-text="HACKED">HACKED</h1>
            <h2 class="hacker-name">By WHITE-DEVIL</h2>
            
            <div class="warning-container">
                <h3 class="warning-title">SYSTEM BREACHED</h3>
                <p class="warning-message">I don't play by the rules, I rewrite them — WHITE-DEVIL</p>
                <p class="warning-message">You are being monitored. Xanon NEFFEX doesn't knock, he takes control.</p>
                <p class="warning-message">Code is my weapon, fear is my signature — WHITE-DEVIL.</p>
            </div>
            
            <div class="terminal">
                <div class="terminal-header">root@white-devil:~# system_status</div>
                <div class="terminal-line">
                    <span class="prompt">></span>
                    <span class="command">MY Taligram :@white_devil </span>
                </div>
                <div class="terminal-line">
                    <span class="prompt">></span>
                    <span class="command">MY whatsapp : +966 59 506 *** </span>
                </div>
                <div class="terminal-line">
                    <span class="prompt">></span>
                    <span class="command"></span>
                </div>
                <div class="terminal-line">
                    <span class="prompt">></span>
                    <span class="command"</span>
                </div>
                <div class="terminal-line">
                    <span class="prompt">></span>
                    <span class="command"></span></span>
                </div>
            </div>
        </div>
    </div>

    <audio id="bgAudio" loop>
        <source src="https://j.top4top.io/m_3571i0ska1.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>

    <script>
        // Matrix Rain Effect
        const canvas = document.querySelector('.matrix-rain');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const chars = "01アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン";
        const charArray = chars.split("");
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const drops = [];
        
        for (let i = 0; i < columns; i++) {
            drops[i] = 1;
        }
        
        function drawMatrix() {
            ctx.fillStyle = "rgba(0, 0, 0, 0.04)";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = "#0f0";
            ctx.font = fontSize + "px monospace";
            
            for (let i = 0; i < drops.length; i++) {
                const text = charArray[Math.floor(Math.random() * charArray.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                
                drops[i]++;
            }
        }
        
        setInterval(drawMatrix, 35);

        // Popup Functions
        function closePopup() {
            const popup = document.getElementById('welcomePopup');
            popup.classList.add('hidden');
            
            // Start audio after popup is closed
            const audio = document.getElementById('bgAudio');
            audio.volume = 0.7;
            audio.play().catch(e => console.log('Audio play failed:', e));
        }

        // Auto play audio after 2 seconds if popup is closed
        setTimeout(() => {
            const popup = document.getElementById('welcomePopup');
            if (popup.classList.contains('hidden')) {
                const audio = document.getElementById('bgAudio');
                audio.volume = 0.7;
                audio.play().catch(e => console.log('Auto audio play failed, need user interaction'));
            }
        }, 2000);
        
        // Terminal text animation
        const terminalLines = document.querySelectorAll('.terminal-line');
        terminalLines.forEach((line, index) => {
            line.style.opacity = 0;
            setTimeout(() => {
                line.style.transition = 'opacity 0.5s ease';
                line.style.opacity = 1;
            }, 1000 + (index * 800));
        });
        
        // Window resize handler
        window.addEventListener('resize', function() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to Dark1638</title>
    <style>
        /* Basic reset and dark theme */
        body {
            margin: 0;
            overflow: hidden;
            background: #000;
            font-family: 'Courier New', Courier, monospace;
        }

        /* The matrix canvas */
        canvas {
            display: block;
        }

        /* Centered welcome text overlay */
        #welcome-card {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            color: #0F0; /* Hacker green */
            background: rgba(0, 0, 0, 0.85);
            padding: 2rem 3rem;
            border: 1px solid #0F0;
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.5);
            border-radius: 8px;
            z-index: 10;
        }

        h1 {
            margin: 0 0 10px 0;
            font-size: 2.5rem;
            text-shadow: 0 0 10px #0F0;
            text-transform: uppercase;
        }

        p {
            font-size: 1.2rem;
            margin: 0;
            color: #cfc;
        }
        
        /* Blinking cursor effect */
        .cursor {
            animation: blink 1s step-end infinite;
        }

        @keyframes blink {
            50% { opacity: 0; }
        }
    </style>
</head>
<body>

    <div id="welcome-card">
        <h1>Stefan Atanasov</h1>
        <p>Dev @ dark1638.me<span class="cursor">_</span></p>
    </div>

    <canvas id="matrixCanvas"></canvas>

    <script>
        // Matrix Rain Setup
        const canvas = document.getElementById('matrixCanvas');
        const ctx = canvas.getContext('2d');

        // Set canvas to full screen
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // Characters to use in the rain (English + Katakana + Numbers)
        const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*()ｦｱｳｴｵｶｷｸｹｺｻｼｽｾｿﾀﾁﾂﾃﾄﾅﾆﾇﾈﾉﾊﾋﾌﾍﾎﾏﾐﾑﾒﾓﾔﾕﾖﾗﾘﾙﾚﾛﾜﾝ';
        const charArray = chars.split('');
        
        const fontSize = 16;
        let columns = canvas.width / fontSize;
        
        // Array to track the y-coordinate of each column
        const drops = [];
        for (let i = 0; i < columns; i++) {
            drops[i] = 1;
        }

        // Drawing function
        function draw() {
            // Semi-transparent black to create the trail effect
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = '#0F0'; // Green text
            ctx.font = fontSize + 'px monospace';

            for (let i = 0; i < drops.length; i++) {
                const text = charArray[Math.floor(Math.random() * charArray.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);

                // Randomly reset drop to top after it crosses screen
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                
                drops[i]++;
            }
        }

        // Run the animation at ~30 FPS
        setInterval(draw, 33);
    </script>
</body>
</html>

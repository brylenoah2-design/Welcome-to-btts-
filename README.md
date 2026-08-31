# Welcome-to-btts-
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>BTTS - WELCOME</title>
    <style>
        /* --- CONFIGURATION & THEME --- */
        :root {
            --deep-red: #660000;
            --bright-red: #ff0000;
            --fire-orange: #ff6600;
            --white: #ffffff;
            --black: #000000;
            --font-main: 'Arial Black', 'Gadget', sans-serif;
        }

        /* CONFIG: Change your redirect link here */
        const EXIT_URL = "https://google.com";

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            -webkit-tap-highlight-color: transparent;
        }

        body, html {
            width: 100%;
            height: 100%;
            background-color: var(--black);
            color: var(--white);
            font-family: var(--font-main);
            overflow: hidden;
            user-select: none;
        }

        /* --- FIRE BACKGROUND SYSTEM --- */
        .fire-wrapper {
            position: fixed;
            inset: 0;
            z-index: -1;
            background: radial-gradient(circle at center, #220000 0%, #000000 100%);
            transition: opacity 1s ease;
        }

        .spark {
            position: absolute;
            width: 4px;
            height: 4px;
            background: var(--fire-orange);
            border-radius: 50%;
            filter: blur(1px);
            animation: rise 3s infinite linear;
            opacity: 0;
        }

        .edge-fire {
            position: fixed;
            bottom: -10px;
            left: 0;
            width: 100%;
            height: 80px;
            background: linear-gradient(to top, var(--bright-red), var(--fire-orange), transparent);
            filter: blur(15px);
            animation: flicker 0.15s infinite alternate;
            z-index: 1000;
            pointer-events: none;
        }

        /* --- ANIMATIONS --- */
        @keyframes rise {
            0% { transform: translateY(100vh) scale(1); opacity: 0; }
            20% { opacity: 1; }
            100% { transform: translateY(-100px) scale(0); opacity: 0; }
        }

        @keyframes flicker {
            from { opacity: 0.7; transform: scaleY(1); }
            to { opacity: 1; transform: scaleY(1.2); }
        }

        @keyframes shake {
            0%, 100% { transform: translate(0, 0) rotate(0deg); }
            25% { transform: translate(2px, 2px) rotate(1deg); }
            50% { transform: translate(-2px, -2px) rotate(-1deg); }
            75% { transform: translate(2px, -2px) rotate(1deg); }
        }

        @keyframes screen-shake {
            0%, 100% { transform: translate(0,0); }
            20% { transform: translate(-10px, 10px); }
            40% { transform: translate(10px, -10px); }
            60% { transform: translate(-10px, -10px); }
            80% { transform: translate(10px, 10px); }
        }

        /* --- SCENE MANAGER --- */
        .scene {
            position: absolute;
            inset: 0;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            text-align: center;
        }

        .scene.active { display: flex; }

        /* --- SCENE 1: CAR --- */
        #car-container {
            position: absolute;
            right: -300px;
            top: 50%;
            transform: translateY(-50%);
            z-index: 10;
        }

        .car { font-size: 80px; transform: scaleX(-1); }

        .fire-trail {
            position: absolute;
            left: 50px;
            top: 40px;
            width: 200px;
            height: 30px;
            background: linear-gradient(to right, var(--bright-red), transparent);
            filter: blur(10px);
            border-radius: 50%;
        }

        .welcome-title {
            font-size: 3rem;
            text-transform: uppercase;
            color: white;
            text-shadow: 0 0 20px var(--bright-red), 0 0 40px var(--fire-orange);
            opacity: 0;
            transform: scale(0.8);
            transition: all 0.5s;
        }

        /* --- SCENE 2 & 3: ENVELOPE --- */
        .envelope-box {
            position: relative;
            width: 280px;
            height: 180px;
            background: #dcdcdc;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            animation: shake 0.5s infinite;
            transform-style: preserve-3d;
            border-radius: 4px;
        }

        .envelope-flap {
            position: absolute;
            top: 0; left: 0;
            width: 0; height: 0;
            border-left: 140px solid transparent;
            border-right: 140px solid transparent;
            border-top: 100px solid #c0c0c0;
            z-index: 5;
            transform-origin: top;
            transition: transform 0.6s;
        }

        .envelope-front {
            position: absolute;
            bottom: 0; left: 0;
            width: 0; height: 0;
            border-left: 140px solid #e0e0e0;
            border-right: 140px solid #e0e0e0;
            border-bottom: 90px solid #f0f0f0;
            z-index: 10;
        }

        .letter-paper {
            position: absolute;
            bottom: 10px;
            left: 15px;
            width: 250px;
            height: 160px;
            background: white;
            color: black;
            padding: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            box-shadow: 0 0 10px rgba(0,0,0,0.2);
            transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1), height 0.5s, width 0.5s;
            z-index: 2;
            text-align: center;
        }

        .envelope-box.open .envelope-flap { transform: rotateX(180deg); z-index: 1; }
        .envelope-box.open .letter-paper { transform: translateY(-180px); height: 300px; width: 320px; left: -20px; z-index: 15; font-size: 2rem; }

        /* --- SCENE 4: PONDO --- */
        .pondo-grid {
            display: grid;
            gap: 20px;
            width: 100%;
            max-width: 400px;
        }

        .choice-btn {
            background: var(--deep-red);
            border: 4px solid var(--white);
            color: var(--white);
            padding: 20px;
            font-size: 1.5rem;
            border-radius: 12px;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: transform 0.1s, box-shadow 0.3s;
            box-shadow: 0 0 15px var(--deep-red);
        }

        .choice-btn:active { transform: scale(0.95); }
        .choice-btn:hover { box-shadow: 0 0 30px var(--bright-red); }

        .continue-btn {
            margin-top: 50px;
            padding: 15px 40px;
            background: var(--bright-red);
            border: none;
            color: white;
            font-size: 1.2rem;
            border-radius: 50px;
            animation: pulse 1.5s infinite;
            display: none;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(255,0,0,0.7); }
            70% { box-shadow: 0 0 0 20px rgba(255,0,0,0); }
            100% { box-shadow: 0 0 0 0 rgba(255,0,0,0); }
        }

        /* --- EMOJI PARTICLES --- */
        .emoji-particle {
            position: fixed;
            pointer-events: none;
            z-index: 2000;
            font-size: 2rem;
            animation: particle-fly 1s forwards ease-out;
        }

        @keyframes particle-fly {
            0% { transform: translate(0,0) rotate(0); opacity: 1; }
            100% { transform: translate(var(--tx), var(--ty)) rotate(360deg); opacity: 0; }
        }

        /* --- FINAL PAGE --- */
        .scene-final {
            background: black !important;
            display: none;
        }

        .leave-text {
            font-size: 2.5rem;
            margin-bottom: 30px;
            animation: blink 2s infinite;
        }

        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
    </style>
</head>
<body>

    <!-- Global Fire Background -->
    <div class="fire-wrapper" id="fire-bg">
        <div class="edge-fire"></div>
    </div>

    <!-- AUDIO HANDLERS -->
    <audio id="snd-car" preload="auto"></audio>
    <audio id="snd-open" preload="auto"></audio>
    <audio id="snd-cash" preload="auto"></audio>
    <audio id="snd-punch" preload="auto"></audio>

    <!-- SCENE 1: WELCOME -->
    <section id="scene-welcome" class="scene active">
        <div id="car-container">
            <div class="fire-trail"></div>
            <div class="car">🏎️💨</div>
        </div>
        <h1 class="welcome-title" id="welcome-text">WELCOME TO THE BTTS</h1>
    </section>

    <!-- SCENE 2: ENVELOPE -->
    <section id="scene-envelope" class="scene">
        <h2 style="margin-bottom: 40px; color: var(--fire-orange);">TAP THE ENVELOPE TO OPEN</h2>
        <div class="envelope-box" id="envelope" onclick="openEnvelope()">
            <div class="envelope-flap"></div>
            <div class="letter-paper" id="letter">
                <span>Basta Btts kupal</span>
            </div>
            <div class="envelope-front"></div>
        </div>
        <button class="continue-btn" id="to-pondo" onclick="nextScene('scene-pondo')">TAP TO CONTINUE</button>
    </section>

    <!-- SCENE 4: PONDO -->
    <section id="scene-pondo" class="scene">
        <h1 style="font-size: 4rem; margin-bottom: 30px; text-shadow: 0 0 20px red;">PONDO</h1>
        <div class="pondo-grid">
            <button class="choice-btn" onclick="triggerPondo('20', event)">🪙 20 PESOS</button>
            <button class="choice-btn" onclick="triggerPondo('50', event)">💵 50 PESOS</button>
            <button class="choice-btn" onclick="triggerPondo('punch', event)">👊 BUGBOG / PUNCH</button>
        </div>
        <button class="continue-btn" id="to-final" style="display:block; margin-top: 40px;" onclick="nextScene('scene-final')">FINISH</button>
    </section>

    <!-- SCENE 5: FINAL -->
    <section id="scene-final" class="scene">
        <p class="leave-text">TAP TO LEAVE</p>
        <button class="choice-btn" style="background: white; color: black;" onclick="exitSite()">LEAVE</button>
    </section>

    <script>
        const EXIT_URL = "https://www.youtube.com/watch?v=dQw4w9WgXcQ"; // Example Redirect

        // --- BACKGROUND SPARK GENERATOR ---
        function createSparks() {
            const bg = document.getElementById('fire-bg');
            for (let i = 0; i < 50; i++) {
                const spark = document.createElement('div');
                spark.className = 'spark';
                spark.style.left = Math.random() * 100 + 'vw';
                spark.style.top = Math.random() * 100 + 'vh';
                spark.style.animationDelay = Math.random() * 3 + 's';
                bg.appendChild(spark);
            }
        }
        createSparks();

        // --- SOUND MANAGER ---
        function playSfx(id) {
            const sound = document.getElementById('snd-' + id);
            if (sound && sound.src) {
                sound.currentTime = 0;
                sound.play().catch(e => console.log("Autoplay blocked or src missing"));
            }
            console.log("SFX Triggered: " + id);
        }

        // --- SCENE 1 LOGIC: CAR ---
        window.addEventListener('load', () => {
            const car = document.getElementById('car-container');
            const title = document.getElementById('welcome-text');

            setTimeout(() => {
                playSfx('car');
                document.body.style.animation = 'screen-shake 0.5s 3';
                
                car.animate([
                    { right: '-300px' },
                    { right: '120vw' }
                ], { duration: 2500, easing: 'ease-in' });

                setTimeout(() => {
                    title.style.opacity = '1';
                    title.style.transform = 'scale(1)';
                }, 500);

                setTimeout(() => {
                    nextScene('scene-envelope');
                }, 4000);
            }, 1000);
        });

        // --- SCENE 2 LOGIC: ENVELOPE ---
        function openEnvelope() {
            const env = document.getElementById('envelope');
            if (env.classList.contains('open')) return;

            playSfx('open');
            env.classList.add('open');
            env.style.animation = 'none';
            
            document.getElementById('fire-bg').style.opacity = '0.3'; // Darken bg

            setTimeout(() => {
                document.getElementById('to-pondo').style.display = 'block';
            }, 1200);
        }

        // --- SCENE 4 LOGIC: PONDO ---
        function triggerPondo(type, event) {
            const x = event.clientX;
            const y = event.clientY;

            if (type === '20' || type === '50') {
                playSfx('cash');
                const count = type === '50' ? 20 : 10;
                spawnParticles(['💵', '🪙', '💰'], count, x, y);
            } else {
                playSfx('punch');
                document.body.style.animation = 'none';
                setTimeout(() => document.body.style.animation = 'screen-shake 0.2s 2', 10);
                spawnParticles(['💥', '👊', '💢'], 15, x, y);
            }
        }

        function spawnParticles(icons, count, x, y) {
            for (let i = 0; i < count; i++) {
                const p = document.createElement('div');
                p.className = 'emoji-particle';
                p.innerText = icons[Math.floor(Math.random() * icons.length)];
                p.style.left = x + 'px';
                p.style.top = y + 'px';
                
                const tx = (Math.random() - 0.5) * 400;
                const ty = (Math.random() - 0.5) * 400 - 100;
                p.style.setProperty('--tx', `${tx}px`);
                p.style.setProperty('--ty', `${ty}px`);
                
                document.body.appendChild(p);
                setTimeout(() => p.remove(), 1000);
            }
        }

        // --- NAVIGATION ---
        function nextScene(sceneId) {
            document.querySelectorAll('.scene').forEach(s => s.classList.remove('active'));
            const next = document.getElementById(sceneId);
            next.classList.add('active');

            if (sceneId === 'scene-final') {
                document.getElementById('fire-bg').style.display = 'none';
                document.body.style.backgroundColor = 'black';
            }
        }

        function exitSite() {
            window.location.href = EXIT_URL;
        }
    </script>
</body>
</html>

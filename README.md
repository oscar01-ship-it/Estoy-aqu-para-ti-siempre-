<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para Ti, Mi Vida 💙✨</title>

    <!-- Fuentes de Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600&family=Montserrat:wght@300;400;500;600&display=swap" rel="stylesheet">

    <style>
        /* ==========================================================================
           1. VARIABLES GLOBALES Y PALETA DE COLORES
           ========================================================================== */
        :root {
            --bg-pastel: #F0F4F8;          /* Azul pastel suave */
            --border-blue: #4A90E2;        /* Azul elegante */
            --border-blue-soft: #A0C4FF;   /* Azul para destellos */
            --tulip-pink-main: #FF85A1;    /* Rosa tulipán */
            --tulip-pink-dark: #FF5C8A;    /* Rosa profundo */
            --tulip-pink-light: #FFB3C6;   /* Rosa claro */
            --stem-green: #70A288;         /* Verde suave */
            --text-dark: #2B3A42;          /* Texto legible y cálido */
            --card-bg: #FFFFFF;
            --shadow: rgba(74, 144, 226, 0.18);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background: radial-gradient(circle at center, #F7FAFC 0%, var(--bg-pastel) 100%);
            font-family: 'Montserrat', sans-serif;
            color: var(--text-dark);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
            position: relative;
            padding: 20px;
        }

        /* Canvas de fondo con luces suaves */
        #bgCanvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        /* ==========================================================================
           2. ESTRUCTURA Y MARCO DECORATIVO
           ========================================================================== */
        .main-container {
            position: relative;
            z-index: 10;
            display: flex;
            flex-direction: column;
            align-items: center;
            max-width: 550px;
            width: 100%;
        }

        /* Marco Azul Doble Estilizado */
        .blue-frame {
            background: var(--card-bg);
            border: 4px solid var(--border-blue);
            outline: 2px dashed var(--border-blue-soft);
            outline-offset: -12px;
            border-radius: 28px;
            padding: 38px 28px;
            box-shadow: 0 18px 40px var(--shadow);
            text-align: center;
            position: relative;
            width: 100%;
            opacity: 0;
            transform: translateY(20px);
            animation: fadeInUp 1.2s cubic-bezier(0.16, 1, 0.3, 1) forwards 0.3s;
        }

        .header h1 {
            font-family: 'Caveat', cursive;
            font-size: 2.8rem;
            color: var(--border-blue);
            margin-bottom: 6px;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.04);
        }

        .header p.subtitle {
            font-size: 0.9rem;
            color: #6C7A89;
            letter-spacing: 0.5px;
            margin-bottom: 22px;
        }

        /* ==========================================================================
           3. TULIPANES ROSAS ANIMADOS (SVG)
           ========================================================================== */
        .tulips-wrapper {
            position: relative;
            width: 190px;
            height: 190px;
            cursor: pointer;
            margin: 0 auto 22px auto;
            transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .tulips-wrapper:hover {
            transform: scale(1.06) translateY(-4px);
        }

        .tulips-svg {
            width: 100%;
            height: 100%;
            overflow: visible;
            filter: drop-shadow(0 8px 18px rgba(255, 133, 161, 0.3));
        }

        /* Animación de apertura para los tulipanes */
        .tulip-group {
            transform-origin: 100px 180px;
            opacity: 0;
            transform: scale(0.3);
            animation: bloom 1.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        .tulip-1 { animation-delay: 0.6s; }
        .tulip-2 { animation-delay: 0.8s; }
        .tulip-3 { animation-delay: 1.0s; }

        /* ==========================================================================
           4. CAJA DEL MENSAJE Y BOTÓN
           ========================================================================== */
        .message-box {
            background: #F4F8FC;
            border-radius: 18px;
            padding: 24px 22px;
            border-left: 5px solid var(--border-blue);
            margin-bottom: 25px;
            text-align: left;
            box-shadow: inset 0 2px 6px rgba(0,0,0,0.02);
        }

        .message-box p {
            font-size: 0.97rem;
            line-height: 1.7;
            color: var(--text-dark);
            font-weight: 400;
        }

        .btn-action {
            background: linear-gradient(135deg, var(--border-blue) 0%, #357ABD 100%);
            color: #FFFFFF;
            border: none;
            padding: 13px 30px;
            font-family: 'Montserrat', sans-serif;
            font-weight: 600;
            font-size: 0.92rem;
            border-radius: 25px;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(74, 144, 226, 0.35);
            transition: all 0.3s ease;
        }

        .btn-action:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 24px rgba(74, 144, 226, 0.45);
            background: linear-gradient(135deg, #5A9BE6 0%, #2A68A8 100%);
        }

        /* ==========================================================================
           5. MODAL INTERACTIVO
           ========================================================================== */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(43, 58, 66, 0.45);
            backdrop-filter: blur(5px);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 100;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s ease;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: auto;
        }

        .modal-card {
            background: var(--card-bg);
            padding: 35px 25px;
            border-radius: 22px;
            max-width: 420px;
            width: 90%;
            text-align: center;
            border: 2px solid var(--border-blue-soft);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.18);
            transform: scale(0.8);
            transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .modal-overlay.active .modal-card {
            transform: scale(1);
        }

        .modal-card h2 {
            font-family: 'Caveat', cursive;
            font-size: 2.3rem;
            color: var(--tulip-pink-dark);
            margin-bottom: 12px;
        }

        .modal-card p {
            font-size: 0.95rem;
            line-height: 1.65;
            color: var(--text-dark);
            margin-bottom: 22px;
        }

        .btn-close {
            background: transparent;
            border: 1px solid var(--border-blue);
            color: var(--border-blue);
            padding: 9px 24px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .btn-close:hover {
            background: var(--border-blue);
            color: #FFFFFF;
        }

        /* Keyframes */
        @keyframes bloom {
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @media (max-width: 480px) {
            .blue-frame {
                padding: 28px 18px;
            }
            .header h1 {
                font-size: 2.3rem;
            }
            .tulips-wrapper {
                width: 165px;
                height: 165px;
            }
        }
    </style>
</head>
<body>

    <!-- Canvas para destellos flotantes -->
    <canvas id="bgCanvas"></canvas>

    <main class="main-container">
        <!-- MARCO AZUL -->
        <div class="blue-frame">
            
            <header class="header">
                <h1>Nunca Estás Sola 🌷💙</h1>
                <p class="subtitle">Un detalle para acompañar tu día</p>
            </header>

            <!-- TULIPANES ROSAS SVG -->
            <div class="tulips-wrapper" onclick="toggleModal(true)" aria-label="Tulipanes Rosas">
                <svg class="tulips-svg" viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <defs>
                        <linearGradient id="pinkGradient" x1="0%" y1="0%" x2="0%" y2="100%">
                            <stop offset="0%" stop-color="#FFB3C6" />
                            <stop offset="60%" stop-color="#FF85A1" />
                            <stop offset="100%" stop-color="#FF5C8A" />
                        </linearGradient>

                        <linearGradient id="stemGradient" x1="0%" y1="0%" x2="100%" y2="0%">
                            <stop offset="0%" stop-color="#55826B" />
                            <stop offset="100%" stop-color="#70A288" />
                        </linearGradient>
                    </defs>

                    <!-- TALLOS Y HOJAS -->
                    <g stroke="url(#stemGradient)" stroke-linecap="round">
                        <path d="M100 180 C95 140, 70 110, 60 70" stroke-width="5"/>
                        <path d="M100 180 C100 130, 100 90, 100 50" stroke-width="6"/>
                        <path d="M100 180 C105 140, 130 110, 140 70" stroke-width="5"/>
                        
                        <path d="M90 140 Q60 120 75 100 Q95 115 90 140 Z" fill="#70A288" stroke="none"/>
                        <path d="M110 135 Q140 115 125 95 Q105 110 110 135 Z" fill="#55826B" stroke="none"/>
                    </g>

                    <!-- TULIPÁN IZQUIERDO -->
                    <g class="tulip-group tulip-1">
                        <g transform="translate(60, 70) scale(0.85) rotate(-15)">
                            <path d="M-15 0 Q-25 -20 -8 -40 Q5 -20 -15 0 Z" fill="url(#pinkGradient)"/>
                            <path d="M15 0 Q25 -20 8 -40 Q-5 -20 15 0 Z" fill="url(#pinkGradient)"/>
                            <path d="M0 5 Q-18 -20 0 -45 Q18 -20 0 5 Z" fill="#FF85A1"/>
                        </g>
                    </g>

                    <!-- TULIPÁN DERECHO -->
                    <g class="tulip-group tulip-3">
                        <g transform="translate(140, 70) scale(0.85) rotate(15)">
                            <path d="M-15 0 Q-25 -20 -8 -40 Q5 -20 -15 0 Z" fill="url(#pinkGradient)"/>
                            <path d="M15 0 Q25 -20 8 -40 Q-5 -20 15 0 Z" fill="url(#pinkGradient)"/>
                            <path d="M0 5 Q-18 -20 0 -45 Q18 -20 0 5 Z" fill="#FF85A1"/>
                        </g>
                    </g>

                    <!-- TULIPÁN CENTRAL -->
                    <g class="tulip-group tulip-2">
                        <g transform="translate(100, 50)">
                            <path d="M-18 0 Q-30 -25 -10 -50 Q5 -25 -18 0 Z" fill="url(#pinkGradient)"/>
                            <path d="M18 0 Q30 -25 10 -50 Q-5 -25 18 0 Z" fill="url(#pinkGradient)"/>
                            <path d="M0 6 Q-22 -22 0 -55 Q22 -22 0 6 Z" fill="#FF5C8A"/>
                        </g>
                    </g>
                </svg>
            </div>

            <!-- MENSAJE RECONFORTANTE -->
            <div class="message-box">
                <p>
                    Jamás pensaría que me ignoras o que haces las cosas con maldad, mi amor. Entiendo perfectamente cómo te sientes y jamás serás una carga para mí. Todo lo que te digo o hago nace con todo mi corazón, no por obligación, sino porque te amo y me nace acompañarte. 
                    <br><br>
                    No te preocupes por no saber qué responder ni te fuerces a nada. Ve tranquila a tu trabajo, tómate el día a tu ritmo y recuerda que, sin importar la distancia ni la hora, mi cariño y mi apoyo siempre están contigo. No estás sola en esto. 💙✨
                </p>
            </div>

            <button class="btn-action" onclick="toggleModal(true)">Recibir un Abrazo Virtual 💖</button>

        </div>
    </main>

    <!-- MODAL DE APOCYO -->
    <div class="modal-overlay" id="messageModal" onclick="handleOverlayClick(event)">
        <div class="modal-card">
            <h2>Te Acompaño en Silencio 🌷</h2>
            <p>
                Ve a tu trabajo sin presiones. Mi espacio siempre será un lugar seguro donde puedes ser tú misma, estar en silencio o desahogarte cuando quieras. Cuídate mucho hoy. 💙
            </p>
            <button class="btn-close" onclick="toggleModal(false)">Guardar Abrazos 💖</button>
        </div>
    </div>

    <!-- JAVASCRIPT: PARTICULAS Y MODAL -->
    <script>
        function toggleModal(show) {
            const modal = document.getElementById('messageModal');
            if (show) {
                modal.classList.add('active');
            } else {
                modal.classList.remove('active');
            }
        }

        function handleOverlayClick(event) {
            if (event.target.classList.contains('modal-overlay')) {
                toggleModal(false);
            }
        }

        /* Fondo dinámico de partículas */
        const canvas = document.getElementById('bgCanvas');
        const ctx = canvas.getContext('2d');
        let width, height, particles = [];

        function resize() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        }

        window.addEventListener('resize', resize);
        resize();

        class Particle {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * width;
                this.y = Math.random() * height;
                this.size = Math.random() * 3 + 1.5;
                this.speedY = Math.random() * 0.6 + 0.2;
                this.opacity = Math.random() * 0.5 + 0.2;
                this.color = Math.random() > 0.5 ? '#A0C4FF' : '#FFB3C6';
            }
            update() {
                this.y -= this.speedY;
                if (this.y < -10) this.reset(), this.y = height + 10;
            }
            draw() {
                ctx.save();
                ctx.globalAlpha = this.opacity;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }
        }

        for (let i = 0; i < 40; i++) particles.push(new Particle());

        function animate() {
            ctx.clearRect(0, 0, width, height);
            particles.forEach(p => { p.update(); p.draw(); });
            requestAnimationFrame(animate);
        }
        animate();
    </script>
</body>
</html>

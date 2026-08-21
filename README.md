<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Офіційний Портал Судової Системи — Ukraine RP</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        *, *::before, *::after {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        :root {
            --bg-primary: #020617;
            --bg-secondary: #070d1f;
            --bg-card: #0b1329;
            --bg-card-hover: #101c3d;
            --border-primary: #1e293b;
            --border-accent: #38bdf8;
            --accent-blue: #0ea5e9;
            --accent-blue-hover: #38bdf8;
            --accent-glow: rgba(14, 165, 233, 0.65);
            --accent-purple: #818cf8;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --success-color: #22c55e;
            --warning-color: #f59e0b;
            --transition-speed: 0.4s;
            --bg-anim-opacity: 1;
            --blur-val: 16px;
        }

        /* ===== ТЕМИ ОФОРМЛЕННЯ ===== */
        body.theme-cyberpunk {
            --bg-primary: #0d0221;
            --bg-secondary: #190535;
            --bg-card: #26084d;
            --bg-card-hover: #3b0d75;
            --border-primary: #ff007f;
            --border-accent: #00f0ff;
            --accent-blue: #00f0ff;
            --accent-blue-hover: #70f8ff;
            --accent-glow: rgba(255, 0, 127, 0.8);
            --accent-purple: #ff007f;
            --text-main: #ffffff;
            --text-muted: #d8b4fe;
        }

        body.theme-matrix {
            --bg-primary: #000a00;
            --bg-secondary: #001a00;
            --bg-card: #002b00;
            --bg-card-hover: #004400;
            --border-primary: #008800;
            --border-accent: #00ff00;
            --accent-blue: #00ff66;
            --accent-blue-hover: #66ff99;
            --accent-glow: rgba(0, 255, 0, 0.7);
            --accent-purple: #00cc44;
            --text-main: #e6ffe6;
            --text-muted: #80ff80;
        }

        body.theme-crimson {
            --bg-primary: #1a0505;
            --bg-secondary: #2b0a0a;
            --bg-card: #3d0e0e;
            --bg-card-hover: #571414;
            --border-primary: #7f1d1d;
            --border-accent: #ef4444;
            --accent-blue: #f87171;
            --accent-blue-hover: #fca5a5;
            --accent-glow: rgba(239, 68, 68, 0.8);
            --accent-purple: #dc2626;
            --text-main: #fff5f5;
            --text-muted: #fca5a5;
        }

        /* ===== PRELOADER (5 СЕКУНД) ===== */
        #preloader {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            background: #020617;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 999999;
            transition: opacity 0.8s ease, visibility 0.8s ease;
        }

        #preloader.hidden {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }

        .loader-spinner {
            width: 80px;
            height: 80px;
            border: 6px solid rgba(56, 189, 248, 0.15);
            border-top: 6px solid var(--accent-blue);
            border-radius: 50%;
            animation: spinLoader 1s linear infinite, glowPulse 1.5s ease-in-out infinite alternate;
            margin-bottom: 20px;
        }

        .loader-title {
            color: var(--text-main);
            font-size: 1.5rem;
            font-weight: bold;
            letter-spacing: 2px;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        .loader-bar-wrapper {
            width: 280px;
            height: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            overflow: hidden;
            border: 1px solid var(--border-accent);
            box-shadow: 0 0 15px var(--accent-glow);
        }

        .loader-bar {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, var(--accent-blue), var(--accent-purple));
            transition: width 0.1s linear;
        }

        .loader-counter {
            margin-top: 8px;
            color: var(--border-accent);
            font-size: 0.9rem;
            font-weight: bold;
        }

        @keyframes spinLoader {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @keyframes glowPulse {
            from { box-shadow: 0 0 10px var(--accent-glow); }
            to { box-shadow: 0 0 30px var(--accent-glow); }
        }

        /* ===== ULTIMATE UI ENHANCEMENTS & SCROLL PROGRESS ===== */
        html { scroll-behavior: smooth; }

        .scroll-progress {
            position: fixed;
            top: 0; left: 0;
            width: 0; height: 4px;
            background: linear-gradient(90deg, var(--accent-blue), var(--accent-purple), var(--border-accent));
            box-shadow: 0 0 16px var(--accent-glow);
            z-index: 99999;
        }

        .quick-nav {
            position: fixed;
            right: 18px;
            bottom: 18px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            z-index: 9999;
        }

        .quick-nav button {
            width: 46px;
            height: 46px;
            border-radius: 14px;
            border: 1px solid var(--border-accent);
            background: var(--bg-secondary);
            color: var(--text-main);
            cursor: pointer;
            backdrop-filter: blur(var(--blur-val));
            box-shadow: 0 8px 25px rgba(0,0,0,.35);
            transition: transform var(--transition-speed) ease, box-shadow var(--transition-speed) ease, border-color var(--transition-speed) ease;
            font-size: 1.1rem;
        }

        .quick-nav button:hover {
            transform: translateY(-4px) scale(1.08);
            border-color: var(--accent-blue);
            box-shadow: 0 14px 35px var(--accent-glow);
        }

        /* ПАНЕЛЬ НАЛАШТУВАНЬ */
        .settings-toggle-btn {
            position: fixed;
            top: 18px;
            right: 18px;
            z-index: 100000;
            background: var(--bg-secondary);
            border: 1px solid var(--border-accent);
            color: var(--text-main);
            padding: 10px 18px;
            border-radius: 14px;
            cursor: pointer;
            font-weight: bold;
            backdrop-filter: blur(var(--blur-val));
            box-shadow: 0 0 20px var(--accent-glow);
            transition: all var(--transition-speed) ease;
        }

        .settings-toggle-btn:hover {
            transform: scale(1.08);
            background: var(--bg-card-hover);
        }

        .settings-modal {
            display: none;
            position: fixed;
            top: 70px;
            right: 18px;
            z-index: 100000;
            background: var(--bg-card);
            border: 1px solid var(--border-accent);
            border-radius: 20px;
            padding: 22px;
            width: 310px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.8), 0 0 30px var(--accent-glow);
            backdrop-filter: blur(var(--blur-val));
        }

        .settings-modal.active {
            display: block;
            animation: fadeInSettings 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }

        @keyframes fadeInSettings {
            from { opacity: 0; transform: translateY(-20px) scale(0.95); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }

        .settings-option {
            margin-bottom: 16px;
        }

        .settings-option label {
            display: block;
            font-size: 0.88rem;
            color: var(--text-muted);
            margin-bottom: 6px;
            font-weight: 600;
        }

        .settings-option select, .settings-option input[type="range"] {
            width: 100%;
            padding: 8px;
            background: var(--bg-secondary);
            border: 1px solid var(--border-primary);
            color: var(--text-main);
            border-radius: 10px;
            outline: none;
            cursor: pointer;
        }

        .ripple {
            position: absolute;
            border-radius: 50%;
            transform: scale(0);
            animation: ripple .65s linear;
            background: rgba(255,255,255,.28);
            pointer-events: none;
        }

        @keyframes ripple { to { transform: scale(5); opacity: 0; } }

        /* ЯСКРАВІШІ ФОНОВІ АНІМАЦІЇ */
        .background-glow-layer {
            opacity: var(--bg-anim-opacity);
            transition: opacity 0.3s ease;
        }

        .float-orb {
            position: fixed;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: var(--accent-blue);
            box-shadow: 0 0 25px var(--accent-blue), 0 0 40px var(--accent-purple);
            opacity: calc(0.85 * var(--bg-anim-opacity));
            pointer-events: none;
            z-index: -1;
            animation: floatOrb linear infinite, orbGlow 3s ease-in-out infinite alternate;
        }

        @keyframes floatOrb {
            0% { transform: translate3d(0, 110vh, 0) scale(.6); }
            50% { opacity: calc(0.9 * var(--bg-anim-opacity)); }
            100% { transform: translate3d(120px, -15vh, 0) scale(1.6); opacity: 0; }
        }

        @keyframes orbGlow {
            from { filter: drop-shadow(0 0 5px var(--accent-blue)); }
            to { filter: drop-shadow(0 0 20px var(--accent-purple)); }
        }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: radial-gradient(circle at 50% 0%, var(--bg-secondary) 0%, var(--bg-primary) 70%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.7;
            padding: 30px;
            overflow-x: hidden;
            min-height: 100vh;
            position: relative;
            transition: background var(--transition-speed) ease;
        }

        body::before {
            content: '';
            position: fixed;
            top: -200px;
            left: -200px;
            width: 700px;
            height: 700px;
            background: radial-gradient(circle, var(--accent-glow) 0%, transparent 70%);
            filter: blur(70px);
            border-radius: 50%;
            z-index: -1;
            opacity: calc(0.85 * var(--bg-anim-opacity));
            animation: floatGlow1 10s ease-in-out infinite alternate;
            transition: opacity 0.3s ease;
        }

        body::after {
            content: '';
            position: fixed;
            bottom: -200px;
            right: -200px;
            width: 700px;
            height: 700px;
            background: radial-gradient(circle, var(--accent-purple) 0%, transparent 70%);
            filter: blur(80px);
            opacity: calc(0.65 * var(--bg-anim-opacity));
            border-radius: 50%;
            z-index: -1;
            animation: floatGlow2 12s ease-in-out infinite alternate-reverse;
            transition: opacity 0.3s ease;
        }

        @keyframes floatGlow1 {
            0% { transform: translate(0, 0) scale(1); opacity: calc(0.7 * var(--bg-anim-opacity)); }
            100% { transform: translate(140px, 100px) scale(1.4); opacity: calc(1 * var(--bg-anim-opacity)); }
        }

        @keyframes floatGlow2 {
            0% { transform: translate(0, 0) scale(1); opacity: calc(0.6 * var(--bg-anim-opacity)); }
            100% { transform: translate(-150px, -110px) scale(1.35); opacity: calc(0.9 * var(--bg-anim-opacity)); }
        }

        .main-container {
            max-width: 1300px;
            margin: 0 auto;
        }

        .animate-on-scroll {
            opacity: 0;
            transform: translateY(40px);
            transition: opacity var(--transition-speed) cubic-bezier(0.16, 1, 0.3, 1), transform var(--transition-speed) cubic-bezier(0.16, 1, 0.3, 1);
        }

        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .portal-header {
            background: linear-gradient(135deg, var(--bg-secondary) 0%, var(--bg-card) 100%);
            backdrop-filter: blur(var(--blur-val));
            border: 1px solid var(--border-accent);
            border-bottom: 5px solid var(--accent-blue);
            padding: 40px 25px;
            text-align: center;
            border-radius: 24px;
            margin-bottom: 35px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.75), 0 0 35px var(--accent-glow), inset 0 1px 0 rgba(255, 255, 255, 0.1);
            position: relative;
            overflow: hidden;
            transition: transform var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
        }

        .portal-header:hover {
            transform: translateY(-3px);
            box-shadow: 0 25px 60px rgba(0, 0, 0, 0.8), 0 0 45px var(--accent-glow);
        }

        .portal-header h1 {
            font-size: clamp(1.8rem, 3.5vw, 2.6rem);
            background: linear-gradient(135deg, var(--accent-blue) 0%, #ffffff 50%, var(--accent-purple) 100%);
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 12px;
            animation: neonGradientMove 6s ease infinite alternate, neonPulse 4s ease-in-out infinite alternate;
        }

        @keyframes neonGradientMove {
            0% { background-position: 0% 50%; }
            100% { background-position: 100% 50%; }
        }

        @keyframes neonPulse {
            0% { filter: drop-shadow(0 0 4px var(--accent-blue)); }
            100% { filter: drop-shadow(0 0 18px var(--accent-purple)); }
        }

        .portal-header p {
            color: var(--text-muted);
            font-size: 1.1rem;
            max-width: 850px;
            margin: 0 auto;
        }

        .live-clock {
            margin-top: 12px;
            color: var(--text-muted);
            font-size: 0.88rem;
            letter-spacing: 0.5px;
        }

        .hero-info-box {
            background: linear-gradient(135deg, var(--bg-card) 0%, var(--bg-secondary) 100%);
            backdrop-filter: blur(var(--blur-val));
            border: 2px solid var(--accent-blue);
            border-radius: 26px;
            padding: 45px 35px;
            margin-bottom: 35px;
            text-align: center;
            box-shadow: 0 0 60px var(--accent-glow), inset 0 0 30px var(--accent-glow);
            transition: transform var(--transition-speed) ease;
        }

        .hero-info-box:hover {
            transform: scale(1.01);
        }

        .hero-info-box h2 {
            font-size: clamp(2.2rem, 5vw, 3.6rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 3px;
            background: linear-gradient(135deg, var(--accent-blue) 0%, var(--accent-purple) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 18px;
            filter: drop-shadow(0 0 30px var(--accent-glow));
        }

        .hero-info-box p {
            color: var(--text-main);
            font-size: 1.18rem;
            max-width: 950px;
            margin: 0 auto 15px auto;
            line-height: 1.8;
        }

        .content-section {
            background: linear-gradient(135deg, var(--bg-card) 0%, var(--bg-secondary) 100%);
            backdrop-filter: blur(var(--blur-val));
            border: 1px solid var(--border-primary);
            border-radius: 24px;
            padding: 40px;
            margin-bottom: 35px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.65);
            position: relative;
            overflow: hidden;
            transition: border-color var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
        }

        .content-section:hover {
            border-color: var(--border-accent);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.75), 0 0 20px var(--accent-glow);
        }

        .section-title {
            color: var(--accent-blue);
            font-size: 1.75rem;
            margin-bottom: 15px;
            border-bottom: 2px solid var(--border-primary);
            padding-bottom: 12px;
            display: inline-block;
            text-shadow: 0 0 15px var(--accent-glow);
        }

        .section-description {
            color: var(--text-muted);
            font-size: 1.02rem;
            margin-bottom: 25px;
        }

        .market-status {
            margin-bottom: 15px;
            display: flex;
            align-items: center;
        }
        .market-status-pill {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: rgba(16, 185, 129, 0.12);
            border: 1px solid rgba(16, 185, 129, 0.3);
            color: #34d399;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 700;
            letter-spacing: 0.5px;
            transition: all var(--transition-speed) ease;
        }
        .market-status-pill.glitch-mode {
            background: rgba(239, 68, 68, 0.2);
            border-color: rgba(239, 68, 68, 0.6);
            color: #f87171;
            box-shadow: 0 0 15px rgba(239, 68, 68, 0.4);
        }
        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: currentColor;
            box-shadow: 0 0 8px currentColor;
            animation: blinkDot 1.5s infinite;
        }
        @keyframes blinkDot {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }

        .chart-box-wrapper {
            position: relative;
            width: 100%;
            height: 480px;
            background: var(--bg-primary);
            padding: 25px;
            border-radius: 20px;
            border: 1px solid var(--border-accent);
            box-shadow: inset 0 0 35px rgba(0,0,0,0.8), 0 0 40px var(--accent-glow);
        }

        .dropdown-element {
            margin-top: 16px;
        }

        .dropdown-toggle-btn {
            background: linear-gradient(135deg, var(--bg-card) 0%, var(--bg-secondary) 100%);
            color: var(--text-main);
            cursor: pointer;
            padding: 18px 24px;
            width: 100%;
            border: 1px solid var(--border-primary);
            text-align: left;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all var(--transition-speed) ease;
        }

        .dropdown-toggle-btn:hover {
            background: var(--bg-card-hover);
            border-color: var(--accent-blue);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px var(--accent-glow);
        }

        .dropdown-panel {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s cubic-bezier(0.4, 0, 0.2, 1), padding 0.3s ease;
            background-color: var(--bg-secondary);
            border-radius: 0 0 16px 16px;
            padding: 0 24px;
            border: 1px solid transparent;
        }

        .dropdown-panel.expanded {
            max-height: 1500px;
            padding: 24px;
            margin-top: 4px;
            border-color: var(--border-accent);
        }

        .dropdown-panel p, .dropdown-panel ul {
            color: var(--text-main);
            font-size: 0.98rem;
            margin-bottom: 12px;
        }

        .dropdown-panel ul { padding-left: 22px; }
        .dropdown-panel li { margin-bottom: 8px; }

        .notice-box {
            background: rgba(14, 165, 233, 0.12);
            border-left: 4px solid var(--accent-blue);
            padding: 16px;
            margin-top: 18px;
            border-radius: 0 12px 12px 0;
            font-size: 0.95rem;
            color: var(--text-main);
        }

        .staff-grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
            gap: 24px;
            margin-top: 25px;
        }

        /* ===== УНІКАЛЬНІ ЕКСТРЕМАЛЬНІ АНІМАЦІЇ ДЛЯ КАРТОК СУДДІВ ===== */
        .staff-profile-card {
            background: linear-gradient(135deg, var(--bg-card) 0%, var(--bg-secondary) 100%);
            border: 1px solid var(--border-primary);
            padding: 35px 22px;
            border-radius: 20px;
            text-align: center;
            position: relative;
            overflow: hidden;
            transform-style: preserve-3d;
            will-change: transform;
            animation-duration: 8s;
            animation-timing-function: cubic-bezier(0.25, 1, 0.5, 1);
            animation-fill-mode: forwards;
            transition: border-color var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
        }

        .staff-profile-card::before {
            content: '';
            position: absolute;
            top: -50%; left: -50%;
            width: 200%; height: 200%;
            background: conic-gradient(transparent, var(--accent-blue), transparent 30%);
            animation: rotateGlow 4s linear infinite;
            z-index: 0;
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .staff-profile-card:hover::before {
            opacity: 1;
        }

        @keyframes rotateGlow {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* 1-ша картка: Потужний 3D-спін з віддаленням */
        .staff-profile-card:nth-child(1) {
            animation-name: animCard1;
        }
        @keyframes animCard1 {
            0% { transform: perspective(1000px) rotateX(720deg) rotateY(1080deg) scale(0.1) translateY(200px); opacity: 0; filter: blur(10px); }
            70% { transform: perspective(1000px) rotateX(120deg) rotateY(180deg) scale(0.85) translateY(-20px); opacity: 0.8; filter: blur(2px); }
            100% { transform: perspective(1000px) rotateX(0deg) rotateY(0deg) scale(1) translateY(0); opacity: 1; filter: blur(0px); }
        }

        /* 2-га картка: Спіральний виліт знизу з розширенням */
        .staff-profile-card:nth-child(2) {
            animation-name: animCard2;
        }
        @keyframes animCard2 {
            0% { transform: perspective(1000px) rotateZ(-45deg) scale(0.2) translateY(300px); opacity: 0; filter: blur(8px); }
            70% { transform: perspective(1000px) rotateZ(10deg) scale(1.05) translateY(15px); opacity: 0.9; filter: blur(1px); }
            100% { transform: perspective(1000px) rotateZ(0deg) scale(1) translateY(0); opacity: 1; filter: blur(0px); }
        }

        /* 3-тя картка: Ефект гойдалки та зближення */
        .staff-profile-card:nth-child(3) {
            animation-name: animCard3;
        }
        @keyframes animCard3 {
            0% { transform: perspective(1000px) rotateY(90deg) scale(0.4) translateX(-200px); opacity: 0; filter: blur(12px); }
            70% { transform: perspective(1000px) rotateY(-20deg) scale(0.9) translateX(15px); opacity: 0.85; filter: blur(3px); }
            100% { transform: perspective(1000px) rotateY(0deg) scale(1) translateX(0); opacity: 1; filter: blur(0px); }
        }

        .staff-profile-card:hover {
            border-color: var(--accent-blue);
            box-shadow: 0 20px 45px var(--accent-glow);
            transform: translateY(-10px) scale(1.02) !important;
        }

        .staff-avatar-wrapper {
            width: 105px;
            height: 105px;
            margin: 0 auto 20px auto;
            position: relative;
            border-radius: 50%;
            padding: 3px;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            z-index: 1;
        }

        .staff-avatar-wrapper img {
            width: 100%; height: 100%; object-fit: cover; border-radius: 50%; border: 3px solid var(--bg-card); display: block;
        }

        .avatar-fallback {
            width: 100%; height: 100%; border-radius: 50%; background: var(--bg-primary); display: flex; align-items: center; justify-content: center; font-size: 2.4rem; border: 3px solid var(--bg-card); color: var(--accent-blue);
        }

        .staff-profile-card h3 { font-size: 1.35rem; margin-bottom: 8px; color: var(--text-main); position: relative; z-index: 1; }
        .staff-role-badge { color: var(--accent-blue); font-size: 0.8rem; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 16px; display: inline-block; background: rgba(14, 165, 233, 0.15); padding: 6px 16px; border-radius: 20px; border: 1px solid var(--border-accent); position: relative; z-index: 1; }
        .staff-contacts-info { font-size: 0.95rem; color: var(--text-muted); word-break: break-all; position: relative; z-index: 1; }
        .staff-contacts-info a { color: var(--accent-blue); text-decoration: none; font-weight: 600; }
        .staff-contacts-info a:hover { color: var(--accent-blue-hover); text-decoration: underline; }

        /* ЧОРНИЙ СПИСОК */
        .blacklist-section {
            background: rgba(30, 10, 15, 0.6);
            border: 1px solid rgba(239, 68, 68, 0.3);
        }
        .blacklist-title {
            color: #f87171 !important;
            border-bottom-color: rgba(239, 68, 68, 0.4) !important;
            text-shadow: 0 0 15px rgba(239, 68, 68, 0.4);
        }
        .blacklist-grid {
            display: flex;
            justify-content: center;
        }
        .blacklist-card {
            background: rgba(40, 15, 20, 0.8);
            border: 1px solid rgba(239, 68, 68, 0.4);
            border-radius: 16px;
            padding: 24px;
            text-align: center;
            max-width: 350px;
            width: 100%;
            position: relative;
            transition: transform var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
        }
        .blacklist-card:hover {
            box-shadow: 0 10px 30px rgba(239, 68, 68, 0.4);
        }
        .blacklist-icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        .blacklist-card h3 {
            color: #fca5a5;
            font-size: 1.3rem;
            margin-bottom: 8px;
        }
        .blacklist-badge {
            display: inline-block;
            background: rgba(239, 68, 68, 0.15);
            color: #f87171;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 700;
            margin-bottom: 12px;
            border: 1px solid rgba(239, 68, 68, 0.3);
        }
        .blacklist-contacts {
            font-size: 0.9rem;
            color: #cbd5e1;
        }
        .blacklist-contacts a {
            color: #f87171;
            text-decoration: none;
        }

        .table-box-wrapper {
            width: 100%; overflow-x: auto; margin-top: 25px; border-radius: 20px; border: 1px solid var(--border-primary); background-color: var(--bg-secondary);
        }

        .analytics-table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.98rem; white-space: nowrap; }
        .analytics-table th, .analytics-table td { padding: 18px 22px; border-bottom: 1px solid var(--border-primary); color: var(--text-main) !important; transition: background-color var(--transition-speed) ease; }
        .analytics-table th { background-color: var(--bg-card) !important; color: var(--accent-blue) !important; font-weight: 600; text-transform: uppercase; font-size: 0.82rem; letter-spacing: 1px; }
        .analytics-table tbody tr { background-color: var(--bg-primary) !important; }
        .analytics-table tr:nth-child(even) { background-color: var(--bg-secondary) !important; }
        .analytics-table tr:hover { background-color: var(--accent-glow) !important; }

        .status-up { color: var(--success-color); font-weight: bold; }
        .status-stable { color: var(--accent-blue); font-weight: bold; }

        .event-detailed-card {
            background: linear-gradient(135deg, var(--accent-glow), var(--bg-secondary));
            border: 1px solid var(--accent-blue); border-radius: 20px; padding: 32px; margin-top: 30px; box-shadow: 0 0 40px var(--accent-glow);
        }
        .event-detailed-card h3 { color: var(--accent-blue); font-size: 1.5rem; margin-bottom: 14px; display: flex; align-items: center; gap: 12px; }
        .event-detailed-card p { color: var(--text-main); font-size: 1rem; margin-bottom: 16px; line-height: 1.7; }
        .event-benefits-list { list-style-type: none; padding-left: 0; margin-bottom: 22px; }
        .event-benefits-list li { position: relative; padding-left: 26px; margin-bottom: 10px; color: var(--text-main); font-size: 0.98rem; }
        .event-benefits-list li::before { content: "✔️"; position: absolute; left: 0; color: var(--success-color); font-weight: bold; }
        .event-schedule-container { display: flex; gap: 14px; flex-wrap: wrap; margin-top: 18px; border-top: 1px solid var(--border-primary); padding-top: 18px; }
        .schedule-badge { background: var(--bg-card); border: 1px solid var(--accent-blue); color: var(--text-main); padding: 12px 20px; border-radius: 14px; font-weight: bold; font-size: 1.02rem; transition: transform var(--transition-speed) ease; }
        .schedule-badge:hover { transform: translateY(-3px) scale(1.05); }

        .owner-news-branch {
            background: linear-gradient(135deg, var(--bg-card) 0%, var(--bg-primary) 100%); border: 1px dashed var(--accent-blue); border-radius: 20px; padding: 32px; margin-top: 35px;
        }
        .owner-news-branch h3 { color: var(--accent-blue); font-size: 1.35rem; margin-bottom: 12px; display: flex; align-items: center; gap: 10px; }
        .owner-news-branch p { color: var(--text-muted); font-size: 0.98rem; margin-bottom: 12px; line-height: 1.7; }

        .portal-footer {
            text-align: center; padding: 30px 20px; background: linear-gradient(135deg, var(--bg-card) 0%, var(--bg-primary) 100%); border: 1px solid var(--border-primary); border-radius: 20px; color: var(--text-muted); font-size: 0.95rem; margin-top: 35px;
        }
    </style>
</head>
<body>
    <!-- PRELOADER 5 СЕКУНД -->
    <div id="preloader">
        <div class="loader-spinner"></div>
        <div class="loader-title">Завантаження Порталу...</div>
        <div class="loader-bar-wrapper">
            <div class="loader-bar" id="loaderBar"></div>
        </div>
        <div class="loader-counter" id="loaderCounter">0%</div>
    </div>

    <div class="scroll-progress" id="scrollProgress"></div>
    
    <button type="button" class="settings-toggle-btn" id="openSettings">⚙️ Налаштування</button>
    <div class="settings-modal" id="settingsModal">
        <div class="settings-option">
            <label for="themeSelect">Тема оформлення</label>
            <select id="themeSelect">
                <option value="default">Стандартна (Cyber Blue)</option>
                <option value="cyberpunk">Neon Cyberpunk</option>
                <option value="matrix">Matrix Green</option>
                <option value="crimson">Crimson Red</option>
            </select>
        </div>
        <div class="settings-option">
            <label for="animSpeed">Швидкість анімацій</label>
            <select id="animSpeed">
                <option value="0.4s" selected>Стандартна</option>
                <option value="0.8s">Повільна (Smooth)</option>
                <option value="0.2s">Швидка</option>
            </select>
        </div>
        <div class="settings-option">
            <label for="blurToggle">Розмиття панелей (Blur)</label>
            <select id="blurToggle">
                <option value="16px" selected>Увімкнено (16px)</option>
                <option value="8px">Легке (8px)</option>
                <option value="0px">Вимкнено (Для слабких ПК)</option>
            </select>
        </div>
        <div class="settings-option">
            <label for="bgOpacity">Прозорість фонових анімацій</label>
            <input type="range" id="bgOpacity" min="0" max="1" step="0.1" value="1">
        </div>
        <div class="settings-option">
            <label for="animToggle">Плаваючі елементи фону</label>
            <select id="animToggle">
                <option value="on">Увімкнено</option>
                <option value="off">Вимкнено</option>
            </select>
        </div>
    </div>

    <div class="quick-nav" aria-label="Швидка навігація">
        <button type="button" id="toTop" title="На початок">↑</button>
        <button type="button" id="toBottom" title="До низу">↓</button>
    </div>
    <div class="background-glow-layer">
        <div class="float-orb" style="left:12%;animation-duration:14s;animation-delay:-3s"></div>
        <div class="float-orb" style="left:35%;animation-duration:18s;animation-delay:-7s"></div>
        <div class="float-orb" style="left:55%;animation-duration:16s;animation-delay:-2s"></div>
        <div class="float-orb" style="left:67%;animation-duration:15s;animation-delay:-5s"></div>
        <div class="float-orb" style="left:88%;animation-duration:20s;animation-delay:-10s"></div>
    </div>

    <div class="main-container">
        
        <header class="portal-header animate-on-scroll">
            <h1>🏛 Офіційний Портал Судової Системи Ukraine RP</h1>
            <p>Централізований державний реєстр судових проваджень, регламентів, звітності та керівного складу колегії</p>
            <div class="live-clock">🕘 Локальний час: <span id="liveClock">--:--:--</span></div>
        </header>

        <div class="hero-info-box animate-on-scroll">
            <h2>⚖️ СУД ІНФО UKRAINE RP ⚖️</h2>
            <p>Головний інформаційний центр судової системи! Тут зібрані всі офіційні правила дотримання законів, регламенти захисту прав громадян, розклад засідань та інструкції з взаємодії з державними органами на нашому сервері.</p>
            <p>Наша мета — забезпечити максимальну прозорість, справедливість та високий рівень рольової гри (RP) для кожного гравця Ukraine RP.</p>
        </div>

        <section class="content-section animate-on-scroll">
            <h2 class="section-title">📈 Біржа Активності та Статистика Суду</h2>
            <p class="section-description">Розширена аналітика, показники продуктивності колегії та інтерактивна динаміка розгляду позовів у реальному часі:</p>
            
            <div class="market-status">
                <div class="market-status-pill" id="marketStatusPill">
                    <span class="status-dot"></span>
                    <span id="marketStatusText">СИСТЕМА МОНІТОРИНГУ АКТИВНА</span>
                </div>
            </div>

            <div class="chart-box-wrapper">
                <canvas id="courtStockChart"></canvas>
            </div>
        </section>

        <section class="content-section animate-on-scroll">
            <h2 class="section-title">⚖️ Нормативно-правова база та Правила Сервера</h2>
            <p class="section-description">Детальні інструкції щодо поведінки, етики, законності дій та нові розширені регламенти:</p>
            
            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>📜 Загальна етика та правила поведінки в суді</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p><strong>Головні норми поведінки для учасників та гостей засідання:</strong></p>
                    <ul>
                        <li><strong>Форма звернення:</strong> До судді слід звертатися виключно офіційно та шанобливо — <em>«Ваша Честь»</em> або <em>«Шановний Судде»</em>.</li>
                        <li><strong>Порядок у залі:</strong> За заборонено перебивати виступи інших сторін, викрикувати, провокувати конфлікти або вести себе деструктивно.</li>
                        <li><strong>Рольова взаємодія:</strong> Усі аргументи повинні подаватися виключно через якісні RP-описи та докази (фрапси, скріншоти, свідчення очевидців).</li>
                    </ul>
                    <div class="notice-box">
                        <strong>⚠️ Важливо:</strong> Порушення регламенту розглядається як неувага до суду та карається сервером або видаленням із зали засідань.
                    </div>
                </div>
            </div>

            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>🛡 Правила обшуку та законність дій держструктур</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p><strong>Стандарти проведения процесуальних дій:</strong></p>
                    <ul>
                        <li>Обшук або затримання вважаються легітимними лише за наявності вагомої RP-підстави та правильного відігравання через команди <code>/me</code>, <code>/do</code>.</li>
                        <li>Будь-які докази, зібрані з порушенням серверних правил або чинного законодавства, визнаються судом недійсними.</li>
                        <li>Кожен громадянин має право на виклик адвоката та оскарження неправомірних дій у судовому порядку.</li>
                    </ul>
                </div>
            </div>

            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>⚖️ Новий регламент: Порядок подачі та розгляду апеляцій</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p><strong>Додаткові логічні правила оскарження рішень:</strong></p>
                    <ul>
                        <li><strong>Строки подачі:</strong> Громадянин або державна структура має право подати апеляційну скаргу протягом 48 годин з моменту оголошення попереднього рішення суду.</li>
                        <li><strong>Пакет документів:</strong> До апеляції обов'язково додається повний відеозахист (фрапс) засідання або копія попереднього протоколу без замальовок чи монтажу.</li>
                        <li><strong>Склад апеляційної колегії:</strong> Розгляд скарги проводиться спеціальною колегією з двох або більше суддів вищої кваліфікації.</li>
                    </ul>
                    <div class="notice-box">
                        <strong>📌 Примітка:</strong> Подання свідомо фальшивих доказів під час апеляції тягне за собою кримінальну відповідальність за статтею про дачу неправдивих свідчень у суді.
                    </div>
                </div>
            </div>

            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>🛡 Новий регламент: Етика та професійні обов'язки адвокатури</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p><strong>Стандарти для представників захисту:</strong></p>
                    <ul>
                        <li><strong>Конфіденційність:</strong> Адвокат зобов'язаний зберігати повну таємницю довіри зі своїм клієнтом під час підготовки до судового процесу.</li>
                        <li><strong>Підготовка лінії захисту:</strong> Представник повинен надати аргументовані докази невинуватості або пом'якшення вироку за 10 хвилин до початку відкриття судового засідання.</li>
                        <li><strong>Коректність у спілкуванні:</strong> Заборонено використовувати ненормативну лексику чи тиснути на свідків під час перехресного допиту.</li>
                    </ul>
                </div>
            </div>

            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>🤖 Про офіційний Судовий Бот Ukraine RP</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p>Наш інтегрований судовий бот створений для автоматизації подачі позовів, перевірки статусів справ та оперативної комунікації з громадянами.</p>
                    <p><strong>Основні можливості бота:</strong></p>
                    <ul>
                        <li>Миттєва подача електронної заяви до суду.</li>
                        <li>Сповіщення про дати та час призначених засідань.</li>
                        <li>Швидкий доступ до контактів суддів та адвокатів.</li>
                    </ul>
                </div>
            </div>
        </section>

        <section class="content-section animate-on-scroll">
            <h2 class="section-title">🏛 Колектив суду та Адвокатура</h2>
            <p class="section-description">Офіційний кадровий склад керівництва, суддівської колегії та представників захисту (з унікальними ефектами появи карток):</p>
            
            <div class="staff-grid-container">
                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <img src="https://via.placeholder.com/150" alt="Arseniy_zabanen" onerror="this.replaceWith(Object.assign(document.createElement('div'), {className: 'avatar-fallback', innerText: '⚖️'}))">
                    </div>
                    <h3>Arseniy_zabanen</h3>
                    <div class="staff-role-badge">Головний Суддя (ГС)</div>
                    <div class="staff-contacts-info">Roblox: Arseniy_zabanen<br>TG: <a href="https://t.me/Samyry228" target="_blank">@Samyry228</a></div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <img src="https://via.placeholder.com/150" alt="mummu228kuku" onerror="this.replaceWith(Object.assign(document.createElement('div'), {className: 'avatar-fallback', innerText: '🛡'}))">
                    </div>
                    <h3>mummu228kuku</h3>
                    <div class="staff-role-badge">Заступник</div>
                    <div class="staff-contacts-info">Roblox: mummu228kuku<br>TG: <a href="https://t.me/here_everyone" target="_blank">@here_everyone</a></div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <img src="https://via.placeholder.com/150" alt="Huhaidjopy" onerror="this.replaceWith(Object.assign(document.createElement('div'), {className: 'avatar-fallback', innerText: '🏛'}))">
                    </div>
                    <h3>Huhaidjopy</h3>
                    <div class="staff-role-badge">Суддя</div>
                    <div class="staff-contacts-info">Roblox: Huhaidjopy<br>TG: <a href="https://t.me/bewewewewewe" target="_blank">@bewewewewewe</a></div>
                </div>
            </div>
        </section>

        <section class="blacklist-section content-section animate-on-scroll" id="blacklist">
            <h2 class="section-title blacklist-title">🚫 Чорний список</h2>
            <p class="section-description">Офіційний запис про звільненого учасника.</p>
            <div class="blacklist-grid">
                <article class="blacklist-card">
                    <div class="blacklist-icon">🚫</div>
                    <h3>heehrhrhl18</h3>
                    <span class="blacklist-badge">ЗВІЛЬНЕНО / ЧОРНИЙ СПИСОК</span>
                    <div class="blacklist-contacts">
                        Roblox: heehrhrhl18<br>
                        TG: <a href="https://t.me/hehr18_UR" target="_blank">@hehr18_UR</a>
                    </div>
                </article>
            </div>
        </section>

        <section class="content-section animate-on-scroll">
            <h2 class="section-title">📊 Детальна архівна таблиця звітів та порушень</h2>
            <p class="section-description">У звітах нижче зібрано повну статистику розгляду справ, аналіз порушень серверних регламентів та ефективність роботи колегії:</p>

            <div class="table-box-wrapper">
                <table class="analytics-table">
                    <thead>
                        <tr>
                            <th>Звітний період</th>
                            <th>Опрацьовано справ</th>
                            <th>Порушення регламентів</th>
                            <th>Статус системи</th>
                            <th>Головна подія періоду</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>4 липня – 3 серпня 2026</strong></td>
                            <td><span class="status-up">573 справи</span></td>
                            <td>9 інцидентів (Пункт 16)</td>
                            <td><span class="status-up">⚡️ Штатний режим</span></td>
                            <td>Оброблено 161 звіт (502 години роботи).</td>
                        </tr>
                        <tr>
                            <td><strong>Червень – Липень 2026</strong></td>
                            <td><span class="status-up">570 справ</span></td>
                            <td>38 інцидентів</td>
                            <td><span class="status-up">🚀 Пік активності</span></td>
                            <td>Максимальна продуктивність колегії.</td>
                        </tr>
                        <tr>
                            <td><strong>Травень – Червень 2026</strong></td>
                            <td>310 справ</td>
                            <td>21 інцидент</td>
                            <td><span class="status-stable">⚖️ Стабільний режим</span></td>
                            <td>Якісне виконання регламентів.</td>
                        </tr>
                        <tr>
                            <td><strong>Січень – Лютий 2026</strong></td>
                            <td>329 засідань</td>
                            <td>29 інцидентів</td>
                            <td><span class="status-stable">🤖 Цифровізація</span></td>
                            <td>Запуск інформаційного бота.</td>
                        </tr>
                        <tr>
                            <td><strong>Грудень 2025 – Січень 2026</strong></td>
                            <td><span class="status-up">657 справ</span></td>
                            <td>52 інциденти</td>
                            <td><span class="status-up">⚡️ Рекорд</span></td>
                            <td>Найвище навантаження в історії.</td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <div class="event-detailed-card">
                <h3>🏛 Івент: День Відкритих Дверей Суду</h3>
                <p><strong>Чому цей івент корисний для гравців?</strong> День відкритих дверей — це унікальна можливість зазирнути за лаштунки судової системи, зрозуміти свої права та навчитися грамотно захищати себе в рольових ситуаціях без порушення правил сервера.</p>
                
                <p><strong>Переваги участі:</strong></p>
                <ul class="event-benefits-list">
                    <li>Живе спілкування з досвідченими суддями та адвокатами.</li>
                    <li>Розбір реальних кейсів та процесуальних помилок.</li>
                    <li>Унікальний ігровий досвід та гарний настрій.</li>
                </ul>
                <p><strong>Графік проведення івенту:</strong></p>
                <div class="event-schedule-container">
                    <span class="schedule-badge">📅 09 число місяця</span>
                    <span class="schedule-badge">📅 17 число місяця</span>
                    <span class="schedule-badge">📅 29 число місяця</span>
                </div>
            </div>

            <div class="owner-news-branch">
                <h3>📢 Новини та оновлення від керівництва суду</h3>
                <p>У цій гілці суд та власник сайту публікують актуальні внутрішні новини, майбутні оновлення судової системи, а також корисні поради щодо покращення рольової гри на сервері. Слідкуйте за оновленнями порталу, щоб бути в курсі найважливіших державних подій Ukraine RP!</p>
            </div>
        </section>

        <footer class="portal-footer animate-on-scroll">
            <p>&copy; 2026 Офіційний Портал Судової Системи Ukraine RP. Усі права захищені.</p>
        </footer>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function() {
            // ===== 5-СЕКУНДНИЙ PRELOADER =====
            const preloader = document.getElementById('preloader');
            const loaderBar = document.getElementById('loaderBar');
            const loaderCounter = document.getElementById('loaderCounter');
            
            let loadProgress = 0;
            const duration = 5000; // 5 секунд
            const intervalTime = 50;
            const step = 100 / (duration / intervalTime);

            const preloaderInterval = setInterval(() => {
                loadProgress += step;
                if (loadProgress >= 100) {
                    loadProgress = 100;
                    clearInterval(preloaderInterval);
                    setTimeout(() => {
                        preloader.classList.add('hidden');
                    }, 200);
                }
                loaderBar.style.width = `${loadProgress}%`;
                loaderCounter.textContent = `${Math.floor(loadProgress)}%`;
            }, intervalTime);

            // МЕНЮ НАЛАШТУВАНЬ
            const settingsBtn = document.getElementById('openSettings');
            const settingsModal = document.getElementById('settingsModal');
            
            settingsBtn?.addEventListener('click', () => {
                settingsModal.classList.toggle('active');
            });

            document.addEventListener('click', (e) => {
                if (!settingsModal.contains(e.target) && !settingsBtn.contains(e.target)) {
                    settingsModal.classList.remove('active');
                }
            });

            // Тема
            const themeSelect = document.getElementById('themeSelect');
            themeSelect?.addEventListener('change', (e) => {
                document.body.className = '';
                if (e.target.value !== 'default') {
                    document.body.classList.add(`theme-${e.target.value}`);
                }
            });

            // Швидкість анімацій
            const animSpeed = document.getElementById('animSpeed');
            animSpeed?.addEventListener('change', (e) => {
                document.documentElement.style.setProperty('--transition-speed', e.target.value);
            });

            // Розмиття (Blur)
            const blurToggle = document.getElementById('blurToggle');
            blurToggle?.addEventListener('change', (e) => {
                document.documentElement.style.setProperty('--blur-val', e.target.value);
            });

            // Прозорість/Яскравість фону
            const bgOpacity = document.getElementById('bgOpacity');
            bgOpacity?.addEventListener('input', (e) => {
                document.documentElement.style.setProperty('--bg-anim-opacity', e.target.value);
            });

            // Вимкнення плаваючих оріб
            const animToggle = document.getElementById('animToggle');
            const bgGlowLayer = document.querySelector('.background-glow-layer');
            animToggle?.addEventListener('change', (e) => {
                if (bgGlowLayer) {
                    bgGlowLayer.style.display = e.target.value === 'off' ? 'none' : 'block';
                }
            });

            // ПРОГРЕС СКРОЛУ
            const progress = document.getElementById('scrollProgress');
            const updateScrollProgress = () => {
                const scrollTop = window.scrollY;
                const max = document.documentElement.scrollHeight - window.innerHeight;
                progress.style.width = `${max > 0 ? (scrollTop / max) * 100 : 0}%`;
            };
            window.addEventListener('scroll', updateScrollProgress, { passive: true });
            updateScrollProgress();

            document.getElementById('toTop')?.addEventListener('click', () => {
                window.scrollTo({ top: 0, behavior: 'smooth' });
            });
            document.getElementById('toBottom')?.addEventListener('click', () => {
                window.scrollTo({ top: document.documentElement.scrollHeight, behavior: 'smooth' });
            });

            // Ефект Ripple
            document.querySelectorAll('button').forEach(button => {
                button.style.position = button.style.position || 'relative';
                button.style.overflow = 'hidden';
                button.addEventListener('click', (event) => {
                    const rect = button.getBoundingClientRect();
                    const ripple = document.createElement('span');
                    ripple.className = 'ripple';
                    const size = Math.max(rect.width, rect.height);
                    ripple.style.width = ripple.style.height = `${size}px`;
                    ripple.style.left = `${event.clientX - rect.left - size / 2}px`;
                    ripple.style.top = `${event.clientY - rect.top - size / 2}px`;
                    button.appendChild(ripple);
                    setTimeout(() => ripple.remove(), 700);
                });
            });

            // 3D Ефект наклону карток
            document.querySelectorAll('.staff-profile-card, .blacklist-card').forEach(card => {
                card.addEventListener('pointermove', (event) => {
                    const rect = card.getBoundingClientRect();
                    const x = (event.clientX - rect.left) / rect.width - .5;
                    const y = (event.clientY - rect.top) / rect.height - .5;
                    card.style.transform = `perspective(900px) rotateX(${-y * 12}deg) rotateY(${x * 12}deg) translateY(-8px) scale(1.02)`;
                });
                card.addEventListener('pointerleave', () => {
                    card.style.transform = '';
                });
            });

            // Годинник
            const clock = document.getElementById('liveClock');
            if (clock) {
                const updateClock = () => {
                    clock.textContent = new Date().toLocaleTimeString('uk-UA');
                };
                updateClock();
                setInterval(updateClock, 1000);
            }

            // Анімації при скролі
            const observerOptions = { threshold: 0.1 };
            const observer = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                        observer.unobserve(entry.target);
                    }
                });
            }, observerOptions);

            document.querySelectorAll('.animate-on-scroll').forEach(el => {
                observer.observe(el);
            });

            // Випадні списки (Dropdown)
            const dropdownBtns = document.querySelectorAll('.dropdown-toggle-btn');
            dropdownBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    const panel = this.nextElementSibling;
                    const arrowSpan = this.querySelector('span:last-child');
                    
                    panel.classList.toggle('expanded');
                    arrowSpan.textContent = panel.classList.contains('expanded') ? '▲' : '▼';
                });
            });

            // Графік Chart.js
            const ctx = document.getElementById('courtStockChart').getContext('2d');
            const chartGradient = ctx.createLinearGradient(0, 0, 0, 400);
            chartGradient.addColorStop(0, 'rgba(14, 165, 233, 0.65)');
            chartGradient.addColorStop(1, 'rgba(14, 165, 233, 0.0)');

            const normalData = [210, 260, 329, 390, 440, 570, 573, 640, 710];
            const glitchData = [90, 520, 110, 840, 190, 990, 420, 210, 890];

            const courtChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Січень', 'Лютий', 'Березень', 'Квітень', 'Травень', 'Червень', 'Липень', 'Серпень (+)', 'Вересень (План)'],
                    datasets: [{
                        label: 'Динаміка успішно розглянутих справ (+ стабільний ріст)',
                        data: normalData,
                        borderColor: '#38bdf8',
                        borderWidth: 4,
                        pointBackgroundColor: '#818cf8',
                        pointBorderColor: '#ffffff',
                        pointBorderWidth: 2,
                        pointRadius: 6,
                        pointHoverRadius: 9,
                        backgroundColor: chartGradient,
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    animation: {
                        duration: 2500,
                        easing: 'easeOutQuart'
                    },
                    plugins: {
                        legend: {
                            labels: {
                                color: '#f8fafc',
                                font: { size: 13, family: "'Segoe UI', Roboto, sans-serif" }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(11, 19, 41, 0.95)',
                            titleColor: '#38bdf8',
                            bodyColor: '#f8fafc',
                            borderColor: '#38bdf8',
                            borderWidth: 1,
                            padding: 12
                        }
                    },
                    scales: {
                        x: {
                            grid: { color: 'rgba(30, 41, 59, 0.5)' },
                            ticks: { color: '#94a3b8', font: { size: 12 } }
                        },
                        y: {
                            grid: { color: 'rgba(30, 41, 59, 0.5)' },
                            ticks: { color: '#94a3b8', font: { size: 12 } }
                        }
                    }
                }
            });

            const statusPill = document.getElementById('marketStatusPill');
            const statusText = document.getElementById('marketStatusText');

            setTimeout(() => {
                courtChart.data.datasets[0].data = glitchData;
                courtChart.data.datasets[0].borderColor = '#ef4444';
                courtChart.update();

                statusPill.classList.add('glitch-mode');
                statusText.textContent = '⚠️ УВАГА: КРИТИЧНИЙ ЗБІЙ СИСТЕМИ ДАНИХ!';

                setTimeout(() => {
                    courtChart.data.datasets[0].data = normalData;
                    courtChart.data.datasets[0].borderColor = '#38bdf8';
                    courtChart.update();

                    statusPill.classList.remove('glitch-mode');
                    statusText.textContent = 'ЗБІЙ СИСТЕМИ ПРОЙШОВ — ТЕПЕР ВОНА СТАБІЛЬНА';
                }, 12000);
            }, 8000);
        });
    </script>
</body>
</html>

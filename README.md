<!DOCTYPE html>
<html lang="uk" data-theme="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Суд Ukraine RP — Офіційний портал судової системи</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --bg-primary: #020617;
            --bg-secondary: #070d1f;
            --bg-card: rgba(11, 19, 41, 0.75);
            --bg-card-hover: rgba(16, 28, 61, 0.9);
            --border-primary: rgba(30, 41, 59, 0.8);
            --border-accent: #38bdf8;
            --accent-blue: #0ea5e9;
            --accent-blue-hover: #38bdf8;
            --accent-glow: rgba(14, 165, 233, 0.35);
            --accent-purple: #818cf8;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --success-color: #22c55e;
            --warning-color: #f59e0b;
            --danger-color: #ef4444;
            --transition-speed: 0.3s;
        }

        [data-theme="light"] {
            --bg-primary: #f8fafc;
            --bg-secondary: #f1f5f9;
            --bg-card: rgba(255, 255, 255, 0.85);
            --bg-card-hover: rgba(226, 232, 240, 0.95);
            --border-primary: rgba(203, 213, 225, 0.8);
            --accent-blue: #0284c7;
            --accent-blue-hover: #0369a1;
            --accent-glow: rgba(2, 132, 199, 0.2);
            --text-main: #0f172a;
            --text-muted: #64748b;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            transition: background-color var(--transition-speed), border-color var(--transition-speed), color var(--transition-speed);
        }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: radial-gradient(circle at 50% 0%, var(--bg-secondary) 0%, var(--bg-primary) 70%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.7;
            padding: 20px;
            padding-top: 100px;
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* Top Sticky Navigation */
        .sticky-navbar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: rgba(7, 13, 31, 0.8);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--border-primary);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 40px;
            z-index: 1000;
            box-shadow: 0 10px 30px rgba(0,0,0,0.4);
        }

        .nav-logo {
            font-size: 1.25rem;
            font-weight: 900;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            filter: drop-shadow(0 0 10px var(--accent-glow));
        }

        .nav-links {
            display: flex;
            gap: 25px;
            list-style: none;
            align-items: center;
        }

        .nav-links a {
            color: var(--text-muted);
            text-decoration: none;
            font-weight: 600;
            font-size: 0.95rem;
            transition: color 0.3s ease;
        }

        .nav-links a:hover, .nav-links a.active {
            color: var(--accent-blue);
            text-shadow: 0 0 12px var(--accent-glow);
        }

        .nav-actions {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .icon-btn {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            color: var(--text-main);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            position: relative;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }

        .icon-btn:hover {
            border-color: var(--accent-blue);
            box-shadow: 0 0 20px var(--accent-glow);
            transform: translateY(-2px);
        }

        .badge-counter {
            position: absolute;
            top: -4px;
            right: -4px;
            background: var(--danger-color);
            color: #fff;
            font-size: 0.7rem;
            width: 18px;
            height: 18px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            box-shadow: 0 0 10px rgba(239, 68, 68, 0.6);
        }

        .main-container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Hero Bento Grid */
        .hero-bento-grid {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 25px;
            margin-bottom: 35px;
        }

        .hero-main-card {
            background: linear-gradient(135deg, rgba(11, 20, 45, 0.85) 0%, rgba(20, 28, 79, 0.85) 100%);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(56, 189, 248, 0.4);
            border-radius: 26px;
            padding: 45px 35px;
            box-shadow: 0 0 50px rgba(14, 165, 233, 0.2), inset 0 0 30px rgba(56, 189, 248, 0.1);
            display: flex;
            flex-direction: column;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .hero-main-card h1 {
            font-size: clamp(2rem, 3.5vw, 2.8rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            background: linear-gradient(135deg, #38bdf8 0%, #818cf8 50%, #c084fc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 15px;
            filter: drop-shadow(0 0 20px var(--accent-glow));
        }

        .hero-main-card p {
            color: #cbd5e1;
            font-size: 1.05rem;
            margin-bottom: 25px;
            line-height: 1.7;
        }

        .hero-actions {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            color: #fff;
            border: none;
            padding: 12px 25px;
            border-radius: 14px;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 5px 20px var(--accent-glow);
            transition: all 0.3s ease;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px var(--accent-glow);
        }

        .btn-secondary {
            background: var(--bg-card);
            color: var(--text-main);
            border: 1px solid var(--border-primary);
            padding: 12px 25px;
            border-radius: 14px;
            font-weight: 700;
            cursor: pointer;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }

        .btn-secondary:hover {
            border-color: var(--accent-blue);
            background: var(--bg-card-hover);
        }

        .hero-side-card {
            background: var(--bg-card);
            backdrop-filter: blur(15px);
            border: 1px solid var(--border-primary);
            border-radius: 26px;
            padding: 30px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
        }

        .hero-side-card h3 {
            color: var(--accent-blue);
            font-size: 1.15rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .live-stat-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid var(--border-primary);
            font-size: 0.95rem;
        }

        .live-stat-row:last-child { border-bottom: none; }

        /* Quick Actions Grid */
        .quick-actions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 15px;
            margin-bottom: 35px;
        }

        .quick-action-btn {
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-primary);
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            color: var(--text-main);
            font-weight: 600;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
            transition: all 0.3s ease;
        }

        .quick-action-btn i {
            font-size: 1.4rem;
            color: var(--accent-blue);
        }

        .quick-action-btn:hover {
            background: var(--bg-card-hover);
            border-color: var(--accent-blue);
            transform: translateY(-4px);
            box-shadow: 0 10px 25px var(--accent-glow);
        }

        /* Content Sections */
        .content-section {
            background: rgba(7, 13, 31, 0.65);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid var(--border-primary);
            border-radius: 24px;
            padding: 35px;
            margin-bottom: 35px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
            position: relative;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 2px solid var(--border-primary);
            padding-bottom: 15px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .section-title {
            color: var(--accent-blue);
            font-size: 1.6rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
            text-shadow: 0 0 15px var(--accent-glow);
        }

        /* Market / Stock Metrics with Live Animation Styles */
        .stock-metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .stock-metric-card {
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-primary);
            border-radius: 18px;
            padding: 22px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0,0,0,0.4);
            transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
        }

        .stock-metric-card:hover {
            transform: translateY(-5px);
            border-color: var(--accent-blue);
            box-shadow: 0 15px 30px var(--accent-glow);
        }

        .stock-metric-title {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .stock-metric-value {
            font-size: 1.8rem;
            font-weight: 800;
            color: var(--text-main);
            margin-bottom: 6px;
            transition: color 0.3s ease;
        }

        /* Анімація для біржових показників */
        .stock-metric-value.updated {
            color: var(--accent-blue);
            text-shadow: 0 0 15px var(--accent-glow);
            transform: scale(1.05);
        }

        .stock-metric-badge {
            display: inline-flex;
            align-items: center;
            gap: 4px;
            font-size: 0.85rem;
            font-weight: 700;
            padding: 4px 10px;
            border-radius: 20px;
            background: rgba(34, 197, 94, 0.15);
            color: var(--success-color);
            border: 1px solid rgba(34, 197, 94, 0.3);
        }

        /* Chart Wrapper */
        .chart-box-wrapper {
            position: relative;
            width: 100%;
            height: 420px;
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            padding: 25px;
            border-radius: 20px;
            border: 1px solid var(--border-primary);
            box-shadow: inset 0 0 35px rgba(0,0,0,0.5);
        }

        .chart-controls {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .filter-btn {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            color: var(--text-muted);
            padding: 8px 16px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85rem;
            transition: all 0.3s ease;
        }

        .filter-btn.active, .filter-btn:hover {
            background: var(--accent-blue);
            color: #fff;
            border-color: var(--accent-blue);
            box-shadow: 0 0 15px var(--accent-glow);
        }

        /* Staff Grid (зменшено кількість суддів за запитом) */
        .staff-grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 24px;
            margin-top: 25px;
        }

        .staff-profile-card {
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-primary);
            padding: 30px 20px;
            border-radius: 20px;
            text-align: center;
            transition: transform 0.4s ease, border-color 0.4s ease, box-shadow 0.4s ease;
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }

        .staff-profile-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 4px;
            background: var(--accent-blue);
        }

        .staff-profile-card:hover {
            transform: translateY(-8px);
            border-color: var(--accent-blue);
            box-shadow: 0 20px 45px var(--accent-glow);
        }

        .staff-avatar-wrapper {
            width: 90px;
            height: 90px;
            margin: 0 auto 15px auto;
            border-radius: 50%;
            padding: 3px;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
        }

        .avatar-fallback {
            width: 100%; height: 100%; border-radius: 50%; background: var(--bg-secondary); display: flex; align-items: center; justify-content: center; font-size: 2.2rem; border: 3px solid var(--bg-card); color: var(--accent-blue);
        }

        .staff-profile-card h3 { font-size: 1.25rem; margin-bottom: 6px; color: var(--text-main); }
        .staff-role-badge { color: var(--accent-blue); font-size: 0.75rem; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 12px; display: inline-block; background: rgba(14, 165, 233, 0.15); padding: 4px 12px; border-radius: 20px; border: 1px solid rgba(14, 165, 233, 0.3); }
        .staff-contacts-info { font-size: 0.9rem; color: var(--text-muted); word-break: break-all; }
        .staff-contacts-info a { color: var(--accent-blue); text-decoration: none; font-weight: 600; }

        /* News Section */
        .news-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .news-card {
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-primary);
            border-radius: 16px;
            padding: 25px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .news-card:hover {
            border-color: var(--accent-blue);
            transform: translateY(-3px);
            box-shadow: 0 10px 25px var(--accent-glow);
        }

        .news-date {
            font-size: 0.8rem;
            color: var(--accent-blue);
            margin-bottom: 8px;
            font-weight: 700;
        }

        .news-title {
            font-size: 1.15rem;
            font-weight: 700;
            margin-bottom: 10px;
            color: var(--text-main);
        }

        .news-desc {
            font-size: 0.92rem;
            color: var(--text-muted);
            margin-bottom: 15px;
        }

        /* Intelligence & System Health Section */
        .intelligence-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }

        .intel-card {
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-primary);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        .intel-card h3 {
            color: var(--accent-blue);
            font-size: 1.1rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .intel-list {
            list-style: none;
        }

        .intel-list li {
            padding: 10px 0;
            border-bottom: 1px solid var(--border-primary);
            font-size: 0.92rem;
            color: var(--text-muted);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .intel-list li:last-child { border-bottom: none; }

        /* Modals */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.75);
            backdrop-filter: blur(10px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: auto;
        }

        .modal-container {
            background: var(--bg-secondary);
            border: 1px solid var(--border-primary);
            border-radius: 24px;
            width: 90%;
            max-width: 600px;
            padding: 35px;
            position: relative;
            box-shadow: 0 25px 60px rgba(0,0,0,0.8);
            transform: translateY(20px);
            transition: transform 0.3s ease;
        }

        .modal-overlay.active .modal-container {
            transform: translateY(0);
        }

        .modal-close {
            position: absolute;
            top: 20px; right: 20px;
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            color: var(--text-muted);
            width: 35px; height: 35px;
            border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .modal-close:hover {
            color: var(--text-main);
            border-color: var(--danger-color);
        }

        /* Footer */
        .portal-footer {
            text-align: center;
            padding: 30px;
            background: var(--bg-secondary);
            backdrop-filter: blur(15px);
            border: 1px solid var(--border-primary);
            border-radius: 20px;
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 40px;
        }

        /* Pulse dot animation */
        .pulse-dot {
            width: 8px;
            height: 8px;
            background: var(--success-color);
            border-radius: 50%;
            box-shadow: 0 0 10px var(--success-color);
            animation: pulseAnim 2s infinite;
        }

        @keyframes pulseAnim {
            0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.7); }
            70% { transform: scale(1); box-shadow: 0 0 0 8px rgba(34, 197, 94, 0); }
            100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0); }
        }

        /* Responsive Layout */
        @media(max-width: 900px) {
            .hero-bento-grid { grid-template-columns: 1fr; }
            .sticky-navbar { padding: 15px 20px; }
            .nav-links { display: none; }
            body { padding-top: 80px; }
        }
    </style>
</head>
<body>

    <nav class="sticky-navbar">
        <div class="nav-logo" onclick="window.scrollTo({top: 0, behavior: 'smooth'})">
            <i class="fa-solid fa-scale-balanced"></i> СУД UKRAINE RP
        </div>
        <ul class="nav-links">
            <li><a href="#dashboard" class="active">Дашборд</a></li>
            <li><a href="#analytics">Аналітика</a></li>
            <li><a href="#staff">Колектив</a></li>
            <li><a href="#market">Біржа</a></li>
            <li><a href="#news">Новини</a></li>
        </ul>
        <div class="nav-actions">
            <button class="icon-btn" id="searchBtn" title="Швидкий пошук"><i class="fa-solid fa-search"></i></button>
            <button class="icon-btn" id="notificationsBtn" title="Сповіщення">
                <i class="fa-solid fa-bell"></i>
                <span class="badge-counter" id="notifCounter">3</span>
            </button>
            <button class="icon-btn" id="settingsBtn" title="Налаштування"><i class="fa-solid fa-gear"></i></button>
        </div>
    </nav>

    <div class="main-container">

        <div class="hero-bento-grid" id="dashboard">
            <div class="hero-main-card">
                <h1>Електронна Судова Система</h1>
                <p>Офіційний портал державного нагляду та правосуддя Ukraine RP. Високий рівень безпеки, прозорі процеси, миттєва апеляційна підтримка та актуальний моніторинг.</p>
                <div class="hero-actions">
                    <button class="btn-primary" onclick="scrollToSection('analytics')"><i class="fa-solid fa-chart-line"></i> Відкрити аналітику</button>
                    <button class="btn-secondary" onclick="scrollToSection('staff')"><i class="fa-solid fa-user-tie"></i> Суддівський склад</button>
                </div>
            </div>
            <div class="hero-side-card">
                <h3><i class="fa-solid fa-server"></i> Стан Системи</h3>
                <div class="live-stat-row">
                    <span>Статус</span>
                    <span style="color: var(--success-color); font-weight: bold; display: flex; align-items: center; gap: 5px;"><span class="pulse-dot"></span> Оперативно</span>
                </div>
                <div class="live-stat-row">
                    <span>Активні гравці</span>
                    <strong id="activeUsersCount" style="color: var(--text-main);">1,248</strong>
                </div>
                <div class="live-stat-row">
                    <span>Судді онлайн</span>
                    <strong style="color: var(--accent-blue);">2 / 3</strong>
                </div>
                <div class="live-stat-row">
                    <span>Uptime</span>
                    <strong style="color: var(--success-color);">99.98%</strong>
                </div>
            </div>
        </div>

        <div class="quick-actions-grid">
            <div class="quick-action-btn" onclick="scrollToSection('analytics')">
                <i class="fa-solid fa-chart-simple"></i>
                <span>Аналітика</span>
            </div>
            <div class="quick-action-btn" onclick="scrollToSection('staff')">
                <i class="fa-solid fa-user-tie"></i>
                <span>Колектив</span>
            </div>
            <div class="quick-action-btn" onclick="scrollToSection('market')">
                <i class="fa-solid fa-bolt"></i>
                <span>Біржа Активності</span>
            </div>
            <div class="quick-action-btn" onclick="scrollToSection('news')">
                <i class="fa-solid fa-bullhorn"></i>
                <span>Новини</span>
            </div>
            <div class="quick-action-btn" onclick="openModal('settingsModal')">
                <i class="fa-solid fa-sliders"></i>
                <span>Налаштування</span>
            </div>
        </div>

        <div class="content-section" id="analytics">
            <div class="section-header">
                <h2 class="section-title"><i class="fa-solid fa-chart-simple"></i> Судова Статистика</h2>
                <div class="chart-controls">
                    <button class="filter-btn active" onclick="updateChartData('day')">День</button>
                    <button class="filter-btn" onclick="updateChartData('week')">Тиждень</button>
                    <button class="filter-btn" onclick="updateChartData('month')">Місяць</button>
                </div>
            </div>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Динаміка завантаженості суддів та розгляду позовів у реальному часі.</p>
            
            <div class="chart-box-wrapper">
                <canvas id="courtActivityChart"></canvas>
            </div>
        </div>

        <div class="content-section" id="market">
            <div class="section-header">
                <h2 class="section-title"><i class="fa-solid fa-bolt"></i> Біржа активності та навантаження</h2>
                <span style="font-size: 0.85rem; color: var(--success-color); font-weight: bold; display: flex; align-items: center; gap: 5px;"><span class="pulse-dot"></span> Жива анімація оновлення (15с)</span>
            </div>
            
            <div class="stock-metrics-grid">
                <div class="stock-metric-card">
                    <div class="stock-metric-title">Показник розгляду справ</div>
                    <div class="stock-metric-value" id="stockMetric1">94.2%</div>
                    <div class="stock-metric-badge"><i class="fa-solid fa-caret-up"></i> +3.1%</div>
                </div>
                <div class="stock-metric-card">
                    <div class="stock-metric-title">Рівень довіри громадян</div>
                    <div class="stock-metric-value" id="stockMetric2">88.7%</div>
                    <div class="stock-metric-badge"><i class="fa-solid fa-caret-up"></i> +1.5%</div>
                </div>
                <div class="stock-metric-card">
                    <div class="stock-metric-title">Швидкість апеляцій</div>
                    <div class="stock-metric-value" id="stockMetric3">12.4 год</div>
                    <div class="stock-metric-badge" style="background: rgba(14, 165, 233, 0.15); color: var(--accent-blue); border-color: rgba(14, 165, 233, 0.3);"><i class="fa-solid fa-check"></i> Норма (48г)</div>
                </div>
            </div>
        </div>

        <div class="content-section" id="staff">
            <div class="section-header">
                <h2 class="section-title"><i class="fa-solid fa-users-gear"></i> Суддівський Колектив</h2>
            </div>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Професійний склад органів судової влади Ukraine RP.</p>
            
            <div class="staff-grid-container">
                <div class="staff-profile-card" onclick="openStaffModal('Mr_Zver3000', 'Суддя / Головний', 'Головує у найважливіших судових засіданнях та контролює дотримання регламенту правосуддя.', 'Roblox: Mr_Zver3000 | TG: @GreyFild_OFF')">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback"><i class="fa-solid fa-bolt"></i></div>
                    </div>
                    <h3>Mr_Zver3000</h3>
                    <div class="staff-role-badge">Суддя / Головний</div>
                    <div class="staff-contacts-info">
                        Roblox: Mr_Zver3000<br>
                        TG: <a href="https://t.me/GreyFild_OFF" target="_blank" onclick="event.stopPropagation()">@GreyFild_OFF</a>
                    </div>
                </div>

                <div class="staff-profile-card" onclick="openStaffModal('heehrhrhl18', 'Стажер-суддя', 'Проходить спеціалізовану підготовку та розглядає базові позови під наглядом керівництва.', 'Активний стажер судової системи')">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback"><i class="fa-solid fa-user-graduate"></i></div>
                    </div>
                    <h3>heehrhrhl18</h3>
                    <div class="staff-role-badge">Стажер-суддя</div>
                    <div class="staff-contacts-info">
                        Статус: Активний стажер<br>
                        Кадровий резерв
                    </div>
                </div>

                <div class="staff-profile-card" onclick="openStaffModal('Itz_raose', 'Стажер-суддя', 'Спеціалізується на фіксації судових засідань та первинній перевірці документації.', 'Активний стажер судової системи')">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback"><i class="fa-solid fa-user-graduate"></i></div>
                    </div>
                    <h3>Itz_raose</h3>
                    <div class="staff-role-badge">Стажер-суддя</div>
                    <div class="staff-contacts-info">
                        Статус: Активний стажер<br>
                        Кадровий резерв
                    </div>
                </div>
            </div>
        </div>

        <div class="content-section" id="news">
            <div class="section-header">
                <h2 class="section-title"><i class="fa-solid fa-bullhorn"></i> Новини та оновлення суду</h2>
            </div>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Актуальні внутрішні новини та регламенти.</p>

            <div class="news-grid">
                <div class="news-card" onclick="openNewsModal('Етика, професійні обов\'язки та апеляції', 'Додано правила конфіденційності, вимоги до лінії захисту, а також встановлено суворий строк подачі апеляцій — 48 годин з визначенням необхідного пакету документів.', 'Вчора, 10 серпня')">
                    <div>
                        <div class="news-date">Вчора, 10 серпня</div>
                        <div class="news-title">Етика, професійні обов'язки та апеляції</div>
                        <div class="news-desc">Додано правила конфіденційності, вимоги до лінії захисту, а також встановлено суворий строк подачі апеляцій — 48 годин з визначенням необхідного пакету документів.</div>
                    </div>
                    <span style="font-size: 0.85rem; color: var(--accent-blue); font-weight: 600;">Детальніше &rarr;</span>
                </div>
                <div class="news-card" onclick="openNewsModal('Масштабний редизайн сайту', 'Покращено темний стиль порталу, додано сучасні градієнти, тіні, ефекти скла, а також анімацію блоків і розширену біржу активності.', 'Сьогодні')">
                    <div>
                        <div class="news-date">Сьогодні</div>
                        <div class="news-title">Масштабний редизайн сайту</div>
                        <div class="news-desc">Покращено темний стиль порталу, додано сучасні градієнти, тіні, ефекти скла, а також анімацію блоків і розширену біржу активності.</div>
                    </div>
                    <span style="font-size: 0.85rem; color: var(--success-color); font-weight: 600;">Версія 2.5.0</span>
                </div>
                <div class="news-card" onclick="openNewsModal('День відкритих дверей', 'Слідкуйте за розкладом івенту для нових стажерів та громадян, які бажають ознайомитися з роботою судової системи Ukraine RP.', 'Анонс')">
                    <div>
                        <div class="news-date">Анонс</div>
                        <div class="news-title">День відкритих дверей</div>
                        <div class="news-desc">Слідкуйте за розкладом івенту для нових стажерів та громадян, які бажають ознайомитися з роботою судової системи Ukraine RP.</div>
                    </div>
                    <span style="font-size: 0.85rem; color: var(--warning-color); font-weight: 600;">Подія</span>
                </div>
            </div>
        </div>

        <div class="content-section">
            <div class="section-header">
                <h2 class="section-title"><i class="fa-solid fa-brain"></i> Інтелект системи та моніторинг</h2>
            </div>
            <div class="intelligence-grid">
                <div class="intel-card">
                    <h3><i class="fa-solid fa-chart-line" style="color: var(--accent-blue);"></i> Аналітичні висновки</h3>
                    <ul class="intel-list">
                        <li><i class="fa-solid fa-circle-check" style="color: var(--success-color);"></i> Активність користувачів виросла на 18% за тиждень.</li>
                        <li><i class="fa-solid fa-circle-check" style="color: var(--success-color);"></i> Найбільш активний період: 18:00–21:00.</li>
                        <li><i class="fa-solid fa-circle-check" style="color: var(--success-color);"></i> Усі апеляції опрацьовуються в межах 48 годин.</li>
                    </ul>
                </div>
                <div class="intel-card">
                    <h3><i class="fa-solid fa-shield-halved" style="color: var(--success-color);"></i> Безпека та Статус</h3>
                    <ul class="intel-list">
                        <li><span>Вебсайт API:</span> <strong style="color: var(--success-color);">Працює штатно</strong></li>
                        <li><span>База даних:</span> <strong style="color: var(--success-color);">Захищено</strong></li>
                        <li><span>Протоколи шифрування:</span> <strong style="color: var(--accent-blue);">Активні</strong></li>
                    </ul>
                </div>
            </div>
        </div>

        <footer class="portal-footer">
            <p>© 2026 Суд Ukraine RP. Всі права захищені. Офіційний портал судової системи.</p>
            <p style="margin-top: 5px; font-size: 0.8rem;">SYSTEM VERSION v2.5.0 • STATUS: ALL SYSTEMS OPERATIONAL</p>
        </footer>

    </div>

    <div class="modal-overlay" id="settingsModal">
        <div class="modal-container">
            <div class="modal-close" onclick="closeModal('settingsModal')"><i class="fa-solid fa-xmark"></i></div>
            <h2 style="color: var(--accent-blue); margin-bottom: 20px;"><i class="fa-solid fa-gear"></i> Налаштування порталу</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Виберіть тему оформлення інтерфейсу:</p>
            <div style="display: flex; gap: 15px; flex-wrap: wrap;">
                <button class="filter-btn active" onclick="setTheme('dark')">Dark Navy</button>
                <button class="filter-btn" onclick="setTheme('light')">Light Mode</button>
            </div>
        </div>
    </div>

    <div class="modal-overlay" id="generalModal">
        <div class="modal-container">
            <div class="modal-close" onclick="closeModal('generalModal')"><i class="fa-solid fa-xmark"></i></div>
            <h2 id="modalTitle" style="color: var(--accent-blue); margin-bottom: 15px;">Заголовок</h2>
            <p id="modalBody" style="color: var(--text-muted); line-height: 1.7;"></p>
        </div>
    </div>

    <script>
        // Smooth scroll helper
        function scrollToSection(id) {
            const el = document.getElementById(id);
            if(el) {
                el.scrollIntoView({ behavior: 'smooth' });
            }
        }

        // Modals Control
        function openModal(modalId) {
            document.getElementById(modalId).classList.add('active');
        }
        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
        }

        function openStaffModal(name, role, desc, contacts) {
            document.getElementById('modalTitle').innerText = name + ' — ' + role;
            document.getElementById('modalBody').innerHTML = '<strong>Опис:</strong> ' + desc + '<br><br><strong>Контакти:</strong> ' + contacts;
            openModal('generalModal');
        }

        function openNewsModal(title, desc, date) {
            document.getElementById('modalTitle').innerText = title;
            document.getElementById('modalBody').innerHTML = '<span style="color: var(--accent-blue); font-weight: bold; display: block; margin-bottom: 10px;">' + date + '</span>' + desc;
            openModal('generalModal');
        }

        document.getElementById('settingsBtn').addEventListener('click', () => openModal('settingsModal'));
        document.getElementById('searchBtn').addEventListener('click', () => {
            alert('Глобальний пошук: введіть ключове слово для швидкого переходу.');
        });
        document.getElementById('notificationsBtn').addEventListener('click', () => {
            alert('Сповіщення: регламент оновлено, система працює стабільно.');
            document.getElementById('notifCounter').style.display = 'none';
        });

        // Theme Switcher & LocalStorage
        function setTheme(themeName) {
            document.documentElement.setAttribute('data-theme', themeName);
            localStorage.setItem('court_theme', themeName);
            document.querySelectorAll('#settingsModal .filter-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
        }

        const savedTheme = localStorage.getItem('court_theme');
        if(savedTheme) {
            document.documentElement.setAttribute('data-theme', savedTheme);
        }

        // Chart.js Configuration
        const ctx = document.getElementById('courtActivityChart').getContext('2d');
        let courtChart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Нд'],
                datasets: [{
                    label: 'Активність суду',
                    data: [12, 19, 15, 25, 22, 30, 38],
                    borderColor: '#0ea5e9',
                    backgroundColor: 'rgba(14, 165, 233, 0.1)',
                    borderWidth: 3,
                    fill: true,
                    tension: 0.4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { labels: { color: '#f8fafc' } }
                },
                scales: {
                    x: { ticks: { color: '#94a3b8' }, grid: { color: 'rgba(255,255,255,0.05)' } },
                    y: { ticks: { color: '#94a3b8' }, grid: { color: 'rgba(255,255,255,0.05)' } }
                }
            }
        });

        function updateChartData(period) {
            document.querySelectorAll('#analytics .filter-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            if(period === 'day') {
                courtChart.data.labels = ['00:00', '04:00', '08:00', '12:00', '16:00', '20:00'];
                courtChart.data.datasets[0].data = [4, 2, 8, 22, 35, 28];
            } else if(period === 'week') {
                courtChart.data.labels = ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Нд'];
                courtChart.data.datasets[0].data = [12, 19, 15, 25, 22, 30, 38];
            } else if(period === 'month') {
                courtChart.data.labels = ['Тиждень 1', 'Тиждень 2', 'Тиждень 3', 'Тиждень 4'];
                courtChart.data.datasets[0].data = [95, 110, 130, 155];
            }
            courtChart.update();
        }

        // Live Animated Market Pulse (оновлення показників біржі кожні 15 секунд з анімацією свічення)
        setInterval(() => {
            const val1El = document.getElementById('stockMetric1');
            const val2El = document.getElementById('stockMetric2');
            
            const randomVal1 = (93 + Math.random() * 3).toFixed(1) + '%';
            const randomVal2 = (87 + Math.random() * 3).toFixed(1) + '%';
            
            val1El.innerText = randomVal1;
            val2El.innerText = randomVal2;

            // Додаємо тимчасовий клас анімації
            val1El.classList.add('updated');
            val2El.classList.add('updated');

            setTimeout(() => {
                val1El.classList.remove('updated');
                val2El.classList.remove('updated');
            }, 1000);
            
            const currentUsers = 1248 + Math.floor(Math.random() * 20) - 10;
            document.getElementById('activeUsersCount').innerText = currentUsers.toLocaleString();
        }, 15000);
    </script>
</body>
</html>

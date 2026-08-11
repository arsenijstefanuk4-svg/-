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
            --bg-card: #0b1329;
            --bg-card-hover: #101c3d;
            --border-primary: #1e293b;
            --border-accent: #38bdf8;
            --accent-blue: #0ea5e9;
            --accent-blue-hover: #38bdf8;
            --accent-glow: rgba(14, 165, 233, 0.45);
            --accent-purple: #818cf8;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --success-color: #22c55e;
            --warning-color: #f59e0b;
            --danger-color: #ef4444;
            --transition-speed: 0.3s;
        }

        [data-theme="midnight"] {
            --bg-primary: #050508;
            --bg-secondary: #0a0a12;
            --bg-card: #12121f;
            --bg-card-hover: #1b1b2f;
            --border-primary: #27273a;
            --accent-blue: #6366f1;
            --accent-blue-hover: #818cf8;
            --accent-glow: rgba(99, 102, 241, 0.45);
            --accent-purple: #a855f7;
        }

        [data-theme="cyber"] {
            --bg-primary: #030712;
            --bg-secondary: #090d16;
            --bg-card: #0f172a;
            --bg-card-hover: #1e293b;
            --border-primary: #334155;
            --accent-blue: #06b6d4;
            --accent-blue-hover: #22d3ee;
            --accent-glow: rgba(6, 182, 212, 0.5);
            --accent-purple: #3b82f6;
        }

        [data-theme="light"] {
            --bg-primary: #f8fafc;
            --bg-secondary: #f1f5f9;
            --bg-card: #ffffff;
            --bg-card-hover: #e2e8f0;
            --border-primary: #cbd5e1;
            --border-accent: #0284c7;
            --accent-blue: #0284c7;
            --accent-blue-hover: #0369a1;
            --accent-glow: rgba(2, 132, 199, 0.25);
            --accent-purple: #6366f1;
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
            position: relative;
        }

        /* Top Navigation */
        .sticky-navbar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: rgba(7, 13, 31, 0.85);
            backdrop-filter: blur(16px);
            border-bottom: 1px solid var(--border-primary);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 40px;
            z-index: 1000;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
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
            text-shadow: 0 0 10px var(--accent-glow);
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
            transition: all 0.3s ease;
        }

        .icon-btn:hover {
            border-color: var(--accent-blue);
            box-shadow: 0 0 15px var(--accent-glow);
            transform: translateY(-2px);
        }

        .badge-counter {
            position: absolute;
            top: -5px;
            right: -5px;
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
        }

        .main-container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Mega Title */
        .mega-title-wrapper {
            text-align: center;
            margin-bottom: 40px;
            padding: 20px;
            position: relative;
        }

        .mega-title {
            font-size: clamp(2.5rem, 6vw, 4.5rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 4px;
            background: linear-gradient(135deg, var(--accent-blue) 0%, #ffffff 50%, var(--accent-purple) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 35px var(--accent-glow));
            margin-bottom: 10px;
        }

        .mega-subtitle {
            color: var(--text-muted);
            font-size: 1.2rem;
            letter-spacing: 1px;
        }

        /* Hero Info Box (System Status Grid) */
        .hero-status-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 20px;
            margin-bottom: 35px;
        }

        .status-card {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            border-radius: 20px;
            padding: 25px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.4);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .status-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 4px;
            background: var(--accent-blue);
        }

        .status-card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            color: var(--text-muted);
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .status-card-value {
            font-size: 2rem;
            font-weight: 800;
            color: var(--text-main);
            margin-bottom: 5px;
        }

        .status-indicator {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 0.85rem;
            font-weight: 700;
            color: var(--success-color);
        }

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

        /* Quick Actions */
        .quick-actions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-bottom: 35px;
        }

        .quick-action-btn {
            background: var(--bg-card);
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
            font-size: 1.5rem;
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
            background: var(--bg-secondary);
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
        }

        .section-title {
            color: var(--accent-blue);
            font-size: 1.75rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
            text-shadow: 0 0 15px var(--accent-glow);
        }

        /* Market / Economy Stock Metrics */
        .stock-metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .stock-metric-card {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            border-radius: 18px;
            padding: 22px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0,0,0,0.4);
            transition: transform 0.3s ease, border-color 0.3s ease;
        }

        .stock-metric-card:hover {
            transform: translateY(-5px);
            border-color: var(--accent-blue);
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
            height: 450px;
            background: var(--bg-card);
            padding: 25px;
            border-radius: 20px;
            border: 1px solid var(--border-primary);
            box-shadow: inset 0 0 35px rgba(0,0,0,0.5);
        }

        .chart-controls {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
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

        /* Staff Grid (зменшено кількість суддів на 1 людину за запитом) */
        .staff-grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 24px;
            margin-top: 25px;
        }

        .staff-profile-card {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            padding: 30px 20px;
            border-radius: 20px;
            text-align: center;
            transition: transform 0.4s ease, border-color 0.4s ease, box-shadow 0.4s ease;
            position: relative;
            overflow: hidden;
        }

        .staff-profile-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 5px;
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

        /* Tables & Analytics */
        .table-box-wrapper {
            width: 100%; overflow-x: auto; margin-top: 25px; border-radius: 20px; border: 1px solid var(--border-primary); background-color: var(--bg-card);
        }

        .analytics-table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.95rem; white-space: nowrap; }
        .analytics-table th, .analytics-table td { padding: 16px 20px; border-bottom: 1px solid var(--border-primary); color: var(--text-main); }
        .analytics-table th { background-color: var(--bg-secondary); color: var(--accent-blue); font-weight: 600; text-transform: uppercase; font-size: 0.8rem; letter-spacing: 1px; }
        .analytics-table tbody tr:hover { background-color: var(--bg-card-hover); }

        /* News & Updates Branch */
        .news-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .news-card {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            border-radius: 16px;
            padding: 25px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: all 0.3s ease;
        }

        .news-card:hover {
            border-color: var(--accent-blue);
            transform: translateY(-3px);
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

        /* Modals & Dialogs */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(8px);
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
            border: 1px solid var(--border-primary);
            border-radius: 20px;
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 40px;
        }

        /* Responsive */
        @media(max-width: 768px) {
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
            <button class="icon-btn" id="searchBtn" title="Пошук (Ctrl+K)"><i class="fa-solid fa-search"></i></button>
            <button class="icon-btn" id="notificationsBtn" title="Сповіщення">
                <i class="fa-solid fa-bell"></i>
                <span class="badge-counter" id="notifCounter">3</span>
            </button>
            <button class="icon-btn" id="settingsBtn" title="Налаштування"><i class="fa-solid fa-gear"></i></button>
        </div>
    </nav>

    <div class="main-container">

        <div class="mega-title-wrapper">
            <h1 class="mega-title">СУДОВИЙ ПОРТАЛ</h1>
            <p class="mega-subtitle">Офіційна електронна система правосуддя та державного нагляду Ukraine RP</p>
        </div>

        <div class="hero-status-grid" id="dashboard">
            <div class="status-card">
                <div class="status-card-header">
                    <span>Статус системи</span>
                    <i class="fa-solid fa-server" style="color: var(--accent-blue);"></i>
                </div>
                <div class="status-card-value">99.98%</div>
                <div class="status-indicator">
                    <span class="pulse-dot"></span> Всі системи штатні
                </div>
            </div>
            <div class="status-card">
                <div class="status-card-header">
                    <span>Активні гравці</span>
                    <i class="fa-solid fa-users" style="color: var(--accent-purple);"></i>
                </div>
                <div class="status-card-value" id="activeUsersCount">1,248</div>
                <div class="status-indicator" style="color: var(--accent-blue);">
                    <i class="fa-solid fa-arrow-trend-up"></i> +12.4% за тиждень
                </div>
            </div>
            <div class="status-card">
                <div class="status-card-header">
                    <span>Судді онлайн</span>
                    <i class="fa-solid fa-gavel" style="color: var(--success-color);"></i>
                </div>
                <div class="status-card-value">2 / 3</div>
                <div class="status-indicator">
                    <span class="pulse-dot"></span> На зв'язку
                </div>
            </div>
            <div class="status-card">
                <div class="status-card-header">
                    <span>Апеляції (48 год)</span>
                    <i class="fa-solid fa-file-shield" style="color: var(--warning-color);"></i>
                </div>
                <div class="status-card-value">0 затримок</div>
                <div class="status-indicator" style="color: var(--warning-color);">
                    Регламент активний
                </div>
            </div>
        </div>

        <div class="quick-actions-grid">
            <div class="quick-action-btn" onclick="scrollToSection('analytics')">
                <i class="fa-solid fa-chart-line"></i>
                <span>Аналітика</span>
            </div>
            <div class="quick-action-btn" onclick="scrollToSection('staff')">
                <i class="fa-solid fa-user-tie"></i>
                <span>Колектив</span>
            </div>
            <div class="quick-action-btn" onclick="scrollToSection('market')">
                <i class="fa-solid fa-chart-pie"></i>
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
                <h2 class="section-title"><i class="fa-solid fa-chart-simple"></i> Статистика та графіка суду</h2>
                <div class="chart-controls">
                    <button class="filter-btn active" onclick="updateChartData('day')">День</button>
                    <button class="filter-btn" onclick="updateChartData('week')">Тиждень</button>
                    <button class="filter-btn" onclick="updateChartData('month')">Місяць</button>
                </div>
            </div>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Динаміка активності судової системи та показники розгляду справ у реальному часі.</p>
            
            <div class="chart-box-wrapper">
                <canvas id="courtActivityChart"></canvas>
            </div>
        </div>

        <div class="content-section" id="market">
            <div class="section-header">
                <h2 class="section-title"><i class="fa-solid fa-bolt"></i> Біржа активності та навантаження</h2>
                <span style="font-size: 0.85rem; color: var(--success-color); font-weight: bold;"><span class="pulse-dot" style="display:inline-block; margin-right:5px;"></span> Оновлення кожні 15 сек</span>
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
                <h2 class="section-title"><i class="fa-solid fa-users-gear"></i> Керівництво та колектив суду</h2>
            </div>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Склад судової системи Ukraine RP, контакти та адміністративні ролі.</p>
            
            <div class="staff-grid-container">
                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback"><i class="fa-solid fa-bolt"></i></div>
                    </div>
                    <h3>Mr_Zver3000</h3>
                    <div class="staff-role-badge">Суддя / Головний</div>
                    <div class="staff-contacts-info">
                        Roblox: Mr_Zver3000<br>
                        TG: <a href="https://t.me/GreyFild_OFF" target="_blank">@GreyFild_OFF</a>
                    </div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback"><i class="fa-solid fa-user-graduate"></i></div>
                    </div>
                    <h3>heehrhrhl18</h3>
                    <div class="staff-role-badge">Стажер-суддя</div>
                    <div class="staff-contacts-info">
                        Статус: Активний стажер<br>
                        TG: Інтегровано в кадри
                    </div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback"><i class="fa-solid fa-user-graduate"></i></div>
                    </div>
                    <h3>Itz_raose</h3>
                    <div class="staff-role-badge">Стажер-суддя</div>
                    <div class="staff-contacts-info">
                        Статус: Активний стажер<br>
                        TG: Інтегровано в кадри
                    </div>
                </div>
            </div>
        </div>

        <div class="content-section" id="news">
            <div class="section-header">
                <h2 class="section-title"><i class="fa-solid fa-bullhorn"></i> Новини та оновлення суду</h2>
            </div>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Актуальні внутрішні новини, регламенти та оновлення порталу.</p>

            <div class="news-grid">
                <div class="news-card">
                    <div>
                        <div class="news-date">Вчора, 10 серпня</div>
                        <div class="news-title">Етика, професійні обов'язки та апеляції</div>
                        <div class="news-desc">Додано правила конфіденційності, вимоги до лінії захисту, а також встановлено суворий строк подачі апеляцій — 48 годин з визначенням необхідного пакету документів.</div>
                    </div>
                    <span style="font-size: 0.85rem; color: var(--accent-blue); font-weight: 600;">Офіційний регламент</span>
                </div>
                <div class="news-card">
                    <div>
                        <div class="news-date">Сьогодні</div>
                        <div class="news-title">Масштабний редизайн сайту</div>
                        <div class="news-desc">Покращено темний стиль порталу, додано сучасні градієнти, тіні, ефекти скла, а також анімацію блоків і розширену біржу активності.</div>
                    </div>
                    <span style="font-size: 0.85rem; color: var(--success-color); font-weight: 600;">Версія 2.5.0</span>
                </div>
                <div class="news-card">
                    <div>
                        <div class="news-date">Анонс</div>
                        <div class="news-title">День відкритих дверей</div>
                        <div class="news-desc">Слідкуйте за розкладом івенту для нових стажерів та громадян, які бажають ознайомитися з роботою судової системи Ukraine RP.</div>
                    </div>
                    <span style="font-size: 0.85rem; color: var(--warning-color); font-weight: 600;">Подія</span>
                </div>
            </div>
        </div>

        <footer class="portal-footer">
            <p>© 2026 Суд Ukraine RP. Всі права захищені. Офіційний портал судової системи.</p>
            <p style="margin-top: 5px; font-size: 0.8rem;">SYSTEM VERSION v2.5.0 • STATUS: OPERATIONAL</p>
        </footer>

    </div>

    <div class="modal-overlay" id="settingsModal">
        <div class="modal-container">
            <div class="modal-close" onclick="closeModal('settingsModal')"><i class="fa-solid fa-xmark"></i></div>
            <h2 style="color: var(--accent-blue); margin-bottom: 20px;"><i class="fa-solid fa-gear"></i> Налаштування порталу</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Виберіть тему оформлення інтерфейсу:</p>
            <div style="display: flex; gap: 15px; flex-wrap: wrap;">
                <button class="filter-btn active" onclick="setTheme('dark')">Dark Navy</button>
                <button class="filter-btn" onclick="setTheme('midnight')">Midnight Black</button>
                <button class="filter-btn" onclick="setTheme('cyber')">Cyber Neon</button>
                <button class="filter-btn" onclick="setTheme('light')">Light Mode</button>
            </div>
        </div>
    </div>

    <script>
        // Smooth scrolling for navigation
        function scrollToSection(id) {
            const el = document.getElementById(id);
            if(el) {
                el.scrollIntoView({ behavior: 'smooth' });
            }
        }

        // Modals Management
        function openModal(modalId) {
            document.getElementById(modalId).classList.add('active');
        }
        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
        }

        document.getElementById('settingsBtn').addEventListener('click', () => openModal('settingsModal'));
        document.getElementById('searchBtn').addEventListener('click', () => {
            alert('Глобальний пошук: введіть запит для швидкого навігування по розділах суду.');
        });
        document.getElementById('notificationsBtn').addEventListener('click', () => {
            alert('У вас 3 нових сповіщення: оновлення регламенту апеляцій, нові стажери-судді та технічні роботи на порталі.');
            document.getElementById('notifCounter').style.display = 'none';
        });

        // Theme Switcher
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

        // Chart.js Setup with live feel
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

        // Animated Stock / Statistics simulation (прыгает каждые 15 секунд по запросу)
        setInterval(() => {
            const randomVal1 = (93 + Math.random() * 3).toFixed(1) + '%';
            const randomVal2 = (87 + Math.random() * 3).toFixed(1) + '%';
            document.getElementById('stockMetric1').innerText = randomVal1;
            document.getElementById('stockMetric2').innerText = randomVal2;
            
            // Randomize active users slightly for realistic feel
            const currentUsers = 1248 + Math.floor(Math.random() * 20) - 10;
            document.getElementById('activeUsersCount').innerText = currentUsers.toLocaleString();
        }, 15000);
    </script>
</body>
</html>

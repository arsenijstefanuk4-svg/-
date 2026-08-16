<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Офіційний Портал Судової Системи | Ukraine RP</title>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary-accent: #38bdf8;
            --primary-glow: rgba(56, 189, 248, 0.35);
            --secondary-accent: #818cf8;
            --bg-dark: #070913;
            --card-bg: rgba(15, 23, 42, 0.65);
            --card-border: rgba(255, 255, 255, 0.08);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --danger: #ef4444;
            --success: #10b981;
            --warning: #f59e0b;
            --radius-lg: 24px;
            --radius-md: 16px;
            --transition-smooth: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }

        /* ТЕМИ */
        [data-theme="purple"] {
            --primary-accent: #a855f7;
            --primary-glow: rgba(168, 85, 247, 0.35);
            --secondary-accent: #ec4899;
        }
        [data-theme="emerald"] {
            --primary-accent: #10b981;
            --primary-glow: rgba(16, 185, 129, 0.35);
            --secondary-accent: #06b6d4;
        }
        [data-theme="sunset"] {
            --primary-accent: #f97316;
            --primary-glow: rgba(249, 115, 22, 0.35);
            --secondary-accent: #eab308;
        }
        [data-theme="neon"] {
            --primary-accent: #00f2fe;
            --primary-glow: rgba(0, 242, 254, 0.4);
            --secondary-accent: #4facfe;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Plus Jakarta Sans', sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 15% 15%, var(--primary-glow) 0%, transparent 40%),
                radial-gradient(circle at 85% 85%, rgba(129, 140, 248, 0.15) 0%, transparent 40%);
            background-attachment: fixed;
            min-height: 100vh;
        }

        /* Scrollbar */
        ::-webkit-scrollbar { width: 10px; }
        ::-webkit-scrollbar-track { background: var(--bg-dark); }
        ::-webkit-scrollbar-thumb { 
            background: rgba(255, 255, 255, 0.15); 
            border-radius: 5px;
            border: 2px solid var(--bg-dark);
        }
        ::-webkit-scrollbar-thumb:hover { background: var(--primary-accent); }

        /* Scroll Progress */
        .scroll-progress {
            position: fixed;
            top: 0;
            left: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary-accent), var(--secondary-accent));
            z-index: 1000;
            width: 0%;
            box-shadow: 0 0 12px var(--primary-accent);
        }

        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 20px;
        }

        /* HEADER & NAV */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 30px;
            background: rgba(15, 23, 42, 0.7);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid var(--card-border);
            border-radius: var(--radius-lg);
            margin-bottom: 40px;
            position: sticky;
            top: 20px;
            z-index: 100;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
        }

        .logo-box {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-icon {
            font-size: 2rem;
            background: linear-gradient(135deg, var(--primary-accent), var(--secondary-accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 10px var(--primary-glow));
        }

        .logo-text h1 {
            font-size: 1.25rem;
            font-weight: 800;
            letter-spacing: -0.5px;
        }

        .logo-text p {
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        .header-controls {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .live-clock {
            background: rgba(255, 255, 255, 0.05);
            padding: 8px 16px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.9rem;
            border: 1px solid var(--card-border);
            letter-spacing: 1px;
        }

        .btn-settings {
            background: linear-gradient(135deg, var(--primary-accent), var(--secondary-accent));
            color: #000;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition-smooth);
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 15px var(--primary-glow);
        }

        .btn-settings:hover {
            transform: translateY(-2px) scale(1.03);
            box-shadow: 0 8px 25px var(--primary-glow);
        }

        /* SECTIONS COMMON */
        .content-section {
            background: var(--card-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--card-border);
            border-radius: var(--radius-lg);
            padding: 40px;
            margin-bottom: 40px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            transition: var(--transition-smooth);
        }

        .section-title {
            font-size: 1.8rem;
            font-weight: 800;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .section-description {
            color: var(--text-muted);
            margin-bottom: 30px;
            font-size: 1rem;
        }

        /* ANALYTICS & CHART */
        .chart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 25px;
        }

        .status-pill {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 8px 18px;
            border-radius: 30px;
            background: rgba(16, 185, 129, 0.1);
            border: 1px solid rgba(16, 185, 129, 0.3);
            color: var(--success);
            font-weight: 600;
            font-size: 0.85rem;
            transition: var(--transition-smooth);
        }

        .status-pill.glitch-mode {
            background: rgba(239, 68, 68, 0.15);
            border-color: rgba(239, 68, 68, 0.4);
            color: var(--danger);
            animation: pulse-danger 1s infinite alternate;
        }

        @keyframes pulse-danger {
            0% { box-shadow: 0 0 5px rgba(239, 68, 68, 0.2); }
            100% { box-shadow: 0 0 20px rgba(239, 68, 68, 0.6); }
        }

        .chart-container {
            position: relative;
            height: 380px;
            width: 100%;
        }

        /* GRID CARDS (STAFF & BLACKLIST) */
        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
        }

        .staff-profile-card, .blacklist-card {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid var(--card-border);
            border-radius: var(--radius-md);
            padding: 25px;
            text-align: center;
            position: relative;
            overflow: hidden;
            transition: var(--transition-smooth);
            transform-style: preserve-3d;
        }

        .staff-profile-card::before, .blacklist-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 4px;
            background: linear-gradient(90deg, var(--primary-accent), var(--secondary-accent));
            opacity: 0;
            transition: var(--transition-smooth);
        }

        .staff-profile-card:hover, .blacklist-card:hover {
            background: rgba(255, 255, 255, 0.05);
            border-color: rgba(255, 255, 255, 0.2);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
        }

        .staff-profile-card:hover::before, .blacklist-card:hover::before {
            opacity: 1;
        }

        .staff-avatar-wrapper {
            width: 90px;
            height: 90px;
            margin: 0 auto 15px;
            border-radius: 50%;
            padding: 3px;
            background: linear-gradient(135deg, var(--primary-accent), var(--secondary-accent));
            box-shadow: 0 8px 20px var(--primary-glow);
        }

        .staff-avatar-wrapper img, .avatar-fallback {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
            background: var(--bg-dark);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
        }

        .staff-role-badge {
            display: inline-block;
            padding: 4px 12px;
            background: rgba(56, 189, 248, 0.1);
            color: var(--primary-accent);
            border-radius: 12px;
            font-size: 0.8rem;
            font-weight: 700;
            margin: 8px 0 15px;
            border: 1px solid rgba(56, 189, 248, 0.2);
        }

        .staff-contacts-info {
            font-size: 0.85rem;
            color: var(--text-muted);
            line-height: 1.6;
        }

        .staff-contacts-info a {
            color: var(--primary-accent);
            text-decoration: none;
            font-weight: 600;
            transition: var(--transition-smooth);
        }

        .staff-contacts-info a:hover {
            text-decoration: underline;
            text-shadow: 0 0 8px var(--primary-glow);
        }

        /* BLACKLIST SPECIFIC */
        .blacklist-card {
            border-color: rgba(239, 68, 68, 0.2);
        }
        
        .blacklist-card::before {
            background: var(--danger) !important;
        }

        .blacklist-icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        .blacklist-badge {
            display: inline-block;
            background: rgba(239, 68, 68, 0.15);
            color: var(--danger);
            padding: 6px 14px;
            border-radius: 12px;
            font-size: 0.75rem;
            font-weight: 800;
            letter-spacing: 0.5px;
            margin: 10px 0;
            border: 1px solid rgba(239, 68, 68, 0.3);
        }

        /* TABLES */
        .table-box-wrapper {
            overflow-x: auto;
            border-radius: var(--radius-md);
            border: 1px solid var(--card-border);
        }

        .analytics-table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
            font-size: 0.95rem;
        }

        .analytics-table th {
            background: rgba(255, 255, 255, 0.03);
            padding: 16px 20px;
            color: var(--text-muted);
            font-weight: 700;
            border-bottom: 1px solid var(--card-border);
            white-space: nowrap;
        }

        .analytics-table td {
            padding: 18px 20px;
            border-bottom: 1px solid var(--card-border);
            background: rgba(15, 23, 42, 0.2);
        }

        .analytics-table tr:last-child td {
            border-bottom: none;
        }

        .analytics-table tr:hover td {
            background: rgba(255, 255, 255, 0.03);
        }

        .status-up { color: var(--success); font-weight: 700; }
        .status-stable { color: var(--primary-accent); font-weight: 700; }

        /* EVENTS & NEWS */
        .event-detailed-card {
            background: linear-gradient(135deg, rgba(56, 189, 248, 0.05), rgba(129, 140, 248, 0.05));
            border: 1px solid var(--card-border);
            border-radius: var(--radius-md);
            padding: 30px;
            margin-top: 30px;
        }

        .event-detailed-card h3 {
            font-size: 1.4rem;
            margin-bottom: 12px;
            color: var(--primary-accent);
        }

        .event-benefits-list {
            list-style: none;
            margin: 15px 0 20px;
        }

        .event-benefits-list li {
            position: relative;
            padding-left: 25px;
            margin-bottom: 10px;
            color: var(--text-muted);
        }

        .event-benefits-list li::before {
            content: '✦';
            position: absolute;
            left: 0;
            color: var(--primary-accent);
        }

        .event-schedule-container {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
            margin-top: 15px;
        }

        .schedule-badge {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--card-border);
            padding: 8px 16px;
            border-radius: 12px;
            font-size: 0.85rem;
            font-weight: 600;
        }

        .owner-news-branch {
            margin-top: 30px;
            padding: 25px;
            border-left: 4px solid var(--primary-accent);
            background: rgba(255, 255, 255, 0.01);
            border-radius: 0 var(--radius-md) var(--radius-md) 0;
        }

        /* MODAL SETTINGS */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(10px);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            pointer-events: none;
            transition: var(--transition-smooth);
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: all;
        }

        .modal-card {
            background: var(--bg-dark);
            border: 1px solid var(--card-border);
            border-radius: var(--radius-lg);
            padding: 35px;
            width: 100%;
            max-width: 450px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.6);
            transform: translateY(20px) scale(0.95);
            transition: var(--transition-smooth);
        }

        .modal-overlay.active .modal-card {
            transform: translateY(0) scale(1);
        }

        .theme-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin: 20px 0;
        }

        .theme-btn {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid var(--card-border);
            padding: 12px;
            border-radius: 12px;
            color: var(--text-main);
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: var(--transition-smooth);
        }

        .theme-btn:hover {
            background: rgba(255, 255, 255, 0.08);
            border-color: rgba(255, 255, 255, 0.2);
        }

        .theme-dot {
            width: 16px;
            height: 16px;
            border-radius: 50%;
        }

        .btn-close-modal {
            width: 100%;
            padding: 12px;
            background: rgba(255, 255, 255, 0.1);
            border: none;
            border-radius: 12px;
            color: #fff;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition-smooth);
        }

        .btn-close-modal:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        /* QUICK NAV FLOATING BUTTONS */
        .quick-nav {
            position: fixed;
            bottom: 30px;
            right: 30px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            z-index: 90;
        }

        .nav-btn {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: rgba(15, 23, 42, 0.8);
            backdrop-filter: blur(8px);
            border: 1px solid var(--card-border);
            color: var(--text-main);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: var(--transition-smooth);
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }

        .nav-btn:hover {
            background: var(--primary-accent);
            color: #000;
            transform: scale(1.1);
        }

        /* ANIMATION UTILS */
        .animate-on-scroll {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* RIPPLE EFFECT */
        .ripple {
            position: absolute;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            transform: scale(0);
            animation: ripple-anim 0.6s linear;
            pointer-events: none;
        }

        @keyframes ripple-anim {
            to { transform: scale(4); opacity: 0; }
        }

        footer {
            text-align: center;
            padding: 30px 0;
            color: var(--text-muted);
            font-size: 0.85rem;
            border-top: 1px solid var(--card-border);
            margin-top: 40px;
        }

        /* RESPONSIVE */
        @media (max-width: 768px) {
            header {
                flex-direction: column;
                gap: 15px;
                text-align: center;
            }
            .content-section { padding: 25px 20px; }
            .chart-container { height: 280px; }
        }
    </style>
</head>
<body>

    <div class="scroll-progress" id="scrollProgress"></div>

    <div class="container">
        <!-- HEADER -->
        <header>
            <div class="logo-box">
                <div class="logo-icon">⚖️</div>
                <div class="logo-text">
                    <h1>Судова Система</h1>
                    <p>Ukraine RP • Офіційний Портал</p>
                </div>
            </div>
            <div class="header-controls">
                <div class="live-clock" id="liveClock">00:00:00</div>
                <button class="btn-settings" id="openSettingsBtn">
                    ⚙️ Налаштування
                </button>
            </div>
        </header>

        <!-- ANALYTICS SECTION -->
        <section class="content-section animate-on-scroll">
            <div class="chart-header">
                <div>
                    <h2 class="section-title">📈 Аналітика та Динаміка Справ</h2>
                    <p class="section-description" style="margin-bottom:0;">Статистика розгляду засідань та навантаження судової колегії</p>
                </div>
                <div class="status-pill" id="marketStatusPill">
                    <span id="statusDot">●</span>
                    <span id="marketStatusText">СИСТЕМА ПРАЦЮЄ В ШТАТНОМУ РЕЖИМІ</span>
                </div>
            </div>

            <div class="chart-container">
                <canvas id="courtStockChart"></canvas>
            </div>
        </section>

        <!-- STAFF SECTION -->
        <section class="content-section animate-on-scroll">
            <h2 class="section-title">🏛 Судова Колегія</h2>
            <p class="section-description">Офіційний склад суддівського корпусу та контакти для зв'язку.</p>

            <div class="cards-grid">
                <!-- Card 1 -->
                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <img src="https://via.placeholder.com/150" alt="mummu228kuku" onerror="this.replaceWith(Object.assign(document.createElement('div'), {className: 'avatar-fallback', innerText: '⚖️'}))">
                    </div>
                    <h3>mummu228kuku</h3>
                    <div class="staff-role-badge">Головний Суддя</div>
                    <div class="staff-contacts-info">
                        Roblox: mummu228kuku<br>
                        TG: <a href="https://t.me/here_everyone" target="_blank">@here_everyone</a>
                    </div>
                </div>

                <!-- Card 2 -->
                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <img src="https://via.placeholder.com/150" alt="Huhaidjopy" onerror="this.replaceWith(Object.assign(document.createElement('div'), {className: 'avatar-fallback', innerText: '🏛'}))">
                    </div>
                    <h3>Huhaidjopy</h3>
                    <div class="staff-role-badge">Суддя</div>
                    <div class="staff-contacts-info">
                        Roblox: Huhaidjopy<br>
                        TG: <a href="https://t.me/bewewewewewe" target="_blank">@bewewewewewe</a>
                    </div>
                </div>
            </div>
        </section>

        <!-- BLACKLIST SECTION -->
        <section class="content-section animate-on-scroll" id="blacklist">
            <h2 class="section-title" style="color: var(--danger);">🚫 Чорний Список</h2>
            <p class="section-description">Записи про звільнених учасників та порушників регламенту.</p>

            <div class="cards-grid">
                <article class="blacklist-card">
                    <div class="blacklist-icon">🚫</div>
                    <h3>heehrhrhl18</h3>
                    <span class="blacklist-badge">ЗВІЛЬНЕНО / ЧОРНИЙ СПИСОК</span>
                    <div class="staff-contacts-info">
                        Roblox: heehrhrhl18<br>
                        TG: <a href="https://t.me/hehr18_UR" target="_blank">@hehr18_UR</a>
                    </div>
                </article>
            </div>
        </section>

        <!-- REPORTS & ARCHIVE TABLE SECTION -->
        <section class="content-section animate-on-scroll">
            <h2 class="section-title">📊 Архів Звітів та Інцидентів</h2>
            <p class="section-description">Деталізована статистика оброблених справ та порушень серверних регламентів:</p>

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

            <!-- EVENT DETAILS -->
            <div class="event-detailed-card">
                <h3>🏛 Івент: День Відкритих Дверей Суду</h3>
                <p><strong>Чому цей івент корисний?</strong> Це унікальна можливість зазирнути за лаштунки судової системи, зрозуміти свої права та навчитися грамотно захищати себе в рольових ситуаціях без порушення правил сервера.</p>
                
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

            <!-- NEWS BRANCH -->
            <div class="owner-news-branch">
                <h3>📢 Новини та оновлення від керівництва</h3>
                <p>У цій гілці публікуються актуальні внутрішні новини, майбутні оновлення судової системи, а також корисні поради щодо покращення рольової гри на сервері. Слідкуйте за оновленнями порталу, щоб бути в курсі найважливіших державних подій Ukraine RP!</p>
            </div>
        </section>

        <!-- FOOTER -->
        <footer class="animate-on-scroll">
            <p>&copy; 2026 Офіційний Портал Судової Системи Ukraine RP. Усі права захищені.</p>
        </footer>
    </div>

    <!-- QUICK NAV BUTTONS -->
    <div class="quick-nav">
        <button class="nav-btn" id="toTop" title="Вгору">▲</button>
        <button class="nav-btn" id="toBottom" title="Вниз">▼</button>
    </div>

    <!-- SETTINGS MODAL -->
    <div class="modal-overlay" id="settingsModal">
        <div class="modal-card">
            <h2>⚙️ Налаштування теми</h2>
            <p style="color: var(--text-muted); font-size: 0.9rem; margin-top: 5px;">Виберіть кольорову гаму для інтерфейсу:</p>

            <div class="theme-options">
                <button class="theme-btn" data-set-theme="default">
                    <span class="theme-dot" style="background: #38bdf8;"></span> Blue Neon
                </button>
                <button class="theme-btn" data-set-theme="purple">
                    <span class="theme-dot" style="background: #a855f7;"></span> Cyber Purple
                </button>
                <button class="theme-btn" data-set-theme="emerald">
                    <span class="theme-dot" style="background: #10b981;"></span> Emerald
                </button>
                <button class="theme-btn" data-set-theme="sunset">
                    <span class="theme-dot" style="background: #f97316;"></span> Sunset Glow
                </button>
            </div>

            <button class="btn-close-modal" id="closeSettingsBtn">Закрити</button>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            // 1. SCROLL PROGRESS
            const progress = document.getElementById('scrollProgress');
            const updateScrollProgress = () => {
                const scrollTop = window.scrollY;
                const max = document.documentElement.scrollHeight - window.innerHeight;
                progress.style.width = `${max > 0 ? (scrollTop / max) * 100 : 0}%`;
            };
            window.addEventListener('scroll', updateScrollProgress, { passive: true });

            // 2. QUICK NAV
            document.getElementById('toTop').addEventListener('click', () => window.scrollTo({ top: 0, behavior: 'smooth' }));
            document.getElementById('toBottom').addEventListener('click', () => window.scrollTo({ top: document.documentElement.scrollHeight, behavior: 'smooth' }));

            // 3. RIPPLE EFFECT ON BUTTONS
            document.querySelectorAll('button').forEach(btn => {
                btn.style.position = 'relative';
                btn.style.overflow = 'hidden';
                btn.addEventListener('click', function(e) {
                    const rect = this.getBoundingClientRect();
                    const ripple = document.createElement('span');
                    ripple.className = 'ripple';
                    const size = Math.max(rect.width, rect.height);
                    ripple.style.width = ripple.style.height = `${size}px`;
                    ripple.style.left = `${e.clientX - rect.left - size / 2}px`;
                    ripple.style.top = `${e.clientY - rect.top - size / 2}px`;
                    this.appendChild(ripple);
                    setTimeout(() => ripple.remove(), 600);
                });
            });

            // 4. 3D CARD TILT EFFECT
            document.querySelectorAll('.staff-profile-card, .blacklist-card').forEach(card => {
                card.addEventListener('pointermove', (e) => {
                    const rect = card.getBoundingClientRect();
                    const x = (e.clientX - rect.left) / rect.width - 0.5;
                    const y = (e.clientY - rect.top) / rect.height - 0.5;
                    card.style.transform = `perspective(1000px) rotateX(${-y * 8}deg) rotateY(${x * 8}deg) translateY(-5px)`;
                });
                card.addEventListener('pointerleave', () => {
                    card.style.transform = '';
                });
            });

            // 5. LIVE CLOCK
            const clock = document.getElementById('liveClock');
            const updateClock = () => { clock.textContent = new Date().toLocaleTimeString('uk-UA'); };
            updateClock();
            setInterval(updateClock, 1000);

            // 6. INTERSECTION OBSERVER FOR ANIMATIONS
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                    }
                });
            }, { threshold: 0.1 });

            document.querySelectorAll('.animate-on-scroll').forEach(el => observer.observe(el));

            // 7. CHART.JS INITIALIZATION
            const ctx = document.getElementById('courtStockChart').getContext('2d');
            
            const normalData = [210, 260, 329, 390, 440, 570, 573, 640, 710];
            const glitchData = [90, 520, 110, 840, 190, 990, 420, 210, 890];

            let accentColor = getComputedStyle(document.documentElement).getPropertyValue('--primary-accent').trim() || '#38bdf8';

            const courtChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Січень', 'Лютий', 'Березень', 'Квітень', 'Травень', 'Червень', 'Липень', 'Серпень (+)', 'Вересень (План)'],
                    datasets: [{
                        label: 'Успішно розглянуті справи',
                        data: normalData,
                        borderColor: accentColor,
                        borderWidth: 3,
                        pointBackgroundColor: '#ffffff',
                        pointBorderColor: accentColor,
                        pointBorderWidth: 2,
                        pointRadius: 5,
                        pointHoverRadius: 8,
                        fill: true,
                        backgroundColor: (context) => {
                            const chart = context.chart;
                            const {ctx, chartArea} = chart;
                            if (!chartArea) return null;
                            const gradient = ctx.createLinearGradient(0, chartArea.top, 0, chartArea.bottom);
                            gradient.addColorStop(0, accentColor + '66');
                            gradient.addColorStop(1, 'transparent');
                            return gradient;
                        },
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { labels: { color: '#f8fafc', font: { family: 'Plus Jakarta Sans' } } }
                    },
                    scales: {
                        x: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#94a3b8' } },
                        y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#94a3b8' } }
                    }
                }
            });

            // 8. SIMULATED SYSTEM GLITCH / UPDATE
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
                    courtChart.data.datasets[0].borderColor = getComputedStyle(document.documentElement).getPropertyValue('--primary-accent').trim();
                    courtChart.update();

                    statusPill.classList.remove('glitch-mode');
                    statusText.textContent = 'ЗБІЙ СИСТЕМИ ПРОЙШОВ — ТЕПЕР ВОНА СТАБІЛЬНА';
                }, 8000);
            }, 4000);

            // 9. MODAL & THEME CHANGING LOGIC
            const settingsModal = document.getElementById('settingsModal');
            document.getElementById('openSettingsBtn').addEventListener('click', () => settingsModal.classList.add('active'));
            document.getElementById('closeSettingsBtn').addEventListener('click', () => settingsModal.classList.remove('active'));

            document.querySelectorAll('[data-set-theme]').forEach(btn => {
                btn.addEventListener('click', function() {
                    const theme = this.getAttribute('data-set-theme');
                    if (theme === 'default') {
                        document.documentElement.removeAttribute('data-theme');
                    } else {
                        document.documentElement.setAttribute('data-theme', theme);
                    }
                    
                    // Update Chart Colors
                    setTimeout(() => {
                        const newAccent = getComputedStyle(document.documentElement).getPropertyValue('--primary-accent').trim();
                        courtChart.data.datasets[0].borderColor = newAccent;
                        courtChart.data.datasets[0].pointBorderColor = newAccent;
                        courtChart.update();
                    }, 100);
                });
            });
        });
    </script>
</body>
</html>

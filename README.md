```html
<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Офіційний Портал Судової Системи — Ukraine RP</title>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        *,
        *::before,
        *::after {
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
            --accent-glow: rgba(14, 165, 233, 0.45);
            --accent-purple: #818cf8;

            --text-main: #f8fafc;
            --text-muted: #94a3b8;

            --success-color: #22c55e;
            --warning-color: #f59e0b;

            --transition-speed: 0.4s;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background:
                radial-gradient(
                    circle at 50% 0%,
                    #0c1836 0%,
                    #020617 70%
                );
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.7;
            padding: 30px;
            overflow-x: hidden;
            min-height: 100vh;
            position: relative;
        }

        body::before {
            content: "";
            position: fixed;
            top: -200px;
            left: -200px;
            width: 600px;
            height: 600px;
            background: radial-gradient(
                circle,
                rgba(14, 165, 233, 0.18) 0%,
                transparent 70%
            );
            filter: blur(80px);
            border-radius: 50%;
            z-index: -1;
            animation: floatGlow1 12s ease-in-out infinite alternate;
            pointer-events: none;
        }

        body::after {
            content: "";
            position: fixed;
            bottom: -200px;
            right: -200px;
            width: 600px;
            height: 600px;
            background: radial-gradient(
                circle,
                rgba(129, 140, 248, 0.15) 0%,
                transparent 70%
            );
            filter: blur(90px);
            border-radius: 50%;
            z-index: -1;
            animation: floatGlow2 15s ease-in-out infinite alternate-reverse;
            pointer-events: none;
        }

        @keyframes floatGlow1 {
            0% {
                transform: translate(0, 0) scale(1);
                opacity: 0.7;
            }

            100% {
                transform: translate(100px, 80px) scale(1.3);
                opacity: 1;
            }
        }

        @keyframes floatGlow2 {
            0% {
                transform: translate(0, 0) scale(1);
                opacity: 0.7;
            }

            100% {
                transform: translate(-120px, -90px) scale(1.25);
                opacity: 1;
            }
        }

        .main-container {
            max-width: 1300px;
            margin: 0 auto;
        }

        .animate-on-scroll {
            opacity: 0;
            transform: translateY(40px);
            transition:
                opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
                transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .portal-header {
            background:
                linear-gradient(
                    135deg,
                    rgba(9, 15, 29, 0.92) 0%,
                    rgba(18, 30, 60, 0.92) 100%
                );
            backdrop-filter: blur(16px);
            border: 1px solid rgba(56, 189, 248, 0.3);
            border-bottom: 5px solid var(--accent-blue);
            padding: 40px 25px;
            text-align: center;
            border-radius: 24px;
            margin-bottom: 35px;
            box-shadow:
                0 20px 50px rgba(0, 0, 0, 0.75),
                0 0 30px rgba(14, 165, 233, 0.15),
                inset 0 1px 0 rgba(255, 255, 255, 0.1);
        }

        .portal-header h1 {
            font-size: clamp(1.8rem, 3.5vw, 2.6rem);
            background:
                linear-gradient(
                    135deg,
                    #38bdf8 0%,
                    #ffffff 50%,
                    #818cf8 100%
                );
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 12px;
            filter: drop-shadow(0 0 20px rgba(56, 189, 248, 0.4));
        }

        .portal-header p {
            color: var(--text-muted);
            font-size: 1.1rem;
            max-width: 850px;
            margin: 0 auto;
        }

        .hero-info-box {
            background:
                linear-gradient(
                    135deg,
                    rgba(11, 20, 45, 0.95) 0%,
                    rgba(20, 28, 79, 0.95) 100%
                );
            backdrop-filter: blur(16px);
            border: 2px solid var(--accent-blue);
            border-radius: 26px;
            padding: 45px 35px;
            margin-bottom: 35px;
            text-align: center;
            box-shadow:
                0 0 60px rgba(14, 165, 233, 0.3),
                inset 0 0 30px rgba(56, 189, 248, 0.15);
        }

        .hero-info-box h2 {
            font-size: clamp(2.2rem, 5vw, 3.6rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 3px;
            background:
                linear-gradient(
                    135deg,
                    #38bdf8 0%,
                    #818cf8 50%,
                    #c084fc 100%
                );
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 18px;
            filter: drop-shadow(0 0 30px rgba(56, 189, 248, 0.6));
        }

        .hero-info-box p {
            color: #cbd5e1;
            font-size: 1.18rem;
            max-width: 950px;
            margin: 0 auto 15px;
            line-height: 1.8;
        }

        .content-section {
            background:
                linear-gradient(
                    135deg,
                    rgba(13, 21, 39, 0.92) 0%,
                    rgba(7, 12, 24, 0.92) 100%
                );
            backdrop-filter: blur(16px);
            border: 1px solid rgba(30, 41, 59, 0.8);
            border-radius: 24px;
            padding: 40px;
            margin-bottom: 35px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.65);
            position: relative;
            overflow: hidden;
        }

        .section-title {
            color: var(--accent-blue);
            font-size: 1.75rem;
            margin-bottom: 15px;
            border-bottom: 2px solid var(--border-primary);
            padding-bottom: 12px;
            display: inline-block;
            text-shadow: 0 0 15px rgba(14, 165, 233, 0.3);
        }

        .section-description {
            color: var(--text-muted);
            font-size: 1.02rem;
            margin-bottom: 25px;
        }

        /* Біржа та активність */

        .stock-metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .stock-metric-card {
            background:
                linear-gradient(
                    135deg,
                    #101c3d 0%,
                    #070d1f 100%
                );
            border: 1px solid rgba(56, 189, 248, 0.3);
            border-radius: 18px;
            padding: 22px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            transition:
                transform 0.3s ease,
                border-color 0.3s ease,
                box-shadow 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stock-metric-card:hover {
            transform: translateY(-5px);
            border-color: var(--accent-blue);
            box-shadow: 0 15px 35px rgba(14, 165, 233, 0.35);
        }

        .stock-metric-title {
            font-size: 0.9rem;
            color: var(--text-muted);
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .stock-metric-value {
            font-size: 1.8rem;
            font-weight: 800;
            color: #ffffff;
            margin-bottom: 6px;
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
        }

        .stock-metric-badge {
            display: inline-flex;
            align-items: center;
            gap: 4px;
            font-size: 0.85rem;
            font-weight: 700;
            padding: 4px 10px;
            border-radius: 20px;
        }

        .stock-badge-positive {
            background: rgba(34, 197, 94, 0.15);
            color: var(--success-color);
            border: 1px solid rgba(34, 197, 94, 0.3);
            text-shadow: 0 0 10px rgba(34, 197, 94, 0.4);
        }

        .chart-box-wrapper {
            position: relative;
            width: 100%;
            height: 480px;
            background:
                linear-gradient(
                    135deg,
                    #070d1f 0%,
                    #030612 100%
                );
            padding: 25px;
            border-radius: 20px;
            border: 1px solid rgba(56, 189, 248, 0.3);
            box-shadow:
                inset 0 0 35px rgba(0, 0, 0, 0.8),
                0 0 40px rgba(14, 165, 233, 0.15);
        }

        /* Випадаючі списки */

        .dropdown-element {
            margin-top: 16px;
        }

        .dropdown-toggle-btn {
            background:
                linear-gradient(
                    135deg,
                    #131d38 0%,
                    #0a1124 100%
                );
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
            transition: all var(--transition-speed);
        }

        .dropdown-toggle-btn:hover {
            background:
                linear-gradient(
                    135deg,
                    #1c2d56 0%,
                    #111a35 100%
                );
            border-color: var(--accent-blue);
            transform: translateY(-2px);
        }

        .dropdown-panel {
            max-height: 0;
            overflow: hidden;
            transition:
                max-height 0.45s cubic-bezier(0.4, 0, 0.2, 1),
                padding 0.3s ease;
            background-color: var(--bg-secondary);
            border-radius: 0 0 16px 16px;
            padding: 0 24px;
            border: 1px solid transparent;
        }

        .dropdown-panel.expanded {
            max-height: 1500px;
            padding: 24px;
            margin-top: 4px;
            border-color: rgba(56, 189, 248, 0.2);
        }

        .dropdown-panel p,
        .dropdown-panel ul {
            color: #d1d5db;
            font-size: 0.98rem;
            margin-bottom: 12px;
        }

        .dropdown-panel ul {
            padding-left: 22px;
        }

        .dropdown-panel li {
            margin-bottom: 8px;
        }

        .dropdown-panel code {
            color: #38bdf8;
            background: rgba(56, 189, 248, 0.1);
            padding: 2px 6px;
            border-radius: 5px;
        }

        .notice-box {
            background: rgba(14, 165, 233, 0.12);
            border-left: 4px solid var(--accent-blue);
            padding: 16px;
            margin-top: 18px;
            border-radius: 0 12px 12px 0;
            font-size: 0.95rem;
            color: #ffffff;
        }

        /* Працівники */

        .staff-grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
            gap: 24px;
            margin-top: 25px;
        }

        .staff-profile-card {
            background:
                linear-gradient(
                    135deg,
                    #131e3b 0%,
                    #080f24 100%
                );
            border: 1px solid var(--border-primary);
            padding: 35px 22px;
            border-radius: 20px;
            text-align: center;
            transition:
                transform 0.4s ease,
                border-color 0.4s ease,
                box-shadow 0.4s ease;
            position: relative;
            overflow: hidden;
        }

        .staff-profile-card::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: var(--accent-blue);
        }

        .staff-profile-card:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: var(--accent-blue);
            box-shadow: 0 20px 45px rgba(14, 165, 233, 0.4);
        }

        .staff-avatar-wrapper {
            width: 105px;
            height: 105px;
            margin: 0 auto 20px;
            position: relative;
            border-radius: 50%;
            padding: 3px;
            background:
                linear-gradient(
                    135deg,
                    var(--accent-blue),
                    var(--accent-purple)
                );
        }

        .staff-avatar-wrapper img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 50%;
            border: 3px solid var(--bg-card);
            display: block;
        }

        .avatar-fallback {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background: #0f172a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.4rem;
            border: 3px solid var(--bg-card);
            color: var(--accent-blue);
        }

        .staff-profile-card h3 {
            font-size: 1.35rem;
            margin-bottom: 8px;
            color: var(--text-main);
        }

        .staff-role-badge {
            color: var(--accent-blue);
            font-size: 0.8rem;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 16px;
            display: inline-block;
            background: rgba(14, 165, 233, 0.15);
            padding: 6px 16px;
            border-radius: 20px;
            border: 1px solid rgba(14, 165, 233, 0.3);
        }

        .staff-contacts-info {
            font-size: 0.95rem;
            color: var(--text-muted);
            word-break: break-word;
        }

        .staff-contacts-info a {
            color: var(--accent-blue);
            text-decoration: none;
            font-weight: 600;
        }

        .staff-contacts-info a:hover {
            color: var(--accent-blue-hover);
            text-decoration: underline;
        }

        /* Таблиця */

        .table-box-wrapper {
            width: 100%;
            overflow-x: auto;
            margin-top: 25px;
            border-radius: 20px;
            border: 1px solid var(--border-primary);
            background-color: var(--bg-secondary);
        }

        .analytics-table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
            font-size: 0.98rem;
            white-space: nowrap;
        }

        .analytics-table th,
        .analytics-table td {
            padding: 18px 22px;
            border-bottom: 1px solid var(--border-primary);
            color: #f8fafc !important;
        }

        .analytics-table th {
            background-color: #111d38 !important;
            color: var(--accent-blue) !important;
            font-weight: 600;
            text-transform: uppercase;
            font-size: 0.82rem;
            letter-spacing: 1px;
        }

        .analytics-table tbody tr {
            background-color: #070d1b !important;
            transition: background-color 0.25s ease;
        }

        .analytics-table tbody tr:nth-child(even) {
            background-color: #0a1226 !important;
        }

        .analytics-table tbody tr:hover {
            background-color: rgba(14, 165, 233, 0.2) !important;
        }

        .status-up {
            color: var(--success-color);
            font-weight: bold;
        }

        .status-stable {
            color: var(--accent-blue);
            font-weight: bold;
        }

        /* Івент */

        .event-detailed-card {
            background:
                linear-gradient(
                    135deg,
                    rgba(14, 165, 233, 0.15),
                    rgba(13, 21, 39, 0.98)
                );
            border: 1px solid var(--accent-blue);
            border-radius: 20px;
            padding: 32px;
            margin-top: 30px;
            box-shadow: 0 0 40px rgba(14, 165, 233, 0.3);
        }

        .event-detailed-card h3 {
            color: var(--accent-blue);
            font-size: 1.5rem;
            margin-bottom: 14px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .event-detailed-card p {
            color: #d1d5db;
            font-size: 1rem;
            margin-bottom: 16px;
            line-height: 1.7;
        }

        .event-benefits-list {
            list-style-type: none;
            padding-left: 0;
            margin-bottom: 22px;
        }

        .event-benefits-list li {
            position: relative;
            padding-left: 26px;
            margin-bottom: 10px;
            color: #e2e8f0;
            font-size: 0.98rem;
        }

        .event-benefits-list li::before {
            content: "✔";
            position: absolute;
            left: 0;
            color: var(--success-color);
            font-weight: bold;
        }

        .event-schedule-container {
            display: flex;
            gap: 14px;
            flex-wrap: wrap;
            margin-top: 18px;
            border-top: 1px solid var(--border-primary);
            padding-top: 18px;
        }

        .schedule-badge {
            background: #111d38;
            border: 1px solid var(--accent-blue);
            color: #ffffff;
            padding: 12px 20px;
            border-radius: 14px;
            font-weight: bold;
            font-size: 1.02rem;
        }

        /* Новини */

        .owner-news-branch {
            background:
                linear-gradient(
                    135deg,
                    #0d1527 0%,
                    #070d1c 100%
                );
            border: 1px dashed var(--accent-blue);
            border-radius: 20px;
            padding: 32px;
            margin-top: 35px;
        }

        .owner-news-branch h3 {
            color: var(--accent-blue);
            font-size: 1.35rem;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .owner-news-branch p {
            color: var(--text-muted);
            font-size: 0.98rem;
            margin-bottom: 12px;
            line-height: 1.7;
        }

        /* Footer */

        .portal-footer {
            text-align: center;
            padding: 30px 20px;
            background:
                linear-gradient(
                    135deg,
                    #0d1527 0%,
                    #070c1a 100%
                );
            border: 1px solid var(--border-primary);
            border-radius: 20px;
            color: var(--text-muted);
            font-size: 0.95rem;
            margin-top: 35px;
        }

        /* Адаптивність */

        @media (max-width: 768px) {
            body {
                padding: 15px;
            }

            .portal-header {
                padding: 30px 20px;
                border-radius: 18px;
            }

            .hero-info-box {
                padding: 35px 20px;
                border-radius: 20px;
            }

            .hero-info-box p {
                font-size: 1rem;
            }

            .content-section {
                padding: 25px 18px;
                border-radius: 18px;
            }

            .chart-box-wrapper {
                height: 360px;
                padding: 15px;
            }

            .staff-grid-container {
                grid-template-columns: 1fr;
            }

            .event-detailed-card,
            .owner-news-branch {
                padding: 24px 18px;
            }

            .analytics-table {
                font-size: 0.85rem;
            }

            .analytics-table th,
            .analytics-table td {
                padding: 13px 15px;
            }
        }

        @media (max-width: 480px) {
            body {
                padding: 10px;
            }

            .portal-header h1 {
                font-size: 1.5rem;
            }

            .hero-info-box h2 {
                font-size: 2rem;
                letter-spacing: 1px;
            }

            .section-title {
                font-size: 1.35rem;
            }

            .dropdown-toggle-btn {
                padding: 15px;
                font-size: 0.95rem;
            }

            .chart-box-wrapper {
                height: 300px;
                padding: 10px;
            }
        }
    </style>
</head>

<body>

    <div class="main-container">

        <!-- Header -->

        <header class="portal-header animate-on-scroll">
            <h1>🏛️ Офіційний Портал Судової Системи Ukraine RP</h1>

            <p>
                Централізований державний реєстр судових проваджень,
                регламентів, звітності та керівного складу колегії
            </p>
        </header>

        <!-- Hero -->

        <div class="hero-info-box animate-on-scroll">
            <h2>⚖️ СУД ІНФО UKRAINE RP ⚖️</h2>

            <p>
                Головний інформаційний центр судової системи!
                Тут зібрані всі офіційні правила дотримання законів,
                регламенти захисту прав громадян, розклад засідань
                та інструкції з взаємодії з державними органами
                на нашому сервері.
            </p>

            <p>
                Наша мета — забезпечити максимальну прозорість,
                справедливість та високий рівень рольової гри (RP)
                для кожного гравця Ukraine RP.
            </p>
        </div>

        <!-- Chart -->

        <section class="content-section animate-on-scroll">

            <h2 class="section-title">
                📈 Біржа Активності та Статистика Суду
            </h2>

            <p class="section-description">
                Розширена аналітика, показники продуктивності колегії
                та інтерактивна динаміка розгляду позовів:
            </p>

            <div class="chart-box-wrapper">
                <canvas id="courtStockChart"></canvas>
            </div>

        </section>

        <!-- Rules -->

        <section class="content-section animate-on-scroll">

            <h2 class="section-title">
                ⚖️ Нормативно-правова база та Правила Сервера
            </h2>

            <p class="section-description">
                Детальні інструкції щодо поведінки, етики,
                законності дій та розширені регламенти:
            </p>

            <!-- Dropdown 1 -->

            <div class="dropdown-element">

                <button class="dropdown-toggle-btn" type="button">
                    <span>
                        📜 Загальна етика та правила поведінки в суді
                    </span>

                    <span class="dropdown-arrow">▼</span>
                </button>

                <div class="dropdown-panel">

                    <p>
                        <strong>
                            Головні норми поведінки для учасників
                            та гостей засідання:
                        </strong>
                    </p>

                    <ul>
                        <li>
                            <strong>Форма звернення:</strong>
                            До судді слід звертатися виключно офіційно
                            та шанобливо — «Ваша Честь» або
                            «Шановний Судде».
                        </li>

                        <li>
                            <strong>Порядок у залі:</strong>
                            Заборонено перебивати виступи інших сторін,
                            викрикувати, провокувати конфлікти або вести
                            себе деструктивно.
                        </li>

                        <li>
                            <strong>Рольова взаємодія:</strong>
                            Усі аргументи повинні подаватися виключно
                            через якісні RP-описи та докази
                            (фрапси, скріншоти, свідчення очевидців).
                        </li>
                    </ul>

                    <div class="notice-box">
                        <strong>⚠️ Важливо:</strong>
                        Порушення регламенту розглядається як неувага
                        до суду та карається сервером або видаленням
                        із зали засідань.
                    </div>

                </div>

            </div>

            <!-- Dropdown 2 -->

            <div class="dropdown-element">

                <button class="dropdown-toggle-btn" type="button">
                    <span>
                        🛡️ Правила обшуку та законність дій держструктур
                    </span>

                    <span class="dropdown-arrow">▼</span>
                </button>

                <div class="dropdown-panel">

                    <p>
                        <strong>
                            Стандарти проведення процесуальних дій:
                        </strong>
                    </p>

                    <ul>
                        <li>
                            Обшук або затримання вважаються легітимними
                            лише за наявності вагомої RP-підстави
                            та правильного відігравання через команди
                            <code>/me</code> та <code>/do</code>.
                        </li>

                        <li>
                            Будь-які докази, зібрані з порушенням
                            серверних правил або чинного законодавства,
                            визнаються судом недійсними.
                        </li>

                        <li>
                            Кожен громадянин має право на виклик адвоката
                            та оскарження неправомірних дій
                            у судовому порядку.
                        </li>
                    </ul>

                </div>

            </div>

            <!-- Dropdown 3 -->

            <div class="dropdown-element">

                <button class="dropdown-toggle-btn" type="button">
                    <span>
                        ⚖️ Новий регламент: Порядок подачі та розгляду апеляцій
                    </span>

                    <span class="dropdown-arrow">▼</span>
                </button>

                <div class="dropdown-panel">

                    <p>
                        <strong>
                            Додаткові логічні правила оскарження рішень:
                        </strong>
                    </p>

                    <ul>
                        <li>
                            <strong>Строки подачі:</strong>
                            Громадянин або державна структура має право
                            подати апеляційну скаргу протягом 48 годин
                            з моменту оголошення попереднього рішення суду.
                        </li>

                        <li>
                            <strong>Пакет документів:</strong>
                            До апеляції обов'язково додається повний
                            відеозахист (фрапс) засідання або копія
                            попереднього протоколу без замальовок
                            чи монтажу.
                        </li>

                        <li>
                            <strong>Склад апеляційної колегії:</strong>
                            Розгляд скарги проводиться спеціальною
                            колегією з двох або більше суддів
                            вищої кваліфікації.
                        </li>
                    </ul>

                    <div class="notice-box">
                        <strong>📌 Примітка:</strong>
                        Подання свідомо фальшивих доказів під час
                        апеляції тягне за собою відповідальність
                        відповідно до правил сервера.
                    </div>

                </div>

            </div>

            <!-- Dropdown 4 -->

            <div class="dropdown-element">

                <button class="dropdown-toggle-btn" type="button">
                    <span>
                        🛡️ Новий регламент: Етика та професійні обов'язки адвокатури
                    </span>

                    <span class="dropdown-arrow">▼</span>
                </button>

                <div class="dropdown-panel">

                    <p>
                        <strong>
                            Стандарти для представників захисту:
                        </strong>
                    </p>

                    <ul>
                        <li>
                            <strong>Конфіденційність:</strong>
                            Адвокат зобов'язаний зберігати повну таємницю
                            довіри зі своїм клієнтом під час підготовки
                            до судового процесу.
                        </li>

                        <li>
                            <strong>Підготовка лінії захисту:</strong>
                            Представник повинен надати аргументовані
                            докази невинуватості або пом'якшення вироку
                            за 10 хвилин до початку відкриття
                            судового засідання.
                        </li>

                        <li>
                            <strong>Коректність у спілкуванні:</strong>
                            Заборонено використовувати ненормативну
                            лексику чи тиснути на свідків під час
                            перехресного допиту.
                        </li>
                    </ul>

                </div>

            </div>

            <!-- Dropdown 5 -->

            <div class="dropdown-element">

                <button class="dropdown-toggle-btn" type="button">
                    <span>
                        🤖 Про офіційний Судовий Бот Ukraine RP
                    </span>

                    <span class="dropdown-arrow">▼</span>
                </button>

                <div class="dropdown-panel">

                    <p>
                        Наш інтегрований судовий бот створений
                        для автоматизації подачі позовів, перевірки
                        статусів справ та оперативної комунікації
                        з громадянами.
                    </p>

                    <p>
                        <strong>Основні можливості бота:</strong>
                    </p>

                    <ul>
                        <li>
                            Миттєва подача електронної заяви до суду.
                        </li>

                        <li>
                            Сповіщення про дати та час
                            призначених засідань.
                        </li>

                        <li>
                            Швидкий доступ до контактів суддів
                            та адвокатів.
                        </li>
                    </ul>

                </div>

            </div>

        </section>

        <!-- Staff -->

        <section class="content-section animate-on-scroll">

            <h2 class="section-title">
                🏛️ Колектив суду та Адвокатура
            </h2>

            <p class="section-description">
                Офіційний кадровий склад керівництва,
                суддівської колегії, стажерів та представників захисту:
            </p>

            <div class="staff-grid-container">

                <!-- 1 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="Arseniy_zabanen"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '⚖️' }))"
                        >
                    </div>

                    <h3>Arseniy_zabanen</h3>

                    <div class="staff-role-badge">
                        Головний Суддя (ГС)
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: Arseniy_zabanen<br>
                        TG:
                        <a
                            href="https://t.me/Samyry228"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @Samyry228
                        </a>
                    </div>

                </div>

                <!-- 2 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="mummu228kuku"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '🛡️' }))"
                        >
                    </div>

                    <h3>mummu228kuku</h3>

                    <div class="staff-role-badge">
                        Заступник
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: mummu228kuku<br>
                        TG:
                        <a
                            href="https://t.me/here_everyone"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @here_everyone
                        </a>
                    </div>

                </div>

                <!-- 3 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="svervanchick"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '📜' }))"
                        >
                    </div>

                    <h3>svervanchick</h3>

                    <div class="staff-role-badge">
                        Суддя
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: svervanchick<br>
                        TG:
                        <a
                            href="https://t.me/Svervanchik"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @Svervanchik
                        </a>
                    </div>

                </div>

                <!-- 4 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="Huhaidjopy"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '🏛️' }))"
                        >
                    </div>

                    <h3>Huhaidjopy</h3>

                    <div class="staff-role-badge">
                        Суддя
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: Huhaidjopy<br>
                        TG:
                        <a
                            href="https://t.me/bewewewewewe"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @bewewewewewe
                        </a>
                    </div>

                </div>

                <!-- 5 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="Mr_Zver3000"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '⚡' }))"
                        >
                    </div>

                    <h3>Mr_Zver3000</h3>

                    <div class="staff-role-badge">
                        Суддя
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: Mr_Zver3000<br>
                        TG:
                        <a
                            href="https://t.me/GreyFild_OFF"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @GreyFild_OFF
                        </a>
                    </div>

                </div>

                <!-- 6 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="Zaj_zuda3"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '💼' }))"
                        >
                    </div>

                    <h3>Zaj_zuda3</h3>

                    <div class="staff-role-badge">
                        Адвокат
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: Zaj_zuda3<br>
                        TG:
                        <a
                            href="https://t.me/Dz7xj"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @Dz7xj
                        </a>
                    </div>

                </div>

                <!-- 7 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="heehrhrhl18"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '🔍' }))"
                        >
                    </div>

                    <h3>heehrhrhl18</h3>

                    <div class="staff-role-badge">
                        Стажер-суддя
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: heehrhrhl18<br>
                        TG:
                        <a
                            href="https://t.me/hehr18_UR"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @hehr18_UR
                        </a>
                    </div>

                </div>

                <!-- 8 -->

                <div class="staff-profile-card">

                    <div class="staff-avatar-wrapper">
                        <img
                            src="https://via.placeholder.com/150"
                            alt="Itz_raose"
                            onerror="this.replaceWith(Object.assign(document.createElement('div'), { className: 'avatar-fallback', innerText: '🔍' }))"
                        >
                    </div>

                    <h3>Itz_raose</h3>

                    <div class="staff-role-badge">
                        Стажер-суддя
                    </div>

                    <div class="staff-contacts-info">
                        Roblox: Itz_raose<br>
                        TG:
                        <a
                            href="https://t.me/ob1zyan"
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            @ob1zyan
                        </a>
                    </div>

                </div>

            </div>

        </section>

        <!-- Statistics -->

        <section class="content-section animate-on-scroll">

            <h2 class="section-title">
                📊 Детальна архівна таблиця звітів та порушень
            </h2>

            <p class="section-description">
                У звітах нижче зібрано статистику розгляду справ,
                аналіз порушень серверних регламентів та ефективність
                роботи колегії:
            </p>

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
                            <td>
                                <strong>4 липня – 3 серпня 2026</strong>
                            </td>

                            <td>
                                <span class="status-up">
                                    573 справи
                                </span>
                            </td>

                            <td>
                                9 інцидентів (Пункт 16)
                            </td>

                            <td>
                                <span class="status-up">
                                    ⚡ Штатний режим
                                </span>
                            </td>

                            <td>
                                Оброблено 161 звіт (502 години роботи).
                            </td>
                        </tr>

                        <tr>
                            <td>
                                <strong>Червень – Липень 2026</strong>
                            </td>

                            <td>
                                <span class="status-up">
                                    570 справ
                                </span>
                            </td>

                            <td>
                                38 інцидентів
                            </td>

                            <td>
                                <span class="status-up">
                                    🚀 Пік активності
                                </span>
                            </td>

                            <td>
                                Максимальна продуктивність колегії.
                            </td>
                        </tr>

                        <tr>
                            <td>
                                <strong>Травень – Червень 2026</strong>
                            </td>

                            <td>
                                310 справ
                            </td>

                            <td>
                                21 інцидент
                            </td>

                            <td>
                                <span class="status-stable">
                                    ⚖️ Стабільний режим
                                </span>
                            </td>

                            <td>
                                Якісне виконання регламентів.
                            </td>
                        </tr>

                        <tr>
                            <td>
                                <strong>Січень – Лютий 2026</strong>
                            </td>

                            <td>
                                329 засідань
                            </td>

                            <td>
                                29 інцидентів
                            </td>

                            <td>
                                <span class="status-stable">
                                    🤖 Цифровізація
                                </span>
                            </td>

                            <td>
                                Запуск інформаційного бота.
                            </td>
                        </tr>

                        <tr>
                            <td>
                                <strong>Грудень 2025 – Січень 2026</strong>
                            </td>

                            <td>
                                <span class="status-up">
                                    657 справ
                                </span>
                            </td>

                            <td>
                                52 інциденти
                            </td>

                            <td>
                                <span class="status-up">
                                    ⚡ Рекорд
                                </span>
                            </td>

                            <td>
                                Найвище навантаження в історії.
                            </td>
                        </tr>

                    </tbody>

                </table>

            </div>

            <!-- Event -->

            <div class="event-detailed-card">

                <h3>
                    🏛️ Івент: День Відкритих Дверей Суду
                </h3>

                <p>
                    <strong>Чому цей івент корисний для гравців?</strong>
                    День відкритих дверей — це унікальна можливість
                    зазирнути за лаштунки судової системи, зрозуміти
                    свої права та навчитися грамотно захищати себе
                    в рольових ситуаціях без порушення правил сервера.
                </p>

                <p>
                    <strong>Переваги участі:</strong>
                </p>

                <ul class="event-benefits-list">

                    <li>
                        Живе спілкування з досвідченими суддями
                        та адвокатами.
                    </li>

                    <li>
                        Розбір реальних кейсів та процесуальних помилок.
                    </li>

                    <li>
                        Унікальний ігровий досвід та гарний настрій.
                    </li>

                </ul>

                <p>
                    <strong>Графік проведення івенту:</strong>
                </p>

                <div class="event-schedule-container">

                    <span class="schedule-badge">
                        📅 09 число місяця
                    </span>

                    <span class="schedule-badge">
                        📅 17 число місяця
                    </span>

                    <span class="schedule-badge">
                        📅 29 число місяця
                    </span>

                </div>

            </div>

            <!-- News -->

            <div class="owner-news-branch">

                <h3>
                    📢 Новини та оновлення від керівництва суду
                </h3>

                <p>
                    У цій гілці суд та власник сайту публікують актуальні
                    внутрішні новини, майбутні оновлення судової системи,
                    а також корисні поради щодо покращення рольової гри
                    на сервері.
                </p>

                <p>
                    Слідкуйте за оновленнями порталу, щоб бути в курсі
                    найважливіших державних подій Ukraine RP!
                </p>

            </div>

        </section>

        <!-- Footer -->

        <footer class="portal-footer animate-on-scroll">

            <p>
                &copy; 2026 Офіційний Портал Судової Системи
                Ukraine RP. Усі права захищені.
            </p>

        </footer>

    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {

            /* Анімація блоків при прокручуванні */

            const observerOptions = {
                threshold: 0.1
            };

            const observer = new IntersectionObserver(
                function (entries, observerInstance) {

                    entries.forEach(function (entry) {

                        if (entry.isIntersecting) {

                            entry.target.classList.add("visible");

                            observerInstance.unobserve(entry.target);
                        }
                    });

                },
                observerOptions
            );

            document
                .querySelectorAll(".animate-on-scroll")
                .forEach(function (element) {

                    observer.observe(element);

                });


            /* Випадаючі блоки */

            const dropdownButtons =
                document.querySelectorAll(".dropdown-toggle-btn");

            dropdownButtons.forEach(function (button) {

                button.addEventListener("click", function () {

                    const panel = this.nextElementSibling;
                    const arrow = this.querySelector(".dropdown-arrow");

                    const isExpanded =
                        panel.classList.toggle("expanded");

                    arrow.textContent =
                        isExpanded ? "▲" : "▼";

                });

            });


            /* Графік */

            const canvas =
                document.getElementById("courtStockChart");

            if (!canvas) {
                return;
            }

            const ctx = canvas.getContext("2d");

            const chartGradient =
                ctx.createLinearGradient(0, 0, 0, 400);

            chartGradient.addColorStop(
                0,
                "rgba(14, 165, 233, 0.55)"
            );

            chartGradient.addColorStop(
                1,
                "rgba(14, 165, 233, 0)"
            );


            new Chart(ctx, {

                type: "line",

                data: {

                    labels: [
                        "Січень",
                        "Лютий",
                        "Березень",
                        "Квітень",
                        "Травень",
                        "Червень",
                        "Липень",
                        "Серпень (+)",
                        "Вересень (План)"
                    ],

                    datasets: [

                        {
                            label:
                                "Динаміка успішно розглянутих справ",

                            data: [
                                210,
                                260,
                                329,
                                390,
                                440,
                                570,
                                573,
                                640,
                                710
                            ],

                            borderColor: "#38bdf8",

                            borderWidth: 4,

                            pointBackgroundColor: "#818cf8",

                            pointBorderColor: "#ffffff",

                            pointBorderWidth: 2,

                            pointRadius: 6,

                            pointHoverRadius: 9,

                            backgroundColor: chartGradient,

                            fill: true,

                            tension: 0.4
                        }

                    ]

                },

                options: {

                    responsive: true,

                    maintainAspectRatio: false,

                    animation: {

                        duration: 2500,

                        easing: "easeOutQuart"
                    },

                    plugins: {

                        legend: {

                            labels: {

                                color: "#f8fafc",

                                font: {
                                    size: 13,
                                    family:
                                        "'Segoe UI', Roboto, sans-serif"
                                }

                            }

                        },

                        tooltip: {

                            backgroundColor:
                                "rgba(11, 19, 41, 0.95)",

                            titleColor: "#38bdf8",

                            bodyColor: "#f8fafc",

                            borderColor: "#38bdf8",

                            borderWidth: 1,

                            padding: 12
                        }

                    },

                    scales: {

                        x: {

                            grid: {
                                color:
                                    "rgba(30, 41, 59, 0.5)"
                            },

                            ticks: {

                                color: "#94a3b8",

                                font: {
                                    size: 12
                                }

                            }

                        },

                        y: {

                            beginAtZero: true,

                            grid: {
                                color:
                                    "rgba(30, 41, 59, 0.5)"
                            },

                            ticks: {

                                color: "#94a3b8",

                                font: {
                                    size: 12
                                }

                            }

                        }

                    }

                }

            });

        });
    </script>

</body>
</html>
```

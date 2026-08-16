<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Офіційний Портал Судової Системи — Ukraine RP v3.5</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        *, *::before, *::after {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        /* ЗМІННІ ТЕМ */
        :root {
            --bg-primary: #020617;
            --bg-secondary: #070d1f;
            --bg-card: #0b1329;
            --border-primary: #1e293b;
            --border-accent: #38bdf8;
            --accent-blue: #0ea5e9;
            --accent-purple: #818cf8;
            --accent-red: #ef4444;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --card-shadow: rgba(0, 0, 0, 0.4);
        }

        body.theme-light {
            --bg-primary: #f1f5f9;
            --bg-secondary: #ffffff;
            --bg-card: #f8fafc;
            --border-primary: #cbd5e1;
            --border-accent: #0284c7;
            --accent-blue: #0284c7;
            --accent-purple: #6366f1;
            --accent-red: #dc2626;
            --text-main: #0f172a;
            --text-muted: #475569;
            --card-shadow: rgba(0, 0, 0, 0.1);
        }

        body.theme-neon {
            --bg-primary: #050014;
            --bg-secondary: #0d0029;
            --bg-card: #180038;
            --border-primary: #ff007f;
            --border-accent: #00f0ff;
            --accent-blue: #00f0ff;
            --accent-purple: #bf00ff;
            --accent-red: #ff0055;
            --text-main: #ffffff;
            --text-muted: #d8b4fe;
            --card-shadow: rgba(0, 240, 255, 0.2);
        }

        body.theme-emerald {
            --bg-primary: #022c22;
            --bg-secondary: #064e3b;
            --bg-card: #065f46;
            --border-primary: #10b981;
            --border-accent: #34d399;
            --accent-blue: #10b981;
            --accent-purple: #059669;
            --accent-red: #f87171;
            --text-main: #ecfdf5;
            --text-muted: #a7f3d0;
            --card-shadow: rgba(16, 185, 129, 0.2);
        }

        html { scroll-behavior: smooth; }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: var(--bg-primary);
            color: var(--text-main);
            line-height: 1.7;
            padding: 30px;
            overflow-x: hidden;
            min-height: 100vh;
            transition: background 0.5s ease, color 0.5s ease;
        }

        /* ===== ЕКРАН ЗАВАНТАЖЕННЯ (10 СЕКУНД) ===== */
        #loader-overlay {
            position: fixed;
            top: 0; left: 0; width: 100vw; height: 100vh;
            background: #020617;
            z-index: 999999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            transition: opacity 0.8s ease, visibility 0.8s ease;
        }

        .loader-spinner {
            width: 90px; height: 90px;
            border: 6px solid rgba(56, 189, 248, 0.15);
            border-top: 6px solid var(--accent-blue);
            border-radius: 50%;
            animation: spin 1s linear infinite, glowPulse 2s ease-in-out infinite alternate;
            margin-bottom: 25px;
        }

        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        @keyframes glowPulse { 0% { box-shadow: 0 0 10px var(--accent-blue); } 100% { box-shadow: 0 0 30px var(--accent-blue); } }

        .loader-title {
            color: #fff; font-size: 1.6rem; font-weight: 700; letter-spacing: 2px; margin-bottom: 15px; text-align: center;
            animation: fadeInOut 1.5s infinite alternate;
        }

        @keyframes fadeInOut { 0% { opacity: 0.6; } 100% { opacity: 1; } }

        .loader-bar-bg {
            width: 320px; height: 12px; background: #0f172a; border-radius: 10px; overflow: hidden; border: 1px solid var(--border-accent);
        }

        .loader-bar-fill {
            width: 0%; height: 100%;
            background: linear-gradient(90deg, var(--accent-blue), var(--accent-purple));
            transition: width 0.1s linear;
        }

        .loader-timer { margin-top: 12px; color: var(--text-muted); font-size: 0.95rem; font-weight: 600; }

        /* ===== СКРОЛ ТА НАВІГАЦІЯ ===== */
        .scroll-progress {
            position: fixed; top: 0; left: 0; width: 0; height: 4px;
            background: linear-gradient(90deg, var(--accent-blue), var(--accent-purple));
            box-shadow: 0 0 16px var(--accent-blue); z-index: 99999;
        }

        .quick-nav {
            position: fixed; right: 20px; bottom: 20px; display: flex; flex-direction: column; gap: 10px; z-index: 9999;
        }

        .quick-nav button {
            width: 48px; height: 48px; border-radius: 14px; border: 1px solid var(--border-accent);
            background: var(--bg-secondary); color: var(--text-main); cursor: pointer;
            backdrop-filter: blur(14px); transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            font-size: 1.2rem;
        }

        .quick-nav button:hover { transform: translateY(-5px) scale(1.1); border-color: var(--accent-blue); box-shadow: 0 10px 20px var(--card-shadow); }

        .main-container { max-width: 1300px; margin: 0 auto; }

        /* ===== АНІМАЦІЇ ПОЯВИ ТА КАРТОК ===== */
        .animate-on-scroll {
            opacity: 0;
            transform: translateY(40px) scale(0.98);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0) scale(1);
        }

        .settings-box {
            background: var(--bg-card); border: 1px solid var(--border-accent); border-radius: 20px;
            padding: 25px; margin-bottom: 35px; box-shadow: 0 10px 30px var(--card-shadow);
            display: flex; flex-wrap: wrap; gap: 20px; align-items: center; justify-content: space-between;
            transition: transform 0.3s ease;
        }

        .settings-box:hover { transform: translateY(-3px); }

        .theme-btn {
            padding: 10px 18px; border-radius: 12px; border: 1px solid var(--border-primary);
            background: var(--bg-secondary); color: var(--text-main); cursor: pointer; font-weight: 600;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .theme-btn:hover, .theme-btn.active {
            border-color: var(--accent-blue); background: var(--accent-blue); color: #fff;
            transform: scale(1.05); box-shadow: 0 0 15px var(--accent-blue);
        }

        .portal-header {
            background: var(--bg-secondary); border: 1px solid var(--border-primary); border-bottom: 5px solid var(--accent-blue);
            padding: 45px 25px; text-align: center; border-radius: 24px; margin-bottom: 35px; box-shadow: 0 20px 50px var(--card-shadow);
            position: relative; overflow: hidden;
        }

        .portal-header h1 {
            font-size: clamp(1.8rem, 3.5vw, 2.6rem); color: var(--accent-blue); text-transform: uppercase; letter-spacing: 2px; margin-bottom: 12px;
            animation: pulseHeader 3s infinite alternate;
        }

        @keyframes pulseHeader {
            0% { transform: scale(1); filter: drop-shadow(0 0 2px var(--accent-blue)); }
            100% { transform: scale(1.01); filter: drop-shadow(0 0 15px var(--accent-blue)); }
        }

        .hero-info-box {
            background: var(--bg-card); border: 2px solid var(--accent-blue); border-radius: 26px;
            padding: 45px 35px; margin-bottom: 35px; text-align: center; box-shadow: 0 0 30px rgba(14, 165, 233, 0.15);
            transition: all 0.4s ease;
        }

        .hero-info-box:hover { transform: translateY(-5px); box-shadow: 0 0 50px rgba(14, 165, 233, 0.3); }

        .content-section {
            background: var(--bg-secondary); border: 1px solid var(--border-primary); border-radius: 24px;
            padding: 40px; margin-bottom: 35px; box-shadow: 0 20px 40px var(--card-shadow); transition: border-color 0.3s ease;
        }

        .content-section:hover { border-color: var(--border-accent); }

        .section-title {
            color: var(--accent-blue); font-size: 1.75rem; margin-bottom: 15px; border-bottom: 2px solid var(--border-primary);
            padding-bottom: 12px; display: inline-block; position: relative;
        }

        .section-title::after {
            content: ''; position: absolute; bottom: -2px; left: 0; width: 50%; height: 2px; background: var(--accent-blue);
            transition: width 0.4s ease;
        }

        .content-section:hover .section-title::after { width: 100%; }

        /* ===== ТАБЛО ЗАСІДАНЬ ТА АНІМАЦІЇ ===== */
        .schedule-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }

        .schedule-card {
            background: var(--bg-card); border: 1px solid var(--border-primary); border-left: 4px solid var(--accent-blue);
            border-radius: 16px; padding: 22px; transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .schedule-card:hover { transform: translateY(-8px) rotateX(4deg); box-shadow: 0 15px 30px var(--card-shadow); border-color: var(--accent-blue); }

        /* ===== СПИСКИ ТА ДРОПДАУНИ ===== */
        .dropdown-element { margin-top: 16px; }

        .dropdown-toggle-btn {
            background: var(--bg-card); color: var(--text-main); cursor: pointer; padding: 20px 24px; width: 100%;
            border: 1px solid var(--border-primary); text-align: left; font-size: 1.1rem; font-weight: 600;
            border-radius: 16px; display: flex; justify-content: space-between; align-items: center;
            transition: all 0.3s ease;
        }

        .dropdown-toggle-btn:hover { border-color: var(--accent-blue); transform: translateX(5px); background: var(--bg-secondary); }

        .dropdown-panel {
            max-height: 0; overflow: hidden; transition: max-height 0.5s cubic-bezier(0, 1, 0, 1), padding 0.3s ease;
            background-color: var(--bg-card); border-radius: 0 0 16px 16px; padding: 0 24px;
        }

        .dropdown-panel.expanded { max-height: 2000px; padding: 24px; margin-top: 4px; border: 1px solid var(--border-primary); }

        /* ===== АНІМОВАНІ КАРТКИ СУДДІВ ===== */
        .staff-grid-container { display: grid; grid-template-columns: repeat(auto-fit, minmax(270px, 1fr)); gap: 25px; margin-top: 25px; }

        .staff-profile-card {
            background: var(--bg-card); border: 1px solid var(--border-primary); padding: 35px 22px; border-radius: 22px;
            text-align: center; position: relative; overflow: hidden; transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .staff-profile-card::before {
            content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%;
            background: radial-gradient(circle, rgba(56, 189, 248, 0.1) 0%, transparent 70%);
            opacity: 0; transition: opacity 0.4s ease; transform: rotate(30deg);
        }

        .staff-profile-card:hover::before { opacity: 1; }

        .staff-profile-card:hover {
            transform: translateY(-12px) scale(1.03); border-color: var(--accent-blue); box-shadow: 0 20px 40px var(--card-shadow);
        }

        .staff-avatar-wrapper {
            width: 105px; height: 105px; margin: 0 auto 20px auto; border-radius: 50%; padding: 3px;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            transition: transform 0.5s ease;
        }

        .staff-profile-card:hover .staff-avatar-wrapper { transform: rotate(360deg); }

        .avatar-fallback {
            width: 100%; height: 100%; border-radius: 50%; background: var(--bg-secondary);
            display: flex; align-items: center; justify-content: center; font-size: 2.4rem;
        }

        .staff-role-badge {
            color: var(--accent-blue); font-size: 0.8rem; font-weight: 800; text-transform: uppercase;
            letter-spacing: 1.5px; margin-bottom: 16px; display: inline-block; background: rgba(14, 165, 233, 0.15);
            padding: 6px 16px; border-radius: 20px; transition: background 0.3s ease;
        }

        .staff-profile-card:hover .staff-role-badge { background: var(--accent-blue); color: #fff; }

        /* ===== ТАБЛИЦІ ТА ЧОРНИЙ СПИСОК ===== */
        .table-box-wrapper { width: 100%; overflow-x: auto; margin-top: 25px; border-radius: 20px; border: 1px solid var(--border-primary); }

        .analytics-table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.98rem; }

        .analytics-table th, .analytics-table td { padding: 18px 22px; border-bottom: 1px solid var(--border-primary); transition: background 0.2s ease; }

        .analytics-table th { background-color: var(--bg-card); color: var(--accent-blue); font-weight: 600; text-transform: uppercase; font-size: 0.82rem; }

        .analytics-table tr:hover td { background-color: rgba(56, 189, 248, 0.05); }

        /* Червоний стиль для Чорного Списку */
        .blacklisted-row:hover td { background-color: rgba(239, 68, 68, 0.1) !important; }

        .status-tag-red { color: var(--accent-red); background: rgba(239, 68, 68, 0.15); padding: 4px 12px; border-radius: 12px; font-weight: bold; font-size: 0.85rem; }

        .portal-footer {
            text-align: center; padding: 30px 20px; background: var(--bg-secondary); border: 1px solid var(--border-primary);
            border-radius: 20px; color: var(--text-muted); font-size: 0.95rem; margin-top: 35px;
        }
    </style>
</head>
<body>

    <!-- ЕКРАН ЗАВАНТАЖЕННЯ (10 СЕКУНД) -->
    <div id="loader-overlay">
        <div class="loader-spinner"></div>
        <div class="loader-title">🏛 ЗАВАНТАЖЕННЯ СУДОВОГО ПОРТАЛУ...</div>
        <div class="loader-bar-bg">
            <div class="loader-bar-fill" id="loaderFill"></div>
        </div>
        <div class="loader-timer" id="loaderTimer">Очікуйте: 10 сек.</div>
    </div>

    <div class="scroll-progress" id="scrollProgress"></div>
    <div class="quick-nav">
        <button type="button" id="toTop" title="На початок">↑</button>
        <button type="button" id="toBottom" title="До низу">↓</button>
    </div>

    <div class="main-container">
        
        <!-- ПАНЕЛЬ НАЛАШТУВАНЬ -->
        <div class="settings-box animate-on-scroll">
            <div class="settings-title" style="font-weight: bold; color: var(--accent-blue);">⚙️ Налаштування Інтерфейсу Сайту</div>
            <div class="theme-buttons-grid" style="display: flex; gap: 10px; flex-wrap: wrap;">
                <button class="theme-btn active" onclick="setTheme('dark', event)">🌙 Темна</button>
                <button class="theme-btn" onclick="setTheme('light', event)">☀️ Яскрава</button>
                <button class="theme-btn" onclick="setTheme('neon', event)">🔮 Неонова</button>
                <button class="theme-btn" onclick="setTheme('emerald', event)">🌲 Смарагдова</button>
            </div>
        </div>

        <header class="portal-header animate-on-scroll">
            <h1>🏛 Офіційний Портал Судової Системи Ukraine RP</h1>
            <p>Централізований державний реєстр судових проваджень, регламентів та керівного складу колегії</p>
        </header>

        <div class="hero-info-box animate-on-scroll">
            <h2>⚖️ СУД ІНФО UKRAINE RP ⚖️</h2>
            <p>Головний інформаційний центр судової системи! Тут зібрані всі офіційні правила дотримання законів, регламенти захисту прав громадян, розклад засідань, статистичні дані та інструкції з взаємодії з державними органами на нашому сервері.</p>
        </div>

        <!-- ОНЛАЙН-ТАБЛО ЗАСІДАНЬ -->
        <section class="content-section animate-on-scroll">
            <h2 class="section-title">📅 Онлайн-табло призначених засідань</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Актуальний розклад найближчих судових слухань у залі суду Ukraine RP:</p>

            <div class="schedule-grid">
                <div class="schedule-card">
                    <div style="font-size: 0.85rem; color: var(--accent-purple); font-weight: bold; margin-bottom: 6px;">Сьогодні о 19:00</div>
                    <div style="font-size: 1.1rem; font-weight: bold; margin-bottom: 8px;">Справа №1042 — Оскарження дій СБУ</div>
                    <div style="font-size: 0.9rem; color: var(--text-muted);">Суддя: Arseniy_zabanen</div>
                </div>
                <div class="schedule-card">
                    <div style="font-size: 0.85rem; color: var(--accent-purple); font-weight: bold; margin-bottom: 6px;">Завтра о 18:30</div>
                    <div style="font-size: 1.1rem; font-weight: bold; margin-bottom: 8px;">Справа №1043 — Цивільний позов відшкодування</div>
                    <div style="font-size: 0.9rem; color: var(--text-muted);">Заступник: mummu228kuku</div>
                </div>
                <div class="schedule-card">
                    <div style="font-size: 0.85rem; color: var(--accent-purple); font-weight: bold; margin-bottom: 6px;">20 Серпня о 20:00</div>
                    <div style="font-size: 1.1rem; font-weight: bold; margin-bottom: 8px;">Справа №1044 — Апеляція державного обвинувачення</div>
                    <div style="font-size: 0.9rem; color: var(--text-muted);">Суддя: Huhaidjopy</div>
                </div>
            </div>
        </section>

        <!-- ПРАВИЛА ТА РЕГЛАМЕНТИ -->
        <section class="content-section animate-on-scroll">
            <h2 class="section-title">⚖️ Нормативно-правова база та Правила Сервера</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Детальні інструкції щодо поведінки, етики, законності дій та регламенти:</p>
            
            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>📜 Загальна етика та правила поведінки в суді</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p><strong>Головні норми поведінки для учасників засідання:</strong></p>
                    <ul style="padding-left: 20px; color: var(--text-muted);">
                        <li><strong>Форма звернення:</strong> Звертайтеся виключно офіційно — <em>«Ваша Честь»</em>.</li>
                        <li><strong>Порядок:</strong> Заборонено перебивати виступи інших сторін та викрикувати.</li>
                        <li><strong>RP-Взаємодія:</strong> Докази надаються через скріншоти або відеозаписи (фрапс).</li>
                    </ul>
                </div>
            </div>

            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>🛡 Правила обшуку та законність дій держструктур</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p>Обшук або затримання вважаються легітимними лише за наявності вагомої RP-підстави (ордер, ордер від Судді, пряма фіксація правопорушення).</p>
                </div>
            </div>

            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>📚 Статті та регламент оскарження вироків</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p>Усі громадянські скарги мають бути подані протягом 48 годин з моменту фіксації порушення. Заявки подаються у відповідний розділ судової гілки.</p>
                </div>
            </div>
        </section>

        <!-- КОЛЕКТИВ СУДУ -->
        <section class="content-section animate-on-scroll">
            <h2 class="section-title">🏛 Колектив суду</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Офіційний кадровий склад керівництва судової колегії:</p>
            
            <div class="staff-grid-container">
                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback">⚖️</div>
                    </div>
                    <h3>Arseniy_zabanen</h3>
                    <div class="staff-role-badge">Головний Суддя (ГС)</div>
                    <div style="font-size: 0.95rem; color: var(--text-muted);">TG: <a href="https://t.me/Samyry228" target="_blank" style="color: var(--accent-blue); text-decoration: none; font-weight: bold;">@Samyry228</a></div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback">🛡</div>
                    </div>
                    <h3>mummu228kuku</h3>
                    <div class="staff-role-badge">Заступник</div>
                    <div style="font-size: 0.95rem; color: var(--text-muted);">TG: <a href="https://t.me/here_everyone" target="_blank" style="color: var(--accent-blue); text-decoration: none; font-weight: bold;">@here_everyone</a></div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback">🏛</div>
                    </div>
                    <h3>Huhaidjopy</h3>
                    <div class="staff-role-badge">Суддя</div>
                    <div style="font-size: 0.95rem; color: var(--text-muted);">TG: <a href="https://t.me/bewewewewewe" target="_blank" style="color: var(--accent-blue); text-decoration: none; font-weight: bold;">@bewewewewewe</a></div>
                </div>
            </div>
        </section>

        <!-- ЧОРНИЙ СПИСОК СУДОВОЇ СИСТЕМИ -->
        <section class="content-section animate-on-scroll">
            <h2 class="section-title" style="color: var(--accent-red);">🚫 Чорний список Судової Системи (ЧС)</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Список осіб, яким заборонено обіймати посади в адвокатурі та суді або брати участь у засіданнях:</p>

            <div class="table-box-wrapper">
                <analytics-table class="analytics-table">
                    <thead>
                        <tr>
                            <th>Нікнейм гравця</th>
                            <th>Причина внесення</th>
                            <th>Дата внесення</th>
                            <th>Статус / Термін</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr class="blacklisted-row">
                            <td style="font-weight: bold;">Ivan_Damagov</td>
                            <td>Численні порушення регламенту суду, неповага</td>
                            <td>01.08.2026</td>
                            <td><span class="status-tag-red">Безстроково</span></td>
                        </tr>
                        <tr class="blacklisted-row">
                            <td style="font-weight: bold;">Sanya_NonRP</td>
                            <td>Спроба підкупу судді / Дача неправдивих свідчень</td>
                            <td>12.08.2026</td>
                            <td><span class="status-tag-red">До 12.11.2026</span></td>
                        </tr>
                    </tbody>
                </analytics-table>
            </div>
        </section>

        <!-- СТАТИСТИКА ТА РЕЄСТР -->
        <section class="content-section animate-on-scroll">
            <h2 class="section-title">📊 Реєстр Розглянутих Справ</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Офіційна архівна статистика розгляду позовів за поточний місяць:</p>

            <div class="table-box-wrapper">
                <table class="analytics-table">
                    <thead>
                        <tr>
                            <th>Номер Справи</th>
                            <th>Позивач</th>
                            <th>Відповідач</th>
                            <th>Вердикт Суду</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>#1039</td>
                            <td>Oleg_Petrov</td>
                            <td>НПУ м. Київ</td>
                            <td style="color: var(--accent-blue); font-weight: bold;">Задоволено частково</td>
                        </tr>
                        <tr>
                            <td>#1040</td>
                            <td>Vadim_Kovalsky</td>
                            <td>СБУ м. Дніпро</td>
                            <td style="color: var(--accent-red); font-weight: bold;">Відхилено (Брак доказів)</td>
                        </tr>
                        <tr>
                            <td>#1041</td>
                            <td>Marta_Sydorova</td>
                            <td>Мерія м. Харків</td>
                            <td style="color: #22c55e; font-weight: bold;">Повністю задоволено</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <footer class="portal-footer animate-on-scroll">
            <p>&copy; 2026 Офіційний Портал Судової Системи Ukraine RP. Усі права захищені.</p>
        </footer>
    </div>

    <script>
        // ЕКРАН ЗАВАНТАЖЕННЯ НА 10 СЕКУНД
        document.addEventListener("DOMContentLoaded", function() {
            let timeLeft = 10;
            const fill = document.getElementById('loaderFill');
            const timerText = document.getElementById('loaderTimer');
            const overlay = document.getElementById('loader-overlay');

            const interval = setInterval(() => {
                timeLeft -= 0.1;
                let percentage = ((10 - timeLeft) / 10) * 100;
                fill.style.width = percentage + "%";
                
                if (timeLeft > 0) {
                    timerText.textContent = `Очікуйте: ${Math.ceil(timeLeft)} сек.`;
                } else {
                    clearInterval(interval);
                    overlay.style.opacity = '0';
                    overlay.style.visibility = 'hidden';
                    document.body.style.overflow = 'auto';
                }
            }, 100);

            // Прогрес скролу
            const progress = document.getElementById('scrollProgress');
            window.addEventListener('scroll', () => {
                const scrollTop = window.scrollY;
                const max = document.documentElement.scrollHeight - window.innerHeight;
                progress.style.width = `${max > 0 ? (scrollTop / max) * 100 : 0}%`;
            });

            // Кнопки Навігації
            document.getElementById('toTop')?.addEventListener('click', () => window.scrollTo({ top: 0, behavior: 'smooth' }));
            document.getElementById('toBottom')?.addEventListener('click', () => window.scrollTo({ top: document.documentElement.scrollHeight, behavior: 'smooth' }));

            // Анімація випливання блоків
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                    }
                });
            }, { threshold: 0.1 });

            document.querySelectorAll('.animate-on-scroll').forEach(el => observer.observe(el));

            // Дропдауни
            document.querySelectorAll('.dropdown-toggle-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const panel = this.nextElementSibling;
                    panel.classList.toggle('expanded');
                });
            });
        });

        // ПЕРЕМИКАННЯ ТЕМ
        function setTheme(themeName, event) {
            document.body.className = '';
            if (themeName !== 'dark') {
                document.body.classList.add('theme-' + themeName);
            }
            document.querySelectorAll('.theme-btn').forEach(btn => btn.classList.remove('active'));
            if(event) event.target.classList.add('active');
        }
    </script>
</body>
</html>

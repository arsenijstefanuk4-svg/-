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

        /* ЗМІННІ ТЕМ (За замовчуванням: Темна) */
        :root {
            --bg-primary: #020617;
            --bg-secondary: #070d1f;
            --bg-card: #0b1329;
            --bg-card-hover: #101c3d;
            --border-primary: #1e293b;
            --border-accent: #38bdf8;
            --accent-blue: #0ea5e9;
            --accent-blue-hover: #38bdf8;
            --accent-purple: #818cf8;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --success-color: #22c55e;
            --transition-speed: 0.4s;
        }

        /* СВІТЛА / ЯСКРАВА ТЕМА */
        body.theme-light {
            --bg-primary: #f1f5f9;
            --bg-secondary: #ffffff;
            --bg-card: #f8fafc;
            --bg-card-hover: #e2e8f0;
            --border-primary: #cbd5e1;
            --border-accent: #0284c7;
            --accent-blue: #0284c7;
            --accent-blue-hover: #0369a1;
            --accent-purple: #6366f1;
            --text-main: #0f172a;
            --text-muted: #475569;
        }

        /* НЕОНОВА ТЕМА (Cyberpunk) */
        body.theme-neon {
            --bg-primary: #050014;
            --bg-secondary: #0d0029;
            --bg-card: #180038;
            --bg-card-hover: #260054;
            --border-primary: #ff007f;
            --border-accent: #00f0ff;
            --accent-blue: #00f0ff;
            --accent-blue-hover: #ff007f;
            --accent-purple: #bf00ff;
            --text-main: #ffffff;
            --text-muted: #d8b4fe;
        }

        /* СМАРАГДОВА ТЕМА (Emerald) */
        body.theme-emerald {
            --bg-primary: #022c22;
            --bg-secondary: #064e3b;
            --bg-card: #065f46;
            --bg-card-hover: #047857;
            --border-primary: #10b981;
            --border-accent: #34d399;
            --accent-blue: #10b981;
            --accent-blue-hover: #34d399;
            --accent-purple: #059669;
            --text-main: #ecfdf5;
            --text-muted: #a7f3d0;
        }

        html { scroll-behavior: smooth; }

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
            width: 90px;
            height: 90px;
            border: 6px solid rgba(56, 189, 248, 0.15);
            border-top: 6px solid var(--accent-blue);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 25px;
            box-shadow: 0 0 25px var(--accent-blue);
        }

        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        .loader-title {
            color: #fff;
            font-size: 1.6rem;
            font-weight: 700;
            letter-spacing: 2px;
            margin-bottom: 15px;
            text-align: center;
        }

        .loader-bar-bg {
            width: 320px;
            height: 12px;
            background: #0f172a;
            border-radius: 10px;
            overflow: hidden;
            border: 1px solid var(--border-accent);
            box-shadow: 0 0 15px rgba(56, 189, 248, 0.3);
        }

        .loader-bar-fill {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, var(--accent-blue), var(--accent-purple));
            transition: width 0.1s linear;
        }

        .loader-timer {
            margin-top: 12px;
            color: var(--text-muted);
            font-size: 0.95rem;
            font-weight: 600;
        }

        /* ===== СКРОЛ ТА НАВІГАЦІЯ ===== */
        .scroll-progress {
            position: fixed;
            top: 0; left: 0;
            width: 0; height: 4px;
            background: linear-gradient(90deg,#38bdf8,#818cf8,#c084fc,#22d3ee);
            box-shadow: 0 0 16px rgba(56,189,248,.8);
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
            backdrop-filter: blur(14px);
            box-shadow: 0 8px 25px rgba(0,0,0,.35);
            transition: transform .25s ease, box-shadow .25s ease, border-color .25s ease;
            font-size: 1.1rem;
        }

        .quick-nav button:hover {
            transform: translateY(-4px) scale(1.05);
            border-color: var(--accent-blue);
        }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: var(--bg-primary);
            color: var(--text-main);
            line-height: 1.7;
            padding: 30px;
            overflow-x: hidden;
            min-height: 100vh;
            position: relative;
            transition: background 0.5s ease, color 0.5s ease;
        }

        .main-container {
            max-width: 1300px;
            margin: 0 auto;
        }

        .animate-on-scroll {
            opacity: 0;
            transform: translateY(40px);
            transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* ===== ПАНЕЛЬ НАЛАШТУВАНЬ ===== */
        .settings-box {
            background: var(--bg-card);
            border: 1px solid var(--border-accent);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 35px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            align-items: center;
            justify-content: space-between;
        }

        .settings-title {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--accent-blue);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .theme-buttons-grid {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .theme-btn {
            padding: 8px 16px;
            border-radius: 12px;
            border: 1px solid var(--border-primary);
            background: var(--bg-secondary);
            color: var(--text-main);
            cursor: pointer;
            font-weight: 600;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }

        .theme-btn:hover, .theme-btn.active {
            border-color: var(--accent-blue);
            background: var(--accent-blue);
            color: #fff;
            box-shadow: 0 0 12px var(--accent-blue);
        }

        .portal-header {
            background: var(--bg-secondary);
            backdrop-filter: blur(16px);
            border: 1px solid var(--border-primary);
            border-bottom: 5px solid var(--accent-blue);
            padding: 40px 25px;
            text-align: center;
            border-radius: 24px;
            margin-bottom: 35px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
            position: relative;
        }

        .portal-header h1 {
            font-size: clamp(1.8rem, 3.5vw, 2.6rem);
            color: var(--accent-blue);
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 12px;
            animation: pulseGlow 3s infinite alternate;
        }

        @keyframes pulseGlow {
            0% { filter: drop-shadow(0 0 2px var(--accent-blue)); }
            100% { filter: drop-shadow(0 0 15px var(--accent-blue)); }
        }

        .portal-header p {
            color: var(--text-muted);
            font-size: 1.1rem;
            max-width: 850px;
            margin: 0 auto;
        }

        .hero-info-box {
            background: var(--bg-card);
            backdrop-filter: blur(16px);
            border: 2px solid var(--accent-blue);
            border-radius: 26px;
            padding: 45px 35px;
            margin-bottom: 35px;
            text-align: center;
            box-shadow: 0 0 40px rgba(14, 165, 233, 0.2);
        }

        .hero-info-box h2 {
            font-size: clamp(2rem, 4vw, 3.2rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--accent-blue);
            margin-bottom: 18px;
        }

        .hero-info-box p {
            color: var(--text-main);
            font-size: 1.15rem;
            max-width: 950px;
            margin: 0 auto 15px auto;
        }

        .content-section {
            background: var(--bg-secondary);
            border: 1px solid var(--border-primary);
            border-radius: 24px;
            padding: 40px;
            margin-bottom: 35px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }

        .section-title {
            color: var(--accent-blue);
            font-size: 1.75rem;
            margin-bottom: 15px;
            border-bottom: 2px solid var(--border-primary);
            padding-bottom: 12px;
            display: inline-block;
        }

        .section-description {
            color: var(--text-muted);
            font-size: 1.02rem;
            margin-bottom: 25px;
        }

        /* ===== ТАБЛО ЗАСІДАНЬ ===== */
        .schedule-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .schedule-card {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            border-left: 4px solid var(--accent-blue);
            border-radius: 16px;
            padding: 20px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .schedule-card:hover {
            transform: translateY(-6px);
            box-shadow: 0 12px 25px rgba(0,0,0,0.4);
        }

        .schedule-time {
            font-size: 0.85rem;
            color: var(--accent-purple);
            font-weight: bold;
            text-transform: uppercase;
            margin-bottom: 6px;
        }

        .schedule-title {
            font-size: 1.1rem;
            font-weight: bold;
            color: var(--text-main);
            margin-bottom: 8px;
        }

        .schedule-judge {
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        /* ===== СПИСКИ ТА ДРОПДАУНИ ===== */
        .dropdown-element { margin-top: 16px; }

        .dropdown-toggle-btn {
            background: var(--bg-card);
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
            border-color: var(--accent-blue);
            transform: translateY(-2px);
        }

        .dropdown-panel {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.45s cubic-bezier(0.4, 0, 0.2, 1), padding 0.3s ease;
            background-color: var(--bg-card);
            border-radius: 0 0 16px 16px;
            padding: 0 24px;
        }

        .dropdown-panel.expanded {
            max-height: 1500px;
            padding: 24px;
            margin-top: 4px;
            border: 1px solid var(--border-primary);
        }

        .dropdown-panel p, .dropdown-panel ul { color: var(--text-muted); font-size: 0.98rem; margin-bottom: 12px; }
        .dropdown-panel ul { padding-left: 22px; }
        .dropdown-panel li { margin-bottom: 8px; }

        .staff-grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
            gap: 24px;
            margin-top: 25px;
        }

        .staff-profile-card {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            padding: 35px 22px;
            border-radius: 20px;
            text-align: center;
            position: relative;
            overflow: hidden;
            transition: transform 0.4s ease, border-color 0.4s ease;
        }

        .staff-profile-card:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: var(--accent-blue);
        }

        .staff-avatar-wrapper {
            width: 105px; height: 105px;
            margin: 0 auto 20px auto;
            border-radius: 50%;
            padding: 3px;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
        }

        .avatar-fallback {
            width: 100%; height: 100%; border-radius: 50%; background: var(--bg-secondary); display: flex; align-items: center; justify-content: center; font-size: 2.4rem; color: var(--accent-blue);
        }

        .staff-profile-card h3 { font-size: 1.35rem; margin-bottom: 8px; color: var(--text-main); }
        .staff-role-badge { color: var(--accent-blue); font-size: 0.8rem; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 16px; display: inline-block; background: rgba(14, 165, 233, 0.15); padding: 6px 16px; border-radius: 20px; }
        .staff-contacts-info { font-size: 0.95rem; color: var(--text-muted); }
        .staff-contacts-info a { color: var(--accent-blue); text-decoration: none; font-weight: 600; }

        .table-box-wrapper {
            width: 100%; overflow-x: auto; margin-top: 25px; border-radius: 20px; border: 1px solid var(--border-primary);
        }

        .analytics-table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.98rem; white-space: nowrap; }
        .analytics-table th, .analytics-table td { padding: 18px 22px; border-bottom: 1px solid var(--border-primary); color: var(--text-main); }
        .analytics-table th { background-color: var(--bg-card); color: var(--accent-blue); font-weight: 600; text-transform: uppercase; font-size: 0.82rem; }

        .portal-footer {
            text-align: center; padding: 30px 20px; background: var(--bg-secondary); border: 1px solid var(--border-primary); border-radius: 20px; color: var(--text-muted); font-size: 0.95rem; margin-top: 35px;
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
            <div class="settings-title">⚙️ Налаштування Інтерфейсу Сайту</div>
            <div class="theme-buttons-grid">
                <button class="theme-btn active" onclick="setTheme('dark')">🌙 Темна</button>
                <button class="theme-btn" onclick="setTheme('light')">☀️ Яскрава</button>
                <button class="theme-btn" onclick="setTheme('neon')">🔮 Неонова</button>
                <button class="theme-btn" onclick="setTheme('emerald')">🌲 Смарагдова</button>
            </div>
        </div>

        <header class="portal-header animate-on-scroll">
            <h1>🏛 Офіційний Портал Судової Системи Ukraine RP</h1>
            <p>Централізований державний реєстр судових проваджень, регламентів та керівного складу колегії</p>
        </header>

        <div class="hero-info-box animate-on-scroll">
            <h2>⚖️ СУД ІНФО UKRAINE RP ⚖️</h2>
            <p>Головний інформаційний центр судової системи! Тут зібрані всі офіційні правила дотримання законів, регламенти захисту прав громадян, розклад засідань та інструкції з взаємодії з державними органами на нашому сервері.</p>
        </div>

        <section class="content-section animate-on-scroll">
            <h2 class="section-title">⚖️ Нормативно-правова база та Правила Сервера</h2>
            <p class="section-description">Детальні інструкції щодо поведінки, етики, законності дій та регламенти:</p>
            
            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>📜 Загальна етика та правила поведінки в суді</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p><strong>Головні норми поведінки для учасників засідання:</strong></p>
                    <ul>
                        <li><strong>Форма звернення:</strong> Звертайтеся виключно офіційно — <em>«Ваша Честь»</em>.</li>
                        <li><strong>Порядок:</strong> Заборонено перебивати виступи інших сторін та викрикувати.</li>
                        <li><strong>RP-Взаємодія:</strong> Докази надаються через скріншоти або фрапси.</li>
                    </ul>
                </div>
            </div>

            <div class="dropdown-element">
                <button class="dropdown-toggle-btn">
                    <span>🛡 Правила обшуку та законність дій держструктур</span> 
                    <span>▼</span>
                </button>
                <div class="dropdown-panel">
                    <p>Обшук або затримання вважаються легітимними лише за наявності вагомої RP-підстави.</p>
                </div>
            </div>
        </section>

        <section class="content-section animate-on-scroll">
            <h2 class="section-title">🏛 Колектив суду</h2>
            <p class="section-description">Офіційний кадровий склад керівництва судової колегії:</p>
            
            <div class="staff-grid-container">
                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback">⚖️</div>
                    </div>
                    <h3>Arseniy_zabanen</h3>
                    <div class="staff-role-badge">Головний Суддя (ГС)</div>
                    <div class="staff-contacts-info">TG: <a href="https://t.me/Samyry228" target="_blank">@Samyry228</a></div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback">🛡</div>
                    </div>
                    <h3>mummu228kuku</h3>
                    <div class="staff-role-badge">Заступник</div>
                    <div class="staff-contacts-info">TG: <a href="https://t.me/here_everyone" target="_blank">@here_everyone</a></div>
                </div>

                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback">🏛</div>
                    </div>
                    <h3>Huhaidjopy</h3>
                    <div class="staff-role-badge">Суддя</div>
                    <div class="staff-contacts-info">TG: <a href="https://t.me/bewewewewewe" target="_blank">@bewewewewewe</a></div>
                </div>
            </div>
        </section>

        <footer class="portal-footer animate-on-scroll">
            <p>&copy; 2026 Офіційний Портал Судової Системи Ukraine RP. Усі права захищені.</p>
        </footer>
    </div>

    <script>
        // ЕКРАН ЗАВАНТАЖЕННЯ РІВНО НА 10 СЕКУНД
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

            // Навігація вгору/вниз
            document.getElementById('toTop')?.addEventListener('click', () => window.scrollTo({ top: 0, behavior: 'smooth' }));
            document.getElementById('toBottom')?.addEventListener('click', () => window.scrollTo({ top: document.documentElement.scrollHeight, behavior: 'smooth' }));

            // Поява блоків при скролі
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                    }
                });
            }, { threshold: 0.1 });

            document.querySelectorAll('.animate-on-scroll').forEach(el => observer.observe(el));

            // Випадаючі списки
            document.querySelectorAll('.dropdown-toggle-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const panel = this.nextElementSibling;
                    panel.classList.toggle('expanded');
                });
            });
        });

        // ПЕРЕММИКАННЯ ТЕМ
        function setTheme(themeName) {
            document.body.className = '';
            if (themeName !== 'dark') {
                document.body.classList.add('theme-' + themeName);
            }
            document.querySelectorAll('.theme-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
        }
    </script>
</body>
</html>

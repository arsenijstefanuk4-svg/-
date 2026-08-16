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
            --border-primary: #1e293b;
            --accent-blue: #0ea5e9;
            --accent-purple: #818cf8;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --success-color: #22c55e;
            --danger-color: #ef4444;
            --glow-color: rgba(14, 165, 233, 0.4);
        }

        /* ТЕМИ */
        body.theme-cyberpunk {
            --bg-primary: #0d0221;
            --bg-secondary: #190535;
            --bg-card: #26084d;
            --border-primary: #ff007f;
            --accent-blue: #00f0ff;
            --accent-purple: #ff007f;
            --glow-color: rgba(255, 0, 127, 0.5);
        }

        body.theme-matrix {
            --bg-primary: #000a00;
            --bg-secondary: #001a00;
            --bg-card: #002b00;
            --border-primary: #00ff00;
            --accent-blue: #00ff66;
            --accent-purple: #00cc44;
            --glow-color: rgba(0, 255, 0, 0.4);
        }

        body.theme-crimson {
            --bg-primary: #1a0505;
            --bg-secondary: #2b0a0a;
            --bg-card: #3d0e0e;
            --border-primary: #991b1b;
            --accent-blue: #f87171;
            --accent-purple: #ef4444;
            --glow-color: rgba(239, 68, 68, 0.4);
        }

        html { scroll-behavior: smooth; }

        body {
            font-family: 'Segoe UI', Roboto, sans-serif;
            background: var(--bg-primary);
            color: var(--text-main);
            line-height: 1.6;
            padding: 30px;
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
            transition: background 0.5s ease;
        }

        /* АНІМОВАНИЙ ЗАДНІЙ ФОН */
        .bg-particle {
            position: fixed;
            border-radius: 50%;
            filter: blur(80px);
            z-index: -1;
            opacity: 0.6;
            animation: floatParticle 10s infinite alternate ease-in-out;
        }

        .bg-p1 {
            top: -100px; left: -100px;
            width: 500px; height: 500px;
            background: var(--accent-blue);
        }

        .bg-p2 {
            bottom: -100px; right: -100px;
            width: 500px; height: 500px;
            background: var(--accent-purple);
            animation-delay: -5s;
        }

        @keyframes floatParticle {
            0% { transform: translate(0, 0) scale(1); }
            100% { transform: translate(120px, 80px) scale(1.3); }
        }

        .main-container { max-width: 1200px; margin: 0 auto; }

        /* НАЛАШТУВАННЯ */
        .settings-btn {
            position: fixed;
            top: 20px; right: 20px;
            z-index: 10000;
            background: var(--bg-secondary);
            border: 1px solid var(--accent-blue);
            color: var(--text-main);
            padding: 10px 16px;
            border-radius: 12px;
            cursor: pointer;
            box-shadow: 0 0 15px var(--glow-color);
            transition: transform 0.3s;
        }

        .settings-btn:hover { transform: scale(1.05); }

        .settings-modal {
            display: none;
            position: fixed;
            top: 70px; right: 20px;
            z-index: 10001;
            background: var(--bg-card);
            border: 1px solid var(--accent-blue);
            padding: 20px;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            width: 250px;
        }

        .settings-modal.active { display: block; }

        .settings-group { margin-bottom: 15px; }
        .settings-group label { display: block; font-size: 0.85rem; margin-bottom: 5px; color: var(--text-muted); }
        .settings-group select {
            width: 100%;
            padding: 8px;
            background: var(--bg-secondary);
            border: 1px solid var(--border-primary);
            color: var(--text-main);
            border-radius: 8px;
        }

        .portal-header {
            background: var(--bg-secondary);
            border: 1px solid var(--border-primary);
            border-bottom: 4px solid var(--accent-blue);
            padding: 30px;
            text-align: center;
            border-radius: 20px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .portal-header h1 {
            font-size: 2rem;
            color: var(--text-main);
            text-transform: uppercase;
            letter-spacing: 2px;
            animation: pulseGlow 3s infinite alternate;
        }

        @keyframes pulseGlow {
            0% { text-shadow: 0 0 5px var(--accent-blue); }
            100% { text-shadow: 0 0 20px var(--accent-blue); }
        }

        .content-section {
            background: var(--bg-secondary);
            border: 1px solid var(--border-primary);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
        }

        .section-title {
            color: var(--accent-blue);
            font-size: 1.5rem;
            margin-bottom: 15px;
            border-bottom: 2px solid var(--border-primary);
            padding-bottom: 8px;
            display: inline-block;
        }

        /* КАРТКИ СУДДІВ З ЕКСТРЕМАЛЬНОЮ АНІМАЦІЄЮ */
        .staff-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .staff-card {
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            padding: 25px;
            border-radius: 16px;
            text-align: center;
            position: relative;
            overflow: hidden;
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            animation: cardEntrance 1s ease-out forwards;
        }

        .staff-card::before {
            content: '';
            position: absolute;
            top: -50%; left: -50%;
            width: 200%; height: 200%;
            background: conic-gradient(transparent, var(--accent-blue), transparent 30%);
            animation: rotateGlow 4s linear infinite;
            z-index: 1;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .staff-card:hover::before { opacity: 1; }

        .staff-card-content {
            position: relative;
            z-index: 2;
            background: var(--bg-card);
            padding: 15px;
            border-radius: 12px;
        }

        .staff-card:hover {
            transform: translateY(-10px) scale(1.03);
            box-shadow: 0 15px 30px var(--glow-color);
            border-color: var(--accent-blue);
        }

        @keyframes rotateGlow {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @keyframes cardEntrance {
            0% { opacity: 0; transform: translateY(50px) rotateX(-30deg); }
            100% { opacity: 1; transform: translateY(0) rotateX(0deg); }
        }

        .avatar {
            width: 80px; height: 80px;
            border-radius: 50%;
            margin: 0 auto 15px;
            background: var(--accent-blue);
            display: flex; align-items: center; justify-content: center;
            font-size: 2rem;
            box-shadow: 0 0 15px var(--glow-color);
        }

        .role-badge {
            display: inline-block;
            background: rgba(14, 165, 233, 0.15);
            color: var(--accent-blue);
            padding: 4px 12px;
            border-radius: 12px;
            font-size: 0.8rem;
            font-weight: bold;
            margin: 10px 0;
        }

        /* АКОРДЕОН */
        .accordion-btn {
            width: 100%;
            background: var(--bg-card);
            border: 1px solid var(--border-primary);
            color: var(--text-main);
            padding: 15px;
            text-align: left;
            border-radius: 10px;
            cursor: pointer;
            margin-top: 10px;
            display: flex;
            justify-content: space-between;
        }

        .accordion-panel {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease;
            background: var(--bg-primary);
            padding: 0 15px;
            border-radius: 0 0 10px 10px;
        }

        .accordion-panel.active {
            max-height: 300px;
            padding: 15px;
            border: 1px solid var(--border-primary);
            border-top: none;
        }

        .chart-container { height: 300px; position: relative; }
        
        a { color: var(--accent-blue); text-decoration: none; }
        a:hover { text-decoration: underline; }
    </style>
</head>
<body>

    <div class="bg-particle bg-p1"></div>
    <div class="bg-particle bg-p2"></div>

    <button class="settings-btn" id="openSettings">⚙️ Налаштування</button>
    <div class="settings-modal" id="settingsModal">
        <div class="settings-group">
            <label for="themeSelect">Тема оформлення</label>
            <select id="themeSelect">
                <option value="default">Стандартна (Cyber Blue)</option>
                <option value="cyberpunk">Neon Cyberpunk</option>
                <option value="matrix">Matrix Green</option>
                <option value="crimson">Crimson Red</option>
            </select>
        </div>
        <div class="settings-group">
            <label for="animToggle">Анімації заднього фону</label>
            <select id="animToggle">
                <option value="on">Увімкнено</option>
                <option value="off">Вимкнено</option>
            </select>
        </div>
    </div>

    <div class="main-container">
        
        <header class="portal-header">
            <h1>🏛 Судова Система Ukraine RP</h1>
            <p>Офіційний портал судових проваджень та регламентів</p>
        </header>

        <section class="content-section">
            <h2 class="section-title">⚖️ Колегія Суддів</h2>
            <div class="staff-grid">
                <div class="staff-card">
                    <div class="staff-card-content">
                        <div class="avatar">⚖️</div>
                        <h3>Arseniy_zabanen</h3>
                        <span class="role-badge">Головний Суддя</span>
                        <p>TG: <a href="https://t.me/Samyry228" target="_blank">@Samyry228</a></p>
                    </div>
                </div>

                <div class="staff-card">
                    <div class="staff-card-content">
                        <div class="avatar">🛡</div>
                        <h3>mummu228kuku</h3>
                        <span class="role-badge">Заступник</span>
                        <p>TG: <a href="https://t.me/here_everyone" target="_blank">@here_everyone</a></p>
                    </div>
                </div>

                <div class="staff-card">
                    <div class="staff-card-content">
                        <div class="avatar">🏛</div>
                        <h3>Huhaidjopy</h3>
                        <span class="role-badge">Суддя</span>
                        <p>TG: <a href="https://t.me/bewewewewewe" target="_blank">@bewewewewewe</a></p>
                    </div>
                </div>
            </div>
        </section>

        <section class="content-section">
            <h2 class="section-title">📈 Активність Суду</h2>
            <div class="chart-container">
                <canvas id="courtChart"></canvas>
            </div>
        </section>

        <section class="content-section">
            <h2 class="section-title">📜 Правила та Регламенти</h2>
            
            <button class="accordion-btn"><span>Етика та поведінка в суді</span> <span>▼</span></button>
            <div class="accordion-panel">
                <p>Звертайтеся до судді «Ваша Честь». Дотримуйтесь порядку та подавайте докази у формі RP (скріншоти/відео).</p>
            </div>

            <button class="accordion-btn"><span>Правила апеляції</span> <span>▼</span></button>
            <div class="accordion-panel">
                <p>Подача апеляції доступна протягом 48 годин після винесення рішення при наявності відеофіксації.</p>
            </div>
        </section>

    </div>

    <script>
        document.addEventListener("DOMContentLoaded", () => {
            // Модалка налаштувань
            const settingsBtn = document.getElementById('openSettings');
            const settingsModal = document.getElementById('settingsModal');
            
            settingsBtn.addEventListener('click', () => {
                settingsModal.classList.toggle('active');
            });

            // Зміна тем
            const themeSelect = document.getElementById('themeSelect');
            themeSelect.addEventListener('change', (e) => {
                document.body.className = '';
                if (e.target.value !== 'default') {
                    document.body.classList.add(`theme-${e.target.value}`);
                }
            });

            // Вимкнення анімацій фону
            const animToggle = document.getElementById('animToggle');
            const particles = document.querySelectorAll('.bg-particle');
            animToggle.addEventListener('change', (e) => {
                particles.forEach(p => p.style.display = e.target.value === 'off' ? 'none' : 'block');
            });

            // Аккордеон
            document.querySelectorAll('.accordion-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    const panel = btn.nextElementSibling;
                    panel.classList.toggle('active');
                });
            });

            // Простий графік
            const ctx = document.getElementById('courtChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Травень', 'Червень', 'Липень', 'Серпень'],
                    datasets: [{
                        label: 'Розглянуті справи',
                        data: [310, 570, 573, 640],
                        borderColor: '#0ea5e9',
                        tension: 0.3,
                        fill: false
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { labels: { color: '#f8fafc' } } },
                    scales: {
                        x: { ticks: { color: '#94a3b8' } },
                        y: { ticks: { color: '#94a3b8' } }
                    }
                }
            });
        });
    </script>
</body>
</html>

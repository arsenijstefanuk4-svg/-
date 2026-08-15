<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Офіційний Портал Судової Системи Ukraine RP</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        /* ===== БАЗОВІ СТИЛІ ТА ТЕМА ===== */
        :root {
            --bg-deep: #050b14;
            --bg-card: rgba(11, 19, 41, 0.75);
            --border-glass: rgba(56, 189, 248, 0.2);
            --accent-blue: #38bdf8;
            --accent-purple: #c084fc;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: var(--bg-deep);
            color: var(--text-main);
            font-family: 'Segoe UI', Roboto, sans-serif;
            min-height: 100vh;
            overflow-x: hidden;
            padding: 24px;
            position: relative;
        }

        /* Фонові світлові орби */
        .bg-glow-orb {
            position: fixed;
            width: 450px;
            height: 450px;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(56, 189, 248, 0.12) 0%, rgba(0,0,0,0) 70%);
            z-index: -2;
            pointer-events: none;
        }
        .orb-1 { top: -100px; left: -100px; }
        .orb-2 { bottom: -100px; right: -100px; background: radial-gradient(circle, rgba(192, 132, 252, 0.1) 0%, rgba(0,0,0,0) 70%); }

        .portal-container {
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
        }

        /* ===== АНІМАЦІЇ ПОЯВИ ===== */
        .animate-on-scroll {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* ===== ШАПКА ТА НЕОНОВИЙ ЗАГОЛОВОК ===== */
        .portal-header {
            text-align: center;
            margin-bottom: 40px;
            padding: 30px;
            background: var(--bg-card);
            backdrop-filter: blur(16px);
            border: 1px solid var(--border-glass);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
            position: relative;
            overflow: hidden;
        }

        .portal-header h1 {
            font-size: 2.5rem;
            font-weight: 800;
            background: linear-gradient(135deg, #38bdf8 0%, #818cf8 50%, #c084fc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(56, 189, 248, 0.4);
            margin-bottom: 12px;
            animation: neonPulse 4s ease-in-out infinite alternate;
        }

        @keyframes neonPulse {
            0% { filter: drop-shadow(0 0 2px rgba(56,189,248,0.5)); }
            100% { filter: drop-shadow(0 0 12px rgba(192,132,252,0.8)); }
        }

        .portal-header p {
            color: var(--text-muted);
            font-size: 1.05rem;
            max-width: 700px;
            margin: 0 auto;
        }

        /* Декоративні лінії та сканер-ефект */
        .portal-header::after {
            content: "";
            position: absolute;
            top: 0; left: -100%;
            width: 100%; height: 2px;
            background: linear-gradient(90deg, transparent, var(--accent-blue), transparent);
            animation: scanLine 6s linear infinite;
        }
        @keyframes scanLine {
            0% { left: -100%; }
            100% { left: 100%; }
        }

        /* ===== ОСНОВНІ КОНТЕНТНІ БЛОКИ ===== */
        .content-section {
            background: var(--bg-card);
            backdrop-filter: blur(16px);
            border: 1px solid var(--border-glass);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
        }

        .section-title {
            font-size: 1.6rem;
            font-weight: 700;
            color: #f1f5f9;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-description {
            color: var(--text-muted);
            margin-bottom: 25px;
            line-height: 1.6;
        }

        /* ===== КАРТКИ СУДДІВ ТА ПЕРСОНАЛУ ===== */
        .staff-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        .staff-profile-card {
            background: rgba(15, 23, 42, 0.6);
            border: 1px solid rgba(56, 189, 248, 0.15);
            border-radius: 16px;
            padding: 24px;
            text-align: center;
            position: relative;
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }

        .staff-profile-card h3 {
            font-size: 1.25rem;
            margin-bottom: 8px;
            color: #ffffff;
        }

        .staff-badge {
            display: inline-block;
            background: rgba(56, 189, 248, 0.1);
            color: var(--accent-blue);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            margin-bottom: 14px;
            border: 1px solid rgba(56, 189, 248, 0.3);
        }

        .staff-contacts {
            font-size: 0.9rem;
            color: var(--text-muted);
            line-height: 1.5;
        }

        .staff-contacts a {
            color: var(--accent-blue);
            text-decoration: none;
            transition: color 0.2s;
        }
        .staff-contacts a:hover {
            color: var(--accent-purple);
            text-decoration: underline;
        }

        /* ===== ЧОРНИЙ СПИСОК (тільки heehrhrhl18) ===== */
        .blacklist-section {
            background: rgba(30, 10, 15, 0.6);
            border: 1px solid rgba(239, 68, 68, 0.3);
        }
        .blacklist-title {
            color: #f87171 !important;
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

        /* ===== ІВЕНТИ ТА РОЗКЛАД ===== */
        .event-schedule-container {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 15px;
        }
        .schedule-badge {
            background: rgba(192, 132, 252, 0.1);
            border: 1px solid rgba(192, 132, 252, 0.3);
            color: #e879f9;
            padding: 8px 16px;
            border-radius: 12px;
            font-weight: 600;
            font-size: 0.9rem;
        }

        .owner-news-branch {
            margin-top: 25px;
            padding-top: 20px;
            border-top: 1px solid rgba(255,255,255,0.08);
        }
        .owner-news-branch h3 {
            font-size: 1.2rem;
            margin-bottom: 10px;
            color: #38bdf8;
        }

        /* ===== БІРЖА ТА ГРАФІК (зі збоєм системи) ===== */
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
            transition: all 0.3s ease;
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
            height: 350px;
            width: 100%;
        }

        /* ===== ФУТЕР ===== */
        .portal-footer {
            text-align: center;
            padding: 20px;
            color: var(--text-muted);
            font-size: 0.9rem;
            border-top: 1px solid var(--border-glass);
            margin-top: 20px;
        }

        /* ===== ULTIMATE UI ENHANCEMENTS (Додані ефекти) ===== */
        html { scroll-behavior: smooth; }

        .scroll-progress {
            position: fixed;
            top: 0; left: 0;
            width: 0; height: 4px;
            background: linear-gradient(90deg,#38bdf8,#818cf8,#c084fc,#22d3ee);
            box-shadow: 0 0 16px rgba(56,189,248,.8);
            z-index: 99999;
        }

        .premium-card {
            transform-style: preserve-3d;
            will-change: transform;
        }

        .premium-card::before {
            content: "";
            position: absolute;
            inset: -1px;
            border-radius: inherit;
            padding: 1px;
            background: linear-gradient(110deg,transparent,rgba(56,189,248,.75),transparent,rgba(167,139,250,.6),transparent);
            background-size: 250% 250%;
            animation: borderFlow 5s linear infinite;
            -webkit-mask: linear-gradient(#000 0 0) content-box,linear-gradient(#000 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            pointer-events: none;
        }

        @keyframes borderFlow {
            0% { background-position: 0% 50%; }
            100% { background-position: 250% 50%; }
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
            border: 1px solid rgba(56,189,248,.35);
            background: rgba(7,13,31,.85);
            color: #fff;
            cursor: pointer;
            backdrop-filter: blur(14px);
            box-shadow: 0 8px 25px rgba(0,0,0,.35);
            transition: transform .25s ease, box-shadow .25s ease, border-color .25s ease;
            font-size: 1.1rem;
        }

        .quick-nav button:hover {
            transform: translateY(-4px) scale(1.05);
            border-color: #38bdf8;
            box-shadow: 0 14px 35px rgba(56,189,248,.25);
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

        .float-orb {
            position: fixed;
            width: 7px;
            height: 7px;
            border-radius: 50%;
            background: #38bdf8;
            box-shadow: 0 0 18px #38bdf8;
            opacity: .4;
            pointer-events: none;
            z-index: -1;
            animation: floatOrb linear infinite;
        }

        @keyframes floatOrb {
            0% { transform: translate3d(0,110vh,0) scale(.5); opacity: 0; }
            20% { opacity: .5; }
            80% { opacity: .35; }
            100% { transform: translate3d(90px,-15vh,0) scale(1.2); opacity: 0; }
        }

        .live-clock {
            margin-top: 16px;
            color: #64748b;
            font-size: .82rem;
            letter-spacing: .5px;
        }

        @media (max-width: 700px) {
            body { padding: 14px; }
            .quick-nav { right: 10px; bottom: 10px; }
            .quick-nav button { width: 42px; height: 42px; }
        }
    </style>
</head>
<body>
    <div class="scroll-progress" id="scrollProgress"></div>
    <div class="quick-nav" aria-label="Швидка навігація">
        <button type="button" id="toTop" title="На початок">↑</button>
        <button type="button" id="toBottom" title="До низу">↓</button>
    </div>
    <div class="float-orb" style="left:12%;animation-duration:18s;animation-delay:-5s"></div>
    <div class="float-orb" style="left:35%;animation-duration:23s;animation-delay:-11s"></div>
    <div class="float-orb" style="left:67%;animation-duration:20s;animation-delay:-8s"></div>
    <div class="float-orb" style="left:88%;animation-duration:26s;animation-delay:-16s"></div>

    <div class="bg-glow-orb orb-1"></div>
    <div class="bg-glow-orb orb-2"></div>

    <div class="portal-container">
        <header class="portal-header animate-on-scroll">
            <h1>Офіційний Портал Судової Системи Ukraine RP</h1>
            <p>Централізована інформаційна система державних судових розглядів, нормативних актів та професійних івентів.</p>
            <div class="live-clock">🕘 Локальний час: <span id="liveClock">--:--:--</span></div>
        </header>

        <section class="content-section animate-on-scroll">
            <h2 class="section-title">⚖️ Склад Верховного Суду</h2>
            <p class="section-description">Список діючих суддів та керівного складу державних інстанцій.</p>
            <div class="staff-grid">
                <article class="staff-profile-card">
                    <h3>Олександр Шевченко</h3>
                    <span class="staff-badge">Верховний Суддя</span>
                    <div class="staff-contacts">
                        Roblox: Alex_Court<br>
                        TG: <a href="https://t.me/" target="_blank">@alex_court_ur</a>
                    </div>
                </article>
                <article class="staff-profile-card">
                    <h3>Максим Коваль</h3>
                    <span class="staff-badge">Суддя Апеляційної інстанції</span>
                    <div class="staff-contacts">
                        Roblox: Koval_Judge<br>
                        TG: <a href="https://t.me/" target="_blank">@koval_ur</a>
                    </div>
                </article>
            </div>
        </section>

        <section class="blacklist-section content-section animate-on-scroll" id="blacklist">
            <h2 class="section-title blacklist-title">🚫 Чорний список</h2>
            <p class="section-description">Офіційний запис про звільненого учасника.</p>
            <div class="blacklist-grid">
                <article class="blacklist-card premium-card">
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
            <h2 class="section-title">📈 Статистика розгляду справ</h2>
            <p class="section-description">Динаміка та аналітика ефективності судових засідань по місяцях.</p>
            
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
            <h2 class="section-title">📅 Майбутні івенти та заходи</h2>
            <p class="section-description">Беріть участь у відкритих сухих слуханнях та рольових тренуваннях разом із досвідченими суддями та адвокатами.</p>
            <ul>
                <li>Розбір реальних кейсів та процесуальних помилок.</li>
                <li>Унікальний ігровий досвід та гарний настрій.</li>
            </ul>
            <p style="margin-top: 15px;"><strong>Графік проведення івенту:</strong></p>
            <div class="event-schedule-container">
                <span class="schedule-badge">📅 09 число місяця</span>
                <span class="schedule-badge">📅 17 число місяця</span>
                <span class="schedule-badge">📅 29 число місяця</span>
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

            // ===== GLOBAL UX / EFFECTS =====
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

            // Ripple for buttons.
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

            // Gentle 3D tilt on premium cards.
            document.querySelectorAll('.staff-profile-card, .blacklist-card').forEach(card => {
                card.classList.add('premium-card');
                card.addEventListener('pointermove', (event) => {
                    const rect = card.getBoundingClientRect();
                    const x = (event.clientX - rect.left) / rect.width - .5;
                    const y = (event.clientY - rect.top) / rect.height - .5;
                    card.style.transform = `perspective(900px) rotateX(${-y * 5}deg) rotateY(${x * 5}deg) translateY(-6px)`;
                });
                card.addEventListener('pointerleave', () => {
                    card.style.transform = '';
                });
            });

            // Live clock.
            const clock = document.getElementById('liveClock');
            if (clock) {
                const updateClock = () => {
                    clock.textContent = new Date().toLocaleTimeString('uk-UA');
                };
                updateClock();
                setInterval(updateClock, 1000);
            }

            // Налаштування та запуск графіка з плавною анімацією та логікою 12-секундного збою
            const ctx = document.getElementById('courtStockChart').getContext('2d');
            const chartGradient = ctx.createLinearGradient(0, 0, 0, 400);
            chartGradient.addColorStop(0, 'rgba(14, 165, 233, 0.55)');
            chartGradient.addColorStop(1, 'rgba(14, 165, 233, 0.0)');

            const normalData = [210, 260, 329, 390, 440, 570, 573, 640, 710];
            const glitchData = [120, 450, 150, 680, 220, 890, 950, 310, 840];

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
                        duration: 2000,
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

            // Логіка 12-секундного сильного збою системи на біржі/графіку
            const statusPill = document.getElementById('marketStatusPill');
            const statusText = document.getElementById('marketStatusText');

            setTimeout(() => {
                // Вмикаємо збій
                courtChart.data.datasets[0].data = glitchData;
                courtChart.data.datasets[0].borderColor = '#ef4444';
                courtChart.update();

                statusPill.classList.add('glitch-mode');
                statusText.textContent = '⚠️ УВАГА: КРИТИЧНИЙ ЗБІЙ СИСТЕМИ ДАНИХ!';

                // Через 12 секунд повертаємо все у нормальний стан
                setTimeout(() => {
                    courtChart.data.datasets[0].data = normalData;
                    courtChart.data.datasets[0].borderColor = '#38bdf8';
                    courtChart.update();

                    statusPill.classList.remove('glitch-mode');
                    statusText.textContent = 'ЗБІЙ СИСТЕМИ ПРОЙШОВ — ТЕПЕР ВОНА СТАБІЛЬНА';
                }, 12000);
            }, 3000);
        });
    </script>
</body>
</html>

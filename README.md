<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Офіційний Портал Судової Системи Ukraine RP</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --bg-dark: #0b1329;
            --card-bg: #0f172a;
            --accent-blue: #38bdf8;
            --danger-red: #ef4444;
            --text-light: #f8fafc;
            --text-muted: #94a3b8;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            font-family: 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 20px;
        }

        .portal-container {
            max-width: 1200px;
            margin: 0 auto;
        }

        /* Повільна анімація появи при скролі (20 секунд) */
        .animate-on-scroll {
            opacity: 0;
            transform: translateY(40px);
            transition: all 20s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* Плавні переходи 20с для інтерактивних елементів */
        .court-card, .dropdown-panel, .schedule-badge, .btn-action, .blacklist-card {
            transition: all 20s ease-in-out !important;
        }

        /* Випадаючі панелі */
        .dropdown-toggle-btn {
            background: rgba(15, 23, 42, 0.8);
            color: var(--text-light);
            border: 1px solid rgba(56, 189, 248, 0.3);
            padding: 12px 20px;
            width: 100%;
            text-align: left;
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 1rem;
            margin-top: 10px;
        }

        .dropdown-panel {
            max-height: 0;
            overflow: hidden;
            background: rgba(15, 23, 42, 0.5);
            border-radius: 0 0 8px 8px;
            padding: 0 20px;
        }

        .dropdown-panel.expanded {
            max-height: 1000px;
            padding: 20px;
            border: 1px solid rgba(56, 189, 248, 0.2);
            border-top: none;
        }

        /* Контейнер графіка з переливанням кольорів рамки */
        .chart-container {
            position: relative;
            height: 400px;
            width: 100%;
            background: rgba(15, 23, 42, 0.8);
            border-radius: 16px;
            padding: 20px;
            border: 1px solid rgba(56, 189, 248, 0.2);
            margin: 30px 0;
            animation: chartBorderHue 20s infinite alternate linear;
        }

        @keyframes chartBorderHue {
            0% { border-color: #38bdf8; box-shadow: 0 0 15px rgba(56, 189, 248, 0.3); }
            33% { border-color: #a855f7; box-shadow: 0 0 15px rgba(168, 85, 247, 0.3); }
            66% { border-color: #ec4899; box-shadow: 0 0 15px rgba(236, 72, 153, 0.3); }
            100% { border-color: #3b82f6; box-shadow: 0 0 15px rgba(59, 130, 246, 0.3); }
        }

        /* Сітка карток */
        .judges-grid, .blacklist-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin: 20px 0;
        }

        .court-card, .blacklist-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 20px;
            width: 280px;
            text-align: center;
        }

        .court-card:hover {
            border-color: var(--accent-blue);
            transform: translateY(-5px);
        }

        .role-badge {
            display: inline-block;
            background: rgba(56, 189, 248, 0.15);
            color: var(--accent-blue);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            margin: 8px 0;
        }

        /* Чорний список */
        .blacklist-section {
            margin-top: 40px;
            padding: 24px;
            background: rgba(239, 68, 68, 0.05);
            border: 1px solid rgba(239, 68, 68, 0.2);
            border-radius: 16px;
        }

        .blacklist-title {
            color: var(--danger-red);
            font-size: 1.5rem;
            margin-bottom: 20px;
        }

        .blacklist-card {
            border-color: rgba(239, 68, 68, 0.4);
        }

        .blacklist-card:hover {
            border-color: var(--danger-red);
            box-shadow: 0 0 20px rgba(239, 68, 68, 0.2);
        }

        .blacklist-badge {
            display: inline-block;
            background: rgba(239, 68, 68, 0.2);
            color: #f87171;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            margin: 8px 0;
        }

        .tg-link {
            color: var(--accent-blue);
            text-decoration: none;
        }

        .event-schedule-container {
            display: flex;
            gap: 10px;
            margin: 15px 0;
        }

        .schedule-badge {
            background: rgba(255, 255, 255, 0.05);
            padding: 8px 14px;
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        footer {
            margin-top: 50px;
            text-align: center;
            color: var(--text-muted);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            padding-top: 20px;
        }
    </style>
</head>
<body>

    <div class="portal-container">

        <section class="animate-on-scroll">
            <h3>📈 Статистика та динаміка судової системи</h3>
            <div class="chart-container">
                <canvas id="courtStockChart"></canvas>
            </div>
        </section>

        <section class="animate-on-scroll">
            <button class="dropdown-toggle-btn">
                <span>Переваги та графік івенту</span>
                <span>▼</span>
            </button>
            <div class="dropdown-panel">
                <ul>
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
        </section>

        <section class="animate-on-scroll" style="margin-top: 30px;">
            <h3>⚖️ Діючий суддівський склад</h3>
            <div class="judges-grid">
                <div class="court-card">
                    <div class="card-avatar-wrapper">
                        <span style="font-size: 2.5rem;">📜</span>
                    </div>
                    <h3 class="judge-name">svervanchick <a href="#" class="tg-link">🔗</a></h3>
                    <span class="role-badge">СУДДЯ</span>
                    <div class="card-details">
                        <p>Roblox: svervanchick</p>
                        <p>TG: <a href="https://t.me/Svervanchick" target="_blank" class="tg-link">@Svervanchick</a></p>
                    </div>
                </div>
            </div>
        </section>

        <section class="blacklist-section animate-on-scroll">
            <h3 class="blacklist-title">🚫 Чорний список суддів</h3>
            <div class="blacklist-grid">
                <div class="blacklist-card">
                    <div class="card-avatar-wrapper">
                        <span style="font-size: 2.5rem;">🔍</span>
                    </div>
                    <h4 class="judge-name">heehrhrhl18</h4>
                    <span class="blacklist-badge">ЗВІЛЬНЕНО / ЧОРНИЙ СПИСОК</span>
                    <div class="card-details">
                        <p>Roblox: heehrhrhl18</p>
                        <p>TG: <a href="https://t.me/hehr18_UR" target="_blank" class="tg-link" style="color: #f87171;">@hehr18_UR</a></p>
                    </div>
                </div>
            </div>
        </section>

        <section class="owner-news-branch animate-on-scroll" style="margin-top: 30px;">
            <h3>📢 Новини та оновлення від керівництва суду</h3>
            <p>У цій гілці суд та власник сайту публікують актуальні внутрішні новини, майбутні оновлення судової системи, а також корисні поради щодо покращення рольової гри на сервері. Слідкуйте за оновленнями порталу, щоб бути в курсі найважливіших державних подій Ukraine RP!</p>
        </section>

        <footer class="portal-footer animate-on-scroll">
            <p>&copy; 2026 Офіційний Портал Судової Системи Ukraine RP. Усі права захищені.</p>
        </footer>

    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function() {
            // Анімація видимості елементів при скролі (20s)
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

            // Обробка випадаючих списків
            const dropdownBtns = document.querySelectorAll('.dropdown-toggle-btn');
            dropdownBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    const panel = this.nextElementSibling;
                    const arrowSpan = this.querySelector('span:last-child');
                    
                    panel.classList.toggle('expanded');
                    arrowSpan.textContent = panel.classList.contains('expanded') ? '▲' : '▼';
                });
            });

            // Налаштування та анімація графіка
            const ctx = document.getElementById('courtStockChart').getContext('2d');
            const finalData = [210, 260, 329, 390, 440, 570, 573, 640, 710];
            const labels = ['Січень', 'Лютий', 'Березень', 'Квітень', 'Травень', 'Червень', 'Липень', 'Серпень (+)', 'Вересень (План)'];

            const courtChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Динаміка успішно розглянутих справ (+ стабільний ріст)',
                        data: [150, 480, 200, 550, 280, 680, 350, 620, 710], // Початковий рух
                        borderColor: '#38bdf8',
                        borderWidth: 4,
                        pointBackgroundColor: '#818cf8',
                        pointBorderColor: '#ffffff',
                        pointRadius: 6,
                        fill: true,
                        backgroundColor: 'rgba(56, 189, 248, 0.25)',
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    animation: {
                        duration: 20000, // Загальна тривалість 20 секунд
                        easing: 'easeOutElastic'
                    },
                    plugins: {
                        legend: { labels: { color: '#f8fafc' } }
                    },
                    scales: {
                        x: { grid: { color: 'rgba(30, 41, 59, 0.5)' }, ticks: { color: '#94a3b8' } },
                        y: { grid: { color: 'rgba(30, 41, 59, 0.5)' }, ticks: { color: '#94a3b8' } }
                    }
                }
            });

            // Зміна кольорів лінії біржі
            let colorHue = 0;
            const colorTimer = setInterval(() => {
                colorHue = (colorHue + 12) % 360;
                courtChart.data.datasets[0].borderColor = `hsl(${colorHue}, 100%, 65%)`;
                courtChart.data.datasets[0].backgroundColor = `hsla(${colorHue}, 100%, 50%, 0.25)`;
                courtChart.update('none');
            }, 250);

            // Ефект "стрибаючої" лінії
            const bounceTimer = setInterval(() => {
                courtChart.data.datasets[0].data = courtChart.data.datasets[0].data.map(val => {
                    return val + (Math.random() * 90 - 45);
                });
                courtChart.update();
            }, 1000);

            // Через 15 секунд лінія заспокоюється і стає на фінальні місця
            setTimeout(() => {
                clearInterval(bounceTimer);
                courtChart.data.datasets[0].data = finalData;
                courtChart.data.datasets[0].borderColor = '#38bdf8';
                courtChart.data.datasets[0].backgroundColor = 'rgba(56, 189, 248, 0.3)';
                courtChart.update({
                    duration: 5000,
                    easing: 'easeInOutQuart'
                });
            }, 15000);

            // Зупинка зміни кольорів на 20 секунді
            setTimeout(() => {
                clearInterval(colorTimer);
            }, 20000);
        });
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Елітний Портал | Екосистема та Біржа</title>
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
            --transition-speed: 0.4s;
        }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: radial-gradient(circle at 50% 0%, #0c1836 0%, #020617 70%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.7;
            padding: 30px;
            overflow-x: hidden;
            min-height: 100vh;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: -200px;
            left: -200px;
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, rgba(14, 165, 233, 0.18) 0%, transparent 70%);
            filter: blur(80px);
            border-radius: 50%;
            z-index: -1;
            animation: floatGlow1 12s ease-in-out infinite alternate;
        }

        body::after {
            content: '';
            position: fixed;
            bottom: -200px;
            right: -200px;
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, rgba(129, 140, 248, 0.15) 0%, transparent 70%);
            filter: blur(90px);
            border-radius: 50%;
            z-index: -1;
            animation: floatGlow2 15s ease-in-out infinite alternate-reverse;
        }

        @keyframes floatGlow1 {
            0% { transform: translate(0, 0) scale(1); opacity: 0.7; }
            100% { transform: translate(100px, 80px) scale(1.3); opacity: 1; }
        }

        @keyframes floatGlow2 {
            0% { transform: translate(0, 0) scale(1); opacity: 0.7; }
            100% { transform: translate(-120px, -90px) scale(1.25); opacity: 1; }
        }

        .main-container {
            max-width: 1300px;
            margin: 0 auto;
        }

        .portal-header {
            background: linear-gradient(135deg, rgba(9, 15, 29, 0.92) 0%, rgba(18, 30, 60, 0.92) 100%);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(56, 189, 248, 0.3);
            border-bottom: 5px solid var(--accent-blue);
            padding: 40px 25px;
            text-align: center;
            border-radius: 24px;
            margin-bottom: 35px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.75), 0 0 30px rgba(14, 165, 233, 0.15), inset 0 1px 0 rgba(255, 255, 255, 0.1);
        }

        .portal-header h1 {
            font-size: clamp(1.8rem, 3.5vw, 2.6rem);
            background: linear-gradient(135deg, #38bdf8 0%, #ffffff 50%, #818cf8 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
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
            background: linear-gradient(135deg, rgba(11, 20, 45, 0.95) 0%, rgba(20, 28, 79, 0.95) 100%);
            backdrop-filter: blur(16px);
            border: 2px solid var(--accent-blue);
            border-radius: 26px;
            padding: 45px 35px;
            margin-bottom: 35px;
            text-align: center;
            box-shadow: 0 0 60px rgba(14, 165, 233, 0.3), inset 0 0 30px rgba(56, 189, 248, 0.15);
        }

        .hero-info-box h2 {
            font-size: clamp(2.2rem, 5vw, 3.6rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 3px;
            background: linear-gradient(135deg, #38bdf8 0%, #818cf8 50%, #c084fc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 18px;
            filter: drop-shadow(0 0 30px rgba(56, 189, 248, 0.6));
        }

        .hero-info-box p {
            color: #cbd5e1;
            font-size: 1.18rem;
            max-width: 950px;
            margin: 0 auto 15px auto;
            line-height: 1.8;
        }

        .content-section {
            background: linear-gradient(135deg, rgba(13, 21, 39, 0.92) 0%, rgba(7, 12, 24, 0.92) 100%);
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

        .stock-metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .stock-metric-card {
            background: linear-gradient(135deg, #101c3d 0%, #070d1f 100%);
            border: 1px solid rgba(56, 189, 248, 0.3);
            border-radius: 18px;
            padding: 22px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
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
            text-shadow: 0 0 15px rgba(255,255,255,0.2);
        }

        .stock-badge-positive {
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
            text-shadow: 0 0 10px rgba(34, 197, 94, 0.4);
        }

        .chart-box-wrapper {
            position: relative;
            width: 100%;
            height: 480px;
            background: linear-gradient(135deg, #070d1f 0%, #030612 100%);
            padding: 25px;
            border-radius: 20px;
            border: 1px solid rgba(56, 189, 248, 0.3);
            box-shadow: inset 0 0 35px rgba(0,0,0,0.8), 0 0 40px rgba(14, 165, 233, 0.15);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Анімація коливання графіка протягом 20 секунд */
        .market-chart-svg {
            width: 100%;
            height: 100%;
            overflow: visible;
        }

        .animated-market-line {
            stroke: var(--accent-blue);
            stroke-width: 3.5;
            fill: none;
            filter: drop-shadow(0 0 10px rgba(14, 165, 233, 0.7));
            animation: chartStabilizeAnimation 20s cubic-bezier(0.25, 1, 0.5, 1) forwards;
        }

        @keyframes chartStabilizeAnimation {
            0% {
                d: path("M 0 300 Q 150 100 300 350 T 600 50 T 900 400 T 1200 200");
                opacity: 0.3;
            }
            15% {
                d: path("M 0 250 Q 150 350 300 100 T 600 400 T 900 150 T 1200 280");
            }
            35% {
                d: path("M 0 320 Q 150 150 300 280 T 600 120 T 900 320 T 1200 220");
            }
            60% {
                d: path("M 0 280 Q 150 220 300 300 T 600 180 T 900 260 T 1200 240");
            }
            85% {
                d: path("M 0 260 Q 150 240 300 270 T 600 220 T 900 240 T 1200 250");
                opacity: 0.9;
            }
            100% {
                d: path("M 0 250 Q 150 230 300 250 T 600 230 T 900 245 T 1200 240");
                opacity: 1;
            }
        }

        .staff-grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
            gap: 24px;
            margin-top: 25px;
            justify-content: center;
        }

        .staff-profile-card {
            background: linear-gradient(135deg, #131e3b 0%, #080f24 100%);
            border: 1px solid var(--border-primary);
            padding: 35px 22px;
            border-radius: 20px;
            text-align: center;
            transition: transform 0.4s ease, border-color 0.4s ease, box-shadow 0.4s ease;
            position: relative;
            overflow: hidden;
            max-width: 350px;
            margin: 0 auto;
            width: 100%;
        }

        .staff-profile-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 5px;
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
            margin: 0 auto 20px auto;
            position: relative;
            border-radius: 50%;
            padding: 3px;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
        }

        .staff-avatar-wrapper img {
            width: 100%; height: 100%; object-fit: cover; border-radius: 50%; border: 3px solid var(--bg-card); display: block;
        }

        .staff-profile-card h3 { font-size: 1.35rem; margin-bottom: 8px; color: var(--text-main); }
        .staff-role-badge { color: var(--accent-blue); font-size: 0.8rem; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 16px; display: inline-block; background: rgba(14, 165, 233, 0.15); padding: 6px 16px; border-radius: 20px; border: 1px solid rgba(14, 165, 233, 0.3); }
        .staff-contacts-info { font-size: 0.95rem; color: var(--text-muted); word-break: break-all; }
        .staff-contacts-info a { color: var(--accent-blue); text-decoration: none; font-weight: 600; }
        .staff-contacts-info a:hover { color: var(--accent-blue-hover); text-decoration: underline; }

        /* Гілка ідей (Interactive Ideas Branch) */
        .ideas-form {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
            margin-bottom: 30px;
        }

        .ideas-input, .ideas-textarea {
            background: rgba(7, 13, 31, 0.8);
            border: 1px solid var(--border-primary);
            border-radius: 12px;
            padding: 14px 18px;
            color: var(--text-main);
            font-size: 1rem;
            outline: none;
            transition: border-color 0.3s ease;
        }

        .ideas-input:focus, .ideas-textarea:focus {
            border-color: var(--accent-blue);
            box-shadow: 0 0 15px rgba(14, 165, 233, 0.2);
        }

        .ideas-textarea {
            resize: vertical;
            min-height: 100px;
        }

        .ideas-submit-btn {
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            color: #ffffff;
            border: none;
            padding: 14px 24px;
            border-radius: 12px;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            transition: opacity 0.3s ease, transform 0.2s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .ideas-submit-btn:hover {
            opacity: 0.9;
            transform: translateY(-2px);
        }

        .ideas-list-container {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .idea-card {
            background: rgba(11, 19, 41, 0.85);
            border: 1px solid rgba(56, 189, 248, 0.2);
            border-radius: 14px;
            padding: 20px;
            position: relative;
            animation: fadeInIdea 0.5s ease;
        }

        @keyframes fadeInIdea {
            from { opacity: 0; transform: translateY(15px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .idea-card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }

        .idea-author {
            font-weight: 700;
            color: var(--accent-blue);
            font-size: 1.05rem;
        }

        .idea-date {
            font-size: 0.85rem;
            color: var(--text-muted);
        }

        .idea-text {
            color: #cbd5e1;
            font-size: 0.98rem;
            margin-bottom: 12px;
        }

        .idea-vote-section {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .vote-btn {
            background: rgba(14, 165, 233, 0.15);
            border: 1px solid rgba(14, 165, 233, 0.3);
            color: var(--accent-blue);
            padding: 6px 14px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.2s;
        }

        .vote-btn:hover {
            background: rgba(14, 165, 233, 0.3);
        }

        .portal-footer {
            text-align: center; padding: 30px 20px; background: linear-gradient(135deg, #0d1527 0%, #070c1a 100%); border: 1px solid var(--border-primary); border-radius: 20px; color: var(--text-muted); font-size: 0.95rem; margin-top: 35px;
        }
    </style>
</head>
<body>

    <div class="main-container">
        
        <header class="portal-header">
            <h1>Елітна Екосистема Порталу</h1>
            <p>Централізований інформаційний хаб, аналітика та управління проєктами</p>
        </header>

        <section class="hero-info-box">
            <h2>Статус: Активно</h2>
            <p>Ласкаво просимо до оновленого простору високих технологій, фінансової стабільності та колективного розвитку.</p>
        </section>

        <section class="content-section">
            <h2 class="section-title">Фінансова Біржа та Ринкова Динаміка</h2>
            <p class="section-description">Спостереження за стабілізацією ринкових індикаторів у режимі реального часу.</p>
            
            <div class="stock-metrics-grid">
                <div class="stock-metric-card">
                    <div class="stock-metric-title">Індекс Актива</div>
                    <div class="stock-metric-value">1,482.90</div>
                    <span class="stock-badge-positive">+4.8% (Стабільно)</span>
                </div>
                <div class="stock-metric-card">
                    <div class="stock-metric-title">Ліквідність ринку</div>
                    <div class="stock-metric-value">$84.2M</div>
                    <span class="stock-badge-positive">+12.1%</span>
                </div>
            </div>

            <div class="chart-box-wrapper">
                <svg class="market-chart-svg" viewBox="0 0 1200 400" preserveAspectRatio="none">
                    <path class="animated-market-line" d="M 0 300 Q 150 100 300 350 T 600 50 T 900 400 T 1200 200" />
                </svg>
            </div>
        </section>

        <section class="content-section">
            <h2 class="section-title">Керівний склад</h2>
            <p class="section-description">Головний координатор та підтримка екосистеми.</p>
            
            <div class="staff-grid-container">
                <div class="staff-profile-card">
                    <div class="staff-avatar-wrapper">
                        <div class="avatar-fallback">⚡</div>
                    </div>
                    <h3>Mr_Zver3000</h3>
                    <span class="staff-role-badge">Суддя</span>
                    <div class="staff-contacts-info">
                        Roblox: Mr_Zver3000<br>
                        TG: <a href="https://t.me/GreyFild_OFF" target="_blank">@GreyFild_OFF</a>
                    </div>
                </div>
            </div>
        </section>

        <section class="content-section">
            <h2 class="section-title">Гілка Ідей та Пропозицій</h2>
            <p class="section-description">Маєте ідею для покращення проєкту? Поділіться нею нижче, і інші учасники зможуть оцінити її проголосувавши!</p>
            
            <div class="ideas-form">
                <input type="text" id="ideaAuthorInput" class="ideas-input" placeholder="Ваше ім'я або нікнейм">
                <textarea id="ideaTextInput" class="ideas-textarea" placeholder="Опишіть вашу ідею детально..."></textarea>
                <button type="button" class="ideas-submit-btn" onclick="submitIdea()">Опублікувати ідею</button>
            </div>

            <div class="ideas-list-container" id="ideasContainer">
                <div class="idea-card">
                    <div class="idea-card-header">
                        <span class="idea-author">CyberUser</span>
                        <span class="idea-date">Сьогодні</span>
                    </div>
                    <div class="idea-text">Було б круто додати темну та світлу тему для зручності перегляду вночі.</div>
                    <div class="idea-vote-section">
                        <button class="vote-btn" onclick="voteIdea(this)">👍 Підтримати (<span class="vote-count">12</span>)</button>
                    </div>
                </div>
            </div>
        </section>

        <footer class="portal-footer">
            <p>&copy; 2026 Елітний Портал. Усі права захищені.</p>
        </footer>

    </div>

    <script>
        // Скрипт для роботи Гілки Ідей (додавання та голосування)
        function submitIdea() {
            const authorInput = document.getElementById('ideaAuthorInput');
            const textInput = document.getElementById('ideaTextInput');
            const container = document.getElementById('ideasContainer');

            const author = authorInput.value.trim();
            const text = textInput.value.trim();

            if (!author || !text) {
                alert('Будь ласка, заповніть усі поля перед відправкою ідеї!');
                return;
            }

            const card = document.createElement('div');
            card.className = 'idea-card';
            card.innerHTML = `
                <div class="idea-card-header">
                    <span class="idea-author">${escapeHtml(author)}</span>
                    <span class="idea-date">Щойно</span>
                </div>
                <div class="idea-text">${escapeHtml(text)}</div>
                <div class="idea-vote-section">
                    <button class="vote-btn" onclick="voteIdea(this)">👍 Підтримати (<span class="vote-count">1</span>)</button>
                </div>
            `;

            container.prepend(card);

            // Очищення полів
            authorInput.value = '';
            textInput.value = '';
        }

        function voteIdea(button) {
            const countSpan = button.querySelector('.vote-count');
            let currentVotes = parseInt(countSpan.textContent);
            countSpan.textContent = currentVotes + 1;
            button.disabled = true;
            button.style.opacity = '0.7';
        }

        function escapeHtml(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>

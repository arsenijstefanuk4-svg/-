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

    .animate-on-scroll {
        opacity: 0;
        transform: translateY(40px);
        transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .animate-on-scroll.visible {
        opacity: 1;
        transform: translateY(0);
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

    /* ПОКРАЩЕНА БІРЖА ТА АКТИВНІСТЬ */
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
        height: 480px; /* Зробили графік вищим і довшим */
        background: linear-gradient(135deg, #070d1f 0%, #030612 100%);
        padding: 25px;
        border-radius: 20px;
        border: 1px solid rgba(56, 189, 248, 0.3);
        box-shadow: inset 0 0 35px rgba(0,0,0,0.8), 0 0 40px rgba(14, 165, 233, 0.15);
    }

    /* Стилі для випадаючих списків */
    .dropdown-element {
        margin-top: 16px;
    }

    .dropdown-toggle-btn {
        background: linear-gradient(135deg, #131d38 0%, #0a1124 100%);
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
        background: linear-gradient(135deg, #1c2d56 0%, #111a35 100%);
        border-color: var(--accent-blue);
        transform: translateY(-2px);
    }

    .dropdown-panel {
        max-height: 0;
        overflow: hidden;
        transition: max-height 0.45s cubic-bezier(0.4, 0, 0.2, 1), padding 0.3s ease;
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

    .dropdown-panel p, .dropdown-panel ul {
        color: #d1d5db;
        font-size: 0.98rem;
        margin-bottom: 12px;
    }

    .dropdown-panel ul { padding-left: 22px; }
    .dropdown-panel li { margin-bottom: 8px; }

    .notice-box {
        background: rgba(14, 165, 233, 0.12);
        border-left: 4px solid var(--accent-blue);
        padding: 16px;
        margin-top: 18px;
        border-radius: 0 12px 12px 0;
        font-size: 0.95rem;
        color: #ffffff;
    }

    .staff-grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
        gap: 24px;
        margin-top: 25px;
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

    .avatar-fallback {
        width: 100%; height: 100%; border-radius: 50%; background: #0f172a; display: flex; align-items: center; justify-content: center; font-size: 2.4rem; border: 3px solid var(--bg-card); color: var(--accent-blue);
    }

    .staff-profile-card h3 { font-size: 1.35rem; margin-bottom: 8px; color: var(--text-main); }
    .staff-role-badge { color: var(--accent-blue); font-size: 0.8rem; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 16px; display: inline-block; background: rgba(14, 165, 233, 0.15); padding: 6px 16px; border-radius: 20px; border: 1px solid rgba(14, 165, 233, 0.3); }
    .staff-contacts-info { font-size: 0.95rem; color: var(--text-muted); word-break: break-all; }
    .staff-contacts-info a { color: var(--accent-blue); text-decoration: none; font-weight: 600; }
    .staff-contacts-info a:hover { color: var(--accent-blue-hover); text-decoration: underline; }

    .table-box-wrapper {
        width: 100%; overflow-x: auto; margin-top: 25px; border-radius: 20px; border: 1px solid var(--border-primary); background-color: var(--bg-secondary);
    }

    .analytics-table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.98rem; white-space: nowrap; }
    .analytics-table th, .analytics-table td { padding: 18px 22px; border-bottom: 1px solid var(--border-primary); color: #f8fafc !important; }
    .analytics-table th { background-color: #111d38 !important; color: var(--accent-blue) !important; font-weight: 600; text-transform: uppercase; font-size: 0.82rem; letter-spacing: 1px; }
    .analytics-table tbody tr { background-color: #070d1b !important; }
    .analytics-table tr:nth-child(even) { background-color: #0a1226 !important; }
    .analytics-table tr:hover { background-color: rgba(14, 165, 233, 0.2) !important; }

    .status-up { color: var(--success-color); font-weight: bold; }
    .status-stable { color: var(--accent-blue); font-weight: bold; }

    .event-detailed-card {
        background: linear-gradient(135deg, rgba(14, 165, 233, 0.15), rgba(13, 21, 39, 0.98));
        border: 1px solid var(--accent-blue); border-radius: 20px; padding: 32px; margin-top: 30px; box-shadow: 0 0 40px rgba(14, 165, 233, 0.3);
    }
    .event-detailed-card h3 { color: var(--accent-blue); font-size: 1.5rem; margin-bottom: 14px; display: flex; align-items: center; gap: 12px; }
    .event-detailed-card p { color: #d1d5db; font-size: 1rem; margin-bottom: 16px; line-height: 1.7; }
    .event-benefits-list { list-style-type: none; padding-left: 0; margin-bottom: 22px; }
    .event-benefits-list li { position: relative; padding-left: 26px; margin-bottom: 10px; color: #e2e8f0; font-size: 0.98rem; }
    .event-benefits-list li::before { content: "✔"; position: absolute; left: 0; color: var(--success-color); font-weight: bold; }
    .event-schedule-container { display: flex; gap: 14px; flex-wrap: wrap; margin-top: 18px; border-top: 1px solid var(--border-primary); padding-top: 18px; }
    .schedule-badge { background: #111d38; border: 1px solid var(--accent-blue); color: #ffffff; padding: 12px 20px; border-radius: 14px; font-weight: bold; font-size: 1.02rem; }

    .owner-news-branch {
        background: linear-gradient(135deg, #0d1527 0%, #070d1c 100%); border: 1px dashed var(--accent-blue); border-radius: 20px; padding: 32px; margin-top: 35px;
    }
    .owner-news-branch h3 { color: var(--accent-blue); font-size: 1.35rem; margin-bottom: 12px; display: flex; align-items: center; gap: 10px; }
    .owner-news-branch p { color: var(--text-muted); font-size: 0.98rem; margin-bottom: 12px; line-height: 1.7; }

    .portal-footer {
        text-align: center; padding: 30px 20px; background: linear-gradient(135deg, #0d1527 0%, #070c1a 100%); border: 1px solid var(--border-primary); border-radius: 20px; color: var(--text-muted); font-size: 0.95rem; margin-top: 35px;
    }
</style>

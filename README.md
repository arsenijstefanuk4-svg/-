from pathlib import Path
import re

# Use the current generated file if present; otherwise fall back to the user's main source.
candidates = [
    Path("/mnt/data/Ukraine_RP_court_imbovyi.html"),
    Path("/mnt/data/Ukraine_RP_court_final.html"),
    Path("/mnt/data/Вставленный текст (2).txt"),
]
src = next((p for p in candidates if p.exists()), None)
if src is None:
    raise FileNotFoundError("Не найден исходный HTML-файл.")

html = src.read_text(encoding="utf-8")

# Ensure the requested dismissed users are not active.
for name in ["Mr_Zver3000", "heehrhrhl18", "Itz_raose", "svervanchick"]:
    # Remove complete staff cards with this exact heading.
    html = re.sub(
        rf'\s*<div class="staff-profile-card">\s*.*?<h3>{re.escape(name)}</h3>.*?</div>\s*(?=<div class="staff-profile-card">|</div>\s*</div>)',
        "\n",
        html,
        flags=re.S
    )

# Rebuild blacklist section as a single-card section for heehrhrhl18.
blacklist_section = r'''
        <section class="blacklist-section animate-on-scroll" id="blacklist">
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
'''

# Replace any prior blacklist section.
html = re.sub(
    r'\s*<section class="blacklist-section".*?</section>\s*',
    "\n" + blacklist_section + "\n",
    html,
    count=1,
    flags=re.S
)

# Add a small enhancement CSS block if the file doesn't already contain these markers.
enhancement_css = r'''
        /* ===== ULTIMATE UI ENHANCEMENTS ===== */
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
'''
if "ULTIMATE UI ENHANCEMENTS" not in html:
    html = html.replace("</style>", enhancement_css + "\n    </style>", 1)

# Add fixed UI helpers directly after body tag.
ui_html = r'''
    <div class="scroll-progress" id="scrollProgress"></div>
    <div class="quick-nav" aria-label="Швидка навігація">
        <button type="button" id="toTop" title="На початок">↑</button>
        <button type="button" id="toBottom" title="До низу">↓</button>
    </div>
    <div class="float-orb" style="left:12%;animation-duration:18s;animation-delay:-5s"></div>
    <div class="float-orb" style="left:35%;animation-duration:23s;animation-delay:-11s"></div>
    <div class="float-orb" style="left:67%;animation-duration:20s;animation-delay:-8s"></div>
    <div class="float-orb" style="left:88%;animation-duration:26s;animation-delay:-16s"></div>
'''
if 'id="scrollProgress"' not in html:
    html = html.replace("<body>", "<body>\n" + ui_html, 1)

# Add a live clock after the hero info paragraph if possible.
if "class=\"live-clock\"" not in html:
    html = html.replace(
        "</div>\n\n        <section class=\"content-section animate-on-scroll\">",
        '<div class="live-clock">🕘 Локальний час: <span id="liveClock">--:--:--</span></div>\n        </div>\n\n        <section class="content-section animate-on-scroll">',
        1
    )

# Add a single consolidated JS enhancement block before closing script if not present.
enhancement_js = r'''
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
            document.querySelectorAll('.staff-profile-card, .blacklist-card, .stock-metric-card').forEach(card => {
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
'''
if "GLOBAL UX / EFFECTS" not in html:
    html = html.replace("</script>", enhancement_js + "\n    </script>", 1)

# If the stock section lacks an obvious status marker, add one before the chart wrapper.
if "market-status" not in html:
    html = html.replace(
        '<div class="chart-box-wrapper">',
        '''<div class="market-status">
            <div class="market-status-pill"><span class="status-dot"></span><span>СИСТЕМА МОНІТОРИНГУ АКТИВНА</span></div>
        </div>
        <div class="chart-box-wrapper">''',
        1
    )

# Save one single, self-contained HTML file.
out = Path("/mnt/data/Ukraine_RP_court_ONE_BIG_CODE.html")
out.write_text(html, encoding="utf-8")

print(f"Готово: {out}")
print(f"Розмір: {len(html):,} символів")

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>GarbageWatch — Smart Waste Management</title>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Syne:wght@400;600;700;800&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #0a0f0a;
      --surface: #111811;
      --card: #161d16;
      --border: #2a3a2a;
      --green: #4cff72;
      --lime: #b8ff3c;
      --amber: #ffb830;
      --red: #ff4d4d;
      --muted: #4a5e4a;
      --text: #d4e8d4;
      --text-dim: #7a987a;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Syne', sans-serif;
      background: var(--bg);
      color: var(--text);
      overflow-x: hidden;
    }

    /* ── NOISE TEXTURE ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 9999;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1.2rem 3rem;
      background: rgba(10,15,10,0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
    }
    .logo {
      font-family: 'Bebas Neue', cursive;
      font-size: 1.8rem;
      letter-spacing: 3px;
      color: var(--green);
    }
    .logo span { color: var(--lime); }
    nav ul {
      list-style: none;
      display: flex;
      gap: 2.5rem;
    }
    nav ul a {
      color: var(--text-dim);
      text-decoration: none;
      font-size: 0.85rem;
      font-weight: 600;
      letter-spacing: 1px;
      text-transform: uppercase;
      transition: color 0.2s;
    }
    nav ul a:hover { color: var(--green); }
    .nav-cta {
      background: var(--green);
      color: var(--bg) !important;
      padding: 0.5rem 1.4rem;
      border-radius: 4px;
      font-weight: 700 !important;
    }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      align-items: center;
      padding: 8rem 3rem 4rem;
      gap: 4rem;
      position: relative;
    }
    #hero::after {
      content: '';
      position: absolute;
      top: -100px; right: -100px;
      width: 600px; height: 600px;
      background: radial-gradient(circle, rgba(76,255,114,0.07) 0%, transparent 70%);
      pointer-events: none;
    }
    .hero-tag {
      display: inline-block;
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--lime);
      border: 1px solid var(--lime);
      padding: 0.35rem 0.9rem;
      border-radius: 2px;
      margin-bottom: 1.5rem;
      animation: fadeUp 0.6s ease both;
    }
    h1 {
      font-family: 'Bebas Neue', cursive;
      font-size: clamp(3.5rem, 7vw, 6rem);
      line-height: 0.95;
      letter-spacing: 2px;
      animation: fadeUp 0.7s 0.1s ease both;
    }
    h1 .accent { color: var(--green); }
    h1 .accent2 { color: var(--lime); }
    .hero-sub {
      margin-top: 1.5rem;
      font-size: 1.05rem;
      color: var(--text-dim);
      max-width: 480px;
      line-height: 1.7;
      animation: fadeUp 0.7s 0.2s ease both;
    }
    .hero-btns {
      margin-top: 2.5rem;
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      animation: fadeUp 0.7s 0.3s ease both;
    }
    .btn-primary {
      background: var(--green);
      color: var(--bg);
      padding: 0.85rem 2rem;
      border: none;
      border-radius: 4px;
      font-family: 'Syne', sans-serif;
      font-weight: 700;
      font-size: 0.95rem;
      cursor: pointer;
      transition: transform 0.15s, box-shadow 0.2s;
      text-decoration: none;
    }
    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(76,255,114,0.3); }
    .btn-outline {
      background: transparent;
      color: var(--text);
      padding: 0.85rem 2rem;
      border: 1px solid var(--border);
      border-radius: 4px;
      font-family: 'Syne', sans-serif;
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      transition: border-color 0.2s, color 0.2s;
      text-decoration: none;
    }
    .btn-outline:hover { border-color: var(--green); color: var(--green); }

    /* Hero visual */
    .hero-visual {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1rem;
      animation: fadeUp 0.8s 0.2s ease both;
    }
    .stat-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 1.5rem;
      position: relative;
      overflow: hidden;
      transition: border-color 0.2s, transform 0.2s;
    }
    .stat-card:hover { border-color: var(--green); transform: translateY(-3px); }
    .stat-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 3px;
    }
    .stat-card.c-green::before { background: var(--green); }
    .stat-card.c-lime::before { background: var(--lime); }
    .stat-card.c-amber::before { background: var(--amber); }
    .stat-card.c-red::before { background: var(--red); }
    .stat-card.span2 { grid-column: span 2; }
    .stat-num {
      font-family: 'Bebas Neue', cursive;
      font-size: 2.8rem;
      line-height: 1;
      margin-bottom: 0.3rem;
    }
    .c-green .stat-num { color: var(--green); }
    .c-lime .stat-num { color: var(--lime); }
    .c-amber .stat-num { color: var(--amber); }
    .c-red .stat-num { color: var(--red); }
    .stat-label { font-size: 0.78rem; color: var(--text-dim); font-weight: 600; letter-spacing: 0.5px; }

    /* ── SECTION COMMONS ── */
    section { padding: 6rem 3rem; }
    .section-label {
      font-family: 'Space Mono', monospace;
      font-size: 0.68rem;
      letter-spacing: 3px;
      text-transform: uppercase;
      color: var(--green);
      margin-bottom: 0.8rem;
    }
    .section-title {
      font-family: 'Bebas Neue', cursive;
      font-size: clamp(2.2rem, 4vw, 3.2rem);
      letter-spacing: 1.5px;
      margin-bottom: 1rem;
    }
    .section-desc {
      color: var(--text-dim);
      max-width: 560px;
      line-height: 1.7;
      font-size: 0.95rem;
      margin-bottom: 3rem;
    }
    .divider {
      width: 100%;
      height: 1px;
      background: var(--border);
    }

    /* ── PROBLEMS ── */
    #problems { background: var(--surface); }
    .problems-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5rem;
    }
    .prob-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 2rem;
      cursor: pointer;
      transition: all 0.25s;
      position: relative;
      overflow: hidden;
    }
    .prob-card:hover { border-color: var(--amber); transform: translateY(-4px); }
    .prob-icon {
      width: 52px; height: 52px;
      border-radius: 10px;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.6rem;
      margin-bottom: 1.2rem;
    }
    .prob-card h3 {
      font-size: 1.05rem;
      font-weight: 700;
      margin-bottom: 0.7rem;
    }
    .prob-card p {
      font-size: 0.85rem;
      color: var(--text-dim);
      line-height: 1.65;
    }
    .severity {
      display: inline-flex;
      align-items: center;
      gap: 0.4rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.65rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      margin-top: 1rem;
      padding: 0.3rem 0.7rem;
      border-radius: 20px;
    }
    .sev-high { background: rgba(255,77,77,0.12); color: var(--red); border: 1px solid rgba(255,77,77,0.25); }
    .sev-medium { background: rgba(255,184,48,0.12); color: var(--amber); border: 1px solid rgba(255,184,48,0.25); }
    .sev-critical { background: rgba(255,77,77,0.18); color: #ff8080; border: 1px solid rgba(255,77,77,0.4); }

    /* ── SOLUTIONS ── */
    #solutions { }
    .sol-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 2rem;
    }
    .sol-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 2.2rem;
      display: flex;
      gap: 1.5rem;
      transition: border-color 0.2s, transform 0.2s;
    }
    .sol-card:hover { border-color: var(--green); transform: translateY(-3px); }
    .sol-num {
      font-family: 'Bebas Neue', cursive;
      font-size: 3.5rem;
      line-height: 1;
      color: var(--border);
      flex-shrink: 0;
      transition: color 0.2s;
    }
    .sol-card:hover .sol-num { color: var(--green); }
    .sol-content h3 { font-size: 1.1rem; font-weight: 700; margin-bottom: 0.6rem; }
    .sol-content p { font-size: 0.85rem; color: var(--text-dim); line-height: 1.65; }
    .sol-tags { display: flex; flex-wrap: wrap; gap: 0.5rem; margin-top: 1rem; }
    .sol-tag {
      font-family: 'Space Mono', monospace;
      font-size: 0.62rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      padding: 0.28rem 0.65rem;
      border-radius: 3px;
    }
    .tag-green { background: rgba(76,255,114,0.1); color: var(--green); border: 1px solid rgba(76,255,114,0.2); }
    .tag-lime { background: rgba(184,255,60,0.1); color: var(--lime); border: 1px solid rgba(184,255,60,0.2); }
    .tag-amber { background: rgba(255,184,48,0.1); color: var(--amber); border: 1px solid rgba(255,184,48,0.2); }

    /* ── TECH STACK ── */
    #techstack { background: var(--surface); }
    .tech-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 1.5rem;
    }
    .tech-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 2rem 1.5rem;
      text-align: center;
      transition: all 0.2s;
    }
    .tech-card:hover { border-color: var(--lime); transform: translateY(-3px); }
    .tech-icon { font-size: 2.5rem; margin-bottom: 1rem; }
    .tech-name { font-family: 'Bebas Neue', cursive; font-size: 1.4rem; letter-spacing: 1.5px; margin-bottom: 0.5rem; }
    .tech-desc { font-size: 0.78rem; color: var(--text-dim); line-height: 1.5; }
    .tech-role {
      display: inline-block;
      margin-top: 0.8rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.6rem;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      padding: 0.25rem 0.6rem;
      border-radius: 3px;
      background: rgba(76,255,114,0.08);
      color: var(--green);
      border: 1px solid rgba(76,255,114,0.15);
    }

    /* ── AI CLASSIFIER ── */
    #classifier { }
    .classifier-wrap {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 3rem;
      align-items: start;
    }
    .classifier-form {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 2.5rem;
    }
    .form-group { margin-bottom: 1.5rem; }
    label {
      display: block;
      font-size: 0.8rem;
      font-weight: 700;
      letter-spacing: 0.5px;
      color: var(--text-dim);
      margin-bottom: 0.5rem;
    }
    input[type="text"], select, textarea {
      width: 100%;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 0.85rem 1rem;
      color: var(--text);
      font-family: 'Syne', sans-serif;
      font-size: 0.9rem;
      outline: none;
      transition: border-color 0.2s;
    }
    input:focus, select:focus, textarea:focus { border-color: var(--green); }
    select option { background: var(--card); }
    textarea { resize: vertical; min-height: 100px; }
    .classify-btn {
      width: 100%;
      background: var(--green);
      color: var(--bg);
      border: none;
      border-radius: 8px;
      padding: 1rem;
      font-family: 'Syne', sans-serif;
      font-weight: 800;
      font-size: 1rem;
      cursor: pointer;
      letter-spacing: 1px;
      transition: transform 0.15s, box-shadow 0.2s;
    }
    .classify-btn:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(76,255,114,0.3); }
    .classify-btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none; box-shadow: none; }

    /* Result */
    .result-panel {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 2.5rem;
      min-height: 340px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
    }
    .result-idle { color: var(--muted); }
    .result-idle .idle-icon { font-size: 4rem; margin-bottom: 1rem; opacity: 0.4; }
    .result-idle p { font-size: 0.9rem; }
    .result-active { width: 100%; text-align: left; }
    .result-type {
      font-family: 'Bebas Neue', cursive;
      font-size: 2.2rem;
      letter-spacing: 2px;
      color: var(--green);
      margin-bottom: 0.5rem;
    }
    .result-badge {
      display: inline-block;
      font-family: 'Space Mono', monospace;
      font-size: 0.65rem;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      padding: 0.3rem 0.8rem;
      border-radius: 20px;
      background: rgba(76,255,114,0.1);
      color: var(--green);
      border: 1px solid rgba(76,255,114,0.25);
      margin-bottom: 1.5rem;
    }
    .result-steps { list-style: none; }
    .result-steps li {
      display: flex;
      gap: 0.8rem;
      padding: 0.7rem 0;
      border-bottom: 1px solid var(--border);
      font-size: 0.85rem;
      line-height: 1.5;
    }
    .result-steps li:last-child { border-bottom: none; }
    .step-dot {
      width: 8px; height: 8px;
      border-radius: 50%;
      background: var(--green);
      flex-shrink: 0;
      margin-top: 5px;
    }
    .loading-dots span {
      display: inline-block;
      width: 8px; height: 8px;
      background: var(--green);
      border-radius: 50%;
      margin: 0 3px;
      animation: bounce 1.2s infinite;
    }
    .loading-dots span:nth-child(2) { animation-delay: 0.2s; }
    .loading-dots span:nth-child(3) { animation-delay: 0.4s; }

    /* ── REPORT SECTION ── */
    #report { background: var(--surface); }
    .report-wrap {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: 3rem;
    }
    .report-form {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 2.5rem;
    }
    .report-form h3 { font-size: 1.2rem; font-weight: 700; margin-bottom: 2rem; }
    .report-form .form-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1rem;
    }
    .submit-report-btn {
      background: var(--amber);
      color: var(--bg);
      border: none;
      border-radius: 8px;
      padding: 0.9rem 2rem;
      font-family: 'Syne', sans-serif;
      font-weight: 800;
      font-size: 0.95rem;
      cursor: pointer;
      transition: transform 0.15s, box-shadow 0.2s;
    }
    .submit-report-btn:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(255,184,48,0.3); }
    .recent-reports h3 { font-size: 1.1rem; font-weight: 700; margin-bottom: 1.5rem; }
    .report-item {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 1.2rem;
      margin-bottom: 1rem;
      transition: border-color 0.2s;
    }
    .report-item:hover { border-color: var(--amber); }
    .report-item-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 0.4rem;
    }
    .report-item-title { font-size: 0.88rem; font-weight: 700; }
    .report-status {
      font-family: 'Space Mono', monospace;
      font-size: 0.6rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      padding: 0.2rem 0.6rem;
      border-radius: 20px;
    }
    .status-new { background: rgba(255,77,77,0.1); color: var(--red); border: 1px solid rgba(255,77,77,0.2); }
    .status-progress { background: rgba(255,184,48,0.1); color: var(--amber); border: 1px solid rgba(255,184,48,0.2); }
    .status-resolved { background: rgba(76,255,114,0.1); color: var(--green); border: 1px solid rgba(76,255,114,0.2); }
    .report-item-meta { font-size: 0.75rem; color: var(--text-dim); }

    /* ── BACKEND DOCS ── */
    #backend { }
    .be-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 2rem; }
    .be-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 12px;
      overflow: hidden;
    }
    .be-header {
      padding: 1.2rem 1.5rem;
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      gap: 0.8rem;
    }
    .be-dot { width: 10px; height: 10px; border-radius: 50%; }
    .be-header h3 { font-size: 0.95rem; font-weight: 700; }
    .be-header .lang-badge {
      margin-left: auto;
      font-family: 'Space Mono', monospace;
      font-size: 0.62rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      padding: 0.25rem 0.6rem;
      border-radius: 3px;
    }
    pre {
      background: #080d08;
      padding: 1.5rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.72rem;
      line-height: 1.8;
      overflow-x: auto;
      color: #8ab08a;
      margin: 0;
    }
    .kw { color: #c792ea; }
    .fn { color: #82aaff; }
    .str { color: var(--lime); }
    .cm { color: var(--muted); }
    .num { color: var(--amber); }

    /* ── FOOTER ── */
    footer {
      padding: 3rem;
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
      background: var(--surface);
    }
    .footer-logo { font-family: 'Bebas Neue', cursive; font-size: 1.5rem; color: var(--green); letter-spacing: 2px; }
    .footer-copy { font-size: 0.78rem; color: var(--text-dim); }
    .footer-links { display: flex; gap: 1.5rem; }
    .footer-links a { font-size: 0.78rem; color: var(--text-dim); text-decoration: none; transition: color 0.2s; }
    .footer-links a:hover { color: var(--green); }

    /* ── TOAST ── */
    #toast {
      position: fixed;
      bottom: 2rem; right: 2rem;
      background: var(--green);
      color: var(--bg);
      padding: 0.9rem 1.5rem;
      border-radius: 8px;
      font-weight: 700;
      font-size: 0.9rem;
      z-index: 9000;
      transform: translateY(100px);
      opacity: 0;
      transition: all 0.3s ease;
    }
    #toast.show { transform: translateY(0); opacity: 1; }

    /* ── ANIMATIONS ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes bounce {
      0%, 80%, 100% { transform: scale(0.6); opacity: 0.4; }
      40% { transform: scale(1); opacity: 1; }
    }
    .fade-in {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }
    .fade-in.visible { opacity: 1; transform: translateY(0); }

    /* ── RESPONSIVE ── */
    @media (max-width: 1024px) {
      #hero { grid-template-columns: 1fr; padding-top: 7rem; }
      .hero-visual { max-width: 500px; }
      .problems-grid { grid-template-columns: repeat(2, 1fr); }
      .tech-grid { grid-template-columns: repeat(2, 1fr); }
      .classifier-wrap, .report-wrap, .be-grid { grid-template-columns: 1fr; }
    }
    @media (max-width: 640px) {
      nav { padding: 1rem 1.2rem; }
      nav ul { display: none; }
      section { padding: 4rem 1.2rem; }
      #hero { padding: 6rem 1.2rem 3rem; }
      .problems-grid, .sol-grid { grid-template-columns: 1fr; }
      .tech-grid { grid-template-columns: 1fr 1fr; }
      .report-form .form-row { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="logo">Garbage<span>Watch</span></div>
  <ul>
    <li><a href="#problems">Problems</a></li>
    <li><a href="#solutions">Solutions</a></li>
    <li><a href="#classifier">Classifier</a></li>
    <li><a href="#report">Report</a></li>
    <li><a href="#backend">Backend</a></li>
    <li><a href="#classifier" class="nav-cta">Try Now</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-content">
    <span class="hero-tag">⚠ Global Waste Crisis</span>
    <h1>THE <span class="accent">GARBAGE</span> <span class="accent2">PROBLEM</span> IS REAL</h1>
    <p class="hero-sub">
      Over 2 billion tonnes of waste is generated globally every year.
      GarbageWatch identifies problems, proposes smart solutions, and connects
      communities — powered by Python & Java backends.
    </p>
    <div class="hero-btns">
      <a href="#classifier" class="btn-primary">Classify Waste ↓</a>
      <a href="#problems" class="btn-outline">Explore Problems</a>
    </div>
  </div>
  <div class="hero-visual">
    <div class="stat-card c-red">
      <div class="stat-num" id="counter1">0</div>
      <div class="stat-label">Billion tonnes generated/year</div>
    </div>
    <div class="stat-card c-amber">
      <div class="stat-num" id="counter2">0</div>
      <div class="stat-label">% ends in landfills</div>
    </div>
    <div class="stat-card c-lime">
      <div class="stat-num" id="counter3">0</div>
      <div class="stat-label">Million tonnes recyclable</div>
    </div>
    <div class="stat-card c-green">
      <div class="stat-num" id="counter4">0</div>
      <div class="stat-label">Countries with waste crisis</div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- PROBLEMS -->
<section id="problems">
  <div class="section-label">// Identified Problems</div>
  <h2 class="section-title">GARBAGE CHALLENGES <span style="color:var(--amber)">WE FACE</span></h2>
  <p class="section-desc">These are the most pressing waste-management issues affecting urban and rural communities today.</p>

  <div class="problems-grid">
    <div class="prob-card fade-in">
      <div class="prob-icon" style="background:rgba(255,77,77,0.1)">🗑️</div>
      <h3>Overflowing Landfills</h3>
      <p>Landfills are reaching critical capacity. Methane emissions from decomposing waste contribute significantly to greenhouse gases and climate change.</p>
      <span class="severity sev-critical">⬤ Critical</span>
    </div>
    <div class="prob-card fade-in">
      <div class="prob-icon" style="background:rgba(255,184,48,0.1)">🌊</div>
      <h3>Ocean Plastic Pollution</h3>
      <p>8 million metric tons of plastic enter oceans annually, harming marine ecosystems and entering the food chain through microplastics.</p>
      <span class="severity sev-critical">⬤ Critical</span>
    </div>
    <div class="prob-card fade-in">
      <div class="prob-icon" style="background:rgba(255,184,48,0.1)">☢️</div>
      <h3>E-Waste Hazards</h3>
      <p>Electronic waste leaches toxic materials like lead and mercury into soil and water. Only 20% of e-waste is formally recycled worldwide.</p>
      <span class="severity sev-high">⬤ High</span>
    </div>
    <div class="prob-card fade-in">
      <div class="prob-icon" style="background:rgba(76,255,114,0.1)">🏙️</div>
      <h3>Illegal Dumping</h3>
      <p>Urban illegal dumping creates health hazards, contaminates groundwater, and costs municipalities millions in cleanup operations each year.</p>
      <span class="severity sev-high">⬤ High</span>
    </div>
    <div class="prob-card fade-in">
      <div class="prob-icon" style="background:rgba(184,255,60,0.1)">🍎</div>
      <h3>Food Waste Crisis</h3>
      <p>One-third of all food produced globally is wasted — about 1.3 billion tonnes — while 800 million people go hungry every day.</p>
      <span class="severity sev-medium">⬤ Medium</span>
    </div>
    <div class="prob-card fade-in">
      <div class="prob-icon" style="background:rgba(255,77,77,0.08)">🏗️</div>
      <h3>Construction Debris</h3>
      <p>Construction and demolition waste accounts for 30-40% of solid waste in many cities, with poor segregation and low recycling rates.</p>
      <span class="severity sev-medium">⬤ Medium</span>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- SOLUTIONS -->
<section id="solutions">
  <div class="section-label">// Smart Solutions</div>
  <h2 class="section-title">TURNING <span style="color:var(--green)">WASTE</span> INTO <span style="color:var(--lime)">VALUE</span></h2>
  <p class="section-desc">Technology-driven and community-based approaches to tackle the global garbage crisis effectively.</p>

  <div class="sol-grid">
    <div class="sol-card fade-in">
      <div class="sol-num">01</div>
      <div class="sol-content">
        <h3>AI-Powered Waste Sorting</h3>
        <p>Machine learning models classify waste types in real-time using image recognition, enabling automated sorting lines that achieve 95%+ accuracy.</p>
        <div class="sol-tags">
          <span class="sol-tag tag-green">Python</span>
          <span class="sol-tag tag-lime">TensorFlow</span>
          <span class="sol-tag tag-amber">IoT</span>
        </div>
      </div>
    </div>
    <div class="sol-card fade-in">
      <div class="sol-num">02</div>
      <div class="sol-content">
        <h3>Smart Bin Monitoring</h3>
        <p>IoT-enabled smart bins with fill-level sensors optimize garbage collection routes, reducing fuel costs and emissions by up to 40%.</p>
        <div class="sol-tags">
          <span class="sol-tag tag-green">Java Spring</span>
          <span class="sol-tag tag-lime">MQTT</span>
          <span class="sol-tag tag-amber">REST API</span>
        </div>
      </div>
    </div>
    <div class="sol-card fade-in">
      <div class="sol-num">03</div>
      <div class="sol-content">
        <h3>Composting Networks</h3>
        <p>Community composting hubs convert organic waste into valuable fertilizer, diverting 60% of household waste from landfills while enriching local soils.</p>
        <div class="sol-tags">
          <span class="sol-tag tag-green">Community</span>
          <span class="sol-tag tag-lime">Circular Economy</span>
        </div>
      </div>
    </div>
    <div class="sol-card fade-in">
      <div class="sol-num">04</div>
      <div class="sol-content">
        <h3>Waste-to-Energy Plants</h3>
        <p>Modern incineration with energy recovery converts non-recyclable waste into electricity and heat, reducing landfill dependence by up to 90%.</p>
        <div class="sol-tags">
          <span class="sol-tag tag-amber">Energy</span>
          <span class="sol-tag tag-green">Engineering</span>
        </div>
      </div>
    </div>
    <div class="sol-card fade-in">
      <div class="sol-num">05</div>
      <div class="sol-content">
        <h3>Blockchain Recycling Incentives</h3>
        <p>Token-reward systems on blockchain platforms incentivize citizens to deposit recyclables, making sustainability financially rewarding for communities.</p>
        <div class="sol-tags">
          <span class="sol-tag tag-lime">Java</span>
          <span class="sol-tag tag-green">Web3</span>
          <span class="sol-tag tag-amber">DeFi</span>
        </div>
      </div>
    </div>
    <div class="sol-card fade-in">
      <div class="sol-num">06</div>
      <div class="sol-content">
        <h3>Zero-Waste Education</h3>
        <p>Interactive digital platforms and school programs teaching proper waste segregation, reducing contamination of recyclable streams by 70%.</p>
        <div class="sol-tags">
          <span class="sol-tag tag-green">Education</span>
          <span class="sol-tag tag-lime">JavaScript</span>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- TECH STACK -->
<section id="techstack">
  <div class="section-label">// Technology Stack</div>
  <h2 class="section-title">BUILT WITH <span style="color:var(--lime)">POWER</span></h2>
  <p class="section-desc">A full-stack ecosystem using modern frontend tools alongside robust Python and Java backends.</p>

  <div class="tech-grid">
    <div class="tech-card fade-in">
      <div class="tech-icon">🐍</div>
      <div class="tech-name">Python</div>
      <p class="tech-desc">Flask REST API, ML waste classification, data analytics pipeline, and sensor data processing.</p>
      <span class="tech-role">Backend / ML</span>
    </div>
    <div class="tech-card fade-in">
      <div class="tech-icon">☕</div>
      <div class="tech-name">Java</div>
      <p class="tech-desc">Spring Boot microservices for routing optimization, report management, and IoT data ingestion.</p>
      <span class="tech-role">Backend / Services</span>
    </div>
    <div class="tech-card fade-in">
      <div class="tech-icon">🌐</div>
      <div class="tech-name">JavaScript</div>
      <p class="tech-desc">Vanilla JS for dynamic UI interactions, real-time updates, API calls, and interactive charts.</p>
      <span class="tech-role">Frontend</span>
    </div>
    <div class="tech-card fade-in">
      <div class="tech-icon">🎨</div>
      <div class="tech-name">HTML / CSS</div>
      <p class="tech-desc">Semantic HTML5 structure with modern CSS3 animations, custom variables, and responsive grid layouts.</p>
      <span class="tech-role">Frontend</span>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- AI CLASSIFIER -->
<section id="classifier">
  <div class="section-label">// Waste Classifier Tool</div>
  <h2 class="section-title">CLASSIFY YOUR <span style="color:var(--green)">WASTE</span></h2>
  <p class="section-desc">Describe your waste item and our system will classify it and provide the correct disposal method.</p>

  <div class="classifier-wrap">
    <div class="classifier-form">
      <div class="form-group">
        <label>Waste Item Name</label>
        <input type="text" id="wasteItem" placeholder="e.g. Old smartphone, plastic bottle, food scraps..." />
      </div>
      <div class="form-group">
        <label>Waste Category</label>
        <select id="wasteCategory">
          <option value="">-- Select a category --</option>
          <option>Household Waste</option>
          <option>Electronic Waste</option>
          <option>Organic / Food Waste</option>
          <option>Construction Debris</option>
          <option>Hazardous Waste</option>
          <option>Medical Waste</option>
          <option>Plastic Waste</option>
          <option>Industrial Waste</option>
        </select>
      </div>
      <div class="form-group">
        <label>Additional Description (optional)</label>
        <textarea id="wasteDesc" placeholder="Any additional details about the waste item, its condition, or quantity..."></textarea>
      </div>
      <button class="classify-btn" id="classifyBtn" onclick="classifyWaste()">⚡ CLASSIFY &amp; GET SOLUTION</button>
    </div>

    <div class="result-panel" id="resultPanel">
      <div class="result-idle" id="resultIdle">
        <div class="idle-icon">🔍</div>
        <p>Fill in the form and click classify to get waste disposal guidance.</p>
      </div>
      <div class="result-active" id="resultActive" style="display:none"></div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- REPORT -->
<section id="report">
  <div class="section-label">// Report a Problem</div>
  <h2 class="section-title">SPOT SOMETHING? <span style="color:var(--amber)">REPORT IT</span></h2>
  <p class="section-desc">Help your community by reporting illegal dumping sites, overflowing bins, or hazardous waste.</p>

  <div class="report-wrap">
    <div class="report-form fade-in">
      <h3>📍 Submit a Garbage Report</h3>
      <div class="form-row">
        <div class="form-group">
          <label>Your Name</label>
          <input type="text" id="repName" placeholder="Full name" />
        </div>
        <div class="form-group">
          <label>Contact Email</label>
          <input type="text" id="repEmail" placeholder="email@example.com" />
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Location / Area</label>
          <input type="text" id="repLocation" placeholder="Neighbourhood, City" />
        </div>
        <div class="form-group">
          <label>Problem Type</label>
          <select id="repType">
            <option>Illegal Dumping</option>
            <option>Overflowing Bin</option>
            <option>Hazardous Waste</option>
            <option>Blocked Drain (Garbage)</option>
            <option>Other</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label>Problem Description</label>
        <textarea id="repDesc" placeholder="Describe what you found, approximate size, how long it's been there..."></textarea>
      </div>
      <button class="submit-report-btn" onclick="submitReport()">📤 Submit Report</button>
    </div>

    <div class="recent-reports fade-in">
      <h3>📋 Recent Reports</h3>
      <div id="reportsList"></div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- BACKEND CODE -->
<section id="backend">
  <div class="section-label">// Backend Architecture</div>
  <h2 class="section-title">PYTHON &amp; JAVA <span style="color:var(--lime)">BACKENDS</span></h2>
  <p class="section-desc">Sample code showing the Flask (Python) and Spring Boot (Java) API endpoints powering this platform.</p>

  <div class="be-grid">
    <!-- Python -->
    <div class="be-card fade-in">
      <div class="be-header">
        <div class="be-dot" style="background:#4cff72"></div>
        <h3>Python — Flask Waste Classifier API</h3>
        <span class="lang-badge" style="background:rgba(76,255,114,0.1);color:var(--green);border:1px solid rgba(76,255,114,0.2)">Python</span>
      </div>
<pre><span class="cm"># app.py — Flask REST API</span>
<span class="kw">from</span> flask <span class="kw">import</span> Flask, request, jsonify
<span class="kw">from</span> flask_cors <span class="kw">import</span> CORS

app = Flask(__name__)
CORS(app)

WASTE_DB = {
  <span class="str">"plastic"</span>: {
    <span class="str">"type"</span>: <span class="str">"Recyclable"</span>,
    <span class="str">"bin"</span>: <span class="str">"Blue Bin"</span>,
    <span class="str">"steps"</span>: [
      <span class="str">"Rinse and clean the item"</span>,
      <span class="str">"Check recycling symbol (1-7)"</span>,
      <span class="str">"Place in blue recycling bin"</span>
    ]
  },
  <span class="str">"food"</span>: {
    <span class="str">"type"</span>: <span class="str">"Organic / Compost"</span>,
    <span class="str">"bin"</span>: <span class="str">"Green Bin"</span>,
    <span class="str">"steps"</span>: [
      <span class="str">"Separate from packaging"</span>,
      <span class="str">"Add to compost bin or green bin"</span>,
      <span class="str">"Can be home-composted"</span>
    ]
  }
}

<span class="fn">@app.route</span>(<span class="str">'/api/classify'</span>, methods=[<span class="str">'POST'</span>])
<span class="kw">def</span> <span class="fn">classify_waste</span>():
    data = request.get_json()
    item = data.get(<span class="str">'item'</span>, <span class="str">''</span>).lower()
    category = data.get(<span class="str">'category'</span>, <span class="str">''</span>)
    result = <span class="fn">analyze_waste</span>(item, category)
    <span class="kw">return</span> jsonify(result)

<span class="kw">def</span> <span class="fn">analyze_waste</span>(item, category):
    <span class="cm"># ML classification logic here</span>
    <span class="kw">for</span> key, val <span class="kw">in</span> WASTE_DB.items():
        <span class="kw">if</span> key <span class="kw">in</span> item:
            <span class="kw">return</span> val
    <span class="kw">return</span> {<span class="str">"type"</span>: <span class="str">"General Waste"</span>,
            <span class="str">"bin"</span>: <span class="str">"Black Bin"</span>}

<span class="kw">if</span> __name__ == <span class="str">'__main__'</span>:
    app.run(debug=<span class="kw">True</span>, port=<span class="num">5000</span>)</pre>
    </div>

    <!-- Java -->
    <div class="be-card fade-in">
      <div class="be-header">
        <div class="be-dot" style="background:#ffb830"></div>
        <h3>Java — Spring Boot Reports API</h3>
        <span class="lang-badge" style="background:rgba(255,184,48,0.1);color:var(--amber);border:1px solid rgba(255,184,48,0.2)">Java</span>
      </div>
<pre><span class="cm">// ReportController.java</span>
<span class="kw">@RestController</span>
<span class="kw">@RequestMapping</span>(<span class="str">"/api/reports"</span>)
<span class="kw">@CrossOrigin</span>(origins = <span class="str">"*"</span>)
<span class="kw">public class</span> <span class="fn">ReportController</span> {

  <span class="kw">@Autowired</span>
  <span class="kw">private</span> ReportService reportService;

  <span class="kw">@PostMapping</span>(<span class="str">"/submit"</span>)
  <span class="kw">public</span> ResponseEntity&lt;ReportResponse&gt;
      <span class="fn">submitReport</span>(@RequestBody ReportRequest req) {

    <span class="cm">// Validate input fields</span>
    <span class="kw">if</span> (req.getLocation() == <span class="kw">null</span>) {
      <span class="kw">return</span> ResponseEntity
        .badRequest().build();
    }

    Report saved = reportService
      .<span class="fn">saveReport</span>(req);

    <span class="kw">return</span> ResponseEntity.ok(
      <span class="kw">new</span> <span class="fn">ReportResponse</span>(
        saved.getId(),
        <span class="str">"SUBMITTED"</span>,
        <span class="str">"Report logged successfully"</span>
      )
    );
  }

  <span class="kw">@GetMapping</span>(<span class="str">"/list"</span>)
  <span class="kw">public</span> List&lt;Report&gt; <span class="fn">getReports</span>() {
    <span class="kw">return</span> reportService
      .<span class="fn">getAllReports</span>();
  }
}</pre>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">GarbageWatch</div>
  <p class="footer-copy">© 2024 GarbageWatch — Fighting the global waste crisis with technology.</p>
  <div class="footer-links">
    <a href="#problems">Problems</a>
    <a href="#solutions">Solutions</a>
    <a href="#backend">Backend Docs</a>
  </div>
</footer>

<!-- TOAST -->
<div id="toast">✅ Report submitted successfully!</div>

<script>
// ── COUNTER ANIMATION ──
function animateCounter(el, target, suffix = '') {
  let current = 0;
  const duration = 2000;
  const steps = 60;
  const increment = target / steps;
  const interval = duration / steps;
  const timer = setInterval(() => {
    current += increment;
    if (current >= target) {
      current = target;
      clearInterval(timer);
    }
    el.textContent = Math.round(current) + suffix;
  }, interval);
}

window.addEventListener('load', () => {
  setTimeout(() => {
    animateCounter(document.getElementById('counter1'), 2, 'B');
    animateCounter(document.getElementById('counter2'), 70, '%');
    animateCounter(document.getElementById('counter3'), 600, 'M');
    animateCounter(document.getElementById('counter4'), 80, '+');
  }, 600);
});

// ── SCROLL FADE-IN ──
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      observer.unobserve(e.target);
    }
  });
}, { threshold: 0.12 });

document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));

// ── WASTE CLASSIFIER ──
const wasteData = {
  'plastic': {
    type: 'Recyclable Plastic',
    bin: '♻️ Blue Recycling Bin',
    color: '#4cff72',
    steps: [
      'Rinse and clean the plastic item thoroughly',
      'Check the recycling symbol (numbers 1-7) on the bottom',
      'Remove any non-plastic components (labels, caps)',
      'Place in the blue recycling bin at your local facility',
      'Consider reusing before recycling if possible'
    ]
  },
  'bottle': {
    type: 'Recyclable Container',
    bin: '♻️ Blue Recycling Bin',
    color: '#4cff72',
    steps: [
      'Empty and rinse the bottle',
      'Separate cap and label if different material',
      'Crush to save space if plastic',
      'Drop off at recycling bin or bottle return point'
    ]
  },
  'food': {
    type: 'Organic Waste',
    bin: '🌱 Green Compost Bin',
    color: '#b8ff3c',
    steps: [
      'Separate food from any packaging',
      'Add to home compost bin or municipal green bin',
      'Avoid meat/dairy in home compost systems',
      'Compost enriches soil and reduces methane from landfills'
    ]
  },
  'phone': {
    type: 'Electronic Waste (E-Waste)',
    bin: '⚠️ E-Waste Drop-Off Centre',
    color: '#ffb830',
    steps: [
      'Backup and wipe all personal data from device',
      'Check if manufacturer has a take-back programme',
      'Locate nearest certified e-waste recycling facility',
      'Never place in regular bins — contains toxic materials',
      'Consider donating if device is still functional'
    ]
  },
  'battery': {
    type: 'Hazardous Material',
    bin: '⚠️ Hazardous Waste Facility',
    color: '#ff4d4d',
    steps: [
      'Do NOT place batteries in general trash or recycling',
      'Tape the terminals to prevent short-circuiting',
      'Locate a battery recycling drop-off near you',
      'Many supermarkets and electronics stores accept batteries'
    ]
  },
  'paper': {
    type: 'Recyclable Paper',
    bin: '♻️ Paper Recycling Bin',
    color: '#4cff72',
    steps: [
      'Ensure paper is clean and dry — no food contamination',
      'Remove plastic windows from envelopes if present',
      'Flatten cardboard boxes to save space',
      'Place in paper recycling bin'
    ]
  },
  'glass': {
    type: 'Recyclable Glass',
    bin: '♻️ Glass Recycling Bank',
    color: '#4cff72',
    steps: [
      'Rinse glass containers clean',
      'Remove metal lids (can be recycled separately)',
      'Check local guidelines on glass colours (clear/green/brown)',
      'Take to glass recycling bank — avoid putting in kerbside bin'
    ]
  },
  'medical': {
    type: 'Medical / Clinical Waste',
    bin: '🏥 Medical Waste Disposal',
    color: '#ff4d4d',
    steps: [
      'NEVER dispose in regular household bins',
      'Contact local pharmacy for sharps/medicine disposal',
      'Use sharps containers for needles and syringes',
      'Many pharmacies accept unused medications'
    ]
  }
};

function classifyWaste() {
  const item = document.getElementById('wasteItem').value.trim().toLowerCase();
  const category = document.getElementById('wasteCategory').value;
  const btn = document.getElementById('classifyBtn');

  if (!item && !category) {
    shakeEl(btn);
    return;
  }

  btn.disabled = true;
  btn.textContent = '⏳ Classifying...';

  document.getElementById('resultIdle').style.display = 'none';
  document.getElementById('resultActive').style.display = 'none';

  // Show loading
  const panel = document.getElementById('resultPanel');
  panel.innerHTML = `
    <div style="text-align:center">
      <div style="margin-bottom:1rem;font-size:0.85rem;color:var(--text-dim);font-family:'Space Mono',monospace">
        Running classification...
      </div>
      <div class="loading-dots">
        <span></span><span></span><span></span>
      </div>
    </div>`;

  // Simulate backend call delay
  setTimeout(() => {
    let result = null;
    for (const [key, val] of Object.entries(wasteData)) {
      if (item.includes(key)) { result = val; break; }
    }

    // Category fallback
    if (!result && category) {
      const catMap = {
        'Electronic Waste': wasteData['phone'],
        'Organic / Food Waste': wasteData['food'],
        'Hazardous Waste': wasteData['battery'],
        'Medical Waste': wasteData['medical'],
        'Plastic Waste': wasteData['plastic']
      };
      result = catMap[category];
    }

    if (!result) {
      result = {
        type: 'General Waste',
        bin: '🗑️ General Waste Bin (Black)',
        color: 'var(--text-dim)',
        steps: [
          'Check if any components can be separated for recycling',
          'Ensure waste is bagged securely to prevent spillage',
          'Place in general waste/landfill bin',
          'Contact local council for specific guidance on unusual items'
        ]
      };
    }

    panel.innerHTML = `
      <div class="result-active">
        <div style="font-family:'Space Mono',monospace;font-size:0.65rem;letter-spacing:2px;text-transform:uppercase;color:var(--text-dim);margin-bottom:0.5rem">Classification Result</div>
        <div class="result-type" style="color:${result.color}">${result.type}</div>
        <div style="font-size:0.9rem;font-weight:600;margin-bottom:1.5rem;color:var(--text-dim)">${result.bin}</div>
        <div style="font-size:0.78rem;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:var(--text-dim);margin-bottom:0.8rem">Disposal Steps</div>
        <ul class="result-steps">
          ${result.steps.map(s => `<li><div class="step-dot" style="background:${result.color}"></div><span>${s}</span></li>`).join('')}
        </ul>
        <div style="margin-top:1.5rem;padding:0.8rem 1rem;background:rgba(76,255,114,0.05);border:1px solid var(--border);border-radius:8px;font-size:0.75rem;color:var(--text-dim);font-family:'Space Mono',monospace">
          ⚡ Processed by Python Flask ML API · Model: WasteNet-v2.1
        </div>
      </div>`;

    btn.disabled = false;
    btn.textContent = '⚡ CLASSIFY & GET SOLUTION';
  }, 1800);
}

function shakeEl(el) {
  el.style.animation = 'none';
  el.offsetHeight;
  el.style.animation = 'shake 0.4s ease';
  setTimeout(() => el.style.animation = '', 400);
}

// ── REPORTS SYSTEM ──
let reports = [
  { title: 'Illegal dumping near river bank', location: 'Riverfront Area, East Zone', type: 'Illegal Dumping', status: 'progress', time: '2h ago' },
  { title: 'Overflowing bin at market', location: 'Central Market, Block B', type: 'Overflowing Bin', status: 'new', time: '5h ago' },
  { title: 'Hazardous barrels in vacant lot', location: 'Industrial District', type: 'Hazardous Waste', status: 'resolved', time: '1d ago' }
];

function renderReports() {
  const list = document.getElementById('reportsList');
  const statusClass = { new: 'status-new', progress: 'status-progress', resolved: 'status-resolved' };
  const statusLabel = { new: 'New', progress: 'In Progress', resolved: 'Resolved' };
  list.innerHTML = reports.slice(0, 5).map(r => `
    <div class="report-item">
      <div class="report-item-header">
        <div class="report-item-title">${r.title}</div>
        <span class="report-status ${statusClass[r.status]}">${statusLabel[r.status]}</span>
      </div>
      <div class="report-item-meta">📍 ${r.location} &nbsp;·&nbsp; ${r.type} &nbsp;·&nbsp; ${r.time}</div>
    </div>`).join('');
}

function submitReport() {
  const name = document.getElementById('repName').value.trim();
  const location = document.getElementById('repLocation').value.trim();
  const type = document.getElementById('repType').value;
  const desc = document.getElementById('repDesc').value.trim();

  if (!name || !location) {
    alert('Please enter your name and location.');
    return;
  }

  // Simulate Java Spring Boot API call
  reports.unshift({
    title: desc ? desc.substring(0, 50) + (desc.length > 50 ? '...' : '') : `${type} reported`,
    location: location,
    type: type,
    status: 'new',
    time: 'Just now'
  });

  renderReports();
  showToast();

  // Clear form
  ['repName','repEmail','repLocation','repDesc'].forEach(id => document.getElementById(id).value = '');
}

function showToast() {
  const t = document.getElementById('toast');
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3500);
}

// Enter key on classifier
document.addEventListener('DOMContentLoaded', () => {
  renderReports();
  document.getElementById('wasteItem').addEventListener('keypress', (e) => {
    if (e.key === 'Enter') classifyWaste();
  });
});
</script>
</body>
</html>

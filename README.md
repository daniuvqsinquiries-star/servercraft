<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ServerCraft — We Build Servers That Grow Communities</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --purple: #6A3DFF;
    --blue: #2F9BFF;
    --teal: #1DD3B0;
    --dark: #1E1F22;
    --darker: #141416;
    --card: #25262B;
    --card2: #2C2D33;
    --white: #FFFFFF;
    --muted: rgba(255,255,255,0.5);
    --border: rgba(106,61,255,0.25);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--darker);
    color: var(--white);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    background: var(--teal);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, background 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--purple);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.18s ease, width 0.2s, height 0.2s, border-color 0.2s;
  }

  /* NOISE OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 9990; opacity: 0.35;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 20px 60px;
    background: rgba(20,20,22,0.7);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }
  .nav-logo {
    font-family: 'Orbitron', sans-serif;
    font-weight: 900; font-size: 1.3rem;
    letter-spacing: 2px;
    background: linear-gradient(135deg, var(--purple), var(--blue));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    text-decoration: none;
  }
  .nav-logo span { color: var(--teal); -webkit-text-fill-color: var(--teal); }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a {
    color: var(--muted); text-decoration: none;
    font-size: 0.85rem; letter-spacing: 1px; text-transform: uppercase;
    font-weight: 500; transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--teal); }
  .nav-cta {
    background: var(--purple); color: var(--white) !important;
    padding: 9px 22px; border-radius: 6px;
    font-weight: 600 !important;
    transition: background 0.2s, box-shadow 0.2s !important;
    color: var(--white) !important;
    -webkit-text-fill-color: var(--white) !important;
  }
  .nav-cta:hover { background: var(--blue) !important; box-shadow: 0 0 20px rgba(47,155,255,0.4) !important; color: var(--white) !important; }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    text-align: center;
    padding: 120px 20px 60px;
    position: relative; overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0; z-index: 0;
    background:
      radial-gradient(ellipse 80% 60% at 50% 30%, rgba(106,61,255,0.22) 0%, transparent 70%),
      radial-gradient(ellipse 50% 40% at 80% 80%, rgba(29,211,176,0.10) 0%, transparent 60%),
      radial-gradient(ellipse 40% 30% at 10% 60%, rgba(47,155,255,0.10) 0%, transparent 60%);
  }
  .hero-grid {
    position: absolute; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(106,61,255,0.07) 1px, transparent 1px),
      linear-gradient(90deg, rgba(106,61,255,0.07) 1px, transparent 1px);
    background-size: 60px 60px;
    mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 0%, transparent 100%);
  }
  .hero-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(106,61,255,0.15);
    border: 1px solid rgba(106,61,255,0.4);
    padding: 6px 18px; border-radius: 100px;
    font-size: 0.78rem; letter-spacing: 2px; text-transform: uppercase;
    color: var(--teal); font-weight: 500; margin-bottom: 28px;
    position: relative; z-index: 1;
    animation: fadeDown 0.8s ease both;
  }
  .hero-badge::before {
    content: ''; width: 6px; height: 6px;
    background: var(--teal); border-radius: 50%;
    animation: pulse 2s infinite;
  }
  @keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.4;transform:scale(1.4)} }

  .hero h1 {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(2.8rem, 7vw, 6rem);
    font-weight: 900;
    line-height: 1.05;
    letter-spacing: -1px;
    position: relative; z-index: 1;
    animation: fadeUp 0.9s ease 0.1s both;
  }
  .hero h1 .line1 { display: block; color: var(--white); }
  .hero h1 .line2 {
    display: block;
    background: linear-gradient(90deg, var(--purple), var(--blue), var(--teal));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-size: 200%; animation: gradMove 4s linear infinite, fadeUp 0.9s ease 0.2s both;
  }
  @keyframes gradMove { 0%{background-position:0%} 100%{background-position:200%} }

  .hero-sub {
    max-width: 600px;
    color: var(--muted); font-size: 1.05rem; line-height: 1.7;
    margin: 24px auto 40px;
    position: relative; z-index: 1;
    animation: fadeUp 0.9s ease 0.3s both;
  }
  .hero-actions {
    display: flex; gap: 16px; flex-wrap: wrap; justify-content: center;
    position: relative; z-index: 1;
    animation: fadeUp 0.9s ease 0.4s both;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--purple), var(--blue));
    color: var(--white); border: none;
    padding: 14px 36px; border-radius: 8px;
    font-size: 0.95rem; font-weight: 600; cursor: none;
    text-decoration: none; display: inline-block;
    transition: transform 0.2s, box-shadow 0.2s;
    box-shadow: 0 4px 30px rgba(106,61,255,0.4);
    font-family: 'DM Sans', sans-serif;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 40px rgba(106,61,255,0.6); }
  .btn-secondary {
    background: transparent; color: var(--white);
    border: 1px solid rgba(255,255,255,0.2);
    padding: 14px 36px; border-radius: 8px;
    font-size: 0.95rem; font-weight: 500; cursor: none;
    text-decoration: none; display: inline-block;
    transition: border-color 0.2s, background 0.2s;
    font-family: 'DM Sans', sans-serif;
  }
  .btn-secondary:hover { border-color: var(--teal); background: rgba(29,211,176,0.07); }

  .hero-stats {
    display: flex; gap: 48px; margin-top: 70px;
    position: relative; z-index: 1;
    animation: fadeUp 0.9s ease 0.5s both;
  }
  .stat { text-align: center; }
  .stat-num {
    font-family: 'Orbitron', sans-serif;
    font-size: 2rem; font-weight: 700;
    background: linear-gradient(135deg, var(--blue), var(--teal));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .stat-label { font-size: 0.78rem; color: var(--muted); letter-spacing: 1px; text-transform: uppercase; margin-top: 4px; }

  @keyframes fadeUp { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }
  @keyframes fadeDown { from{opacity:0;transform:translateY(-20px)} to{opacity:1;transform:translateY(0)} }

  /* SECTION BASE */
  section { padding: 100px 20px; }
  .container { max-width: 1160px; margin: 0 auto; }
  .section-tag {
    font-size: 0.72rem; letter-spacing: 3px; text-transform: uppercase;
    color: var(--teal); font-weight: 600; margin-bottom: 12px;
    display: flex; align-items: center; gap: 10px;
  }
  .section-tag::before { content:''; flex:0 0 24px; height:1px; background:var(--teal); }
  .section-title {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    font-weight: 700; line-height: 1.2;
    margin-bottom: 16px;
  }
  .section-sub { color: var(--muted); font-size: 1rem; line-height: 1.7; max-width: 540px; }

  /* SERVICES */
  #services { background: var(--dark); }
  .services-header { text-align: center; margin-bottom: 64px; }
  .services-header .section-tag { justify-content: center; }
  .services-header .section-tag::before { display:none; }
  .services-header .section-sub { margin: 0 auto; }

  .packages { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }

  .pkg-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px; padding: 36px 32px;
    position: relative; overflow: hidden;
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
    display: flex; flex-direction: column;
  }
  .pkg-card::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(106,61,255,0.06), transparent);
    opacity: 0; transition: opacity 0.3s;
  }
  .pkg-card:hover { transform: translateY(-6px); border-color: rgba(106,61,255,0.5); box-shadow: 0 20px 60px rgba(0,0,0,0.4); }
  .pkg-card:hover::before { opacity: 1; }

  .pkg-card.featured {
    border-color: var(--purple);
    background: linear-gradient(160deg, rgba(106,61,255,0.15), var(--card) 60%);
  }
  .pkg-badge-pop {
    position: absolute; top: 20px; right: 20px;
    background: linear-gradient(135deg, var(--purple), var(--blue));
    padding: 4px 12px; border-radius: 100px;
    font-size: 0.7rem; font-weight: 700; letter-spacing: 1px;
  }
  .pkg-icon {
    width: 48px; height: 48px; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.4rem; margin-bottom: 20px;
  }
  .pkg-icon.starter { background: rgba(29,211,176,0.15); }
  .pkg-icon.pro { background: rgba(106,61,255,0.15); }
  .pkg-icon.ultimate { background: rgba(47,155,255,0.15); }

  .pkg-name {
    font-family: 'Orbitron', sans-serif;
    font-size: 1rem; font-weight: 700; letter-spacing: 1px;
    text-transform: uppercase; margin-bottom: 8px;
  }
  .pkg-desc { color: var(--muted); font-size: 0.88rem; line-height: 1.6; margin-bottom: 24px; }

  .pkg-price {
    display: flex; align-items: baseline; gap: 6px; margin-bottom: 6px;
  }
  .pkg-price .amount {
    font-family: 'Orbitron', sans-serif;
    font-size: 2.4rem; font-weight: 900;
    background: linear-gradient(135deg, var(--blue), var(--teal));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .pkg-price .cur { font-size: 1.2rem; font-weight: 600; color: var(--muted); margin-top: 6px; }
  .pkg-robux { font-size: 0.8rem; color: var(--muted); margin-bottom: 28px; }
  .pkg-robux span { color: var(--teal); font-weight: 600; }

  .pkg-features { list-style: none; flex: 1; margin-bottom: 32px; }
  .pkg-features li {
    padding: 8px 0; font-size: 0.88rem; color: rgba(255,255,255,0.75);
    display: flex; align-items: center; gap: 10px;
    border-bottom: 1px solid rgba(255,255,255,0.05);
  }
  .pkg-features li:last-child { border-bottom: none; }
  .pkg-features li::before {
    content: '✓'; color: var(--teal); font-weight: 700; font-size: 0.8rem;
    flex: 0 0 16px;
  }
  .pkg-btn {
    display: block; text-align: center;
    padding: 12px; border-radius: 8px;
    font-size: 0.88rem; font-weight: 600;
    text-decoration: none; transition: all 0.2s;
    cursor: none;
  }
  .pkg-btn.ghost {
    border: 1px solid rgba(255,255,255,0.2); color: var(--white);
  }
  .pkg-btn.ghost:hover { border-color: var(--purple); background: rgba(106,61,255,0.1); }
  .pkg-btn.solid {
    background: linear-gradient(135deg, var(--purple), var(--blue));
    color: var(--white);
    box-shadow: 0 4px 20px rgba(106,61,255,0.35);
  }
  .pkg-btn.solid:hover { box-shadow: 0 6px 30px rgba(106,61,255,0.55); transform: translateY(-1px); }

  /* FEATURES */
  #features { background: var(--darker); }
  .features-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center; }
  .features-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .feat-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 12px; padding: 24px 20px;
    transition: border-color 0.2s, transform 0.2s;
  }
  .feat-card:hover { border-color: rgba(29,211,176,0.35); transform: translateY(-3px); }
  .feat-icon { font-size: 1.6rem; margin-bottom: 12px; }
  .feat-title { font-size: 0.9rem; font-weight: 600; margin-bottom: 6px; }
  .feat-desc { font-size: 0.8rem; color: var(--muted); line-height: 1.5; }

  /* PROCESS */
  #process { background: var(--dark); }
  .process-header { text-align: center; margin-bottom: 64px; }
  .process-header .section-tag { justify-content: center; }
  .process-header .section-tag::before { display:none; }
  .process-header .section-sub { margin: 0 auto; }
  .steps { display: grid; grid-template-columns: repeat(4, 1fr); gap: 0; position: relative; }
  .steps::before {
    content: ''; position: absolute;
    top: 28px; left: 10%; right: 10%; height: 1px;
    background: linear-gradient(90deg, transparent, var(--purple), var(--blue), var(--teal), transparent);
  }
  .step { text-align: center; padding: 0 16px; }
  .step-num {
    width: 56px; height: 56px; border-radius: 50%;
    background: linear-gradient(135deg, var(--purple), var(--blue));
    display: flex; align-items: center; justify-content: center;
    margin: 0 auto 20px;
    font-family: 'Orbitron', sans-serif; font-weight: 700; font-size: 1rem;
    position: relative; z-index: 1;
    box-shadow: 0 0 30px rgba(106,61,255,0.4);
  }
  .step-title { font-size: 0.95rem; font-weight: 600; margin-bottom: 8px; }
  .step-desc { font-size: 0.82rem; color: var(--muted); line-height: 1.5; }

  /* ROLES */
  #roles { background: var(--darker); }
  .roles-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: start; }
  .roles-list { display: flex; flex-direction: column; gap: 10px; }
  .role-item {
    display: flex; align-items: center; gap: 14px;
    background: var(--card); border: 1px solid var(--border);
    border-radius: 10px; padding: 14px 18px;
    transition: transform 0.2s, border-color 0.2s;
  }
  .role-item:hover { transform: translateX(6px); }
  .role-dot { width: 10px; height: 10px; border-radius: 50%; flex: 0 0 10px; }
  .role-name { font-size: 0.9rem; font-weight: 600; }
  .role-desc { font-size: 0.78rem; color: var(--muted); margin-left: auto; text-align: right; }

  /* BOTS */
  .bots-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 12px; margin-top: 40px; }
  .bot-chip {
    background: var(--card2); border: 1px solid var(--border);
    border-radius: 10px; padding: 14px 10px; text-align: center;
    font-size: 0.8rem; font-weight: 600; color: var(--muted);
    transition: border-color 0.2s, color 0.2s, transform 0.2s;
  }
  .bot-chip:hover { border-color: var(--blue); color: var(--white); transform: translateY(-3px); }
  .bot-chip .bot-icon { font-size: 1.4rem; margin-bottom: 6px; display: block; }

  /* EXTRAS */
  #extras { background: var(--dark); }
  .extras-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; margin-top: 48px; }
  .extra-item {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 10px; padding: 20px 18px;
    display: flex; align-items: center; gap: 14px;
    font-size: 0.88rem; font-weight: 500;
    transition: border-color 0.2s, background 0.2s;
  }
  .extra-item:hover { border-color: var(--teal); background: rgba(29,211,176,0.05); }
  .extra-item .ei { font-size: 1.2rem; }

  /* CTA */
  #cta {
    background: var(--darker);
    text-align: center; padding: 120px 20px;
  }
  .cta-inner {
    max-width: 680px; margin: 0 auto;
    background: linear-gradient(135deg, rgba(106,61,255,0.18), rgba(47,155,255,0.10));
    border: 1px solid rgba(106,61,255,0.35);
    border-radius: 24px; padding: 72px 60px;
    position: relative; overflow: hidden;
  }
  .cta-inner::before {
    content: ''; position: absolute;
    inset: -1px; border-radius: 24px;
    background: linear-gradient(135deg, var(--purple), var(--blue), var(--teal));
    z-index: -1; opacity: 0.3;
  }
  .cta-inner h2 {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(1.5rem, 3.5vw, 2.4rem);
    font-weight: 700; margin-bottom: 16px;
  }
  .cta-inner p { color: var(--muted); font-size: 1rem; margin-bottom: 36px; line-height: 1.7; }
  .cta-actions { display: flex; gap: 14px; justify-content: center; flex-wrap: wrap; }

  /* FOOTER */
  footer {
    background: #111113;
    border-top: 1px solid var(--border);
    padding: 48px 20px 32px;
  }
  .footer-inner { max-width: 1160px; margin: 0 auto; }
  .footer-top {
    display: flex; justify-content: space-between; align-items: flex-start;
    gap: 40px; flex-wrap: wrap; margin-bottom: 48px;
  }
  .footer-brand .logo {
    font-family: 'Orbitron', sans-serif; font-weight: 900;
    font-size: 1.2rem; letter-spacing: 2px;
    background: linear-gradient(135deg, var(--purple), var(--blue));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    display: block; margin-bottom: 10px;
  }
  .footer-brand p { font-size: 0.85rem; color: var(--muted); max-width: 240px; line-height: 1.6; }
  .footer-links h4 { font-size: 0.75rem; letter-spacing: 2px; text-transform: uppercase; color: var(--muted); margin-bottom: 16px; }
  .footer-links ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
  .footer-links a { color: rgba(255,255,255,0.65); text-decoration: none; font-size: 0.88rem; transition: color 0.2s; }
  .footer-links a:hover { color: var(--teal); }
  .footer-bottom {
    border-top: 1px solid var(--border);
    padding-top: 24px;
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 12px;
  }
  .footer-bottom p { font-size: 0.78rem; color: var(--muted); }
  .footer-teal { color: var(--teal); }

  /* SCROLL FADE IN */
  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: none; }

  /* RESPONSIVE */
  @media (max-width: 900px) {
    nav { padding: 18px 24px; }
    .nav-links { display: none; }
    .packages { grid-template-columns: 1fr; max-width: 440px; margin: 0 auto; }
    .features-layout { grid-template-columns: 1fr; gap: 40px; }
    .steps { grid-template-columns: 1fr 1fr; gap: 32px; }
    .steps::before { display: none; }
    .roles-layout { grid-template-columns: 1fr; }
    .bots-grid { grid-template-columns: repeat(3, 1fr); }
    .extras-grid { grid-template-columns: 1fr 1fr; }
    .cta-inner { padding: 40px 24px; }
    .hero-stats { gap: 28px; flex-wrap: wrap; justify-content: center; }
  }
  @media (max-width: 600px) {
    .extras-grid { grid-template-columns: 1fr; }
    .features-grid { grid-template-columns: 1fr; }
    .bots-grid { grid-template-columns: repeat(2, 1fr); }
    .footer-top { flex-direction: column; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">Server<span>Craft</span></a>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#features">Features</a></li>
    <li><a href="#process">Process</a></li>
    <li><a href="#roles">Roles</a></li>
    <li><a href="#cta" class="nav-cta">Open a Ticket</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>
  <div class="hero-badge">🟢 Currently Accepting New Clients</div>
  <h1>
    <span class="line1">BUILD YOUR</span>
    <span class="line2">DREAM SERVER.</span>
  </h1>
  <p class="hero-sub">
    Professional Discord server setups for gaming communities, Roblox groups, and growing brands. Custom roles, bots, embeds, and ticket systems — built right the first time.
  </p>
  <div class="hero-actions">
    <a href="#cta" class="btn-primary">🎟 Open a Ticket</a>
    <a href="#services" class="btn-secondary">View Packages →</a>
  </div>
  <div class="hero-stats">
    <div class="stat">
      <div class="stat-num">150+</div>
      <div class="stat-label">Servers Built</div>
    </div>
    <div class="stat">
      <div class="stat-num">24h</div>
      <div class="stat-label">Avg Delivery</div>
    </div>
    <div class="stat">
      <div class="stat-num">100%</div>
      <div class="stat-label">Satisfaction</div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section id="services">
  <div class="container">
    <div class="services-header reveal">
      <div class="section-tag">Packages</div>
      <h2 class="section-title">Choose Your Setup</h2>
      <p class="section-sub">Every package includes professional design, fast delivery, and post-setup support. Available in USD or Robux.</p>
    </div>
    <div class="packages">
      <!-- Starter -->
      <div class="pkg-card reveal">
        <div class="pkg-icon starter">🌱</div>
        <div class="pkg-name">Starter</div>
        <div class="pkg-desc">Perfect for new communities, small friend groups, or hobby servers.</div>
        <div class="pkg-price">
          <span class="cur">$</span>
          <span class="amount">5</span>
        </div>
        <div class="pkg-robux">or <span>50 Robux</span> for Roblox groups</div>
        <ul class="pkg-features">
          <li>10 organized channels</li>
          <li>Basic role hierarchy</li>
          <li>Channel permissions setup</li>
          <li>Welcome & rules embed</li>
          <li>Post-setup support</li>
        </ul>
        <a href="#cta" class="pkg-btn ghost">Get Started</a>
      </div>

      <!-- Professional -->
      <div class="pkg-card featured reveal">
        <div class="pkg-badge-pop">⭐ POPULAR</div>
        <div class="pkg-icon pro">⚡</div>
        <div class="pkg-name">Professional</div>
        <div class="pkg-desc">For growing communities that need automation, bots, and a polished look.</div>
        <div class="pkg-price">
          <span class="cur">$</span>
          <span class="amount">15</span>
        </div>
        <div class="pkg-robux">or <span>150 Robux</span> for Roblox groups</div>
        <ul class="pkg-features">
          <li>25+ channels + categories</li>
          <li>Reaction roles via Carl-bot</li>
          <li>Custom embeds & branding</li>
          <li>Bot setup (Dyno, MEE6)</li>
          <li>Moderation configuration</li>
          <li>FAQ & info channels</li>
        </ul>
        <a href="#cta" class="pkg-btn solid">Get Started</a>
      </div>

      <!-- Ultimate -->
      <div class="pkg-card reveal">
        <div class="pkg-icon ultimate">👑</div>
        <div class="pkg-name">Ultimate</div>
        <div class="pkg-desc">The full package — for large communities, brands, and serious server owners.</div>
        <div class="pkg-price">
          <span class="cur">$</span>
          <span class="amount">30</span>
        </div>
        <div class="pkg-robux">or <span>2,400 Robux</span> for Roblox groups</div>
        <ul class="pkg-features">
          <li>Unlimited channels & categories</li>
          <li>Ticket system (Helper.gg)</li>
          <li>Verification + auto-roles</li>
          <li>Custom embeds & graphics</li>
          <li>Full moderation bot config</li>
          <li>Server security setup (Wick)</li>
          <li>Level system setup</li>
          <li>Priority support</li>
        </ul>
        <a href="#cta" class="pkg-btn ghost">Get Started</a>
      </div>
    </div>
  </div>
</section>

<!-- FEATURES -->
<section id="features">
  <div class="container">
    <div class="features-layout">
      <div class="reveal">
        <div class="section-tag">What We Deliver</div>
        <h2 class="section-title">Everything Your Server Needs</h2>
        <p class="section-sub">Our experienced builders don't just create channels — they craft an entire ecosystem for your community to thrive in.</p>
        <br><br>
        <a href="#cta" class="btn-primary">Start Building Today</a>
      </div>
      <div class="features-grid reveal">
        <div class="feat-card">
          <div class="feat-icon">🗂</div>
          <div class="feat-title">Channel Architecture</div>
          <div class="feat-desc">Organized categories and channels tailored to your community's workflow.</div>
        </div>
        <div class="feat-card">
          <div class="feat-icon">🎭</div>
          <div class="feat-title">Custom Roles</div>
          <div class="feat-desc">Color-coded hierarchy with permission levels designed for your team.</div>
        </div>
        <div class="feat-card">
          <div class="feat-icon">🤖</div>
          <div class="feat-title">Bot Integration</div>
          <div class="feat-desc">Dyno, Carl-bot, MEE6, Wick, Helper.gg — fully configured and ready.</div>
        </div>
        <div class="feat-card">
          <div class="feat-icon">🎟</div>
          <div class="feat-title">Ticket System</div>
          <div class="feat-desc">Professional support ticket flows so your team can handle requests smoothly.</div>
        </div>
        <div class="feat-card">
          <div class="feat-icon">✉️</div>
          <div class="feat-title">Custom Embeds</div>
          <div class="feat-desc">Beautiful, branded embed messages for welcome, rules, and announcements.</div>
        </div>
        <div class="feat-card">
          <div class="feat-icon">🛡</div>
          <div class="feat-title">Security Setup</div>
          <div class="feat-desc">Anti-raid, verification, and logging so your server stays protected 24/7.</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PROCESS -->
<section id="process">
  <div class="container">
    <div class="process-header reveal">
      <div class="section-tag">How It Works</div>
      <h2 class="section-title">4 Simple Steps</h2>
      <p class="section-sub">From opening a ticket to launching your server — we handle everything.</p>
    </div>
    <div class="steps">
      <div class="step reveal">
        <div class="step-num">01</div>
        <div class="step-title">Open a Ticket</div>
        <div class="step-desc">Click the ticket button in our Discord and describe your vision. We respond fast.</div>
      </div>
      <div class="step reveal">
        <div class="step-num">02</div>
        <div class="step-title">Share Your Plan</div>
        <div class="step-desc">Tell us your community type, theme, preferred bots, and any special requirements.</div>
      </div>
      <div class="step reveal">
        <div class="step-num">03</div>
        <div class="step-title">We Build It</div>
        <div class="step-desc">Our builders get to work. Most setups are delivered within 24 hours.</div>
      </div>
      <div class="step reveal">
        <div class="step-num">04</div>
        <div class="step-title">Launch & Grow</div>
        <div class="step-desc">Review your new server, request any tweaks, and grow your community with confidence.</div>
      </div>
    </div>
  </div>
</section>

<!-- ROLES & BOTS -->
<section id="roles">
  <div class="container">
    <div class="roles-layout">
      <div>
        <div class="section-tag reveal">Team Structure</div>
        <h2 class="section-title reveal">Our Staff Roles</h2>
        <p class="section-sub reveal">A dedicated team across management, building, and client support — ensuring every server is handled with care.</p>
        <div class="roles-list" style="margin-top:32px;">
          <div class="role-item reveal">
            <div class="role-dot" style="background:#FFD700"></div>
            <div class="role-name">Director of Operations</div>
            <div class="role-desc">Owner</div>
          </div>
          <div class="role-item reveal">
            <div class="role-dot" style="background:#FF4444"></div>
            <div class="role-name">Director of Client Services</div>
            <div class="role-desc">Client Relations</div>
          </div>
          <div class="role-item reveal">
            <div class="role-dot" style="background:#6A3DFF"></div>
            <div class="role-name">Director of Development</div>
            <div class="role-desc">Technical Builds</div>
          </div>
          <div class="role-item reveal">
            <div class="role-dot" style="background:#8855FF"></div>
            <div class="role-name">Builder</div>
            <div class="role-desc">Server Creation</div>
          </div>
          <div class="role-item reveal">
            <div class="role-dot" style="background:#2F9BFF"></div>
            <div class="role-name">Support</div>
            <div class="role-desc">Ticket Handling</div>
          </div>
          <div class="role-item reveal">
            <div class="role-dot" style="background:#1DD3B0"></div>
            <div class="role-name">Customer / Verified / Member</div>
            <div class="role-desc">Community</div>
          </div>
        </div>
      </div>

      <div>
        <div class="section-tag reveal">Recommended Bots</div>
        <h2 class="section-title reveal">Powered by the Best</h2>
        <p class="section-sub reveal">We configure and deploy the top Discord bots — so your server runs on autopilot from day one.</p>
        <div class="bots-grid reveal">
          <div class="bot-chip"><span class="bot-icon">🛡</span>Dyno</div>
          <div class="bot-chip"><span class="bot-icon">🃏</span>Carl-bot</div>
          <div class="bot-chip"><span class="bot-icon">🎟</span>Ticket Tool</div>
          <div class="bot-chip"><span class="bot-icon">🔰</span>Wick</div>
          <div class="bot-chip"><span class="bot-icon">⭐</span>MEE6</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- EXTRAS -->
<section id="extras">
  <div class="container">
    <div class="reveal">
      <div class="section-tag">Pro Add-ons</div>
      <h2 class="section-title">Extra Features to Stand Out</h2>
      <p class="section-sub">Available as add-ons or included in the Ultimate package — these features take your server to the next level.</p>
    </div>
    <div class="extras-grid">
      <div class="extra-item reveal"><span class="ei">✅</span> Auto Verification Systems</div>
      <div class="extra-item reveal"><span class="ei">👋</span> Custom Welcome Messages</div>
      <div class="extra-item reveal"><span class="ei">🎭</span> Reaction Role Menus</div>
      <div class="extra-item reveal"><span class="ei">📈</span> Level Systems (XP)</div>
      <div class="extra-item reveal"><span class="ei">🔒</span> Server Security Setup</div>
      <div class="extra-item reveal"><span class="ei">📅</span> Event Channels</div>
      <div class="extra-item reveal"><span class="ei">🤖</span> Auto Moderation</div>
      <div class="extra-item reveal"><span class="ei">🔄</span> Server Revamps</div>
      <div class="extra-item reveal"><span class="ei">📦</span> Bot-Only Setups</div>
    </div>
  </div>
</section>

<!-- CTA -->
<section id="cta">
  <div class="container">
    <div class="cta-inner reveal">
      <div class="section-tag" style="justify-content:center;margin-bottom:16px;">
        <span style="color:var(--teal);font-size:0.72rem;letter-spacing:3px;text-transform:uppercase;font-weight:600;">Ready?</span>
      </div>
      <h2>Need a Professional Discord Server?</h2>
      <p>Join our Discord server to see our portfolio, chat with our team, and open a ticket to get started. Fast delivery ⚡ Affordable prices 💰</p>
      <div class="cta-actions">
        <a href="https://discord.gg/servercraft" class="btn-primary" target="_blank">🎟 Open a Ticket</a>
        <a href="#services" class="btn-secondary">View Packages</a>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div class="footer-top">
      <div class="footer-brand">
        <span class="logo">ServerCraft</span>
        <p>We Build Servers That Grow Communities. Professional Discord setups for every need.</p>
      </div>
      <div class="footer-links">
        <h4>Services</h4>
        <ul>
          <li><a href="#services">Starter Package</a></li>
          <li><a href="#services">Professional Package</a></li>
          <li><a href="#services">Ultimate Package</a></li>
          <li><a href="#extras">Add-ons</a></li>
        </ul>
      </div>
      <div class="footer-links">
        <h4>Community</h4>
        <ul>
          <li><a href="#process">How It Works</a></li>
          <li><a href="#roles">Our Team</a></li>
          <li><a href="#cta">Portfolio</a></li>
          <li><a href="#cta">Reviews</a></li>
        </ul>
      </div>
      <div class="footer-links">
        <h4>Contact</h4>
        <ul>
          <li><a href="https://discord.gg/servercraft" target="_blank">Discord Server</a></li>
          <li><a href="#cta">Open a Ticket</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2025 <span class="footer-teal">ServerCraft</span>. All rights reserved.</p>
      <p style="font-size:0.75rem;">Built with ⚡ for growing communities.</p>
    </div>
  </div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animCursor() {
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();
  document.querySelectorAll('a, button').forEach(el => {
    el.addEventListener('mouseenter', () => { ring.style.width='52px'; ring.style.height='52px'; ring.style.borderColor='var(--teal)'; });
    el.addEventListener('mouseleave', () => { ring.style.width='36px'; ring.style.height='36px'; ring.style.borderColor='var(--purple)'; });
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        const delay = (Array.from(e.target.parentNode.children).indexOf(e.target)) * 80;
        setTimeout(() => e.target.classList.add('visible'), delay);
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });
  reveals.forEach(el => observer.observe(el));

  // Nav scroll effect
  const nav = document.querySelector('nav');
  window.addEventListener('scroll', () => {
    nav.style.background = window.scrollY > 60
      ? 'rgba(14,14,16,0.95)'
      : 'rgba(20,20,22,0.7)';
  });
</script>
</body>
</html>

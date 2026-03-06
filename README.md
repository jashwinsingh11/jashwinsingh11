<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Jashwin Singh — Developer Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg: #050a0f;
    --surface: #0a1520;
    --surface2: #0f1e2d;
    --accent: #00d9ff;
    --accent2: #00ff88;
    --accent3: #ff6b35;
    --gold: #ffd700;
    --text: #e8f4fd;
    --muted: #6a8fa8;
    --border: rgba(0,217,255,0.12);
    --glow: 0 0 40px rgba(0,217,255,0.15);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transition: transform 0.1s ease;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid rgba(0,217,255,0.5);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: transform 0.25s ease, opacity 0.2s;
  }

  /* Noise texture overlay */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 0; opacity: 0.4;
  }

  /* Grid background */
  body::after {
    content: '';
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(0,217,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,217,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none; z-index: 0;
  }

  /* Hero */
  .hero {
    position: relative; z-index: 1;
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center; align-items: center;
    padding: 80px 40px;
    text-align: center;
    overflow: hidden;
  }

  .hero-orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
  }
  .orb-1 { width: 600px; height: 600px; background: radial-gradient(circle, rgba(0,217,255,0.12), transparent); top: -100px; left: -150px; animation: drift 8s ease-in-out infinite; }
  .orb-2 { width: 500px; height: 500px; background: radial-gradient(circle, rgba(0,255,136,0.08), transparent); bottom: -100px; right: -100px; animation: drift 10s ease-in-out infinite reverse; }
  .orb-3 { width: 400px; height: 400px; background: radial-gradient(circle, rgba(255,107,53,0.07), transparent); top: 50%; left: 50%; transform: translate(-50%,-50%); animation: pulse-slow 6s ease-in-out infinite; }

  @keyframes drift { 0%,100%{transform:translate(0,0)} 50%{transform:translate(30px,-20px)} }
  @keyframes pulse-slow { 0%,100%{opacity:0.5;transform:translate(-50%,-50%) scale(1)} 50%{opacity:1;transform:translate(-50%,-50%) scale(1.2)} }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.8s 0.2s forwards;
    border: 1px solid var(--border);
    padding: 6px 16px;
    border-radius: 2px;
    background: rgba(0,217,255,0.05);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(56px, 10vw, 110px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -3px;
    background: linear-gradient(135deg, #ffffff 0%, var(--accent) 50%, var(--accent2) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    opacity: 0;
    animation: fadeUp 0.8s 0.4s forwards;
    margin-bottom: 8px;
  }

  .hero-subtitle {
    font-family: 'Space Mono', monospace;
    font-size: clamp(13px, 2vw, 17px);
    color: var(--muted);
    letter-spacing: 1px;
    opacity: 0;
    animation: fadeUp 0.8s 0.6s forwards;
    margin-bottom: 40px;
  }

  .hero-subtitle span { color: var(--accent); }

  .hero-pills {
    display: flex; flex-wrap: wrap; gap: 10px;
    justify-content: center;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
    margin-bottom: 50px;
  }

  .pill {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    padding: 8px 18px;
    border-radius: 2px;
    border: 1px solid var(--border);
    color: var(--muted);
    text-transform: uppercase;
    background: rgba(255,255,255,0.02);
    transition: all 0.3s ease;
  }
  .pill:hover { border-color: var(--accent); color: var(--accent); background: rgba(0,217,255,0.05); }

  .hero-links {
    display: flex; gap: 16px; flex-wrap: wrap; justify-content: center;
    opacity: 0;
    animation: fadeUp 0.8s 1s forwards;
  }

  .btn {
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 14px 28px;
    border-radius: 2px;
    text-decoration: none;
    border: 1px solid;
    transition: all 0.3s ease;
    position: relative; overflow: hidden;
  }
  .btn::before {
    content: '';
    position: absolute; inset: 0;
    background: currentColor;
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    opacity: 0.08;
  }
  .btn:hover::before { transform: translateX(0); }
  .btn-primary { color: var(--accent); border-color: var(--accent); }
  .btn-primary:hover { box-shadow: 0 0 30px rgba(0,217,255,0.3); }
  .btn-secondary { color: var(--accent2); border-color: var(--accent2); }
  .btn-secondary:hover { box-shadow: 0 0 30px rgba(0,255,136,0.3); }
  .btn-tertiary { color: var(--muted); border-color: rgba(106,143,168,0.3); }

  .scroll-indicator {
    position: absolute; bottom: 40px; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    opacity: 0; animation: fadeUp 1s 1.4s forwards;
  }
  .scroll-indicator span {
    font-family: 'Space Mono', monospace; font-size: 9px;
    letter-spacing: 3px; color: var(--muted); text-transform: uppercase;
  }
  .scroll-line {
    width: 1px; height: 60px;
    background: linear-gradient(to bottom, var(--accent), transparent);
    animation: scroll-pulse 2s ease-in-out infinite;
  }
  @keyframes scroll-pulse { 0%,100%{opacity:0.3} 50%{opacity:1} }

  @keyframes fadeUp { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }

  /* Sections */
  .section {
    position: relative; z-index: 1;
    max-width: 1200px; margin: 0 auto;
    padding: 100px 40px;
  }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px; letter-spacing: 5px;
    color: var(--accent); text-transform: uppercase;
    margin-bottom: 16px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-label::after {
    content: ''; flex: 1; height: 1px;
    background: linear-gradient(to right, var(--border), transparent);
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(36px, 5vw, 64px);
    font-weight: 800; letter-spacing: -2px;
    color: var(--text);
    margin-bottom: 60px;
    line-height: 1;
  }
  .section-title em { font-style: normal; color: var(--accent); }

  /* About / Code block */
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 40px; align-items: start;
  }
  @media (max-width: 800px) { .about-grid { grid-template-columns: 1fr; } }

  .code-block {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    font-family: 'Space Mono', monospace;
  }
  .code-header {
    padding: 14px 20px;
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 8px;
  }
  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-r { background: #ff5f56; }
  .dot-y { background: #ffbd2e; }
  .dot-g { background: #27c93f; }
  .code-filename {
    font-size: 11px; color: var(--muted); letter-spacing: 1px; margin-left: 8px;
  }
  .code-body { padding: 28px; font-size: 13px; line-height: 2; }
  .c-key { color: var(--accent); }
  .c-val { color: var(--accent2); }
  .c-str { color: #f9a03c; }
  .c-com { color: var(--muted); font-style: italic; }
  .c-brace { color: #c792ea; }

  .about-info { display: flex; flex-direction: column; gap: 28px; }

  .info-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 28px;
    position: relative; overflow: hidden;
    transition: border-color 0.3s ease, transform 0.3s ease;
  }
  .info-card::before {
    content: '';
    position: absolute; top: 0; left: 0;
    width: 3px; height: 100%;
    background: var(--accent);
  }
  .info-card:hover { border-color: rgba(0,217,255,0.3); transform: translateX(6px); }

  .info-card h3 {
    font-family: 'Syne', sans-serif; font-size: 13px;
    letter-spacing: 3px; text-transform: uppercase;
    color: var(--muted); margin-bottom: 12px;
  }
  .info-card p {
    font-size: 15px; color: var(--text); line-height: 1.7;
  }
  .info-card .highlight { color: var(--accent); font-weight: 500; }

  .focus-list { list-style: none; display: flex; flex-direction: column; gap: 8px; }
  .focus-list li {
    font-size: 14px; color: var(--text);
    display: flex; align-items: center; gap: 10px;
    padding: 8px 0; border-bottom: 1px solid var(--border);
  }
  .focus-list li:last-child { border-bottom: none; }
  .focus-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--accent2); flex-shrink: 0; }

  /* Skills */
  .skills-container { display: flex; flex-direction: column; gap: 48px; }

  .skill-category { }

  .skill-cat-label {
    font-family: 'Space Mono', monospace;
    font-size: 11px; letter-spacing: 3px; text-transform: uppercase;
    color: var(--accent); margin-bottom: 20px;
    display: flex; align-items: center; gap: 10px;
  }
  .skill-cat-label::after { content: ''; flex: 1; height: 1px; background: var(--border); }

  .skill-tags { display: flex; flex-wrap: wrap; gap: 10px; }

  .skill-tag {
    font-family: 'Space Mono', monospace;
    font-size: 12px; letter-spacing: 1px;
    padding: 10px 16px; border-radius: 2px;
    border: 1px solid var(--border);
    color: var(--text);
    background: var(--surface);
    cursor: default;
    transition: all 0.25s ease;
    position: relative; overflow: hidden;
  }
  .skill-tag::after {
    content: '';
    position: absolute; bottom: 0; left: 0;
    width: 0; height: 2px;
    background: var(--accent);
    transition: width 0.3s ease;
  }
  .skill-tag:hover { color: var(--accent); border-color: rgba(0,217,255,0.4); background: rgba(0,217,255,0.05); }
  .skill-tag:hover::after { width: 100%; }
  .skill-tag.accent2::after { background: var(--accent2); }
  .skill-tag.accent2:hover { color: var(--accent2); border-color: rgba(0,255,136,0.4); background: rgba(0,255,136,0.05); }
  .skill-tag.accent3::after { background: var(--accent3); }
  .skill-tag.accent3:hover { color: var(--accent3); border-color: rgba(255,107,53,0.4); background: rgba(255,107,53,0.05); }

  /* Philosophy */
  .philosophy-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 24px;
  }

  .phil-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 36px 28px;
    position: relative; overflow: hidden;
    transition: all 0.3s ease;
  }
  .phil-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 2px;
  }
  .phil-card:nth-child(1)::before { background: var(--accent); }
  .phil-card:nth-child(2)::before { background: var(--accent2); }
  .phil-card:nth-child(3)::before { background: var(--accent3); }
  .phil-card:nth-child(4)::before { background: var(--gold); }
  .phil-card:nth-child(5)::before { background: #c792ea; }

  .phil-card:hover { transform: translateY(-6px); box-shadow: var(--glow); }

  .phil-num {
    font-family: 'Syne', sans-serif;
    font-size: 64px; font-weight: 800;
    color: rgba(255,255,255,0.04);
    position: absolute; top: 10px; right: 20px;
    line-height: 1;
  }

  .phil-title {
    font-family: 'Space Mono', monospace;
    font-size: 10px; letter-spacing: 3px;
    text-transform: uppercase; color: var(--muted);
    margin-bottom: 14px;
  }

  .phil-value {
    font-family: 'Syne', sans-serif;
    font-size: 18px; font-weight: 600;
    color: var(--text); line-height: 1.5;
    margin-bottom: 12px;
  }

  .phil-desc {
    font-size: 13px; color: var(--muted); line-height: 1.7;
  }

  /* Connect */
  .connect-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 16px;
  }

  .connect-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 28px 24px;
    text-decoration: none;
    display: flex; flex-direction: column; gap: 12px;
    transition: all 0.3s ease;
    position: relative; overflow: hidden;
  }
  .connect-card::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(0,217,255,0.05), transparent);
    opacity: 0; transition: opacity 0.3s;
  }
  .connect-card:hover { transform: translateY(-4px); border-color: rgba(0,217,255,0.3); }
  .connect-card:hover::before { opacity: 1; }

  .connect-icon { font-size: 28px; }
  .connect-platform {
    font-family: 'Space Mono', monospace;
    font-size: 10px; letter-spacing: 3px;
    text-transform: uppercase; color: var(--muted);
  }
  .connect-handle {
    font-family: 'Syne', sans-serif;
    font-size: 16px; font-weight: 600; color: var(--text);
  }
  .connect-arrow {
    font-size: 18px; color: var(--accent);
    transition: transform 0.3s ease;
  }
  .connect-card:hover .connect-arrow { transform: translate(4px, -4px); }

  /* Mission */
  .mission-block {
    max-width: 900px; margin: 0 auto; text-align: center;
  }
  .mission-quote {
    font-family: 'Syne', sans-serif;
    font-size: clamp(22px, 3.5vw, 36px);
    font-weight: 600; line-height: 1.5;
    color: var(--text); margin-bottom: 32px;
  }
  .mission-quote em { font-style: normal; color: var(--accent); }

  .seeking-tags { display: flex; flex-wrap: wrap; gap: 12px; justify-content: center; }
  .seeking-tag {
    font-family: 'Space Mono', monospace; font-size: 12px;
    padding: 10px 20px; border-radius: 2px;
    border: 1px solid var(--border); color: var(--muted);
    background: var(--surface);
    transition: all 0.3s ease; letter-spacing: 1px;
  }
  .seeking-tag:hover { color: var(--accent2); border-color: var(--accent2); background: rgba(0,255,136,0.05); }

  /* Divider */
  .divider {
    position: relative; z-index: 1;
    height: 1px; margin: 0 40px;
    background: linear-gradient(to right, transparent, var(--border), transparent);
  }

  /* Footer */
  footer {
    position: relative; z-index: 1;
    text-align: center; padding: 60px 40px;
    border-top: 1px solid var(--border);
  }
  .footer-name {
    font-family: 'Syne', sans-serif;
    font-size: 48px; font-weight: 800;
    letter-spacing: -2px;
    color: rgba(255,255,255,0.05);
    margin-bottom: 16px;
  }
  .footer-text {
    font-family: 'Space Mono', monospace;
    font-size: 11px; letter-spacing: 3px;
    color: var(--muted); text-transform: uppercase;
  }
  .footer-text span { color: var(--accent); }

  /* Animated entrance for sections */
  .reveal { opacity: 0; transform: translateY(40px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* Stats row */
  .stats-row {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 24px; margin-bottom: 60px;
  }
  @media (max-width: 600px) { .stats-row { grid-template-columns: 1fr; } }

  .stat-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 4px; padding: 32px 24px; text-align: center;
    transition: all 0.3s ease;
  }
  .stat-card:hover { border-color: rgba(0,217,255,0.3); transform: translateY(-4px); }

  .stat-num {
    font-family: 'Syne', sans-serif; font-size: 48px; font-weight: 800;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    line-height: 1; margin-bottom: 8px;
  }
  .stat-label {
    font-family: 'Space Mono', monospace; font-size: 10px;
    letter-spacing: 3px; text-transform: uppercase; color: var(--muted);
  }

  /* Quote block */
  .quote-block {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 4px; padding: 40px 48px;
    position: relative; overflow: hidden;
    margin-top: 60px;
  }
  .quote-block::before {
    content: '"';
    font-family: 'Syne', sans-serif; font-size: 200px; font-weight: 800;
    color: rgba(0,217,255,0.04); position: absolute;
    top: -30px; left: 20px; line-height: 1;
    pointer-events: none;
  }
  .quote-text {
    font-family: 'Syne', sans-serif; font-size: 20px; font-weight: 600;
    color: var(--text); line-height: 1.7; position: relative; z-index: 1;
  }
  .quote-source {
    font-family: 'Space Mono', monospace; font-size: 11px;
    color: var(--muted); letter-spacing: 2px; text-transform: uppercase;
    margin-top: 16px; position: relative; z-index: 1;
  }

</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- HERO -->
<section class="hero">
  <div class="hero-orb orb-1"></div>
  <div class="hero-orb orb-2"></div>
  <div class="hero-orb orb-3"></div>

  <div class="hero-tag">Portfolio · 2025</div>
  <h1 class="hero-name">Jashwin Singh</h1>
  <p class="hero-subtitle">Software Engineering Student · <span>Suva, Fiji 🌴</span></p>

  <div class="hero-pills">
    <span class="pill">Full-Stack Developer</span>
    <span class="pill">Mobile · Web · Cloud</span>
    <span class="pill">AI/ML Enthusiast</span>
    <span class="pill">Open Source Advocate</span>
  </div>

  <div class="hero-links">
    <a href="https://jashwinsingh.com" class="btn btn-primary" target="_blank">🌐 Website</a>
    <a href="https://github.com/jashwinsingh11" class="btn btn-secondary" target="_blank">GitHub</a>
    <a href="https://linkedin.com/in/jashwinsingh" class="btn btn-tertiary" target="_blank">LinkedIn</a>
    <a href="mailto:hello@jashwinsingh.com" class="btn btn-tertiary">Email</a>
  </div>

  <div class="scroll-indicator">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<div class="divider"></div>

<!-- ABOUT -->
<section class="section reveal" id="about">
  <div class="section-label">01 &mdash; About</div>
  <h2 class="section-title">Who <em>I am</em></h2>

  <div class="stats-row">
    <div class="stat-card">
      <div class="stat-num">10+</div>
      <div class="stat-label">Tech Stacks</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">∞</div>
      <div class="stat-label">Curiosity Level</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">1</div>
      <div class="stat-label">Goal: Make a Difference</div>
    </div>
  </div>

  <div class="about-grid">
    <div class="code-block">
      <div class="code-header">
        <div class="dot dot-r"></div>
        <div class="dot dot-y"></div>
        <div class="dot dot-g"></div>
        <span class="code-filename">jashwin.ts</span>
      </div>
      <div class="code-body">
        <span class="c-key">const</span> <span class="c-val">jashwin</span>: <span class="c-str">Developer</span> = {<br/>
        &nbsp;&nbsp;<span class="c-key">name</span>: <span class="c-str">"Jashwin Singh"</span>,<br/>
        &nbsp;&nbsp;<span class="c-key">title</span>: <span class="c-str">"Software Engineering Student"</span>,<br/>
        &nbsp;&nbsp;<span class="c-key">location</span>: <span class="c-str">"Suva, Fiji 🌴"</span>,<br/>
        &nbsp;&nbsp;<span class="c-key">education</span>: <span class="c-str">"Bachelor of Software Engineering"</span>,<br/>
        <br/>
        &nbsp;&nbsp;<span class="c-key">currentFocus</span>: [<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;<span class="c-str">"🔨 Scalable full-stack applications"</span>,<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;<span class="c-str">"📱 Seamless mobile experiences"</span>,<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;<span class="c-str">"🤖 AI/ML innovations"</span>,<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;<span class="c-str">"☁️ Cloud-native solutions"</span><br/>
        &nbsp;&nbsp;],<br/>
        <br/>
        &nbsp;&nbsp;<span class="c-key">lifeGoal</span>: <span class="c-str">"Building products that make a difference 🚀"</span><br/>
        <span class="c-brace">}</span>;<br/>
        <br/>
        <span class="c-com">// Philosophy in 4 lines:</span><br/>
        <span class="c-com">// code: "Clean, efficient, and maintainable"</span><br/>
        <span class="c-com">// design: "User-centric and accessible"</span><br/>
        <span class="c-com">// learning: "Continuous and passionate"</span><br/>
        <span class="c-com">// collaboration: "Open-source advocate"</span>
      </div>
    </div>

    <div class="about-info">
      <div class="info-card">
        <h3>Education</h3>
        <p>Pursuing a <span class="highlight">Bachelor of Software Engineering</span>, building strong foundations across the full development spectrum — from algorithms to cloud architecture.</p>
      </div>
      <div class="info-card">
        <h3>Current Focus</h3>
        <ul class="focus-list">
          <li><div class="focus-dot"></div>Building scalable full-stack applications</li>
          <li><div class="focus-dot"></div>Crafting seamless mobile experiences</li>
          <li><div class="focus-dot"></div>Exploring AI/ML innovations</li>
          <li><div class="focus-dot"></div>Architecting cloud-native solutions</li>
        </ul>
      </div>
      <div class="info-card">
        <h3>Location</h3>
        <p>Based in <span class="highlight">Suva, Fiji 🌴</span> — developing world-class software from a Pacific island paradise. Remote-ready, globally minded.</p>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- SKILLS -->
<section class="section reveal" id="skills">
  <div class="section-label">02 &mdash; Skills</div>
  <h2 class="section-title">Technologies &amp; <em>Expertise</em></h2>

  <div class="skills-container">
    <div class="skill-category">
      <div class="skill-cat-label">Languages</div>
      <div class="skill-tags">
        <span class="skill-tag">Python</span>
        <span class="skill-tag">TypeScript</span>
        <span class="skill-tag">JavaScript</span>
        <span class="skill-tag">Java</span>
        <span class="skill-tag">Kotlin</span>
        <span class="skill-tag">Swift</span>
        <span class="skill-tag">C++</span>
        <span class="skill-tag">C#</span>
        <span class="skill-tag">PHP</span>
        <span class="skill-tag">Go</span>
      </div>
    </div>
    <div class="skill-category">
      <div class="skill-cat-label">Frontend Development</div>
      <div class="skill-tags">
        <span class="skill-tag accent2">React</span>
        <span class="skill-tag accent2">Next.js</span>
        <span class="skill-tag accent2">Vue</span>
        <span class="skill-tag accent2">Svelte</span>
        <span class="skill-tag accent2">Angular</span>
        <span class="skill-tag accent2">HTML5</span>
        <span class="skill-tag accent2">CSS3</span>
        <span class="skill-tag accent2">Sass</span>
        <span class="skill-tag accent2">Tailwind</span>
        <span class="skill-tag accent2">Material UI</span>
      </div>
    </div>
    <div class="skill-category">
      <div class="skill-cat-label">Backend &amp; APIs</div>
      <div class="skill-tags">
        <span class="skill-tag">Node.js</span>
        <span class="skill-tag">Express</span>
        <span class="skill-tag">NestJS</span>
        <span class="skill-tag">Spring</span>
        <span class="skill-tag">.NET</span>
        <span class="skill-tag">Django</span>
        <span class="skill-tag">Flask</span>
        <span class="skill-tag">FastAPI</span>
        <span class="skill-tag">GraphQL</span>
      </div>
    </div>
    <div class="skill-category">
      <div class="skill-cat-label">Mobile Development</div>
      <div class="skill-tags">
        <span class="skill-tag accent3">React Native</span>
        <span class="skill-tag accent3">Flutter</span>
        <span class="skill-tag accent3">Kotlin</span>
        <span class="skill-tag accent3">Swift</span>
        <span class="skill-tag accent3">Android Studio</span>
        <span class="skill-tag accent3">Xcode</span>
      </div>
    </div>
    <div class="skill-category">
      <div class="skill-cat-label">Databases &amp; Storage</div>
      <div class="skill-tags">
        <span class="skill-tag">PostgreSQL</span>
        <span class="skill-tag">MySQL</span>
        <span class="skill-tag">MongoDB</span>
        <span class="skill-tag">Redis</span>
        <span class="skill-tag">Supabase</span>
        <span class="skill-tag">Firebase</span>
        <span class="skill-tag">DynamoDB</span>
        <span class="skill-tag">Elasticsearch</span>
      </div>
    </div>
    <div class="skill-category">
      <div class="skill-cat-label">Cloud &amp; DevOps</div>
      <div class="skill-tags">
        <span class="skill-tag accent2">AWS</span>
        <span class="skill-tag accent2">Azure</span>
        <span class="skill-tag accent2">GCP</span>
        <span class="skill-tag accent2">Docker</span>
        <span class="skill-tag accent2">Kubernetes</span>
        <span class="skill-tag accent2">Jenkins</span>
        <span class="skill-tag accent2">GitHub Actions</span>
        <span class="skill-tag accent2">Terraform</span>
        <span class="skill-tag accent2">Nginx</span>
      </div>
    </div>
    <div class="skill-category">
      <div class="skill-cat-label">AI/ML &amp; Data Science</div>
      <div class="skill-tags">
        <span class="skill-tag accent3">TensorFlow</span>
        <span class="skill-tag accent3">PyTorch</span>
        <span class="skill-tag accent3">OpenCV</span>
        <span class="skill-tag accent3">scikit-learn</span>
      </div>
    </div>
    <div class="skill-category">
      <div class="skill-cat-label">Tools &amp; Platforms</div>
      <div class="skill-tags">
        <span class="skill-tag">Git</span>
        <span class="skill-tag">GitHub</span>
        <span class="skill-tag">GitLab</span>
        <span class="skill-tag">VS Code</span>
        <span class="skill-tag">IntelliJ IDEA</span>
        <span class="skill-tag">Postman</span>
        <span class="skill-tag">Figma</span>
        <span class="skill-tag">Photoshop</span>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- PHILOSOPHY -->
<section class="section reveal" id="philosophy">
  <div class="section-label">03 &mdash; Philosophy</div>
  <h2 class="section-title">Development <em>Principles</em></h2>

  <div class="philosophy-grid">
    <div class="phil-card">
      <div class="phil-num">01</div>
      <div class="phil-title">User Experience</div>
      <div class="phil-value">Design with empathy, build with purpose</div>
      <div class="phil-desc">Every interface should feel intuitive, accessible, and genuinely delightful to use.</div>
    </div>
    <div class="phil-card">
      <div class="phil-num">02</div>
      <div class="phil-title">Code Quality</div>
      <div class="phil-value">Clean code comes from caring, not rules</div>
      <div class="phil-desc">Maintainable, efficient, and readable code is a sign of craftsmanship — not just compliance.</div>
    </div>
    <div class="phil-card">
      <div class="phil-num">03</div>
      <div class="phil-title">Performance</div>
      <div class="phil-value">Speed is a feature, not a luxury</div>
      <div class="phil-desc">Optimized experiences respect users' time and directly drive product success.</div>
    </div>
    <div class="phil-card">
      <div class="phil-num">04</div>
      <div class="phil-title">Security</div>
      <div class="phil-value">Security by design, not afterthought</div>
      <div class="phil-desc">Build trust into the architecture from day one — not patched on at the end.</div>
    </div>
    <div class="phil-card">
      <div class="phil-num">05</div>
      <div class="phil-title">Mindset</div>
      <div class="phil-value">Stay curious, stay humble, stay hungry</div>
      <div class="phil-desc">Don't just follow trends — create them. Innovation comes from questioning the obvious.</div>
    </div>
  </div>

  <div class="quote-block">
    <div class="quote-text">
      Crafting exceptional digital experiences that not only meet technical excellence but create meaningful impact in people's lives. Every line of code is an opportunity to make a difference.
    </div>
    <div class="quote-source">— Mission Statement</div>
  </div>
</section>

<div class="divider"></div>

<!-- CONNECT -->
<section class="section reveal" id="connect">
  <div class="section-label">04 &mdash; Connect</div>
  <h2 class="section-title">Let's <em>Work Together</em></h2>

  <div class="connect-grid">
    <a href="https://linkedin.com/in/jashwinsingh" class="connect-card" target="_blank">
      <div class="connect-icon">💼</div>
      <div class="connect-platform">Professional</div>
      <div class="connect-handle">LinkedIn</div>
      <div class="connect-arrow">↗</div>
    </a>
    <a href="https://jashwinsingh.com" class="connect-card" target="_blank">
      <div class="connect-icon">🌐</div>
      <div class="connect-platform">Portfolio</div>
      <div class="connect-handle">jashwinsingh.com</div>
      <div class="connect-arrow">↗</div>
    </a>
    <a href="https://github.com/jashwinsingh11" class="connect-card" target="_blank">
      <div class="connect-icon">⚡</div>
      <div class="connect-platform">Development</div>
      <div class="connect-handle">GitHub</div>
      <div class="connect-arrow">↗</div>
    </a>
    <a href="https://stackoverflow.com/users/jashwinsingh" class="connect-card" target="_blank">
      <div class="connect-icon">🧠</div>
      <div class="connect-platform">Knowledge</div>
      <div class="connect-handle">Stack Overflow</div>
      <div class="connect-arrow">↗</div>
    </a>
    <a href="https://twitter.com/jashwinsingh" class="connect-card" target="_blank">
      <div class="connect-icon">🐦</div>
      <div class="connect-platform">Social</div>
      <div class="connect-handle">Twitter / X</div>
      <div class="connect-arrow">↗</div>
    </a>
    <a href="mailto:hello@jashwinsingh.com" class="connect-card">
      <div class="connect-icon">✉️</div>
      <div class="connect-platform">Email</div>
      <div class="connect-handle">hello@jashwinsingh.com</div>
      <div class="connect-arrow">↗</div>
    </a>
  </div>
</section>

<div class="divider"></div>

<!-- SEEKING -->
<section class="section reveal">
  <div class="section-label">05 &mdash; Currently Seeking</div>
  <div class="mission-block">
    <div class="mission-quote">
      Building products that <em>solve real problems</em> and create lasting impact — one commit at a time.
    </div>
    <div class="seeking-tags">
      <span class="seeking-tag">🚀 Innovative Product Development</span>
      <span class="seeking-tag">🤝 Open-Source Collaborations</span>
      <span class="seeking-tag">💼 Remote Full-Stack Roles</span>
      <span class="seeking-tag">🎯 Challenging Freelance Projects</span>
      <span class="seeking-tag">📚 Mentorship &amp; Knowledge Sharing</span>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-name">Jashwin Singh</div>
  <div class="footer-text">Crafting Digital Excellence · <span>Suva, Fiji 🌴</span> · Building Tomorrow's Solutions</div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.transform = `translate(${mx - 6}px, ${my - 6}px)`;
  });

  function animRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.transform = `translate(${rx - 18}px, ${ry - 18}px)`;
    requestAnimationFrame(animRing);
  }
  animRing();

  document.addEventListener('mousedown', () => cursor.style.transform += ' scale(1.8)');
  document.addEventListener('mouseup', () => {});

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
  }, { threshold: 0.1 });
  reveals.forEach(r => observer.observe(r));
</script>
</body>
</html>

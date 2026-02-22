<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Jashwin Singh — Software Engineer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050810;
    --surface: #0c1220;
    --surface2: #111827;
    --cyan: #00e5ff;
    --cyan-dim: rgba(0,229,255,0.12);
    --cyan-glow: rgba(0,229,255,0.35);
    --violet: #7c3aed;
    --violet-dim: rgba(124,58,237,0.15);
    --text: #e2e8f0;
    --text-muted: #64748b;
    --border: rgba(0,229,255,0.1);
    --border-hover: rgba(0,229,255,0.35);
    --grid-color: rgba(0,229,255,0.04);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* ── Grid background ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(var(--grid-color) 1px, transparent 1px),
      linear-gradient(90deg, var(--grid-color) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
  }

  canvas#particles {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 1;
    opacity: 0.5;
  }

  /* ── Layout ── */
  .container {
    position: relative;
    z-index: 2;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 6rem 0 4rem;
    position: relative;
  }

  .hero-eyebrow {
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 0.25em;
    color: var(--cyan);
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.2s forwards;
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }
  .hero-eyebrow::before {
    content: '';
    display: inline-block;
    width: 40px;
    height: 1px;
    background: var(--cyan);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(3.5rem, 10vw, 8rem);
    font-weight: 800;
    line-height: 0.9;
    letter-spacing: -0.03em;
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.35s forwards;
  }

  .hero-name .line1 { color: var(--text); display: block; }
  .hero-name .line2 {
    display: block;
    background: linear-gradient(135deg, var(--cyan) 0%, var(--violet) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-tagline {
    font-size: 1.2rem;
    color: var(--text-muted);
    max-width: 520px;
    margin-bottom: 2.5rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.5s forwards;
    font-weight: 300;
  }

  .hero-tagline strong {
    color: var(--text);
    font-weight: 500;
  }

  .hero-cta {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s 0.65s forwards;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.8rem 1.8rem;
    border-radius: 4px;
    font-family: 'Space Mono', monospace;
    font-size: 0.78rem;
    letter-spacing: 0.05em;
    text-decoration: none;
    transition: all 0.25s;
    cursor: pointer;
    border: none;
  }

  .btn-primary {
    background: var(--cyan);
    color: #000;
    font-weight: 700;
    box-shadow: 0 0 30px var(--cyan-glow);
  }
  .btn-primary:hover {
    background: #fff;
    box-shadow: 0 0 50px var(--cyan-glow);
    transform: translateY(-2px);
  }

  .btn-ghost {
    background: transparent;
    color: var(--cyan);
    border: 1px solid var(--border-hover);
  }
  .btn-ghost:hover {
    background: var(--cyan-dim);
    transform: translateY(-2px);
  }

  .hero-scroll {
    position: absolute;
    bottom: 2.5rem;
    left: 0;
    display: flex;
    align-items: center;
    gap: 0.75rem;
    font-family: 'Space Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.2em;
    color: var(--text-muted);
    text-transform: uppercase;
    opacity: 0;
    animation: fadeUp 1s 1s forwards;
  }
  .hero-scroll::after {
    content: '';
    display: inline-block;
    width: 1px;
    height: 60px;
    background: linear-gradient(to bottom, var(--cyan), transparent);
    animation: scrollLine 1.5s ease-in-out infinite;
  }

  /* ── Section ── */
  section { padding: 7rem 0; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.3em;
    color: var(--cyan);
    text-transform: uppercase;
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }
  .section-label::before {
    content: '';
    display: inline-block;
    width: 30px;
    height: 1px;
    background: var(--cyan);
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 800;
    letter-spacing: -0.02em;
    margin-bottom: 1rem;
  }

  /* ── About ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: start;
    margin-top: 3rem;
  }

  .about-text p {
    color: var(--text-muted);
    margin-bottom: 1.25rem;
    font-size: 1.05rem;
    font-weight: 300;
    line-height: 1.8;
  }
  .about-text p strong { color: var(--text); font-weight: 500; }

  .about-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
  }

  .stat-card {
    background: var(--surface);
    padding: 2rem 1.5rem;
    text-align: center;
    transition: background 0.2s;
  }
  .stat-card:hover { background: var(--surface2); }

  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 2.8rem;
    font-weight: 800;
    color: var(--cyan);
    letter-spacing: -0.03em;
    line-height: 1;
    margin-bottom: 0.4rem;
  }

  .stat-label {
    font-size: 0.78rem;
    color: var(--text-muted);
    font-family: 'Space Mono', monospace;
    letter-spacing: 0.05em;
  }

  /* ── Skills ── */
  .skills-categories {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }

  .skill-category {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 2rem;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .skill-category::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--cyan), var(--violet));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }
  .skill-category:hover {
    border-color: var(--border-hover);
    background: var(--surface2);
    transform: translateY(-4px);
  }
  .skill-category:hover::before { transform: scaleX(1); }

  .skill-cat-title {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--cyan);
    margin-bottom: 1.25rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .skill-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .skill-tag {
    background: var(--cyan-dim);
    color: var(--text);
    border: 1px solid rgba(0,229,255,0.15);
    border-radius: 3px;
    padding: 0.3rem 0.75rem;
    font-size: 0.78rem;
    font-family: 'Space Mono', monospace;
    transition: all 0.2s;
  }
  .skill-tag:hover {
    background: var(--cyan-glow);
    border-color: var(--cyan);
    color: var(--bg);
  }

  /* ── Philosophy ── */
  .philosophy-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }

  .philosophy-card {
    padding: 2.5rem 2rem;
    border: 1px solid var(--border);
    border-radius: 8px;
    background: var(--surface);
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
  }
  .philosophy-card:hover {
    border-color: var(--border-hover);
    transform: translateY(-4px);
  }

  .philosophy-card .card-icon {
    font-size: 2rem;
    margin-bottom: 1.25rem;
    display: block;
  }

  .philosophy-card h3 {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 1.05rem;
    margin-bottom: 0.75rem;
    color: var(--text);
  }

  .philosophy-card p {
    font-size: 0.88rem;
    color: var(--text-muted);
    line-height: 1.7;
  }

  .philosophy-card .card-number {
    position: absolute;
    bottom: 1rem;
    right: 1.25rem;
    font-family: 'Space Mono', monospace;
    font-size: 4rem;
    font-weight: 700;
    color: rgba(0,229,255,0.04);
    line-height: 1;
    pointer-events: none;
    user-select: none;
  }

  /* ── Connect ── */
  .connect-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-top: 3rem;
  }

  .connect-link {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1.25rem 1.5rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    text-decoration: none;
    color: var(--text);
    transition: all 0.25s;
  }
  .connect-link:hover {
    border-color: var(--border-hover);
    background: var(--cyan-dim);
    transform: translateX(4px);
    color: var(--cyan);
  }

  .connect-icon {
    font-size: 1.4rem;
    flex-shrink: 0;
  }

  .connect-info { flex: 1; }
  .connect-platform {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 0.2rem;
  }
  .connect-handle {
    font-weight: 500;
    font-size: 0.9rem;
  }

  .connect-arrow {
    color: var(--cyan);
    opacity: 0;
    transition: opacity 0.2s, transform 0.2s;
    font-family: 'Space Mono', monospace;
  }
  .connect-link:hover .connect-arrow {
    opacity: 1;
    transform: translateX(4px);
  }

  /* ── Footer ── */
  footer {
    border-top: 1px solid var(--border);
    padding: 3rem 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    color: var(--text-muted);
    letter-spacing: 0.05em;
    position: relative;
    z-index: 2;
  }

  .footer-logo {
    font-family: 'Syne', sans-serif;
    font-size: 1.1rem;
    font-weight: 800;
    color: var(--text);
    letter-spacing: -0.02em;
  }

  .footer-logo span { color: var(--cyan); }

  /* ── Animations ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @keyframes scrollLine {
    0%, 100% { transform: scaleY(1); opacity: 1; }
    50% { transform: scaleY(0.3); opacity: 0.4; }
  }

  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 20px var(--cyan-glow); }
    50% { box-shadow: 0 0 50px var(--cyan-glow), 0 0 80px var(--cyan-glow); }
  }

  .fade-in-up {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s, transform 0.7s;
  }
  .fade-in-up.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* ── Code block ── */
  .code-block {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 2rem;
    font-family: 'Space Mono', monospace;
    font-size: 0.82rem;
    color: var(--text-muted);
    line-height: 1.9;
    overflow-x: auto;
    margin-top: 3rem;
    position: relative;
  }

  .code-block::before {
    content: '● ● ●';
    display: block;
    color: #374151;
    font-size: 0.75rem;
    letter-spacing: 0.4em;
    margin-bottom: 1.5rem;
  }

  .code-block .kw { color: var(--cyan); }
  .code-block .str { color: #a3e635; }
  .code-block .prop { color: #f59e0b; }
  .code-block .comment { color: #374151; }

  /* ── Divider ── */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    margin: 0;
    opacity: 0.25;
  }

  /* Responsive */
  @media (max-width: 768px) {
    .about-grid { grid-template-columns: 1fr; gap: 2.5rem; }
    .hero-name { font-size: clamp(3rem, 15vw, 6rem); }
    footer { flex-direction: column; text-align: center; }
  }

  /* Glow orbs */
  .orb {
    position: fixed;
    border-radius: 50%;
    pointer-events: none;
    z-index: 0;
    filter: blur(80px);
  }
  .orb-1 {
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(0,229,255,0.06) 0%, transparent 70%);
    top: -100px; right: -100px;
  }
  .orb-2 {
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(124,58,237,0.07) 0%, transparent 70%);
    bottom: 20%; left: -100px;
  }
</style>
</head>
<body>

<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<canvas id="particles"></canvas>

<!-- ── HERO ── -->
<section class="hero">
  <div class="container">
    <div class="hero-eyebrow">Suva, Fiji 🌴 — Software Engineering Student</div>
    <h1 class="hero-name">
      <span class="line1">Jashwin</span>
      <span class="line2">Singh.</span>
    </h1>
    <p class="hero-tagline">
      Building <strong>full-stack experiences</strong> at the intersection of design and engineering.
      Passionate about <strong>AI, mobile</strong>, and products that actually matter.
    </p>
    <div class="hero-cta">
      <a href="https://jashwinsingh.com" class="btn btn-primary" target="_blank">↗ View Portfolio</a>
      <a href="mailto:hello@jashwinsingh.com" class="btn btn-ghost">Say Hello</a>
    </div>
    <div class="hero-scroll">Scroll to explore</div>
  </div>
</section>

<div class="divider"></div>

<!-- ── ABOUT ── -->
<section id="about">
  <div class="container">
    <div class="section-label fade-in-up">About</div>
    <h2 class="section-title fade-in-up">Who I Am</h2>
    <div class="about-grid">
      <div class="about-text fade-in-up">
        <p>I'm a <strong>Bachelor of Software Engineering</strong> student based in Fiji, building software that is thoughtful, performant, and beautiful. I care deeply about the craft of writing code — not just making things work, but making them work <strong>well</strong>.</p>
        <p>My toolkit spans the full stack: from pixel-perfect UIs in <strong>React and Next.js</strong> to robust APIs in <strong>Node.js and Python</strong>, scalable cloud infrastructure on <strong>AWS and GCP</strong>, and native mobile apps for iOS and Android.</p>
        <p>Currently exploring the frontier of <strong>AI/ML</strong> and how it can be embedded meaningfully into products — not as a feature, but as genuine value.</p>
        <div style="margin-top: 2rem;">
          <a href="https://github.com/jashwinsingh11" class="btn btn-ghost" style="font-size:0.75rem;" target="_blank">↗ GitHub Profile</a>
        </div>
      </div>
      <div class="about-stats fade-in-up">
        <div class="stat-card">
          <div class="stat-num">∞</div>
          <div class="stat-label">Lines of Curiosity</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">10+</div>
          <div class="stat-label">Tech Stacks</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">Full</div>
          <div class="stat-label">Stack Coverage</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">🌴</div>
          <div class="stat-label">Building from Paradise</div>
        </div>
      </div>
    </div>

    <!-- Code snippet -->
    <div class="code-block fade-in-up">
      <span class="kw">const</span> jashwin = {<br>
      &nbsp;&nbsp;<span class="prop">expertise</span>: [<span class="str">"React"</span>, <span class="str">"Next.js"</span>, <span class="str">"Node.js"</span>, <span class="str">"Flutter"</span>, <span class="str">"AWS"</span>, <span class="str">"TensorFlow"</span>],<br>
      &nbsp;&nbsp;<span class="prop">currentFocus</span>: <span class="str">"Building AI-powered full-stack products"</span>,<br>
      &nbsp;&nbsp;<span class="prop">openTo</span>: [<span class="str">"Remote roles"</span>, <span class="str">"Freelance"</span>, <span class="str">"Open source"</span>, <span class="str">"Collabs"</span>],<br>
      &nbsp;&nbsp;<span class="prop">philosophy</span>: <span class="str">"Clean code isn't written by following rules — it's written by caring."</span>,<br>
      &nbsp;&nbsp;<span class="prop">email</span>: <span class="str">"hello@jashwinsingh.com"</span><br>
      };<br><br>
      <span class="comment">// Let's build something extraordinary together 🚀</span>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ── SKILLS ── -->
<section id="skills">
  <div class="container">
    <div class="section-label fade-in-up">Expertise</div>
    <h2 class="section-title fade-in-up">Skills &amp; Stack</h2>

    <div class="skills-categories">

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">⚡ Languages</div>
        <div class="skill-tags">
          <span class="skill-tag">TypeScript</span>
          <span class="skill-tag">Python</span>
          <span class="skill-tag">JavaScript</span>
          <span class="skill-tag">Java</span>
          <span class="skill-tag">Kotlin</span>
          <span class="skill-tag">Swift</span>
          <span class="skill-tag">Go</span>
          <span class="skill-tag">C++</span>
        </div>
      </div>

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">🎨 Frontend</div>
        <div class="skill-tags">
          <span class="skill-tag">React</span>
          <span class="skill-tag">Next.js</span>
          <span class="skill-tag">Vue</span>
          <span class="skill-tag">Svelte</span>
          <span class="skill-tag">TypeScript</span>
          <span class="skill-tag">Tailwind CSS</span>
          <span class="skill-tag">Framer Motion</span>
        </div>
      </div>

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">⚙️ Backend</div>
        <div class="skill-tags">
          <span class="skill-tag">Node.js</span>
          <span class="skill-tag">FastAPI</span>
          <span class="skill-tag">Spring Boot</span>
          <span class="skill-tag">NestJS</span>
          <span class="skill-tag">Django</span>
          <span class="skill-tag">GraphQL</span>
          <span class="skill-tag">REST</span>
        </div>
      </div>

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">📱 Mobile</div>
        <div class="skill-tags">
          <span class="skill-tag">React Native</span>
          <span class="skill-tag">Flutter</span>
          <span class="skill-tag">Kotlin</span>
          <span class="skill-tag">Swift</span>
          <span class="skill-tag">Expo</span>
        </div>
      </div>

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">☁️ Cloud & DevOps</div>
        <div class="skill-tags">
          <span class="skill-tag">AWS</span>
          <span class="skill-tag">GCP</span>
          <span class="skill-tag">Azure</span>
          <span class="skill-tag">Docker</span>
          <span class="skill-tag">Kubernetes</span>
          <span class="skill-tag">Terraform</span>
          <span class="skill-tag">GitHub Actions</span>
        </div>
      </div>

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">🤖 AI / ML</div>
        <div class="skill-tags">
          <span class="skill-tag">TensorFlow</span>
          <span class="skill-tag">PyTorch</span>
          <span class="skill-tag">Scikit-learn</span>
          <span class="skill-tag">OpenCV</span>
          <span class="skill-tag">LLM APIs</span>
          <span class="skill-tag">RAG</span>
        </div>
      </div>

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">🗄️ Databases</div>
        <div class="skill-tags">
          <span class="skill-tag">PostgreSQL</span>
          <span class="skill-tag">MongoDB</span>
          <span class="skill-tag">Redis</span>
          <span class="skill-tag">Firebase</span>
          <span class="skill-tag">Supabase</span>
          <span class="skill-tag">DynamoDB</span>
        </div>
      </div>

      <div class="skill-category fade-in-up">
        <div class="skill-cat-title">🛠 Tools</div>
        <div class="skill-tags">
          <span class="skill-tag">Git</span>
          <span class="skill-tag">Figma</span>
          <span class="skill-tag">Postman</span>
          <span class="skill-tag">VS Code</span>
          <span class="skill-tag">IntelliJ</span>
          <span class="skill-tag">Linear</span>
        </div>
      </div>

    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ── PHILOSOPHY ── -->
<section id="philosophy">
  <div class="container">
    <div class="section-label fade-in-up">Principles</div>
    <h2 class="section-title fade-in-up">How I Think</h2>

    <div class="philosophy-grid">

      <div class="philosophy-card fade-in-up">
        <span class="card-icon">🎯</span>
        <h3>User First</h3>
        <p>Great products start with deep empathy. I design with purpose and build with precision — because the user experience is the product.</p>
        <div class="card-number">01</div>
      </div>

      <div class="philosophy-card fade-in-up">
        <span class="card-icon">🔬</span>
        <h3>Clean Code</h3>
        <p>Clean code isn't written by following rules — it's written by <em>caring</em>. Every function, every variable, every abstraction is a deliberate choice.</p>
        <div class="card-number">02</div>
      </div>

      <div class="philosophy-card fade-in-up">
        <span class="card-icon">⚡</span>
        <h3>Performance</h3>
        <p>Speed is a feature, not a luxury. Users don't wait — performance is respect. I optimise from the architecture down.</p>
        <div class="card-number">03</div>
      </div>

      <div class="philosophy-card fade-in-up">
        <span class="card-icon">🔐</span>
        <h3>Security First</h3>
        <p>Security is baked in by design, not bolted on later. Writing secure software is a non-negotiable part of the craft.</p>
        <div class="card-number">04</div>
      </div>

      <div class="philosophy-card fade-in-up">
        <span class="card-icon">♾️</span>
        <h3>Always Learning</h3>
        <p>Stay curious, stay humble, stay hungry. The best engineers are perpetual beginners — there's always more to discover.</p>
        <div class="card-number">05</div>
      </div>

      <div class="philosophy-card fade-in-up">
        <span class="card-icon">🤝</span>
        <h3>Build Together</h3>
        <p>Alone we can do so little; together we can do so much. I believe in open source, shared knowledge, and lifting others up.</p>
        <div class="card-number">06</div>
      </div>

    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ── CONNECT ── -->
<section id="connect">
  <div class="container">
    <div class="section-label fade-in-up">Contact</div>
    <h2 class="section-title fade-in-up">Let's Connect</h2>
    <p style="color: var(--text-muted); margin-top: 0.75rem; margin-bottom: 0; font-weight: 300; max-width: 480px;" class="fade-in-up">
      Always open to interesting problems, collaborations, or a good conversation about tech.
    </p>

    <div class="connect-grid">
      <a href="https://jashwinsingh.com" class="connect-link fade-in-up" target="_blank">
        <div class="connect-icon">🌐</div>
        <div class="connect-info">
          <div class="connect-platform">Portfolio</div>
          <div class="connect-handle">jashwinsingh.com</div>
        </div>
        <div class="connect-arrow">→</div>
      </a>

      <a href="https://github.com/jashwinsingh11" class="connect-link fade-in-up" target="_blank">
        <div class="connect-icon">🐙</div>
        <div class="connect-info">
          <div class="connect-platform">GitHub</div>
          <div class="connect-handle">jashwinsingh11</div>
        </div>
        <div class="connect-arrow">→</div>
      </a>

      <a href="https://linkedin.com/in/jashwinsingh" class="connect-link fade-in-up" target="_blank">
        <div class="connect-icon">💼</div>
        <div class="connect-info">
          <div class="connect-platform">LinkedIn</div>
          <div class="connect-handle">jashwinsingh</div>
        </div>
        <div class="connect-arrow">→</div>
      </a>

      <a href="mailto:hello@jashwinsingh.com" class="connect-link fade-in-up">
        <div class="connect-icon">✉️</div>
        <div class="connect-info">
          <div class="connect-platform">Email</div>
          <div class="connect-handle">hello@jashwinsingh.com</div>
        </div>
        <div class="connect-arrow">→</div>
      </a>

      <a href="https://twitter.com/jashwinsingh" class="connect-link fade-in-up" target="_blank">
        <div class="connect-icon">𝕏</div>
        <div class="connect-info">
          <div class="connect-platform">Twitter / X</div>
          <div class="connect-handle">@jashwinsingh</div>
        </div>
        <div class="connect-arrow">→</div>
      </a>

      <a href="https://stackoverflow.com/users/jashwinsingh" class="connect-link fade-in-up" target="_blank">
        <div class="connect-icon">📚</div>
        <div class="connect-info">
          <div class="connect-platform">Stack Overflow</div>
          <div class="connect-handle">jashwinsingh</div>
        </div>
        <div class="connect-arrow">→</div>
      </a>
    </div>
  </div>
</section>

<!-- ── FOOTER ── -->
<footer>
  <div class="container" style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:1rem; width:100%;">
    <div class="footer-logo">Jashwin<span>.</span></div>
    <div>Crafting digital excellence — from Suva, Fiji 🌴</div>
    <div>© 2025 — All rights reserved</div>
  </div>
</footer>

<script>
// ── Particles ──
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let particles = [];
let W, H;

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.vx = (Math.random() - 0.5) * 0.25;
    this.vy = (Math.random() - 0.5) * 0.25;
    this.r = Math.random() * 1.5 + 0.3;
    this.alpha = Math.random() * 0.4 + 0.1;
  }
  update() {
    this.x += this.vx;
    this.y += this.vy;
    if (this.x < 0 || this.x > W || this.y < 0 || this.y > H) this.reset();
  }
  draw() {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(0,229,255,${this.alpha})`;
    ctx.fill();
  }
}

for (let i = 0; i < 80; i++) particles.push(new Particle());

function drawLines() {
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if (dist < 120) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = `rgba(0,229,255,${0.06 * (1 - dist/120)})`;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
}

function animate() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => { p.update(); p.draw(); });
  drawLines();
  requestAnimationFrame(animate);
}
animate();

// ── Scroll reveal ──
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
    }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });

document.querySelectorAll('.fade-in-up').forEach((el, i) => {
  el.style.transitionDelay = `${(i % 6) * 0.08}s`;
  observer.observe(el);
});

// ── Orb parallax ──
const orb1 = document.querySelector('.orb-1');
const orb2 = document.querySelector('.orb-2');
window.addEventListener('mousemove', e => {
  const xP = e.clientX / window.innerWidth;
  const yP = e.clientY / window.innerHeight;
  orb1.style.transform = `translate(${xP * -30}px, ${yP * -30}px)`;
  orb2.style.transform = `translate(${xP * 20}px, ${yP * 20}px)`;
});
</script>
</body>
</html>

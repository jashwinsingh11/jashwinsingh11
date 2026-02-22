<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Jashwin Singh — Software Engineer</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: #050810;
    color: #e2e8f0;
    overflow-x: hidden;
    line-height: 1.6;
  }

  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(0,229,255,.035) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,.035) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none; z-index: 0;
  }

  #particles {
    position: fixed; inset: 0;
    width: 100%; height: 100%;
    pointer-events: none; z-index: 1; opacity: .55;
  }

  .orb {
    position: fixed; border-radius: 50%;
    pointer-events: none; z-index: 0; filter: blur(70px);
  }
  .orb1 { width: 600px; height: 600px; top: -150px; right: -150px; background: radial-gradient(circle, rgba(0,229,255,.08) 0%, transparent 65%); }
  .orb2 { width: 500px; height: 500px; bottom: 5%; left: -120px; background: radial-gradient(circle, rgba(124,58,237,.09) 0%, transparent 65%); }

  main { position: relative; z-index: 2; }

  .wrap { max-width: 1060px; margin: 0 auto; padding: 0 2rem; }

  /* ── HERO ── */
  .hero { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; padding: 6rem 0 4rem; }

  .eyebrow {
    font-family: 'Space Mono', monospace; font-size: .7rem;
    letter-spacing: .25em; color: #00e5ff; text-transform: uppercase;
    margin-bottom: 1.5rem; display: flex; align-items: center; gap: .75rem;
    animation: fadeUp .7s .15s both;
  }
  .eyebrow::before { content: ''; width: 36px; height: 1px; background: #00e5ff; flex-shrink: 0; }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(3.5rem, 10vw, 7.5rem);
    font-weight: 800; line-height: .9; letter-spacing: -.03em;
    margin-bottom: 1.5rem;
    animation: fadeUp .8s .3s both;
  }
  .hero-name .line1 { display: block; color: #e2e8f0; }
  .hero-name .line2 {
    display: block;
    background: linear-gradient(135deg, #00e5ff 0%, #7c3aed 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }

  .tagline {
    font-size: 1.1rem; color: #64748b; max-width: 490px;
    margin-bottom: 2.5rem; font-weight: 300; line-height: 1.8;
    animation: fadeUp .8s .45s both;
  }
  .tagline strong { color: #e2e8f0; font-weight: 500; }

  .cta { display: flex; gap: 1rem; flex-wrap: wrap; animation: fadeUp .8s .6s both; }

  .btn {
    display: inline-flex; align-items: center; gap: .5rem;
    padding: .8rem 1.8rem; border-radius: 4px;
    font-family: 'Space Mono', monospace; font-size: .75rem;
    letter-spacing: .06em; text-decoration: none; border: none;
    cursor: pointer; transition: all .22s;
  }
  .btn-primary { background: #00e5ff; color: #000; font-weight: 700; box-shadow: 0 0 28px rgba(0,229,255,.35); }
  .btn-primary:hover { background: #fff; box-shadow: 0 0 50px rgba(0,229,255,.5); transform: translateY(-2px); }
  .btn-ghost { background: transparent; color: #00e5ff; border: 1px solid rgba(0,229,255,.4); }
  .btn-ghost:hover { background: rgba(0,229,255,.1); transform: translateY(-2px); }

  /* ── DIVIDER ── */
  .divider { height: 1px; background: linear-gradient(90deg, transparent, rgba(0,229,255,.25), transparent); }

  /* ── SECTIONS ── */
  section { padding: 5.5rem 0; }

  .sec-label {
    font-family: 'Space Mono', monospace; font-size: .65rem;
    letter-spacing: .3em; color: #00e5ff; text-transform: uppercase;
    margin-bottom: .75rem; display: flex; align-items: center; gap: .75rem;
  }
  .sec-label::before { content: ''; width: 28px; height: 1px; background: #00e5ff; }

  h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 800; letter-spacing: -.02em; margin-bottom: .5rem;
  }

  /* ── ABOUT ── */
  .about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; align-items: start; margin-top: 2.5rem; }

  .about-text p { color: #94a3b8; margin-bottom: 1.2rem; font-size: 1rem; font-weight: 300; line-height: 1.85; }
  .about-text p strong { color: #e2e8f0; font-weight: 500; }

  .stats { display: grid; grid-template-columns: 1fr 1fr; gap: 1px; background: rgba(0,229,255,.1); border: 1px solid rgba(0,229,255,.1); border-radius: 8px; overflow: hidden; }
  .stat { background: #0c1220; padding: 1.6rem 1.25rem; text-align: center; transition: background .2s; }
  .stat:hover { background: #111827; }
  .stat-num { font-family: 'Syne', sans-serif; font-size: 2.5rem; font-weight: 800; color: #00e5ff; line-height: 1; margin-bottom: .3rem; }
  .stat-lbl { font-size: .65rem; color: #64748b; font-family: 'Space Mono', monospace; letter-spacing: .06em; }

  .code-block {
    background: #0c1220; border: 1px solid rgba(0,229,255,.12);
    border-radius: 8px; padding: 1.75rem 2rem;
    font-family: 'Space Mono', monospace; font-size: .78rem;
    color: #64748b; line-height: 2; overflow-x: auto; margin-top: 2.5rem;
  }
  .code-dots { display: flex; gap: 6px; margin-bottom: 1.25rem; }
  .code-dot { width: 10px; height: 10px; border-radius: 50%; }
  .kw { color: #00e5ff; } .prop { color: #f59e0b; } .str { color: #86efac; } .cmt { color: #374151; }

  /* ── SKILLS ── */
  .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 1.25rem; margin-top: 2.5rem; }
  .skill-card { background: #0c1220; border: 1px solid rgba(0,229,255,.1); border-radius: 8px; padding: 1.6rem; transition: all .28s; position: relative; overflow: hidden; }
  .skill-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, #00e5ff, #7c3aed); transform: scaleX(0); transform-origin: left; transition: transform .35s; }
  .skill-card:hover { border-color: rgba(0,229,255,.4); background: #111827; transform: translateY(-4px); }
  .skill-card:hover::before { transform: scaleX(1); }
  .skill-title { font-family: 'Space Mono', monospace; font-size: .63rem; letter-spacing: .15em; text-transform: uppercase; color: #00e5ff; margin-bottom: 1rem; }
  .tags { display: flex; flex-wrap: wrap; gap: .4rem; }
  .tag { background: rgba(0,229,255,.07); color: #cbd5e1; border: 1px solid rgba(0,229,255,.12); border-radius: 3px; padding: .25rem .65rem; font-size: .7rem; font-family: 'Space Mono', monospace; transition: all .18s; cursor: default; }
  .tag:hover { background: rgba(0,229,255,.18); border-color: #00e5ff; color: #fff; }

  /* ── PHILOSOPHY ── */
  .phil-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 1.25rem; margin-top: 2.5rem; }
  .phil-card { padding: 2rem 1.6rem; border: 1px solid rgba(0,229,255,.1); border-radius: 8px; background: #0c1220; position: relative; overflow: hidden; transition: all .28s; }
  .phil-card:hover { border-color: rgba(0,229,255,.4); transform: translateY(-4px); }
  .phil-icon { font-size: 1.75rem; margin-bottom: 1rem; display: block; }
  .phil-card h3 { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 1rem; margin-bottom: .6rem; }
  .phil-card p { font-size: .83rem; color: #64748b; line-height: 1.75; }
  .phil-num { position: absolute; bottom: .5rem; right: 1rem; font-family: 'Space Mono', monospace; font-size: 3.5rem; font-weight: 700; color: rgba(0,229,255,.04); line-height: 1; pointer-events: none; user-select: none; }

  /* ── CONNECT ── */
  .conn-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1rem; margin-top: 2.5rem; }
  .conn-link { display: flex; align-items: center; gap: 1rem; padding: 1.15rem 1.35rem; background: #0c1220; border: 1px solid rgba(0,229,255,.1); border-radius: 8px; text-decoration: none; color: #e2e8f0; transition: all .22s; }
  .conn-link:hover { border-color: rgba(0,229,255,.4); background: rgba(0,229,255,.08); transform: translateX(5px); color: #00e5ff; }
  .conn-icon { font-size: 1.3rem; flex-shrink: 0; }
  .conn-plat { font-family: 'Space Mono', monospace; font-size: .58rem; letter-spacing: .1em; text-transform: uppercase; color: #64748b; margin-bottom: .12rem; }
  .conn-handle { font-size: .85rem; font-weight: 500; }
  .conn-arr { margin-left: auto; color: #00e5ff; opacity: 0; transition: opacity .2s, transform .2s; font-size: .9rem; }
  .conn-link:hover .conn-arr { opacity: 1; transform: translateX(3px); }

  /* ── FOOTER ── */
  footer { border-top: 1px solid rgba(0,229,255,.08); padding: 2.5rem 0; position: relative; z-index: 2; }
  .footer-inner { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem; font-family: 'Space Mono', monospace; font-size: .62rem; color: #475569; letter-spacing: .05em; }
  .footer-logo { font-family: 'Syne', sans-serif; font-size: 1.1rem; font-weight: 800; color: #e2e8f0; letter-spacing: -.02em; }
  .footer-logo span { color: #00e5ff; }

  /* ── REVEAL ── */
  .rv { opacity: 0; transform: translateY(28px); transition: opacity .65s, transform .65s; }
  .rv.in { opacity: 1; transform: translateY(0); }

  @keyframes fadeUp { from { opacity: 0; transform: translateY(24px); } to { opacity: 1; transform: translateY(0); } }

  @media (max-width: 700px) { .about-grid { grid-template-columns: 1fr; gap: 2.5rem; } }
</style>
</head>
<body>

<div class="orb orb1"></div>
<div class="orb orb2"></div>
<canvas id="particles"></canvas>

<main>

  <!-- HERO -->
  <section class="hero">
    <div class="wrap">
      <div class="eyebrow">Suva, Fiji &#127796; &mdash; Software Engineering Student</div>
      <div class="hero-name">
        <span class="line1">Jashwin</span>
        <span class="line2">Singh.</span>
      </div>
      <p class="tagline">
        Building <strong>full-stack experiences</strong> at the intersection of design and engineering.
        Passionate about <strong>AI, mobile</strong>, and products that actually matter.
      </p>
      <div class="cta">
        <a href="https://jashwinsingh.com" class="btn btn-primary" target="_blank">&#8599; View Portfolio</a>
        <a href="mailto:hello@jashwinsingh.com" class="btn btn-ghost">Say Hello</a>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ABOUT -->
  <section>
    <div class="wrap">
      <div class="sec-label rv">About</div>
      <h2 class="rv">Who I Am</h2>
      <div class="about-grid">
        <div class="about-text rv">
          <p>I&rsquo;m a <strong>Bachelor of Software Engineering</strong> student based in Fiji, building software that is thoughtful, performant, and beautiful. I care deeply about the craft &mdash; not just making things work, but making them work <strong>well</strong>.</p>
          <p>My toolkit spans the full stack: pixel-perfect UIs in <strong>React &amp; Next.js</strong>, robust APIs in <strong>Node.js &amp; Python</strong>, scalable cloud on <strong>AWS &amp; GCP</strong>, and native mobile apps for both <strong>iOS and Android</strong>.</p>
          <p>Currently exploring how <strong>AI/ML</strong> can be embedded meaningfully into products &mdash; not as a feature, but as genuine value.</p>
          <div style="margin-top:1.75rem">
            <a href="https://github.com/jashwinsingh11" class="btn btn-ghost" style="font-size:.72rem" target="_blank">&#8599; GitHub Profile</a>
          </div>
        </div>
        <div class="stats rv">
          <div class="stat"><div class="stat-num">&#8734;</div><div class="stat-lbl">Lines of Curiosity</div></div>
          <div class="stat"><div class="stat-num">10+</div><div class="stat-lbl">Tech Stacks</div></div>
          <div class="stat"><div class="stat-num">Full</div><div class="stat-lbl">Stack Coverage</div></div>
          <div class="stat"><div class="stat-num">&#127796;</div><div class="stat-lbl">Paradise HQ</div></div>
        </div>
      </div>

      <div class="code-block rv">
        <div class="code-dots">
          <div class="code-dot" style="background:#ef4444"></div>
          <div class="code-dot" style="background:#f59e0b"></div>
          <div class="code-dot" style="background:#22c55e"></div>
        </div>
        <span class="kw">const</span> jashwin = {<br>
        &nbsp;&nbsp;<span class="prop">expertise</span>: [<span class="str">"React"</span>, <span class="str">"Next.js"</span>, <span class="str">"Node.js"</span>, <span class="str">"Flutter"</span>, <span class="str">"AWS"</span>, <span class="str">"TensorFlow"</span>],<br>
        &nbsp;&nbsp;<span class="prop">currentFocus</span>: <span class="str">"Building AI-powered full-stack products"</span>,<br>
        &nbsp;&nbsp;<span class="prop">openTo</span>: [<span class="str">"Remote roles"</span>, <span class="str">"Freelance"</span>, <span class="str">"Open source"</span>],<br>
        &nbsp;&nbsp;<span class="prop">philosophy</span>: <span class="str">"Clean code isn&rsquo;t written by rules &mdash; it&rsquo;s written by caring."</span>,<br>
        &nbsp;&nbsp;<span class="prop">email</span>: <span class="str">"hello@jashwinsingh.com"</span><br>
        };<br><br>
        <span class="cmt">// Let&rsquo;s build something extraordinary together &#128640;</span>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- SKILLS -->
  <section>
    <div class="wrap">
      <div class="sec-label rv">Expertise</div>
      <h2 class="rv">Skills &amp; Stack</h2>
      <div class="skills-grid">
        <div class="skill-card rv"><div class="skill-title">&#9889; Languages</div><div class="tags"><span class="tag">TypeScript</span><span class="tag">Python</span><span class="tag">JavaScript</span><span class="tag">Java</span><span class="tag">Kotlin</span><span class="tag">Swift</span><span class="tag">Go</span><span class="tag">C++</span></div></div>
        <div class="skill-card rv"><div class="skill-title">&#127912; Frontend</div><div class="tags"><span class="tag">React</span><span class="tag">Next.js</span><span class="tag">Vue</span><span class="tag">Svelte</span><span class="tag">Tailwind CSS</span><span class="tag">Framer Motion</span></div></div>
        <div class="skill-card rv"><div class="skill-title">&#9881; Backend</div><div class="tags"><span class="tag">Node.js</span><span class="tag">FastAPI</span><span class="tag">Spring Boot</span><span class="tag">NestJS</span><span class="tag">Django</span><span class="tag">GraphQL</span></div></div>
        <div class="skill-card rv"><div class="skill-title">&#128241; Mobile</div><div class="tags"><span class="tag">React Native</span><span class="tag">Flutter</span><span class="tag">Kotlin</span><span class="tag">Swift</span><span class="tag">Expo</span></div></div>
        <div class="skill-card rv"><div class="skill-title">&#9729; Cloud &amp; DevOps</div><div class="tags"><span class="tag">AWS</span><span class="tag">GCP</span><span class="tag">Azure</span><span class="tag">Docker</span><span class="tag">Kubernetes</span><span class="tag">Terraform</span><span class="tag">GitHub Actions</span></div></div>
        <div class="skill-card rv"><div class="skill-title">&#129302; AI / ML</div><div class="tags"><span class="tag">TensorFlow</span><span class="tag">PyTorch</span><span class="tag">Scikit-learn</span><span class="tag">OpenCV</span><span class="tag">LLM APIs</span><span class="tag">RAG</span></div></div>
        <div class="skill-card rv"><div class="skill-title">&#128452; Databases</div><div class="tags"><span class="tag">PostgreSQL</span><span class="tag">MongoDB</span><span class="tag">Redis</span><span class="tag">Firebase</span><span class="tag">Supabase</span><span class="tag">DynamoDB</span></div></div>
        <div class="skill-card rv"><div class="skill-title">&#128295; Tools</div><div class="tags"><span class="tag">Git</span><span class="tag">Figma</span><span class="tag">Postman</span><span class="tag">VS Code</span><span class="tag">IntelliJ</span><span class="tag">Linear</span></div></div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- PHILOSOPHY -->
  <section>
    <div class="wrap">
      <div class="sec-label rv">Principles</div>
      <h2 class="rv">How I Think</h2>
      <div class="phil-grid">
        <div class="phil-card rv"><span class="phil-icon">&#127919;</span><h3>User First</h3><p>Great products start with deep empathy. I design with purpose and build with precision &mdash; because the user experience <em>is</em> the product.</p><div class="phil-num">01</div></div>
        <div class="phil-card rv"><span class="phil-icon">&#128302;</span><h3>Clean Code</h3><p>Clean code isn&rsquo;t written by following rules &mdash; it&rsquo;s written by caring. Every function, every abstraction is a deliberate choice.</p><div class="phil-num">02</div></div>
        <div class="phil-card rv"><span class="phil-icon">&#9889;</span><h3>Performance</h3><p>Speed is a feature, not a luxury. Users don&rsquo;t wait &mdash; performance is respect. I optimise from the architecture down to the last byte.</p><div class="phil-num">03</div></div>
        <div class="phil-card rv"><span class="phil-icon">&#128272;</span><h3>Security First</h3><p>Security is baked in by design, never bolted on later. Writing secure software is a non-negotiable part of the craft.</p><div class="phil-num">04</div></div>
        <div class="phil-card rv"><span class="phil-icon">&#9854;</span><h3>Always Learning</h3><p>Stay curious, stay humble, stay hungry. The best engineers are perpetual beginners &mdash; there&rsquo;s always more to discover.</p><div class="phil-num">05</div></div>
        <div class="phil-card rv"><span class="phil-icon">&#129309;</span><h3>Build Together</h3><p>Alone we can do so little; together we can do so much. I believe in open source, shared knowledge, and lifting others up.</p><div class="phil-num">06</div></div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- CONNECT -->
  <section>
    <div class="wrap">
      <div class="sec-label rv">Contact</div>
      <h2 class="rv">Let&rsquo;s Connect</h2>
      <p class="rv" style="color:#64748b;margin-top:.5rem;font-weight:300;max-width:460px;line-height:1.8">
        Always open to interesting problems, collaborations, or a good conversation about tech.
      </p>
      <div class="conn-grid">
        <a class="conn-link rv" href="https://jashwinsingh.com" target="_blank"><div class="conn-icon">&#127760;</div><div><div class="conn-plat">Portfolio</div><div class="conn-handle">jashwinsingh.com</div></div><div class="conn-arr">&#8594;</div></a>
        <a class="conn-link rv" href="https://github.com/jashwinsingh11" target="_blank"><div class="conn-icon">&#128025;</div><div><div class="conn-plat">GitHub</div><div class="conn-handle">jashwinsingh11</div></div><div class="conn-arr">&#8594;</div></a>
        <a class="conn-link rv" href="https://linkedin.com/in/jashwinsingh" target="_blank"><div class="conn-icon">&#128188;</div><div><div class="conn-plat">LinkedIn</div><div class="conn-handle">jashwinsingh</div></div><div class="conn-arr">&#8594;</div></a>
        <a class="conn-link rv" href="mailto:hello@jashwinsingh.com"><div class="conn-icon">&#9993;</div><div><div class="conn-plat">Email</div><div class="conn-handle">hello@jashwinsingh.com</div></div><div class="conn-arr">&#8594;</div></a>
        <a class="conn-link rv" href="https://twitter.com/jashwinsingh" target="_blank"><div class="conn-icon">&#120143;</div><div><div class="conn-plat">Twitter / X</div><div class="conn-handle">@jashwinsingh</div></div><div class="conn-arr">&#8594;</div></a>
        <a class="conn-link rv" href="https://stackoverflow.com/users/jashwinsingh" target="_blank"><div class="conn-icon">&#128218;</div><div><div class="conn-plat">Stack Overflow</div><div class="conn-handle">jashwinsingh</div></div><div class="conn-arr">&#8594;</div></a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="wrap">
      <div class="footer-inner">
        <div class="footer-logo">Jashwin<span>.</span></div>
        <div>Crafting digital excellence &mdash; from Suva, Fiji &#127796;</div>
        <div>&copy; 2025 &mdash; All rights reserved</div>
      </div>
    </div>
  </footer>

</main>

<script>
  // Particles
  var cv = document.getElementById('particles');
  var cx = cv.getContext('2d');
  var W, H, pts = [];

  function resize() { W = cv.width = window.innerWidth; H = cv.height = window.innerHeight; }
  resize();
  window.addEventListener('resize', resize);

  for (var i = 0; i < 70; i++) {
    pts.push({
      x: Math.random() * window.innerWidth,
      y: Math.random() * window.innerHeight,
      vx: (Math.random() - .5) * .35,
      vy: (Math.random() - .5) * .35,
      r: Math.random() * 1.5 + .3,
      a: Math.random() * .4 + .1
    });
  }

  function draw() {
    cx.clearRect(0, 0, W, H);
    for (var i = 0; i < pts.length; i++) {
      var p = pts[i];
      p.x += p.vx; p.y += p.vy;
      if (p.x < 0 || p.x > W) p.vx *= -1;
      if (p.y < 0 || p.y > H) p.vy *= -1;
      for (var j = i + 1; j < pts.length; j++) {
        var q = pts[j];
        var d = Math.sqrt((p.x-q.x)*(p.x-q.x) + (p.y-q.y)*(p.y-q.y));
        if (d < 110) {
          cx.beginPath(); cx.moveTo(p.x, p.y); cx.lineTo(q.x, q.y);
          cx.strokeStyle = 'rgba(0,229,255,' + (.07 * (1 - d/110)) + ')';
          cx.lineWidth = .5; cx.stroke();
        }
      }
      cx.beginPath(); cx.arc(p.x, p.y, p.r, 0, Math.PI*2);
      cx.fillStyle = 'rgba(0,229,255,' + p.a + ')'; cx.fill();
    }
    requestAnimationFrame(draw);
  }
  draw();

  // Orb parallax
  var o1 = document.querySelector('.orb1'), o2 = document.querySelector('.orb2');
  window.addEventListener('mousemove', function(e) {
    var xp = e.clientX / window.innerWidth, yp = e.clientY / window.innerHeight;
    o1.style.transform = 'translate(' + (xp * -40) + 'px,' + (yp * -40) + 'px)';
    o2.style.transform = 'translate(' + (xp * 30) + 'px,' + (yp * 30) + 'px)';
  });

  // Scroll reveal
  var obs = new IntersectionObserver(function(entries) {
    entries.forEach(function(e) { if (e.isIntersecting) e.target.classList.add('in'); });
  }, { threshold: .1, rootMargin: '0px 0px -30px 0px' });

  document.querySelectorAll('.rv').forEach(function(el, i) {
    el.style.transitionDelay = (i % 5) * .08 + 's';
    obs.observe(el);
  });
</script>
</body>
</html>

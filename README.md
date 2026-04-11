<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dida Dhungana — CS Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=JetBrains+Mono:wght@300;400;500&family=Sora:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg: #04040a;
    --bg2: #080812;
    --bg3: #0c0c1a;
    --card: #0f0f1e;
    --card2: #13132a;
    --accent: #00e5a0;
    --accent2: #00b87d;
    --amber: #f0a500;
    --blue: #3d8ef0;
    --text: #e8eaf2;
    --muted: #6b7096;
    --border: rgba(0,229,160,0.12);
    --border2: rgba(0,229,160,0.25);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Sora', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9999;
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: transform 0.08s ease, width 0.2s, height 0.2s, opacity 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9998;
    width: 36px; height: 36px;
    border: 1px solid rgba(0,229,160,0.5);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: transform 0.18s ease, border-color 0.2s;
  }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--accent2); border-radius: 2px; }

  /* ─── CANVAS ─── */
  #particles-canvas {
    position: fixed; inset: 0; z-index: 0;
    pointer-events: none; opacity: 0.4;
  }

  /* ─── NAV ─── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.2rem 4rem;
    background: rgba(4,4,10,0.8);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--border);
    transition: all 0.3s;
  }
  .nav-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.8rem;
    letter-spacing: 2px;
    color: var(--accent);
    text-decoration: none;
  }
  .nav-links { display: flex; gap: 2.5rem; list-style: none; }
  .nav-links a {
    text-decoration: none;
    font-size: 0.78rem;
    font-weight: 500;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    transition: color 0.2s;
    font-family: 'JetBrains Mono', monospace;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-cta {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    padding: 0.5rem 1.4rem;
    border: 1px solid var(--border2);
    color: var(--accent);
    text-decoration: none;
    border-radius: 2px;
    transition: all 0.25s;
  }
  .nav-cta:hover { background: var(--accent); color: var(--bg); }

  /* ─── HERO ─── */
  #hero {
    position: relative;
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center;
    padding: 0 4rem;
    z-index: 1;
  }
  .hero-eyebrow {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.82rem;
    letter-spacing: 3px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 1.4rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.3s ease forwards;
  }
  .hero-eyebrow::before { content: '> '; color: var(--muted); }

  h1.hero-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(4.5rem, 12vw, 10rem);
    line-height: 0.92;
    letter-spacing: 3px;
    background: linear-gradient(135deg, #ffffff 0%, #a0ffd8 55%, #00e5a0 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    opacity: 0;
    animation: fadeUp 0.8s 0.5s ease forwards;
  }
  .hero-name .glitch {
    position: relative; display: inline-block;
  }
  .hero-name .glitch:hover::before {
    content: attr(data-text);
    position: absolute; left: 3px; top: 0;
    background: linear-gradient(135deg, #ff006e 0%, #ff6b6b 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: glitch1 0.3s steps(2) infinite;
  }
  .hero-name .glitch:hover::after {
    content: attr(data-text);
    position: absolute; left: -3px; top: 0;
    background: linear-gradient(135deg, #00f0ff 0%, #3d8ef0 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: glitch2 0.3s steps(2) infinite;
  }
  @keyframes glitch1 {
    0%{clip-path:polygon(0 15%,100% 15%,100% 40%,0 40%)}
    50%{clip-path:polygon(0 55%,100% 55%,100% 75%,0 75%)}
    100%{clip-path:polygon(0 5%,100% 5%,100% 20%,0 20%)}
  }
  @keyframes glitch2 {
    0%{clip-path:polygon(0 60%,100% 60%,100% 80%,0 80%)}
    50%{clip-path:polygon(0 25%,100% 25%,100% 50%,0 50%)}
    100%{clip-path:polygon(0 70%,100% 70%,100% 90%,0 90%)}
  }

  .hero-subtitle {
    margin-top: 1.8rem;
    font-size: 1.05rem;
    color: var(--muted);
    font-weight: 300;
    max-width: 560px;
    line-height: 1.7;
    opacity: 0;
    animation: fadeUp 0.8s 0.7s ease forwards;
  }
  .hero-subtitle span { color: var(--text); font-weight: 500; }

  .typing-wrap {
    display: inline-block;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.95rem;
    color: var(--accent);
    margin-top: 1rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.9s ease forwards;
  }
  .typing-cursor {
    display: inline-block;
    width: 2px; height: 1.1em;
    background: var(--accent);
    vertical-align: text-bottom;
    margin-left: 2px;
    animation: blink 1s steps(1) infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  .hero-actions {
    display: flex; gap: 1.2rem; margin-top: 2.8rem; flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s 1.1s ease forwards;
  }
  .btn {
    display: inline-flex; align-items: center; gap: 0.5rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.8rem; letter-spacing: 1.5px;
    text-transform: uppercase;
    text-decoration: none;
    padding: 0.85rem 2rem;
    border-radius: 2px;
    transition: all 0.25s ease;
    position: relative; overflow: hidden;
  }
  .btn-primary {
    background: var(--accent);
    color: var(--bg);
    font-weight: 600;
  }
  .btn-primary:hover {
    background: #00ffb0;
    transform: translateY(-2px);
    box-shadow: 0 12px 30px rgba(0,229,160,0.3);
  }
  .btn-outline {
    border: 1px solid var(--border2);
    color: var(--accent);
  }
  .btn-outline:hover {
    border-color: var(--accent);
    background: rgba(0,229,160,0.07);
    transform: translateY(-2px);
  }

  .hero-scroll {
    position: absolute; bottom: 2.5rem; left: 4rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem; letter-spacing: 2px;
    color: var(--muted); text-transform: uppercase;
    display: flex; align-items: center; gap: 0.8rem;
    opacity: 0; animation: fadeUp 0.8s 1.4s ease forwards;
  }
  .scroll-line {
    width: 50px; height: 1px;
    background: linear-gradient(90deg, var(--accent), transparent);
    position: relative; overflow: hidden;
  }
  .scroll-line::after {
    content: ''; position: absolute; inset: 0;
    background: var(--accent);
    transform: translateX(-100%);
    animation: slide 2s 2s ease infinite;
  }
  @keyframes slide { 0%{transform:translateX(-100%)} 100%{transform:translateX(100%)} }

  /* ─── SECTION SHELL ─── */
  section { position: relative; z-index: 1; }
  .section-inner {
    max-width: 1200px; margin: 0 auto;
    padding: 7rem 4rem;
  }
  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem; letter-spacing: 3px;
    color: var(--accent); text-transform: uppercase;
    margin-bottom: 0.7rem;
    opacity: 0; transform: translateX(-20px);
    transition: opacity 0.6s, transform 0.6s;
  }
  .section-label.revealed { opacity: 1; transform: translateX(0); }
  h2.section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(2.4rem, 5vw, 3.8rem);
    letter-spacing: 2px;
    color: var(--text);
    line-height: 1;
    margin-bottom: 0.3rem;
    opacity: 0; transform: translateY(20px);
    transition: opacity 0.7s 0.1s, transform 0.7s 0.1s;
  }
  h2.section-title.revealed { opacity: 1; transform: translateY(0); }
  .section-divider {
    width: 60px; height: 2px;
    background: linear-gradient(90deg, var(--accent), transparent);
    margin-bottom: 3.5rem;
    opacity: 0; transition: opacity 0.8s 0.2s, width 0.8s 0.2s;
  }
  .section-divider.revealed { opacity: 1; width: 80px; }

  /* ─── ABOUT ─── */
  #about { background: var(--bg2); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: center;
  }
  .about-text p {
    font-size: 1rem; line-height: 1.85;
    color: var(--muted); margin-bottom: 1.2rem; font-weight: 300;
  }
  .about-text p strong { color: var(--text); font-weight: 500; }
  .quote-block {
    border-left: 2px solid var(--accent);
    padding: 1.2rem 1.5rem;
    margin-top: 2rem;
    background: rgba(0,229,160,0.04);
    border-radius: 0 4px 4px 0;
  }
  .quote-block p {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.88rem;
    color: var(--accent) !important;
    margin: 0 !important;
    font-style: italic;
  }
  .about-stats {
    display: grid; grid-template-columns: 1fr 1fr; gap: 1.2rem;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1.8rem 1.5rem;
    transition: all 0.3s ease;
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.6s, transform 0.6s, border-color 0.3s, background 0.3s;
  }
  .stat-card.revealed { opacity: 1; transform: translateY(0); }
  .stat-card:hover { border-color: var(--border2); background: var(--card2); }
  .stat-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2.8rem; color: var(--accent);
    line-height: 1; margin-bottom: 0.3rem;
  }
  .stat-label {
    font-size: 0.78rem; color: var(--muted); letter-spacing: 1px;
    text-transform: uppercase; font-family: 'JetBrains Mono', monospace;
  }

  /* ─── SKILLS ─── */
  #skills { background: var(--bg); }
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 1.5rem;
  }
  .skill-group {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 1.8rem;
    transition: all 0.3s;
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.6s, transform 0.6s, border-color 0.3s, box-shadow 0.3s;
  }
  .skill-group.revealed { opacity: 1; transform: translateY(0); }
  .skill-group:hover {
    border-color: var(--border2);
    box-shadow: 0 0 30px rgba(0,229,160,0.06);
  }
  .skill-group-header {
    display: flex; align-items: center; gap: 0.8rem;
    margin-bottom: 1.4rem;
  }
  .skill-icon {
    width: 36px; height: 36px;
    border-radius: 6px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1rem;
  }
  .skill-icon.green { background: rgba(0,229,160,0.12); }
  .skill-icon.amber { background: rgba(240,165,0,0.12); }
  .skill-icon.blue  { background: rgba(61,142,240,0.12); }
  .skill-group-title {
    font-size: 0.78rem; letter-spacing: 2px;
    text-transform: uppercase; color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
  }
  .skill-item {
    margin-bottom: 1rem;
  }
  .skill-row {
    display: flex; justify-content: space-between;
    align-items: center; margin-bottom: 0.4rem;
  }
  .skill-name { font-size: 0.88rem; color: var(--text); font-weight: 400; }
  .skill-pct  { font-family: 'JetBrains Mono', monospace; font-size: 0.75rem; color: var(--accent); }
  .skill-bar-bg {
    height: 3px; background: rgba(255,255,255,0.06);
    border-radius: 2px; overflow: hidden;
  }
  .skill-bar-fill {
    height: 100%; border-radius: 2px;
    width: 0; transition: width 1.2s cubic-bezier(.4,0,.2,1);
  }
  .fill-accent { background: linear-gradient(90deg, var(--accent2), var(--accent)); }
  .fill-amber  { background: linear-gradient(90deg, #c07a00, var(--amber)); }
  .fill-blue   { background: linear-gradient(90deg, #1a5fbf, var(--blue)); }

  .tag-cloud { display: flex; flex-wrap: wrap; gap: 0.5rem; margin-top: 0.5rem; }
  .tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.73rem; letter-spacing: 0.5px;
    padding: 0.3rem 0.75rem;
    border-radius: 2px;
    border: 1px solid;
    transition: all 0.2s;
    cursor: default;
  }
  .tag-green { color: var(--accent); border-color: rgba(0,229,160,0.25); }
  .tag-green:hover { background: rgba(0,229,160,0.1); border-color: var(--accent); }
  .tag-amber { color: var(--amber); border-color: rgba(240,165,0,0.25); }
  .tag-amber:hover { background: rgba(240,165,0,0.1); border-color: var(--amber); }
  .tag-blue  { color: var(--blue);  border-color: rgba(61,142,240,0.25); }
  .tag-blue:hover  { background: rgba(61,142,240,0.1); border-color: var(--blue); }

  /* ─── PROJECTS ─── */
  #projects { background: var(--bg2); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
  .projects-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
  }
  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 2rem;
    position: relative; overflow: hidden;
    transition: all 0.35s ease;
    cursor: pointer;
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.6s, transform 0.6s, border-color 0.3s, box-shadow 0.35s;
  }
  .project-card.revealed { opacity: 1; transform: translateY(0); }
  .project-card::before {
    content: ''; position: absolute;
    inset: 0; opacity: 0;
    background: linear-gradient(135deg, rgba(0,229,160,0.04), transparent);
    transition: opacity 0.3s;
  }
  .project-card:hover { border-color: var(--border2); box-shadow: 0 8px 40px rgba(0,229,160,0.08); }
  .project-card:hover::before { opacity: 1; }
  .project-featured {
    background: linear-gradient(135deg, rgba(0,229,160,0.05), rgba(0,229,160,0.02));
    border-color: rgba(0,229,160,0.3);
  }
  .project-badge {
    display: inline-block;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem; letter-spacing: 2px;
    text-transform: uppercase;
    padding: 0.25rem 0.7rem;
    background: rgba(0,229,160,0.12);
    color: var(--accent);
    border-radius: 2px;
    margin-bottom: 1rem;
  }
  .project-title {
    font-size: 1.1rem; font-weight: 600; color: var(--text);
    margin-bottom: 0.7rem; line-height: 1.3;
  }
  .project-desc {
    font-size: 0.88rem; color: var(--muted);
    line-height: 1.7; margin-bottom: 1.5rem; font-weight: 300;
  }
  .project-stack { display: flex; flex-wrap: wrap; gap: 0.4rem; }
  .stack-pill {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    padding: 0.2rem 0.6rem;
    background: rgba(255,255,255,0.05);
    color: var(--muted);
    border-radius: 2px;
    border: 1px solid rgba(255,255,255,0.07);
  }
  .project-arrow {
    position: absolute; top: 1.5rem; right: 1.5rem;
    width: 28px; height: 28px; border-radius: 50%;
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    color: var(--muted); font-size: 0.8rem;
    transition: all 0.25s;
  }
  .project-card:hover .project-arrow {
    border-color: var(--accent); color: var(--accent);
    background: rgba(0,229,160,0.1);
    transform: translate(2px, -2px);
  }

  /* ─── TOOLS ─── */
  #tools { background: var(--bg); }
  .tools-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 1rem;
  }
  .tool-item {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 1.4rem 1rem;
    text-align: center;
    transition: all 0.25s;
    opacity: 0; transform: scale(0.92);
    transition: opacity 0.5s, transform 0.5s, border-color 0.25s, box-shadow 0.25s;
  }
  .tool-item.revealed { opacity: 1; transform: scale(1); }
  .tool-item:hover {
    border-color: var(--border2);
    transform: translateY(-4px) scale(1.02);
    box-shadow: 0 12px 28px rgba(0,229,160,0.08);
  }
  .tool-icon { font-size: 1.6rem; margin-bottom: 0.6rem; display: block; }
  .tool-name {
    font-size: 0.78rem; color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
    letter-spacing: 0.5px;
  }

  /* ─── FOOTER ─── */
  footer {
    background: var(--bg2);
    border-top: 1px solid var(--border);
    padding: 4rem;
    position: relative; z-index: 1;
  }
  .footer-inner {
    max-width: 1200px; margin: 0 auto;
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 2rem;
  }
  .footer-left {}
  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2rem; letter-spacing: 3px;
    color: var(--accent); display: block; margin-bottom: 0.4rem;
  }
  .footer-tagline { font-size: 0.8rem; color: var(--muted); font-style: italic; }
  .footer-links { display: flex; gap: 1.5rem; }
  .footer-links a {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem; letter-spacing: 1.5px;
    color: var(--muted); text-decoration: none;
    text-transform: uppercase; transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--accent); }
  .footer-copy {
    font-size: 0.75rem; color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
    text-align: center; margin-top: 2.5rem;
    border-top: 1px solid var(--border);
    max-width: 1200px; margin: 2.5rem auto 0;
    padding-top: 1.5rem;
  }
  .footer-copy span { color: var(--accent); }

  /* ─── ANIMATIONS ─── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ─── HORIZONTAL RULE GLOW ─── */
  .glow-line {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    margin: 0;
    opacity: 0.3;
  }

  /* DSA Terminal Block */
  .terminal-block {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 1.5rem;
    margin-top: 0.5rem;
    font-family: 'JetBrains Mono', monospace;
  }
  .terminal-header {
    display: flex; gap: 0.4rem; margin-bottom: 1rem;
  }
  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-red { background: #ff5f57; }
  .dot-amber { background: #febc2e; }
  .dot-green { background: #28c840; }
  .terminal-line {
    font-size: 0.82rem; color: var(--muted); line-height: 1.8;
  }
  .terminal-line .cmd { color: var(--accent); }
  .terminal-line .val { color: #f0a500; }
  .terminal-line .cmt { color: #3a3a60; }

  @media (max-width: 900px) {
    nav { padding: 1rem 2rem; }
    .nav-links { display: none; }
    .section-inner { padding: 5rem 2rem; }
    #hero { padding: 0 2rem; }
    .about-grid { grid-template-columns: 1fr; gap: 3rem; }
    .hero-scroll { left: 2rem; }
    footer { padding: 3rem 2rem; }
    .footer-inner { flex-direction: column; }
  }
</style>
</head>
<body>

<!-- Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursor-ring"></div>

<!-- Canvas -->
<canvas id="particles-canvas"></canvas>

<!-- Nav -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">DD</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#tools">Tools</a></li>
  </ul>
  <a href="https://github.com/dida91" target="_blank" class="nav-cta">GitHub ↗</a>
</nav>

<!-- HERO -->
<section id="hero">
  <p class="hero-eyebrow">Hello, World</p>
  <h1 class="hero-name">
    <span class="glitch" data-text="DIDA">DIDA</span><br>
    <span class="glitch" data-text="DHUNGANA">DHUNGANA</span>
  </h1>
  <p class="hero-subtitle">
    <span>Computer Science Student</span> — building strong fundamentals in
    Python, DSA, and applied machine learning. Focused on crafting
    <span>software that actually solves problems.</span>
  </p>
  <div class="typing-wrap">
    <span id="typed-text"></span><span class="typing-cursor"></span>
  </div>
  <div class="hero-actions">
    <a href="#projects" class="btn btn-primary">View Projects</a>
    <a href="https://github.com/dida91" target="_blank" class="btn btn-outline">GitHub ↗</a>
  </div>
  <div class="hero-scroll">
    <div class="scroll-line"></div>
    Scroll to explore
  </div>
</section>

<div class="glow-line"></div>

<!-- ABOUT -->
<section id="about">
  <div class="section-inner">
    <p class="section-label">// 01 — About</p>
    <h2 class="section-title">Who I Am</h2>
    <div class="section-divider"></div>
    <div class="about-grid">
      <div class="about-text">
        <p>
          I'm <strong>Dida Dhungana</strong>, a Computer Science student deeply passionate about
          programming, mathematics, and core CS concepts. I believe that strong fundamentals
          are the bedrock of every great software system.
        </p>
        <p>
          My journey spans from <strong>Python & C programming</strong> to
          <strong>data structures & algorithms</strong>, relational databases,
          operating systems, and entry-level machine learning. I learn by building,
          breaking things, and building again.
        </p>
        <p>
          I practice regularly on <strong>LeetCode</strong> and <strong>HackerRank</strong>,
          and I'm always looking for meaningful projects to challenge my understanding.
        </p>
        <div class="quote-block">
          <p>"Strong fundamentals build strong software."</p>
        </div>
      </div>
      <div class="about-stats">
        <div class="stat-card">
          <div class="stat-num">2+</div>
          <div class="stat-label">Years Coding</div>
        </div>
        <div class="stat-card" style="transition-delay:0.1s">
          <div class="stat-num">50+</div>
          <div class="stat-label">Problems Solved</div>
        </div>
        <div class="stat-card" style="transition-delay:0.2s">
          <div class="stat-num">5+</div>
          <div class="stat-label">Projects Built</div>
        </div>
        <div class="stat-card" style="transition-delay:0.3s">
          <div class="stat-num">∞</div>
          <div class="stat-label">Curiosity Level</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-inner">
    <p class="section-label">// 02 — Skills</p>
    <h2 class="section-title">Expertise</h2>
    <div class="section-divider"></div>

    <div class="skills-grid">

      <!-- Programming -->
      <div class="skill-group">
        <div class="skill-group-header">
          <div class="skill-icon green">💻</div>
          <div class="skill-group-title">Programming</div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Python</span><span class="skill-pct">90%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-accent" data-width="90"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">C Programming</span><span class="skill-pct">60%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-accent" data-width="60"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">OOP Concepts</span><span class="skill-pct">80%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-accent" data-width="80"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Clean Code</span><span class="skill-pct">75%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-accent" data-width="75"></div></div>
        </div>
      </div>

      <!-- DSA -->
      <div class="skill-group" style="transition-delay:0.1s">
        <div class="skill-group-header">
          <div class="skill-icon amber">🧩</div>
          <div class="skill-group-title">DSA & Problem Solving</div>
        </div>
        <div class="terminal-block">
          <div class="terminal-header">
            <div class="dot dot-red"></div>
            <div class="dot dot-amber"></div>
            <div class="dot dot-green"></div>
          </div>
          <div class="terminal-line"><span class="cmd">structures</span> = [<span class="val">"Arrays"</span>, <span class="val">"Linked List"</span>,</div>
          <div class="terminal-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="val">"Stack"</span>, <span class="val">"Queue"</span>,</div>
          <div class="terminal-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="val">"Trees"</span>]</div>
          <div class="terminal-line" style="margin-top:0.5rem"><span class="cmd">platforms</span> = [<span class="val">"LeetCode"</span>, <span class="val">"HackerRank"</span>]</div>
          <div class="terminal-line" style="margin-top:0.5rem"><span class="cmt"># Searching & Sorting mastered</span></div>
        </div>
      </div>

      <!-- Mathematics -->
      <div class="skill-group" style="transition-delay:0.15s">
        <div class="skill-group-header">
          <div class="skill-icon blue">📐</div>
          <div class="skill-group-title">Mathematics</div>
        </div>
        <div class="tag-cloud">
          <span class="tag tag-blue">Algebra</span>
          <span class="tag tag-blue">Calculus</span>
          <span class="tag tag-blue">Probability</span>
          <span class="tag tag-blue">Statistics</span>
          <span class="tag tag-blue">Matrices</span>
        </div>
        <div style="margin-top:1.2rem">
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Applied Math</span><span class="skill-pct">72%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-blue" data-width="72"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Linear Algebra</span><span class="skill-pct">68%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-blue" data-width="68"></div></div>
        </div>
        </div>
      </div>

      <!-- Data Science & ML -->
      <div class="skill-group" style="transition-delay:0.2s">
        <div class="skill-group-header">
          <div class="skill-icon amber">🤖</div>
          <div class="skill-group-title">Data Science & ML</div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Data Analysis</span><span class="skill-pct">78%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-amber" data-width="78"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Data Visualization</span><span class="skill-pct">75%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-amber" data-width="75"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Supervised Learning</span><span class="skill-pct">65%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-amber" data-width="65"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Unsupervised Learning</span><span class="skill-pct">55%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-amber" data-width="55"></div></div>
        </div>
      </div>

      <!-- Database -->
      <div class="skill-group" style="transition-delay:0.25s">
        <div class="skill-group-header">
          <div class="skill-icon green">🗄️</div>
          <div class="skill-group-title">Database</div>
        </div>
        <div class="tag-cloud">
          <span class="tag tag-green">SQL</span>
          <span class="tag tag-green">SELECT</span>
          <span class="tag tag-green">JOIN</span>
          <span class="tag tag-green">GROUP BY</span>
          <span class="tag tag-green">DB Design</span>
        </div>
        <div style="margin-top:1.2rem">
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">SQL Queries</span><span class="skill-pct">74%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-accent" data-width="74"></div></div>
        </div>
        </div>
      </div>

      <!-- Core CS -->
      <div class="skill-group" style="transition-delay:0.3s">
        <div class="skill-group-header">
          <div class="skill-icon blue">🌐</div>
          <div class="skill-group-title">Core CS</div>
        </div>
        <div class="tag-cloud">
          <span class="tag tag-blue">Operating Systems</span>
          <span class="tag tag-blue">Networks</span>
          <span class="tag tag-blue">Computer Org.</span>
          <span class="tag tag-blue">DBMS</span>
        </div>
        <div style="margin-top:1.2rem">
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">OS Fundamentals</span><span class="skill-pct">65%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-blue" data-width="65"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-row"><span class="skill-name">Networking Basics</span><span class="skill-pct">60%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill fill-blue" data-width="60"></div></div>
        </div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-inner">
    <p class="section-label">// 03 — Projects</p>
    <h2 class="section-title">What I've Built</h2>
    <div class="section-divider"></div>
    <div class="projects-grid">

      <div class="project-card project-featured">
        <div class="project-arrow">↗</div>
        <div class="project-badge">Featured</div>
        <div class="project-title">Student Marks Prediction System</div>
        <div class="project-desc">A machine learning model that predicts student academic performance based on input features such as study hours, attendance, and prior scores. Built with scikit-learn and deployed via Jupyter Notebook.</div>
        <div class="project-stack">
          <span class="stack-pill">Python</span>
          <span class="stack-pill">scikit-learn</span>
          <span class="stack-pill">Pandas</span>
          <span class="stack-pill">Matplotlib</span>
          <span class="stack-pill">Jupyter</span>
        </div>
      </div>

      <div class="project-card" style="transition-delay:0.1s">
        <div class="project-arrow">↗</div>
        <div class="project-badge">Data Analysis</div>
        <div class="project-title">Data Analysis Projects</div>
        <div class="project-desc">Collection of end-to-end data projects: cleaning messy real-world datasets, performing EDA, and producing visual insights using NumPy, Pandas, and Matplotlib.</div>
        <div class="project-stack">
          <span class="stack-pill">NumPy</span>
          <span class="stack-pill">Pandas</span>
          <span class="stack-pill">Matplotlib</span>
          <span class="stack-pill">Python</span>
        </div>
      </div>

      <div class="project-card" style="transition-delay:0.2s">
        <div class="project-arrow">↗</div>
        <div class="project-badge">DSA</div>
        <div class="project-title">Mini Coding Projects</div>
        <div class="project-desc">A portfolio of small algorithmic programs: sorting visualizers, stack/queue implementations, searching algorithms, and OOP-based mini-applications written in Python.</div>
        <div class="project-stack">
          <span class="stack-pill">Python</span>
          <span class="stack-pill">OOP</span>
          <span class="stack-pill">Algorithms</span>
          <span class="stack-pill">GitHub</span>
        </div>
      </div>

      <div class="project-card" style="transition-delay:0.3s">
        <div class="project-arrow">↗</div>
        <div class="project-badge">Machine Learning</div>
        <div class="project-title">Basic ML Projects</div>
        <div class="project-desc">Hands-on implementations of supervised and unsupervised learning algorithms — classification, regression, and clustering — to build intuition for real ML pipelines.</div>
        <div class="project-stack">
          <span class="stack-pill">scikit-learn</span>
          <span class="stack-pill">Python</span>
          <span class="stack-pill">Pandas</span>
          <span class="stack-pill">Jupyter</span>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- TOOLS -->
<section id="tools">
  <div class="section-inner">
    <p class="section-label">// 04 — Toolbox</p>
    <h2 class="section-title">Tools & Tech</h2>
    <div class="section-divider"></div>
    <div class="tools-grid">
      <div class="tool-item"><span class="tool-icon">🐍</span><div class="tool-name">Python</div></div>
      <div class="tool-item" style="transition-delay:0.05s"><span class="tool-icon">📊</span><div class="tool-name">NumPy</div></div>
      <div class="tool-item" style="transition-delay:0.1s"><span class="tool-icon">🐼</span><div class="tool-name">Pandas</div></div>
      <div class="tool-item" style="transition-delay:0.15s"><span class="tool-icon">📈</span><div class="tool-name">Matplotlib</div></div>
      <div class="tool-item" style="transition-delay:0.2s"><span class="tool-icon">📓</span><div class="tool-name">Jupyter</div></div>
      <div class="tool-item" style="transition-delay:0.25s"><span class="tool-icon">🌿</span><div class="tool-name">Git</div></div>
      <div class="tool-item" style="transition-delay:0.3s"><span class="tool-icon">🐙</span><div class="tool-name">GitHub</div></div>
      <div class="tool-item" style="transition-delay:0.35s"><span class="tool-icon">🔵</span><div class="tool-name">C Language</div></div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div class="footer-left">
      <span class="footer-logo">Dida Dhungana</span>
      <span class="footer-tagline">CS Student · Python Developer · ML Learner</span>
    </div>
    <div class="footer-links">
      <a href="https://github.com/dida91" target="_blank">GitHub</a>
      <a href="#about">About</a>
      <a href="#projects">Projects</a>
      <a href="#skills">Skills</a>
    </div>
  </div>
  <div class="footer-copy">
    Built with passion from <span>Kathmandu, Nepal 🇳🇵</span> — Always open to learning & collaborating.
  </div>
</footer>

<script>
/* ── Cursor ── */
const cursor = document.getElementById('cursor');
const ring   = document.getElementById('cursor-ring');
let mx = 0, my = 0, rx = 0, ry = 0;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
(function tick() {
  rx += (mx - rx) * 0.14;
  ry += (my - ry) * 0.14;
  cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
  ring.style.left   = rx + 'px'; ring.style.top  = ry + 'px';
  requestAnimationFrame(tick);
})();
document.querySelectorAll('a,button,.project-card,.tool-item,.stat-card').forEach(el => {
  el.addEventListener('mouseenter', () => { cursor.style.transform='translate(-50%,-50%) scale(2.5)'; ring.style.borderColor=getComputedStyle(document.documentElement).getPropertyValue('--accent'); });
  el.addEventListener('mouseleave', () => { cursor.style.transform='translate(-50%,-50%) scale(1)'; ring.style.borderColor='rgba(0,229,160,0.5)'; });
});

/* ── Particles Canvas ── */
const canvas = document.getElementById('particles-canvas');
const ctx    = canvas.getContext('2d');
let W, H, particles = [];
function resize() { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; }
resize(); window.addEventListener('resize', resize);
class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W; this.y = Math.random() * H;
    this.vx = (Math.random()-0.5)*0.4; this.vy = (Math.random()-0.5)*0.4;
    this.r  = Math.random()*1.5+0.3;
    this.alpha = Math.random()*0.5+0.1;
  }
  update() {
    this.x += this.vx; this.y += this.vy;
    if (this.x<0||this.x>W||this.y<0||this.y>H) this.reset();
  }
  draw() {
    ctx.beginPath(); ctx.arc(this.x,this.y,this.r,0,Math.PI*2);
    ctx.fillStyle = `rgba(0,229,160,${this.alpha})`;
    ctx.fill();
  }
}
for (let i=0; i<100; i++) particles.push(new Particle());
function drawConnections() {
  for (let i=0; i<particles.length; i++)
  for (let j=i+1; j<particles.length; j++) {
    const dx=particles[i].x-particles[j].x, dy=particles[i].y-particles[j].y;
    const d=Math.sqrt(dx*dx+dy*dy);
    if (d<100) {
      ctx.beginPath();
      ctx.moveTo(particles[i].x,particles[i].y);
      ctx.lineTo(particles[j].x,particles[j].y);
      ctx.strokeStyle=`rgba(0,229,160,${0.08*(1-d/100)})`;
      ctx.lineWidth=0.5; ctx.stroke();
    }
  }
}
function animParticles() {
  ctx.clearRect(0,0,W,H);
  particles.forEach(p=>{p.update();p.draw();});
  drawConnections();
  requestAnimationFrame(animParticles);
}
animParticles();

/* ── Typing effect ── */
const phrases = [
  'Python Programmer',
  'DSA Practitioner',
  'Data Analyst',
  'ML Explorer',
  'Problem Solver'
];
let pi=0, ci=0, deleting=false;
const typed = document.getElementById('typed-text');
function typeLoop() {
  const phrase = phrases[pi];
  if (!deleting) {
    typed.textContent = phrase.slice(0, ++ci);
    if (ci === phrase.length) { deleting=true; setTimeout(typeLoop, 1600); return; }
  } else {
    typed.textContent = phrase.slice(0, --ci);
    if (ci === 0) { deleting=false; pi=(pi+1)%phrases.length; }
  }
  setTimeout(typeLoop, deleting ? 45 : 90);
}
setTimeout(typeLoop, 1800);

/* ── Scroll reveal ── */
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('revealed');
      /* animate bars */
      e.target.querySelectorAll('.skill-bar-fill').forEach(bar => {
        setTimeout(()=>{ bar.style.width = bar.dataset.width + '%'; }, 100);
      });
    }
  });
}, { threshold: 0.15 });

document.querySelectorAll(
  '.section-label, .section-title, .section-divider, .stat-card, .skill-group, .project-card, .tool-item'
).forEach(el => observer.observe(el));

/* Nav shadow on scroll */
window.addEventListener('scroll', () => {
  document.getElementById('navbar').style.boxShadow =
    window.scrollY > 40 ? '0 4px 40px rgba(0,0,0,0.6)' : 'none';
});
</script>
</body>
</html>

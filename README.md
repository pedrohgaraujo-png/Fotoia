<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Edição Profissional de Fotos – Transforme suas imagens</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
:root {
  --bg:       #060810;
  --bg2:      #0a0e1a;
  --blue:     #4a9eff;
  --blue2:    #7ec8ff;
  --blue-dim: rgba(74,158,255,0.12);
  --white:    #eef4ff;
  --muted:    #4a6a8a;
  --border:   rgba(74,158,255,0.18);
}

*, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }

html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--white);
  font-family: 'DM Sans', sans-serif;
  font-weight: 300;
  overflow-x: hidden;
}

/* ══════════════════════════════
   CURSOR PERSONALIZADO
══════════════════════════════ */
body { cursor: none; }
@media (max-width: 768px) {
  body { cursor: auto; }
  #cursor, #cursor-ring { display: none; }
}
#cursor {
  width: 12px; height: 12px;
  background: var(--blue);
  border-radius: 50%;
  position: fixed;
  pointer-events: none;
  z-index: 9999;
  transition: transform 0.15s ease, background 0.2s;
  mix-blend-mode: screen;
}
#cursor-ring {
  width: 36px; height: 36px;
  border: 1px solid rgba(74,158,255,0.5);
  border-radius: 50%;
  position: fixed;
  pointer-events: none;
  z-index: 9998;
  transition: transform 0.35s ease, width 0.3s, height 0.3s;
}

/* ══════════════════════════════
   NAV
══════════════════════════════ */
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  padding: 20px 5%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(6,8,16,0.7);
  backdrop-filter: blur(16px);
  border-bottom: 1px solid rgba(74,158,255,0.08);
}

.nav-logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 1.4rem;
  letter-spacing: -0.02em;
  text-decoration: none;
  color: var(--white);
}
.nav-logo span { color: var(--blue); }

.nav-links {
  display: flex;
  gap: 32px;
  list-style: none;
}

.hamburger {
  display: none;
  flex-direction: column;
  gap: 6px;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 101;
}
.hamburger span {
  width: 24px;
  height: 2px;
  background: var(--white);
  border-radius: 1px;
  transition: transform 0.3s, opacity 0.3s;
}
.hamburger.active span:nth-child(1) {
  transform: rotate(45deg) translateY(12px);
}
.hamburger.active span:nth-child(2) {
  opacity: 0;
}
.hamburger.active span:nth-child(3) {
  transform: rotate(-45deg) translateY(-12px);
}
.nav-links a {
  text-decoration: none;
  font-size: 0.88rem;
  color: var(--muted);
  letter-spacing: 0.05em;
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--white); }

.nav-cta {
  background: var(--blue);
  color: var(--bg) !important;
  padding: 10px 24px;
  border-radius: 100px;
  font-weight: 500 !important;
  font-size: 0.85rem !important;
  letter-spacing: 0.05em;
  transition: background 0.2s, transform 0.2s !important;
  min-width: 44px;
  min-height: 44px;
}
.nav-cta:hover { background: var(--blue2) !important; transform: translateY(-1px); }

/* ══════════════════════════════
   HERO
══════════════════════════════ */
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 120px 5% 80px;
  position: relative;
  overflow: hidden;
}

/* Grade de fundo */
.hero::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(74,158,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(74,158,255,0.04) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 30%, transparent 100%);
}

/* Glow central */
.hero-glow {
  position: absolute;
  width: 700px; height: 700px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(74,158,255,0.14) 0%, transparent 70%);
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
  animation: pulse 4s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: translate(-50%,-50%) scale(1); opacity:1; }
  50%       { transform: translate(-50%,-50%) scale(1.1); opacity:0.7; }
}

/* Partículas */
.particles {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
}
.particle {
  position: absolute;
  width: 2px; height: 2px;
  background: var(--blue);
  border-radius: 50%;
  animation: float linear infinite;
  opacity: 0;
}
@keyframes float {
  0%   { transform: translateY(100vh) translateX(0); opacity:0; }
  10%  { opacity: 0.6; }
  90%  { opacity: 0.3; }
  100% { transform: translateY(-10vh) translateX(40px); opacity:0; }
}

.hero-eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  border: 1px solid var(--border);
  background: var(--blue-dim);
  color: var(--blue);
  font-size: 0.75rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  padding: 7px 18px;
  border-radius: 100px;
  margin-bottom: 36px;
  animation: fadeUp 0.7s ease both;
}
.hero-eyebrow::before {
  content: '';
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--blue);
  animation: blink 1.5s ease-in-out infinite;
}
@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

.hero h1 {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: clamp(3rem, 9vw, 7.5rem);
  line-height: 0.95;
  letter-spacing: -0.03em;
  max-width: 900px;
  animation: fadeUp 0.7s 0.1s ease both;
  position: relative;
}

.hero h1 .accent {
  color: transparent;
  -webkit-text-stroke: 1.5px var(--blue);
  display: block;
}

.hero h1 .solid { color: var(--white); display: block; }

.hero-sub {
  margin-top: 32px;
  font-size: clamp(1rem, 2vw, 1.2rem);
  color: var(--muted);
  max-width: 480px;
  line-height: 1.7;
  animation: fadeUp 0.7s 0.2s ease both;
}

.hero-buttons {
  margin-top: 52px;
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
  justify-content: center;
  animation: fadeUp 0.7s 0.3s ease both;
}

.btn-blue {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: var(--blue);
  color: var(--bg);
  padding: 16px 36px;
  border-radius: 100px;
  font-size: 0.95rem;
  font-weight: 500;
  text-decoration: none;
  letter-spacing: 0.02em;
  transition: background 0.2s, transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 0 30px rgba(74,158,255,0.3);
  min-height: 44px;
  min-width: 44px;
}
.btn-blue:hover {
  background: var(--blue2);
  transform: translateY(-3px);
  box-shadow: 0 0 50px rgba(74,158,255,0.5);
}

.btn-outline {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  border: 1px solid var(--border);
  color: var(--white);
  padding: 16px 36px;
  border-radius: 100px;
  font-size: 0.95rem;
  text-decoration: none;
  letter-spacing: 0.02em;
  transition: border-color 0.2s, transform 0.2s, background 0.2s;
  min-height: 44px;
  min-width: 44px;
}
.btn-outline:hover {
  border-color: var(--blue);
  background: var(--blue-dim);
  transform: translateY(-3px);
}

/* Scroll indicator */
.scroll-hint {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  color: var(--muted);
  font-size: 0.72rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  animation: fadeUp 1s 0.8s ease both;
}
.scroll-line {
  width: 1px; height: 50px;
  background: linear-gradient(to bottom, var(--blue), transparent);
  animation: scrollDrop 1.8s ease-in-out infinite;
}
@keyframes scrollDrop {
  0%   { transform: scaleY(0); transform-origin: top; opacity:1; }
  50%  { transform: scaleY(1); transform-origin: top; opacity:1; }
  100% { transform: scaleY(1); transform-origin: bottom; opacity:0; }
}

/* ══════════════════════════════
   STATS STRIP
══════════════════════════════ */
.stats {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background: var(--bg2);
  padding: 40px 5%;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 0;
}

.stat {
  flex: 1;
  min-width: 160px;
  text-align: center;
  padding: 16px 32px;
  border-right: 1px solid var(--border);
}
.stat:last-child { border-right: none; }

.stat-num {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 2.4rem;
  color: var(--blue);
  line-height: 1;
}

.stat-label {
  font-size: 0.8rem;
  color: var(--muted);
  margin-top: 6px;
  letter-spacing: 0.05em;
}

/* ══════════════════════════════
   O QUE FAZEMOS
══════════════════════════════ */
.section {
  padding: 110px 5%;
  max-width: 1200px;
  margin: 0 auto;
}

.section-tag {
  display: inline-block;
  font-size: 0.72rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--blue);
  margin-bottom: 16px;
}

.section-h2 {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: clamp(2rem, 5vw, 3.8rem);
  letter-spacing: -0.03em;
  line-height: 1.05;
  max-width: 640px;
}

.section-h2 em {
  font-style: normal;
  color: var(--blue);
}

/* CARDS DE SERVIÇO */
.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 20px;
  margin-top: 64px;
}

.svc {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 36px 32px;
  position: relative;
  overflow: hidden;
  transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
}
.svc:hover {
  transform: translateY(-8px);
  border-color: rgba(74,158,255,0.5);
  box-shadow: 0 20px 60px rgba(74,158,255,0.1);
}

.svc::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 2px;
  background: linear-gradient(90deg, transparent, var(--blue), transparent);
  opacity: 0;
  transition: opacity 0.3s;
}
.svc:hover::before { opacity: 1; }

.svc-icon {
  width: 52px; height: 52px;
  border-radius: 14px;
  background: var(--blue-dim);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  margin-bottom: 24px;
}

.svc h3 {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1.15rem;
  margin-bottom: 10px;
  letter-spacing: -0.01em;
}

.svc p {
  font-size: 0.88rem;
  color: var(--muted);
  line-height: 1.75;
}

.svc-price {
  margin-top: 24px;
  display: inline-block;
  background: var(--blue-dim);
  color: var(--blue);
  border: 1px solid var(--border);
  font-size: 0.82rem;
  font-weight: 500;
  padding: 5px 14px;
  border-radius: 100px;
  letter-spacing: 0.05em;
}

/* ══════════════════════════════
   PROCESSO
══════════════════════════════ */
.process-section {
  background: var(--bg2);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  padding: 110px 5%;
}

.process-inner {
  max-width: 1200px;
  margin: 0 auto;
}

.process-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 2px;
  margin-top: 64px;
  position: relative;
}

.process-steps::before {
  content: '';
  position: absolute;
  top: 40px;
  left: 10%;
  right: 10%;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--blue), transparent);
  opacity: 0.3;
}

.step-block {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 36px 28px;
  text-align: center;
  position: relative;
  transition: border-color 0.3s, background 0.3s;
}
.step-block:hover {
  border-color: rgba(74,158,255,0.45);
  background: rgba(74,158,255,0.04);
}

.step-num-big {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 3.5rem;
  color: rgba(74,158,255,0.12);
  line-height: 1;
  margin-bottom: 16px;
}

.step-icon-circle {
  width: 56px; height: 56px;
  border-radius: 50%;
  border: 1px solid var(--blue);
  background: var(--blue-dim);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.4rem;
  margin: 0 auto 20px;
}

.step-block h3 {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1rem;
  margin-bottom: 10px;
  letter-spacing: -0.01em;
}

.step-block p {
  font-size: 0.84rem;
  color: var(--muted);
  line-height: 1.7;
}

/* ══════════════════════════════
   CTA FINAL
══════════════════════════════ */
.cta-section {
  padding: 110px 5%;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.cta-section::before {
  content: '';
  position: absolute;
  width: 800px; height: 800px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(74,158,255,0.1) 0%, transparent 65%);
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
}

.cta-box {
  max-width: 760px;
  margin: 0 auto;
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 28px;
  padding: 72px 48px;
  position: relative;
  overflow: hidden;
}

.cta-box::before {
  content: '';
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse 60% 40% at 50% 0%, rgba(74,158,255,0.12) 0%, transparent 70%);
  pointer-events: none;
}

.cta-box h2 {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: clamp(2rem, 5vw, 3.2rem);
  letter-spacing: -0.03em;
  line-height: 1.05;
  margin-bottom: 20px;
}

.cta-box p {
  color: var(--muted);
  font-size: 1rem;
  line-height: 1.7;
  max-width: 440px;
  margin: 0 auto 48px;
}

.cta-buttons {
  display: flex;
  gap: 14px;
  justify-content: center;
  flex-wrap: wrap;
}

/* Botão Instagram */
.btn-insta {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: linear-gradient(135deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
  color: #fff;
  padding: 16px 36px;
  border-radius: 100px;
  font-size: 0.95rem;
  font-weight: 500;
  text-decoration: none;
  transition: transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 0 30px rgba(220,39,67,0.25);
  min-height: 44px;
  min-width: 44px;
}
.btn-insta:hover {
  transform: translateY(-3px);
  box-shadow: 0 0 50px rgba(220,39,67,0.4);
}

/* Botão WhatsApp */
.btn-wpp {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: #25d366;
  color: #fff;
  padding: 16px 36px;
  border-radius: 100px;
  font-size: 0.95rem;
  font-weight: 500;
  text-decoration: none;
  transition: transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 0 30px rgba(37,211,102,0.25);
  min-height: 44px;
  min-width: 44px;
}
.btn-wpp:hover {
  transform: translateY(-3px);
  box-shadow: 0 0 50px rgba(37,211,102,0.4);
}

/* ══════════════════════════════
   FOOTER
══════════════════════════════ */
footer {
  border-top: 1px solid var(--border);
  padding: 36px 5%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
}

.footer-logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 1.1rem;
  text-decoration: none;
  color: var(--white);
}
.footer-logo span { color: var(--blue); }

.footer-copy {
  font-size: 0.8rem;
  color: var(--muted);
}

/* ══════════════════════════════
   ANIMAÇÕES GERAIS
══════════════════════════════ */
@keyframes fadeUp {
  from { opacity:0; transform: translateY(28px); }
  to   { opacity:1; transform: translateY(0); }
}

.reveal {
  opacity: 0;
  transform: translateY(32px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

/* ══════════════════════════════
   RESPONSIVO
══════════════════════════════ */
@media (max-width: 768px) {
  .hamburger { display: flex; }
  
  nav {
    padding: 16px 5%;
  }
  
  .nav-logo {
    font-size: 1.1rem;
  }
  
  .nav-links {
    position: absolute;
    top: 60px;
    left: 0;
    right: 0;
    flex-direction: column;
    gap: 0;
    background: rgba(6,8,16,0.95);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid rgba(74,158,255,0.08);
    padding: 20px 5%;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s;
  }
  
  .nav-links.active {
    max-height: 300px;
  }
  
  .nav-links li {
    padding: 12px 0;
    border-top: 1px solid rgba(74,158,255,0.08);
  }
  
  .nav-links a {
    font-size: 0.95rem;
    min-height: 44px;
    display: flex;
    align-items: center;
  }
  
  .hero {
    padding: 100px 5% 60px;
    min-height: auto;
  }
  
  .hero h1 {
    font-size: clamp(2rem, 8vw, 3.5rem);
  }
  
  .hero-sub {
    font-size: 1rem;
    margin-top: 20px;
  }
  
  .hero-buttons {
    flex-direction: column;
    margin-top: 32px;
  }
  
  .hero-buttons a {
    width: 100%;
    justify-content: center;
    padding: 14px 24px;
  }
  
  .stat {
    min-width: 100px;
    padding: 20px 16px;
    font-size: 0.9rem;
  }
  
  .stat-num {
    font-size: 1.8rem;
  }
  
  .section {
    padding: 60px 5%;
  }
  
  .section-h2 {
    font-size: clamp(1.5rem, 5vw, 2.5rem);
  }
  
  .services-grid {
    grid-template-columns: 1fr;
    gap: 16px;
    margin-top: 40px;
  }
  
  .svc {
    padding: 28px 24px;
  }
  
  .svc p {
    font-size: 0.9rem;
  }
  
  .process-section {
    padding: 60px 5%;
  }
  
  .process-steps {
    grid-template-columns: 1fr;
    gap: 16px;
    margin-top: 40px;
  }
  
  .process-steps::before {
    display: none;
  }
  
  .step-block {
    padding: 24px 20px;
  }
  
  .step-num-big {
    font-size: 2.5rem;
  }
  
  .cta-section {
    padding: 60px 5%;
  }
  
  .cta-box {
    padding: 40px 24px;
    border-radius: 20px;
  }
  
  .cta-box h2 {
    font-size: clamp(1.5rem, 5vw, 2.2rem);
    line-height: 1.2;
  }
  
  .cta-box p {
    font-size: 0.95rem;
    margin: 16px auto 32px;
  }
  
  .cta-buttons {
    flex-direction: column;
    gap: 12px;
  }
  
  .cta-buttons a {
    width: 100%;
    justify-content: center;
    padding: 14px 24px;
    font-size: 0.9rem;
  }
  
  footer {
    flex-direction: column;
    padding: 24px 5%;
    gap: 12px;
    text-align: center;
  }
  
  .footer-logo {
    font-size: 1rem;
  }
}
</style>
</head>
<body>

<!-- Cursor -->
<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">Foto<span>Pro</span></a>
  <ul class="nav-links">
    <li><a href="#servicos">Serviços</a></li>
    <li><a href="#como-funciona">Como funciona</a></li>
    <li><a href="#contato" class="nav-cta">Pedir agora</a></li>
  </ul>
  <button class="hamburger">
    <span></span>
    <span></span>
    <span></span>
  </button>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-glow"></div>
  <div class="particles" id="particles"></div>

  <div class="hero-eyebrow">Edição e transformação profissional de fotos</div>

  <h1>
    <span class="solid">Sua foto.</span>
    <span class="accent">Reinventada.</span>
  </h1>

  <p class="hero-sub">
    Transformo qualquer foto em algo extraordinário — novos cenários, novos visuais, retoques ultra-realistas. Com foco em criar o que você imagina.
  </p>

  <div class="hero-buttons">
    <a href="#contato" class="btn-blue">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm-1 14l-4-4 1.41-1.41L11 13.17l6.59-6.58L19 8l-8 8z"/></svg>
      Quero transformar minha foto
    </a>
    <a href="#servicos" class="btn-outline">Ver o que fazemos</a>
  </div>

  <div class="scroll-hint">
    <div class="scroll-line"></div>
    Scroll
  </div>
</section>

<!-- STATS -->
<div class="stats">
  <div class="stat">
    <div class="stat-num">100%</div>
    <div class="stat-label">Fotos realistas</div>
  </div>
  <div class="stat">
    <div class="stat-num">1h</div>
    <div class="stat-label">Tempo de entrega</div>
  </div>
  <div class="stat">
    <div class="stat-num">∞</div>
    <div class="stat-label">Possibilidades</div>
  </div>
  <div class="stat">
    <div class="stat-num">800+</div>
    <div class="stat-label">Fotos editadas</div>
  </div>
</div>

<!-- SERVIÇOS -->
<section class="section" id="servicos">
  <p class="section-tag">O que fazemos</p>
  <h2 class="section-h2">Como eu transformo suas fotos</h2>

  <div class="services-grid">
    <div class="svc reveal">
      <div class="svc-icon">🌍</div>
      <h3>Troca de Cenário</h3>
      <p>Paris, Dubai, Nova York, Maldivas — coloque-se em qualquer lugar do mundo sem sair de casa. O fundo muda, você continua sendo você.</p>
      <span class="svc-price">R$ 12</span>
    </div>

    <div class="svc reveal">
      <div class="svc-icon">💄</div>
      <h3>Novo Visual</h3>
      <p>Cabelo diferente, roupa nova, maquiagem marcante. Experimente qualquer estilo antes de se comprometer com ele na vida real.</p>
      <span class="svc-price">R$ 13</span>
    </div>

    <div class="svc reveal">
      <div class="svc-icon">✨</div>
      <h3>Retoque Profissional</h3>
      <p>Iluminação de estúdio, pele perfeita, qualidade de editorial. Resultado que parece caro — e não é.</p>
      <span class="svc-price">R$ 10</span>
    </div>

    <div class="svc reveal">
      <div class="svc-icon">🎭</div>
      <h3>Estilo Temático</h3>
      <p>Personagem de série, aesthetic Y2K, cyberpunk, moda editorial, capa de revista. Qualquer universo visual que você quiser habitar.</p>
      <span class="svc-price">R$ 15</span>
    </div>
  </div>
</section>

<!-- COMO FUNCIONA -->
<section class="process-section" id="como-funciona">
  <div class="process-inner">
    <p class="section-tag">Passo a passo</p>
    <h2 class="section-h2">Simples assim</h2>

    <div class="process-steps">
      <div class="step-block reveal">
        <div class="step-num-big">01</div>
        <div class="step-icon-circle">📸</div>
        <h3>Você manda a foto</h3>
        <p>Envia pelo Instagram ou WhatsApp. Pode ser selfie, foto de corpo inteiro — qualquer ângulo funciona.</p>
      </div>

      <div class="step-block reveal">
        <div class="step-num-big">02</div>
        <div class="step-icon-circle">💬</div>
        <h3>Descreve o que quer</h3>
        <p>Me conta sua ideia: novo fundo, look diferente, retoque... sem limites para imaginar.</p>
      </div>

      <div class="step-block reveal">
        <div class="step-num-big">03</div>
        <div class="step-icon-circle">✨</div>
        <h3>Eu faço a mágica</h3>
        <p>Com as ferramentas mais avançadas disponíveis, edito sua foto mantendo seu rosto e características originais perfeitos.</p>
      </div>

      <div class="step-block reveal">
        <div class="step-num-big">04</div>
        <div class="step-icon-circle">🎁</div>
        <h3>Recebe o resultado</h3>
        <p>Entrega em até 1h. Se não gostar, revisão gratuita. Simples e sem complicação.</p>
      </div>
    </div>
  </div>
</section>

<!-- CTA FINAL -->
<section class="cta-section" id="contato">
  <div class="cta-box reveal">
    <h2>Pronto para se<br>reinventar?</h2>
    <p>Manda sua foto agora. A transformação começa em minutos.</p>
    <div class="cta-buttons">
      <a href="https://ig.me/m/fotoia_" target="_blank" class="btn-insta">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
        </svg>
        Instagram
      </a>
      <a href="https://wa.me/5579991214281" target="_blank" class="btn-wpp">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
        </svg>
        WhatsApp
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <a href="#" class="footer-logo">Foto<span>Pro</span></a>
  <p class="footer-copy">© 2025 FotoPro · Transformação profissional de fotos</p>
</footer>

<script>
// ── Menu Hamburger ──
const hamburger = document.querySelector('.hamburger');
const navLinks = document.querySelector('.nav-links');

hamburger.addEventListener('click', () => {
  hamburger.classList.toggle('active');
  navLinks.classList.toggle('active');
});

// Fechar menu ao clicar em um link
navLinks.querySelectorAll('a').forEach(link => {
  link.addEventListener('click', () => {
    hamburger.classList.remove('active');
    navLinks.classList.remove('active');
  });
});

// Fechar menu ao redimensionar para desktop
window.addEventListener('resize', () => {
  if (window.innerWidth > 768) {
    hamburger.classList.remove('active');
    navLinks.classList.remove('active');
  }
});

// ── Cursor personalizado ──
const cur = document.getElementById('cursor');
const ring = document.getElementById('cursor-ring');
let mx = 0, my = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cur.style.left  = mx - 6 + 'px';
  cur.style.top   = my - 6 + 'px';
});

(function animRing() {
  rx += (mx - rx - 18) * 0.12;
  ry += (my - ry - 18) * 0.12;
  ring.style.left = rx + 'px';
  ring.style.top  = ry + 'px';
  requestAnimationFrame(animRing);
})();

document.querySelectorAll('a, button').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cur.style.transform = 'scale(2.5)';
    ring.style.width = '56px';
    ring.style.height = '56px';
  });
  el.addEventListener('mouseleave', () => {
    cur.style.transform = 'scale(1)';
    ring.style.width = '36px';
    ring.style.height = '36px';
  });
});

// ── Partículas ──
const pc = document.getElementById('particles');
for (let i = 0; i < 28; i++) {
  const p = document.createElement('div');
  p.className = 'particle';
  p.style.cssText = `
    left: ${Math.random()*100}%;
    width: ${Math.random()*3+1}px;
    height: ${Math.random()*3+1}px;
    animation-duration: ${Math.random()*12+8}s;
    animation-delay: ${Math.random()*10}s;
    opacity: ${Math.random()*0.5+0.1};
  `;
  pc.appendChild(p);
}

// ── Scroll reveal ──
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      // stagger filhos
      e.target.parentElement.querySelectorAll('.reveal').forEach((el, i) => {
        el.style.transitionDelay = i * 0.1 + 's';
      });
    }
  });
}, { threshold: 0.12 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>
</body>
</html>

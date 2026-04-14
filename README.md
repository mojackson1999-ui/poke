<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PokéDex World — Catch the Legend</title>
<link href="https://fonts.googleapis.com/css2?family=Bangers&family=Space+Grotesk:wght@300;400;500;600;700&family=Permanent+Marker&display=swap" rel="stylesheet">
<style>
  :root {
    --red: #FF1C1C;
    --red-dark: #C0000F;
    --yellow: #FFD700;
    --yellow-light: #FFF176;
    --blue: #1A237E;
    --blue-mid: #3949AB;
    --white: #FAFAFA;
    --black: #0D0D0D;
    --gray: #E8E8E8;
    --gray-mid: #9E9E9E;
    --green: #4CAF50;
    --fire: #FF6D00;
    --water: #0288D1;
    --psychic: #AD1457;
    --electric: #F9A825;
    --grass: #2E7D32;
    --shadow: rgba(0,0,0,0.15);
    --ink: rgba(0,0,0,0.08);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Space Grotesk', sans-serif;
    background: var(--white);
    color: var(--black);
    overflow-x: hidden;
  }

  /* ─── NAV ─── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1rem 2.5rem;
    background: var(--black);
    border-bottom: 3px solid var(--yellow);
  }
  .nav-logo {
    font-family: 'Bangers', cursive;
    font-size: 2rem;
    color: var(--yellow);
    letter-spacing: 2px;
    text-shadow: 2px 2px 0 var(--red);
  }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a {
    color: var(--white);
    text-decoration: none;
    font-size: 0.85rem;
    font-weight: 600;
    letter-spacing: 1px;
    text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--yellow); }

  /* ─── HERO ─── */
  #hero {
    min-height: 100vh;
    background: var(--black);
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    padding: 8rem 2.5rem 4rem;
    position: relative;
    overflow: hidden;
  }
  .hero-bg-circle {
    position: absolute;
    width: 600px; height: 600px;
    border-radius: 50%;
    border: 3px solid rgba(255,255,255,0.04);
    top: 50%; right: -100px;
    transform: translateY(-50%);
    pointer-events: none;
  }
  .hero-bg-circle::before {
    content: '';
    position: absolute;
    width: 80%; height: 80%;
    border-radius: 50%;
    border: 3px solid rgba(255,215,0,0.06);
    top: 10%; left: 10%;
  }
  .hero-stripe {
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 6px;
    background: linear-gradient(90deg, var(--red) 0%, var(--red) 49%, var(--white) 49%, var(--white) 51%, #222 51%);
  }
  .hero-content { z-index: 1; }
  .hero-eyebrow {
    font-size: 0.75rem;
    font-weight: 700;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--yellow);
    margin-bottom: 1rem;
    opacity: 0;
    animation: fadeUp 0.6s 0.2s forwards;
  }
  .hero-title {
    font-family: 'Bangers', cursive;
    font-size: clamp(5rem, 10vw, 9rem);
    line-height: 0.9;
    color: var(--white);
    letter-spacing: 3px;
    opacity: 0;
    animation: fadeUp 0.6s 0.35s forwards;
  }
  .hero-title span { color: var(--yellow); text-shadow: 4px 4px 0 var(--red); }
  .hero-subtitle {
    margin-top: 1.5rem;
    font-size: 1.1rem;
    line-height: 1.7;
    color: var(--gray-mid);
    max-width: 460px;
    opacity: 0;
    animation: fadeUp 0.6s 0.5s forwards;
  }
  .hero-cta {
    margin-top: 2.5rem;
    display: flex; gap: 1rem; flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.6s 0.65s forwards;
  }
  .btn-primary {
    background: var(--red);
    color: var(--white);
    padding: 0.9rem 2rem;
    font-family: 'Bangers', cursive;
    font-size: 1.2rem;
    letter-spacing: 2px;
    border: 3px solid var(--red-dark);
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
    transition: transform 0.15s, box-shadow 0.15s;
    box-shadow: 4px 4px 0 var(--red-dark);
  }
  .btn-primary:hover { transform: translate(-2px, -2px); box-shadow: 6px 6px 0 var(--red-dark); }
  .btn-secondary {
    background: transparent;
    color: var(--yellow);
    padding: 0.9rem 2rem;
    font-family: 'Bangers', cursive;
    font-size: 1.2rem;
    letter-spacing: 2px;
    border: 3px solid var(--yellow);
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
    transition: background 0.15s, color 0.15s;
  }
  .btn-secondary:hover { background: var(--yellow); color: var(--black); }

  /* Pokéball SVG hero graphic */
  .hero-graphic {
    display: flex; justify-content: center; align-items: center;
    z-index: 1;
    opacity: 0;
    animation: fadeIn 0.8s 0.8s forwards;
  }
  .pokeball-hero {
    width: min(420px, 90%);
    animation: float 4s ease-in-out infinite;
  }

  /* ─── GENERATION TICKER ─── */
  .ticker {
    background: var(--red);
    border-top: 3px solid var(--red-dark);
    border-bottom: 3px solid var(--red-dark);
    padding: 0.75rem 0;
    overflow: hidden;
    white-space: nowrap;
  }
  .ticker-inner {
    display: inline-flex; gap: 3rem;
    animation: ticker 20s linear infinite;
  }
  .ticker-item {
    font-family: 'Bangers', cursive;
    font-size: 1.1rem;
    letter-spacing: 2px;
    color: var(--yellow-light);
  }
  .ticker-dot { color: var(--white); opacity: 0.5; }

  /* ─── TYPES SECTION ─── */
  #types {
    padding: 7rem 2.5rem;
    background: var(--white);
  }
  .section-header {
    margin-bottom: 3.5rem;
  }
  .section-label {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--gray-mid);
    margin-bottom: 0.5rem;
  }
  .section-title {
    font-family: 'Bangers', cursive;
    font-size: clamp(3rem, 6vw, 5rem);
    letter-spacing: 2px;
    line-height: 1;
    color: var(--black);
  }
  .section-title em { color: var(--red); font-style: normal; }
  .types-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 1rem;
  }
  .type-card {
    padding: 1.5rem 1.25rem;
    border: 3px solid var(--black);
    cursor: default;
    position: relative;
    overflow: hidden;
    transition: transform 0.15s;
    box-shadow: 4px 4px 0 var(--black);
  }
  .type-card:hover { transform: translate(-3px, -3px); box-shadow: 7px 7px 0 var(--black); }
  .type-icon { font-size: 2rem; margin-bottom: 0.75rem; }
  .type-name {
    font-family: 'Bangers', cursive;
    font-size: 1.6rem;
    letter-spacing: 1px;
    color: var(--white);
  }
  .type-desc { font-size: 0.75rem; color: rgba(255,255,255,0.7); margin-top: 0.25rem; line-height: 1.4; }
  .type-card.fire { background: var(--fire); }
  .type-card.water { background: var(--water); }
  .type-card.grass { background: var(--grass); }
  .type-card.electric { background: var(--electric); }
  .type-card.psychic { background: var(--psychic); }
  .type-card.ice { background: #00ACC1; }
  .type-card.dragon { background: #4527A0; }
  .type-card.dark { background: #263238; }
  .type-card.normal { background: #757575; }
  .type-card.fighting { background: #B71C1C; }
  .type-card.ghost { background: #4A148C; }
  .type-card.rock { background: #795548; }

  /* ─── SPOTLIGHT ─── */
  #spotlight {
    padding: 7rem 2.5rem;
    background: var(--black);
    position: relative;
    overflow: hidden;
  }
  #spotlight .section-title { color: var(--white); }
  #spotlight .section-label { color: rgba(255,255,255,0.4); }
  .spotlight-grid {
    display: grid;
    grid-template-columns: 1fr 1.3fr;
    gap: 4rem;
    align-items: start;
    margin-top: 3.5rem;
  }
  .spotlight-featured {
    background: #111;
    border: 3px solid var(--yellow);
    padding: 2.5rem;
    position: relative;
    box-shadow: 8px 8px 0 var(--yellow);
  }
  .featured-number {
    font-family: 'Bangers', cursive;
    font-size: 5rem;
    color: rgba(255,255,255,0.06);
    position: absolute;
    top: 1rem; right: 1.5rem;
    line-height: 1;
  }
  .featured-label {
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--yellow);
    margin-bottom: 1rem;
  }
  .featured-name {
    font-family: 'Bangers', cursive;
    font-size: 4rem;
    color: var(--white);
    letter-spacing: 2px;
    line-height: 1;
  }
  .featured-types { display: flex; gap: 0.5rem; margin: 1rem 0; }
  .type-badge {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 1px;
    text-transform: uppercase;
    padding: 0.3rem 0.75rem;
    border-radius: 2px;
  }
  .tb-fire { background: var(--fire); color: var(--white); }
  .tb-flying { background: #7986CB; color: var(--white); }
  .tb-water { background: var(--water); color: var(--white); }
  .tb-ice { background: #00ACC1; color: var(--white); }
  .tb-psychic { background: var(--psychic); color: var(--white); }
  .tb-dragon { background: #4527A0; color: var(--white); }
  .tb-electric { background: var(--electric); color: var(--black); }
  .featured-desc {
    font-size: 0.9rem;
    line-height: 1.7;
    color: var(--gray-mid);
    margin-top: 1rem;
  }
  .stat-bars { margin-top: 1.5rem; display: flex; flex-direction: column; gap: 0.6rem; }
  .stat-row { display: grid; grid-template-columns: 90px 30px 1fr; gap: 0.75rem; align-items: center; }
  .stat-name { font-size: 0.7rem; font-weight: 700; letter-spacing: 1px; text-transform: uppercase; color: var(--gray-mid); }
  .stat-val { font-size: 0.8rem; font-weight: 700; color: var(--white); text-align: right; }
  .stat-bar-bg { height: 6px; background: #222; border-radius: 3px; overflow: hidden; }
  .stat-bar-fill { height: 100%; background: var(--yellow); border-radius: 3px; transition: width 1s ease; }
  .spotlight-list { display: flex; flex-direction: column; gap: 1rem; }
  .poke-row {
    display: grid;
    grid-template-columns: 3rem 1fr auto;
    align-items: center;
    gap: 1rem;
    padding: 1rem 1.25rem;
    border: 1px solid rgba(255,255,255,0.08);
    cursor: pointer;
    transition: background 0.15s, border-color 0.15s;
  }
  .poke-row:hover { background: rgba(255,255,255,0.04); border-color: rgba(255,255,255,0.2); }
  .poke-num {
    font-family: 'Bangers', cursive;
    font-size: 1.3rem;
    color: rgba(255,255,255,0.2);
  }
  .poke-info-name {
    font-family: 'Bangers', cursive;
    font-size: 1.4rem;
    letter-spacing: 1px;
    color: var(--white);
  }
  .poke-info-type { font-size: 0.7rem; color: var(--gray-mid); margin-top: 2px; }
  .poke-arrow { color: var(--yellow); font-size: 1.2rem; }

  /* ─── GENERATIONS SECTION ─── */
  #generations {
    padding: 7rem 2.5rem;
    background: var(--gray);
  }
  .gen-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }
  .gen-card {
    background: var(--white);
    border: 3px solid var(--black);
    padding: 2rem;
    box-shadow: 5px 5px 0 var(--black);
    transition: transform 0.15s, box-shadow 0.15s;
  }
  .gen-card:hover { transform: translate(-3px, -3px); box-shadow: 8px 8px 0 var(--black); }
  .gen-number {
    font-family: 'Bangers', cursive;
    font-size: 4.5rem;
    line-height: 1;
    color: var(--ink);
    color: rgba(0,0,0,0.07);
  }
  .gen-name {
    font-family: 'Bangers', cursive;
    font-size: 2rem;
    letter-spacing: 1px;
    color: var(--black);
    margin-top: -0.5rem;
  }
  .gen-region {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 0.75rem;
  }
  .gen-desc { font-size: 0.85rem; line-height: 1.6; color: #555; }
  .gen-count {
    margin-top: 1.25rem;
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--gray-mid);
    letter-spacing: 1px;
  }
  .gen-count strong { color: var(--black); font-size: 1rem; }

  /* ─── TRIVIA SECTION ─── */
  #trivia {
    padding: 7rem 2.5rem;
    background: var(--red);
  }
  #trivia .section-title { color: var(--white); }
  #trivia .section-label { color: rgba(255,255,255,0.5); }
  .trivia-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }
  .trivia-card {
    background: rgba(0,0,0,0.2);
    border: 2px solid rgba(255,255,255,0.2);
    padding: 2rem;
    transition: background 0.15s;
  }
  .trivia-card:hover { background: rgba(0,0,0,0.35); }
  .trivia-num {
    font-family: 'Bangers', cursive;
    font-size: 3rem;
    color: var(--yellow);
    line-height: 1;
    margin-bottom: 0.5rem;
  }
  .trivia-label {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: rgba(255,255,255,0.6);
    margin-bottom: 0.4rem;
  }
  .trivia-text { font-size: 1rem; font-weight: 500; color: var(--white); line-height: 1.5; }

  /* ─── STARTERS ─── */
  #starters {
    padding: 7rem 2.5rem;
    background: var(--black);
    text-align: center;
  }
  #starters .section-header { text-align: center; }
  #starters .section-title { color: var(--white); }
  #starters .section-label { color: rgba(255,255,255,0.4); }
  .starters-row {
    display: flex;
    gap: 2rem;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: 3.5rem;
  }
  .starter-card {
    width: 220px;
    padding: 2.5rem 1.5rem 2rem;
    border: 3px solid;
    text-align: center;
    transition: transform 0.2s, box-shadow 0.2s;
    cursor: default;
  }
  .starter-card:hover { transform: translateY(-8px); }
  .starter-card.grass-card { border-color: var(--grass); box-shadow: 0 0 30px rgba(46,125,50,0.3); }
  .starter-card.fire-card { border-color: var(--fire); box-shadow: 0 0 30px rgba(255,109,0,0.3); }
  .starter-card.water-card { border-color: var(--water); box-shadow: 0 0 30px rgba(2,136,209,0.3); }
  .starter-icon { font-size: 3.5rem; margin-bottom: 1rem; }
  .starter-name {
    font-family: 'Bangers', cursive;
    font-size: 2.2rem;
    letter-spacing: 2px;
    color: var(--white);
    margin-bottom: 0.25rem;
  }
  .starter-type {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 1rem;
  }
  .starter-card.grass-card .starter-type { color: #81C784; }
  .starter-card.fire-card .starter-type { color: #FFB74D; }
  .starter-card.water-card .starter-type { color: #4FC3F7; }
  .starter-desc { font-size: 0.82rem; line-height: 1.6; color: var(--gray-mid); }

  /* ─── FOOTER ─── */
  footer {
    background: #0a0a0a;
    border-top: 3px solid var(--yellow);
    padding: 3rem 2.5rem;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 2rem;
    align-items: start;
  }
  .footer-brand .nav-logo { font-size: 2.5rem; }
  .footer-tagline { font-size: 0.85rem; color: var(--gray-mid); margin-top: 0.5rem; line-height: 1.6; }
  .footer-col-title {
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--yellow);
    margin-bottom: 1rem;
  }
  .footer-links { list-style: none; display: flex; flex-direction: column; gap: 0.5rem; }
  .footer-links a {
    color: var(--gray-mid);
    text-decoration: none;
    font-size: 0.85rem;
    transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--white); }
  .footer-bottom {
    background: #0a0a0a;
    padding: 1rem 2.5rem;
    text-align: center;
    font-size: 0.75rem;
    color: #444;
    border-top: 1px solid rgba(255,255,255,0.05);
  }

  /* ─── ANIMATIONS ─── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; transform: scale(0.9); }
    to { opacity: 1; transform: scale(1); }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
  }
  @keyframes ticker {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }
  @keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.6s, transform 0.6s;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* ─── RESPONSIVE ─── */
  @media (max-width: 768px) {
    nav { padding: 1rem 1.25rem; }
    .nav-links { display: none; }
    #hero { grid-template-columns: 1fr; padding: 6rem 1.25rem 3rem; }
    .hero-graphic { margin-top: 2rem; }
    .spotlight-grid { grid-template-columns: 1fr; gap: 2rem; }
    footer { grid-template-columns: 1fr; }
    #types, #spotlight, #generations, #trivia, #starters { padding: 4rem 1.25rem; }
  }
</style>
</head>
<body>

<nav aria-label="Main navigation">
  <div class="nav-logo">PokéDex</div>
  <ul class="nav-links">
    <li><a href="#types">Types</a></li>
    <li><a href="#spotlight">Pokémon</a></li>
    <li><a href="#generations">Generations</a></li>
    <li><a href="#starters">Starters</a></li>
  </ul>
</nav>

<section id="hero" aria-label="Hero section">
  <div class="hero-stripe" aria-hidden="true"></div>
  <div class="hero-bg-circle" aria-hidden="true"></div>

  <div class="hero-content">
    <p class="hero-eyebrow">The Ultimate Pokémon Universe</p>
    <h1 class="hero-title">Gotta<br><span>Catch</span><br>'Em All</h1>
    <p class="hero-subtitle">Over 1,000 species. Nine generations of adventure. One world where creatures of unimaginable power live alongside humanity — waiting to be discovered, trained, and befriended.</p>
    <div class="hero-cta">
      <a href="#spotlight" class="btn-primary" aria-label="Explore Pokémon">Explore Now</a>
      <a href="#types" class="btn-secondary" aria-label="Learn about types">All Types →</a>
    </div>
  </div>

  <div class="hero-graphic" aria-hidden="true">
    <svg class="pokeball-hero" viewBox="0 0 400 400" xmlns="http://www.w3.org/2000/svg" aria-label="Pokéball illustration">
      <circle cx="200" cy="200" r="190" fill="none" stroke="rgba(255,255,255,0.08)" stroke-width="4"/>
      <circle cx="200" cy="200" r="150" fill="none" stroke="rgba(255,215,0,0.12)" stroke-width="2"/>
      <path d="M10,200 A190,190 0 0,1 390,200 Z" fill="#FF1C1C"/>
      <path d="M10,200 A190,190 0 0,0 390,200 Z" fill="#FAFAFA"/>
      <rect x="0" y="185" width="400" height="30" fill="#0D0D0D"/>
      <circle cx="200" cy="200" r="42" fill="#0D0D0D"/>
      <circle cx="200" cy="200" r="32" fill="#FAFAFA"/>
      <circle cx="200" cy="200" r="24" fill="none" stroke="rgba(255,215,0,0.6)" stroke-width="3"/>
      <circle cx="186" cy="186" r="7" fill="rgba(255,255,255,0.5)"/>
    </svg>
  </div>
</section>

<div class="ticker" aria-hidden="true">
  <div class="ticker-inner">
    <span class="ticker-item">Generation I — Kanto</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation II — Johto</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation III — Hoenn</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation IV — Sinnoh</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation V — Unova</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation VI — Kalos</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation VII — Alola</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation VIII — Galar</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation IX — Paldea</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation I — Kanto</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation II — Johto</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation III — Hoenn</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation IV — Sinnoh</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation V — Unova</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation VI — Kalos</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation VII — Alola</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation VIII — Galar</span><span class="ticker-dot">◆</span>
    <span class="ticker-item">Generation IX — Paldea</span><span class="ticker-dot">◆</span>
  </div>
</div>

<section id="types" aria-label="Pokémon types">
  <div class="section-header reveal">
    <p class="section-label">Battle Mechanics</p>
    <h2 class="section-title">Master the <em>18 Types</em></h2>
  </div>

  <div class="types-grid">
    <div class="type-card fire reveal" role="article">
      <div class="type-icon" aria-hidden="true">🔥</div>
      <div class="type-name">Fire</div>
      <div class="type-desc">Scorching offense. Melts Steel, burns Grass & Ice</div>
    </div>
    <div class="type-card water reveal" role="article">
      <div class="type-icon" aria-hidden="true">💧</div>
      <div class="type-name">Water</div>
      <div class="type-desc">Adaptable & powerful. Dominates Fire & Rock</div>
    </div>
    <div class="type-card grass reveal" role="article">
      <div class="type-icon" aria-hidden="true">🌿</div>
      <div class="type-name">Grass</div>
      <div class="type-desc">Nature's resilience. Absorbs Ground & Water</div>
    </div>
    <div class="type-card electric reveal" role="article">
      <div class="type-icon" aria-hidden="true">⚡</div>
      <div class="type-name">Electric</div>
      <div class="type-desc">Shocking speed. Only Ground escapes its sparks</div>
    </div>
    <div class="type-card psychic reveal" role="article">
      <div class="type-icon" aria-hidden="true">🔮</div>
      <div class="type-name">Psychic</div>
      <div class="type-desc">Mind over matter. Crushes Poison & Fighting</div>
    </div>
    <div class="type-card ice reveal" role="article">
      <div class="type-icon" aria-hidden="true">❄️</div>
      <div class="type-name">Ice</div>
      <div class="type-desc">Fragile but deadly. Freezes Dragon in its tracks</div>
    </div>
    <div class="type-card dragon reveal" role="article">
      <div class="type-icon" aria-hidden="true">🐉</div>
      <div class="type-name">Dragon</div>
      <div class="type-desc">Raw legendary power. Weak only to itself & Fairy</div>
    </div>
    <div class="type-card dark reveal" role="article">
      <div class="type-icon" aria-hidden="true">🌑</div>
      <div class="type-name">Dark</div>
      <div class="type-desc">Underhanded tactics. Counters Psychic & Ghost</div>
    </div>
    <div class="type-card normal reveal" role="article">
      <div class="type-icon" aria-hidden="true">⭐</div>
      <div class="type-name">Normal</div>
      <div class="type-desc">Jack of all trades. No super-effective hits</div>
    </div>
    <div class="type-card fighting reveal" role="article">
      <div class="type-icon" aria-hidden="true">👊</div>
      <div class="type-name">Fighting</div>
      <div class="type-desc">Brute strength. Cracks Steel, Rock & Ice with ease</div>
    </div>
    <div class="type-card ghost reveal" role="article">
      <div class="type-icon" aria-hidden="true">👻</div>
      <div class="type-name">Ghost</div>
      <div class="type-desc">Immune to Normal. Haunts Psychic & Ghost types</div>
    </div>
    <div class="type-card rock reveal" role="article">
      <div class="type-icon" aria-hidden="true">🪨</div>
      <div class="type-name">Rock</div>
      <div class="type-desc">Defensive fortress. Pelts Flying & Fire harshly</div>
    </div>
  </div>
</section>

<section id="spotlight" aria-label="Pokémon spotlight">
  <div class="section-header reveal">
    <p class="section-label">Hall of Fame</p>
    <h2 class="section-title">Legendary <em>Icons</em></h2>
  </div>

  <div class="spotlight-grid">
    <div class="spotlight-featured reveal" aria-label="Featured Pokémon: Charizard">
      <div class="featured-number" aria-hidden="true">#006</div>
      <div class="featured-label">Featured Pokémon</div>
      <div class="featured-name">Charizard</div>
      <div class="featured-types">
        <span class="type-badge tb-fire">Fire</span>
        <span class="type-badge tb-flying">Flying</span>
      </div>
      <p class="featured-desc">
        The flame on the tip of its tail indicates Charizard's life force. If it is healthy, the flame burns brightly. Soaring through clouds at 4,600 feet, it spits fire hot enough to melt boulders — making it one of the most recognizable and beloved Pokémon in history.
      </p>
      <div class="stat-bars" aria-label="Charizard base stats">
        <div class="stat-row">
          <span class="stat-name">HP</span>
          <span class="stat-val">78</span>
          <div class="stat-bar-bg"><div class="stat-bar-fill" style="width:0%" data-width="52%"></div></div>
        </div>
        <div class="stat-row">
          <span class="stat-name">Attack</span>
          <span class="stat-val">84</span>
          <div class="stat-bar-bg"><div class="stat-bar-fill" style="width:0%" data-width="56%"></div></div>
        </div>
        <div class="stat-row">
          <span class="stat-name">Sp. Attack</span>
          <span class="stat-val">109</span>
          <div class="stat-bar-bg"><div class="stat-bar-fill" style="width:0%" data-width="73%"></div></div>
        </div>
        <div class="stat-row">
          <span class="stat-name">Speed</span>
          <span class="stat-val">100</span>
          <div class="stat-bar-bg"><div class="stat-bar-fill" style="width:0%" data-width="67%"></div></div>
        </div>
      </div>
    </div>

    <div class="spotlight-list reveal" aria-label="Other notable Pokémon">
      <div class="poke-row" role="article" tabindex="0" aria-label="Mewtwo, number 150, Psychic type">
        <div class="poke-num">#150</div>
        <div>
          <div class="poke-info-name">Mewtwo</div>
          <div class="poke-info-type"><span class="type-badge tb-psychic" style="font-size:0.6rem;padding:0.2rem 0.5rem;">Psychic</span></div>
        </div>
        <div class="poke-arrow">→</div>
      </div>
      <div class="poke-row" role="article" tabindex="0" aria-label="Pikachu, number 25, Electric type">
        <div class="poke-num">#025</div>
        <div>
          <div class="poke-info-name">Pikachu</div>
          <div class="poke-info-type"><span class="type-badge tb-electric" style="font-size:0.6rem;padding:0.2rem 0.5rem;">Electric</span></div>
        </div>
        <div class="poke-arrow">→</div>
      </div>
      <div class="poke-row" role="article" tabindex="0" aria-label="Gengar, number 94, Ghost and Poison type">
        <div class="poke-num">#094</div>
        <div>
          <div class="poke-info-name">Gengar</div>
          <div class="poke-info-type"><span class="type-badge tb-flying" style="font-size:0.6rem;padding:0.2rem 0.5rem;background:#4A148C;">Ghost</span></div>
        </div>
        <div class="poke-arrow">→</div>
      </div>
      <div class="poke-row" role="article" tabindex="0" aria-label="Dragonite, number 149, Dragon and Flying type">
        <div class="poke-num">#149</div>
        <div>
          <div class="poke-info-name">Dragonite</div>
          <div class="poke-info-type"><span class="type-badge tb-dragon" style="font-size:0.6rem;padding:0.2rem 0.5rem;">Dragon</span></div>
        </div>
        <div class="poke-arrow">→</div>
      </div>
      <div class="poke-row" role="article" tabindex="0" aria-label="Lucario, number 448, Fighting and Steel type">
        <div class="poke-num">#448</div>
        <div>
          <div class="poke-info-name">Lucario</div>
          <div class="poke-info-type"><span class="type-badge" style="font-size:0.6rem;padding:0.2rem 0.5rem;background:#B71C1C;color:white;">Fighting</span></div>
        </div>
        <div class="poke-arrow">→</div>
      </div>
      <div class="poke-row" role="article" tabindex="0" aria-label="Gyarados, number 130, Water and Flying type">
        <div class="poke-num">#130</div>
        <div>
          <div class="poke-info-name">Gyarados</div>
          <div class="poke-info-type"><span class="type-badge tb-water" style="font-size:0.6rem;padding:0.2rem 0.5rem;">Water</span></div>
        </div>
        <div class="poke-arrow">→</div>
      </div>
      <div class="poke-row" role="article" tabindex="0" aria-label="Eevee, number 133, Normal type">
        <div class="poke-num">#133</div>
        <div>
          <div class="poke-info-name">Eevee</div>
          <div class="poke-info-type"><span class="type-badge" style="font-size:0.6rem;padding:0.2rem 0.5rem;background:#757575;color:white;">Normal</span></div>
        </div>
        <div class="poke-arrow">→</div>
      </div>
    </div>
  </div>
</section>

<section id="generations" aria-label="Pokémon generations">
  <div class="section-header reveal">
    <p class="section-label">Journey Through Time</p>
    <h2 class="section-title">Nine <em>Generations</em></h2>
  </div>

  <div class="gen-grid">
    <div class="gen-card reveal" role="article">
      <div class="gen-number" aria-hidden="true">I</div>
      <div class="gen-region">Kanto Region</div>
      <div class="gen-name">Red & Blue</div>
      <p class="gen-desc">Where it all began. Professor Oak hands you a Pokédex in Pallet Town and an entire world opens up. The original 151 became cultural icons overnight.</p>
      <div class="gen-count"><strong>151</strong> Pokémon · 1996</div>
    </div>
    <div class="gen-card reveal" role="article">
      <div class="gen-number" aria-hidden="true">II</div>
      <div class="gen-region">Johto Region</div>
      <div class="gen-name">Gold & Silver</div>
      <p class="gen-desc">Day and night cycles changed everything. The addition of breeding, held items, and two full regions to explore cemented Pokémon as a franchise for life.</p>
      <div class="gen-count"><strong>100</strong> Pokémon · 1999</div>
    </div>
    <div class="gen-card reveal" role="article">
      <div class="gen-number" aria-hidden="true">III</div>
      <div class="gen-region">Hoenn Region</div>
      <div class="gen-name">Ruby & Sapphire</div>
      <p class="gen-desc">A tropical paradise of water routes and secret bases. Contests, double battles, and abilities reinvented competitive play entirely.</p>
      <div class="gen-count"><strong>135</strong> Pokémon · 2002</div>
    </div>
    <div class="gen-card reveal" role="article">
      <div class="gen-number" aria-hidden="true">IV</div>
      <div class="gen-region">Sinnoh Region</div>
      <div class="gen-name">Diamond & Pearl</div>
      <p class="gen-desc">Mythology and time travel. Dialga, Palkia, and Giratina introduced cosmic stakes while the Underground brought players together in brand new ways.</p>
      <div class="gen-count"><strong>107</strong> Pokémon · 2006</div>
    </div>
    <div class="gen-card reveal" role="article">
      <div class="gen-number" aria-hidden="true">V</div>
      <div class="gen-region">Unova Region</div>
      <div class="gen-name">Black & White</div>
      <p class="gen-desc">The most ambitious story in the series. A cinematic adventure questioning whether Pokémon battles are ethical — and featuring the best rival cast in franchise history.</p>
      <div class="gen-count"><strong>156</strong> Pokémon · 2010</div>
    </div>
    <div class="gen-card reveal" role="article">
      <div class="gen-number" aria-hidden="true">IX</div>
      <div class="gen-region">Paldea Region</div>
      <div class="gen-name">Scarlet & Violet</div>
      <p class="gen-desc">The first truly open-world Pokémon games. Three intertwining storylines let you blaze your own path through a sun-drenched Mediterranean landscape filled with new discoveries.</p>
      <div class="gen-count"><strong>120</strong> Pokémon · 2022</div>
    </div>
  </div>
</section>

<section id="trivia" aria-label="Pokémon facts and statistics">
  <div class="section-header reveal">
    <p class="section-label">By the Numbers</p>
    <h2 class="section-title">The Scale of <em>Pokémon</em></h2>
  </div>

  <div class="trivia-grid">
    <div class="trivia-card reveal" role="article">
      <div class="trivia-num">1,025</div>
      <div class="trivia-label">Total Species</div>
      <div class="trivia-text">Pokémon officially registered in the National Pokédex as of Generation IX</div>
    </div>
    <div class="trivia-card reveal" role="article">
      <div class="trivia-num">18</div>
      <div class="trivia-label">Types</div>
      <div class="trivia-text">Unique elemental types governing 324 possible matchup combinations</div>
    </div>
    <div class="trivia-card reveal" role="article">
      <div class="trivia-num">440M+</div>
      <div class="trivia-label">Games Sold</div>
      <div class="trivia-text">Making Pokémon the highest-grossing media franchise of all time — over $150 billion</div>
    </div>
    <div class="trivia-card reveal" role="article">
      <div class="trivia-num">900+</div>
      <div class="trivia-label">Anime Episodes</div>
      <div class="trivia-text">Ash Ketchum's journey spanned 26 years before he finally became World Champion</div>
    </div>
    <div class="trivia-card reveal" role="article">
      <div class="trivia-num">43.2B</div>
      <div class="trivia-label">Cards Sold</div>
      <div class="trivia-text">The Pokémon Trading Card Game remains one of the world's most collected hobbies</div>
    </div>
    <div class="trivia-card reveal" role="article">
      <div class="trivia-num">1996</div>
      <div class="trivia-label">Year Born</div>
      <div class="trivia-text">Satoshi Tajiri's childhood dream of insect collecting became the world's greatest monster franchise</div>
    </div>
  </div>
</section>

<section id="starters" aria-label="Original starter Pokémon">
  <div class="section-header">
    <p class="section-label reveal">The Classic Choice</p>
    <h2 class="section-title reveal">Choose Your <em>Starter</em></h2>
  </div>

  <div class="starters-row">
    <div class="starter-card grass-card reveal" role="article" aria-label="Bulbasaur, Grass type starter">
      <div class="starter-icon" aria-hidden="true">🌱</div>
      <div class="starter-name">Bulbasaur</div>
      <div class="starter-type">Grass / Poison</div>
      <p class="starter-desc">Born with a bulb on its back, this dinosaur-frog hybrid is the easiest choice for first-time trainers — its Vine Whip dominates the first two gyms.</p>
    </div>
    <div class="starter-card fire-card reveal" role="article" aria-label="Charmander, Fire type starter">
      <div class="starter-icon" aria-hidden="true">🔥</div>
      <div class="starter-name">Charmander</div>
      <div class="starter-type">Fire</div>
      <p class="starter-desc">The hard-mode starter with the highest payoff. Evolves into the iconic Charizard — the single most popular Pokémon ever created, and a fan favorite for 30 years.</p>
    </div>
    <div class="starter-card water-card reveal" role="article" aria-label="Squirtle, Water type starter">
      <div class="starter-icon" aria-hidden="true">💧</div>
      <div class="starter-name">Squirtle</div>
      <div class="starter-type">Water</div>
      <p class="starter-desc">The well-rounded choice. Squirtle's squad is legendary. It evolves into Blastoise, a tank-like powerhouse that fires jets of water with pinpoint accuracy.</p>
    </div>
  </div>
</section>

<footer aria-label="Footer">
  <div class="footer-brand">
    <div class="nav-logo">PokéDex</div>
    <p class="footer-tagline">A fan-made celebration of the Pokémon universe. Not affiliated with Nintendo, Game Freak, or The Pokémon Company.</p>
  </div>
  <div>
    <div class="footer-col-title">Explore</div>
    <ul class="footer-links">
      <li><a href="#types">Battle Types</a></li>
      <li><a href="#spotlight">Hall of Fame</a></li>
      <li><a href="#generations">All Generations</a></li>
      <li><a href="#starters">Starter Pokémon</a></li>
    </ul>
  </div>
  <div>
    <div class="footer-col-title">Discover</div>
    <ul class="footer-links">
      <li><a href="#trivia">Pokémon Facts</a></li>
      <li><a href="#hero">Back to Top</a></li>
    </ul>
  </div>
</footer>
<div class="footer-bottom">
  <p>Pokémon and all related names are trademarks of Nintendo / Creatures Inc. / GAME FREAK inc. Fan tribute only.</p>
</div>

<script>
  // Intersection observer for reveal animations
  const revealEls = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), 80);
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });

  revealEls.forEach(el => observer.observe(el));

  // Stagger sibling reveals
  document.querySelectorAll('.types-grid, .gen-grid, .trivia-grid, .starters-row, .spotlight-list').forEach(grid => {
    const children = grid.querySelectorAll('.reveal');
    children.forEach((child, i) => {
      child.style.transitionDelay = `${i * 60}ms`;
    });
  });

  // Animate stat bars when they come into view
  const statObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.querySelectorAll('.stat-bar-fill').forEach(bar => {
          const target = bar.dataset.width;
          bar.style.width = target;
        });
        statObserver.unobserve(entry.target);
      }
    });
  }, { threshold: 0.3 });

  const featured = document.querySelector('.spotlight-featured');
  if (featured) statObserver.observe(featured);
</script>
</body>
</html>

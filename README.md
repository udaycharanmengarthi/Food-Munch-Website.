<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>FoodMunch — Eat Bold. Live Loud.</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --cream: #FAF5EC;
      --deep: #1A0A00;
      --ember: #E84A0C;
      --gold: #F5A623;
      --moss: #3D5A3E;
      --warm-white: #FFF8F0;
      --charcoal: #2C2016;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--cream);
      color: var(--deep);
      font-family: 'DM Sans', sans-serif;
      overflow-x: hidden;
      cursor: none;
    }

    /* CUSTOM CURSOR */
    .cursor {
      width: 12px; height: 12px;
      background: var(--ember);
      border-radius: 50%;
      position: fixed; top: 0; left: 0;
      pointer-events: none;
      z-index: 9999;
      transform: translate(-50%, -50%);
      transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
      mix-blend-mode: multiply;
    }
    .cursor-ring {
      width: 36px; height: 36px;
      border: 1.5px solid var(--ember);
      border-radius: 50%;
      position: fixed; top: 0; left: 0;
      pointer-events: none;
      z-index: 9998;
      transform: translate(-50%, -50%);
      transition: transform 0.18s ease, width 0.25s, height 0.25s, opacity 0.2s;
      opacity: 0.6;
    }
    body:hover .cursor { opacity: 1; }

    /* NAV */
    nav {
      position: fixed; top: 0; left: 0; right: 0;
      z-index: 100;
      padding: 24px 6vw;
      display: flex; align-items: center; justify-content: space-between;
      background: transparent;
      transition: background 0.4s, backdrop-filter 0.4s;
    }
    nav.scrolled {
      background: rgba(250,245,236,0.92);
      backdrop-filter: blur(14px);
      padding: 16px 6vw;
      box-shadow: 0 1px 0 rgba(0,0,0,0.07);
    }
    .logo {
      font-family: 'Playfair Display', serif;
      font-size: 1.7rem;
      font-weight: 900;
      letter-spacing: -0.02em;
      color: var(--deep);
      text-decoration: none;
    }
    .logo span { color: var(--ember); }
    .nav-links { display: flex; gap: 36px; list-style: none; }
    .nav-links a {
      font-family: 'Syne', sans-serif;
      font-size: 0.82rem;
      font-weight: 700;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      text-decoration: none;
      color: var(--charcoal);
      opacity: 0.7;
      transition: opacity 0.2s, color 0.2s;
    }
    .nav-links a:hover { opacity: 1; color: var(--ember); }
    .nav-cta {
      font-family: 'Syne', sans-serif;
      font-size: 0.8rem;
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      background: var(--ember);
      color: #fff;
      border: none;
      padding: 12px 28px;
      border-radius: 100px;
      cursor: none;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .nav-cta:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 30px rgba(232,74,12,0.35);
    }

    /* HERO */
    .hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      padding: 0 6vw;
      padding-top: 100px;
      position: relative;
      overflow: hidden;
      align-items: center;
    }
    .hero-bg-circle {
      position: absolute;
      width: 700px; height: 700px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(245,166,35,0.18) 0%, transparent 70%);
      top: -100px; right: -100px;
      animation: pulse 6s ease-in-out infinite;
      pointer-events: none;
    }
    @keyframes pulse { 0%,100%{transform:scale(1);} 50%{transform:scale(1.06);} }

    .hero-noise {
      position: absolute; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
      pointer-events: none; opacity: 0.5;
    }

    .hero-left { position: relative; z-index: 2; }
    .hero-tag {
      display: inline-flex; align-items: center; gap: 8px;
      background: rgba(232,74,12,0.1);
      border: 1px solid rgba(232,74,12,0.25);
      color: var(--ember);
      font-family: 'Syne', sans-serif;
      font-size: 0.72rem;
      font-weight: 700;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      padding: 7px 16px;
      border-radius: 100px;
      margin-bottom: 28px;
      animation: fadeUp 0.7s 0.1s both;
    }
    .hero-tag::before { content:''; width:6px;height:6px;background:var(--ember);border-radius:50%;animation:blink 1.4s infinite; }
    @keyframes blink { 0%,100%{opacity:1;} 50%{opacity:0.2;} }

    .hero-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(3.2rem, 6vw, 6.5rem);
      font-weight: 900;
      line-height: 1.0;
      letter-spacing: -0.03em;
      color: var(--deep);
      margin-bottom: 28px;
      animation: fadeUp 0.7s 0.2s both;
    }
    .hero-title em {
      font-style: italic;
      color: var(--ember);
      position: relative;
      display: inline-block;
    }
    .hero-title em::after {
      content: '';
      position: absolute;
      bottom: 4px; left: 0; right: 0; height: 4px;
      background: var(--gold);
      border-radius: 2px;
      transform-origin: left;
      animation: underline-grow 0.8s 0.9s both;
    }
    @keyframes underline-grow { from{transform:scaleX(0);} to{transform:scaleX(1);} }

    .hero-sub {
      font-size: 1.05rem;
      font-weight: 300;
      color: var(--charcoal);
      opacity: 0.7;
      max-width: 420px;
      line-height: 1.75;
      margin-bottom: 44px;
      animation: fadeUp 0.7s 0.35s both;
    }

    .hero-actions { display: flex; gap: 16px; align-items: center; animation: fadeUp 0.7s 0.5s both; }
    .btn-primary {
      font-family: 'Syne', sans-serif;
      font-size: 0.88rem;
      font-weight: 700;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      background: var(--deep);
      color: var(--cream);
      border: none;
      padding: 16px 36px;
      border-radius: 100px;
      cursor: none;
      transition: transform 0.2s, box-shadow 0.2s, background 0.25s;
      position: relative; overflow: hidden;
    }
    .btn-primary::after {
      content: '';
      position: absolute; inset: 0;
      background: var(--ember);
      border-radius: inherit;
      transform: translateX(-101%);
      transition: transform 0.35s cubic-bezier(0.4,0,0.2,1);
    }
    .btn-primary:hover::after { transform: translateX(0); }
    .btn-primary span { position: relative; z-index: 1; }
    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 12px 36px rgba(26,10,0,0.25); }

    .btn-outline {
      font-family: 'Syne', sans-serif;
      font-size: 0.88rem;
      font-weight: 700;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      background: transparent;
      color: var(--deep);
      border: 2px solid var(--deep);
      padding: 15px 32px;
      border-radius: 100px;
      cursor: none;
      transition: background 0.25s, color 0.25s, transform 0.2s;
      text-decoration: none;
    }
    .btn-outline:hover { background: var(--deep); color: var(--cream); transform: translateY(-2px); }

    .hero-stats {
      display: flex; gap: 40px;
      margin-top: 56px;
      padding-top: 40px;
      border-top: 1px solid rgba(26,10,0,0.1);
      animation: fadeUp 0.7s 0.65s both;
    }
    .stat-num {
      font-family: 'Playfair Display', serif;
      font-size: 2.2rem;
      font-weight: 900;
      color: var(--ember);
      line-height: 1;
    }
    .stat-label {
      font-size: 0.75rem;
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--charcoal);
      opacity: 0.6;
      margin-top: 4px;
    }

    /* HERO RIGHT — food visual */
    .hero-right {
      position: relative; z-index: 2;
      display: flex; justify-content: center; align-items: center;
      padding: 40px 0;
      animation: fadeIn 1s 0.3s both;
    }
    @keyframes fadeIn { from{opacity:0;} to{opacity:1;} }

    .hero-plate {
      position: relative;
      width: 460px; height: 460px;
    }
    .plate-circle {
      position: absolute; inset: 0;
      border-radius: 50%;
      background: radial-gradient(circle at 38% 38%, #fff9f0, #f5e9d0);
      box-shadow:
        0 30px 80px rgba(26,10,0,0.18),
        0 8px 20px rgba(26,10,0,0.1),
        inset 0 -4px 10px rgba(26,10,0,0.06);
    }
    .plate-ring {
      position: absolute; inset: -16px;
      border-radius: 50%;
      border: 2px solid rgba(245,166,35,0.3);
      animation: spin 18s linear infinite;
    }
    .plate-ring-2 {
      position: absolute; inset: -32px;
      border-radius: 50%;
      border: 1px dashed rgba(232,74,12,0.2);
      animation: spin 28s linear infinite reverse;
    }
    @keyframes spin { to{transform:rotate(360deg);} }

    .food-emoji-main {
      position: absolute; inset: 0;
      display: flex; justify-content: center; align-items: center;
      font-size: 9rem;
      animation: float 4s ease-in-out infinite;
    }
    @keyframes float { 0%,100%{transform:translateY(0) rotate(-3deg);} 50%{transform:translateY(-16px) rotate(3deg);} }

    .food-orbits {
      position: absolute; inset: -50px;
    }
    .orbit-item {
      position: absolute;
      width: 70px; height: 70px;
      background: white;
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.8rem;
      box-shadow: 0 8px 24px rgba(26,10,0,0.12);
    }
    .orbit-item:nth-child(1) { top: 10%; right: 5%; animation: floatOrbit 3.5s 0s ease-in-out infinite; }
    .orbit-item:nth-child(2) { bottom: 20%; left: 0%; animation: floatOrbit 3.5s 0.8s ease-in-out infinite; }
    .orbit-item:nth-child(3) { top: 50%; right: -2%; animation: floatOrbit 3.5s 1.6s ease-in-out infinite; }
    .orbit-item:nth-child(4) { top: 5%; left: 10%; animation: floatOrbit 3.5s 2.2s ease-in-out infinite; }
    @keyframes floatOrbit { 0%,100%{transform:translateY(0);} 50%{transform:translateY(-10px);} }

    .hero-badge {
      position: absolute;
      bottom: 30px; left: -20px;
      background: var(--deep);
      color: var(--cream);
      border-radius: 16px;
      padding: 14px 20px;
      display: flex; align-items: center; gap: 12px;
      box-shadow: 0 12px 32px rgba(26,10,0,0.25);
      animation: floatOrbit 4s 1s ease-in-out infinite;
    }
    .badge-icon { font-size: 1.5rem; }
    .badge-text-top { font-family: 'Syne', sans-serif; font-size: 0.7rem; font-weight: 700; opacity: 0.6; letter-spacing: 0.1em; text-transform: uppercase; }
    .badge-text-main { font-family: 'Playfair Display', serif; font-size: 1.05rem; font-weight: 700; }

    .hero-badge-2 {
      position: absolute;
      top: 20px; right: -20px;
      background: var(--ember);
      color: white;
      border-radius: 16px;
      padding: 12px 18px;
      display: flex; align-items: center; gap: 10px;
      box-shadow: 0 12px 32px rgba(232,74,12,0.35);
      animation: floatOrbit 4s 0.5s ease-in-out infinite;
    }
    .hero-badge-2 .badge-icon { font-size: 1.3rem; }
    .hero-badge-2 .badge-text-top { opacity: 0.8; }

    @keyframes fadeUp { from{opacity:0;transform:translateY(28px);} to{opacity:1;transform:translateY(0);} }

    /* MARQUEE */
    .marquee-section {
      background: var(--deep);
      padding: 20px 0;
      overflow: hidden;
    }
    .marquee-track {
      display: flex; gap: 0;
      animation: marquee 18s linear infinite;
      width: max-content;
    }
    .marquee-item {
      font-family: 'Playfair Display', serif;
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--cream);
      white-space: nowrap;
      padding: 0 32px;
      display: flex; align-items: center; gap: 16px;
    }
    .marquee-dot { color: var(--gold); font-size: 1.4rem; line-height: 1; }
    @keyframes marquee { to { transform: translateX(-50%); } }

    /* MENU */
    .menu-section {
      padding: 120px 6vw;
    }
    .section-label {
      font-family: 'Syne', sans-serif;
      font-size: 0.72rem;
      font-weight: 700;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--ember);
      margin-bottom: 16px;
    }
    .section-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2.4rem, 4vw, 4rem);
      font-weight: 900;
      line-height: 1.1;
      letter-spacing: -0.02em;
      color: var(--deep);
      margin-bottom: 60px;
      max-width: 560px;
    }
    .section-title em { font-style: italic; color: var(--ember); }

    .menu-filter {
      display: flex; gap: 12px; flex-wrap: wrap;
      margin-bottom: 52px;
    }
    .filter-btn {
      font-family: 'Syne', sans-serif;
      font-size: 0.78rem;
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      padding: 10px 22px;
      border-radius: 100px;
      border: 1.5px solid rgba(26,10,0,0.15);
      background: transparent;
      color: var(--charcoal);
      cursor: none;
      transition: all 0.2s;
    }
    .filter-btn.active, .filter-btn:hover {
      background: var(--ember);
      color: white;
      border-color: var(--ember);
    }

    .menu-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 28px;
    }
    .menu-card {
      background: var(--warm-white);
      border-radius: 24px;
      overflow: hidden;
      transition: transform 0.3s, box-shadow 0.3s;
      cursor: none;
      border: 1px solid rgba(26,10,0,0.06);
    }
    .menu-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 24px 60px rgba(26,10,0,0.12);
    }
    .menu-card.featured {
      grid-column: span 1;
      background: var(--deep);
      color: var(--cream);
    }
    .card-img {
      height: 200px;
      display: flex; align-items: center; justify-content: center;
      font-size: 5rem;
      background: linear-gradient(135deg, rgba(245,166,35,0.12), rgba(232,74,12,0.08));
      position: relative;
    }
    .featured .card-img {
      background: linear-gradient(135deg, rgba(245,166,35,0.15), rgba(232,74,12,0.12));
    }
    .card-badge {
      position: absolute; top: 16px; right: 16px;
      background: var(--ember);
      color: white;
      font-family: 'Syne', sans-serif;
      font-size: 0.65rem;
      font-weight: 700;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 5px 12px;
      border-radius: 100px;
    }
    .card-body { padding: 24px; }
    .card-category {
      font-family: 'Syne', sans-serif;
      font-size: 0.68rem;
      font-weight: 700;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--ember);
      margin-bottom: 8px;
    }
    .card-name {
      font-family: 'Playfair Display', serif;
      font-size: 1.25rem;
      font-weight: 700;
      margin-bottom: 8px;
      color: inherit;
    }
    .card-desc {
      font-size: 0.85rem;
      opacity: 0.6;
      line-height: 1.6;
      margin-bottom: 20px;
    }
    .card-footer { display: flex; align-items: center; justify-content: space-between; }
    .card-price {
      font-family: 'Playfair Display', serif;
      font-size: 1.4rem;
      font-weight: 900;
      color: var(--ember);
    }
    .add-btn {
      width: 38px; height: 38px;
      border-radius: 50%;
      background: var(--deep);
      color: var(--cream);
      border: none;
      font-size: 1.3rem;
      display: flex; align-items: center; justify-content: center;
      cursor: none;
      transition: transform 0.2s, background 0.2s;
    }
    .featured .add-btn { background: var(--ember); }
    .add-btn:hover { transform: scale(1.15); }
    .card-stars { font-size: 0.8rem; color: var(--gold); margin-bottom: 4px; }

    /* WHY US */
    .why-section {
      background: var(--deep);
      padding: 120px 6vw;
      position: relative;
      overflow: hidden;
    }
    .why-section .section-title { color: var(--cream); }
    .why-section .section-label { color: var(--gold); }
    .why-bg {
      position: absolute; inset: 0;
      background: radial-gradient(ellipse at 80% 50%, rgba(232,74,12,0.12) 0%, transparent 65%);
      pointer-events: none;
    }
    .why-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 48px;
      align-items: center;
    }
    .why-features { display: flex; flex-direction: column; gap: 28px; }
    .why-feat {
      display: flex; gap: 20px; align-items: flex-start;
      padding: 28px;
      border-radius: 20px;
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(255,255,255,0.06);
      transition: background 0.3s, transform 0.3s;
    }
    .why-feat:hover { background: rgba(255,255,255,0.08); transform: translateX(8px); }
    .feat-icon {
      width: 52px; height: 52px; min-width: 52px;
      border-radius: 14px;
      background: linear-gradient(135deg, var(--ember), var(--gold));
      display: flex; align-items: center; justify-content: center;
      font-size: 1.5rem;
    }
    .feat-title {
      font-family: 'Syne', sans-serif;
      font-size: 1.05rem;
      font-weight: 700;
      color: var(--cream);
      margin-bottom: 6px;
    }
    .feat-desc { font-size: 0.88rem; color: rgba(255,255,255,0.5); line-height: 1.65; }

    .why-visual {
      position: relative;
      display: flex; justify-content: center; align-items: center;
      height: 480px;
    }
    .why-card-big {
      background: linear-gradient(145deg, #2e1a06, #1a0a00);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 28px;
      padding: 40px;
      width: 100%; max-width: 340px;
      text-align: center;
      box-shadow: 0 40px 80px rgba(0,0,0,0.4);
    }
    .why-card-big .big-emoji { font-size: 6rem; margin-bottom: 16px; display: block; animation: float 4s ease-in-out infinite; }
    .why-card-big h3 { font-family: 'Playfair Display', serif; font-size: 1.6rem; font-weight: 900; color: var(--cream); margin-bottom: 8px; }
    .why-card-big p { font-size: 0.88rem; color: rgba(255,255,255,0.5); margin-bottom: 24px; line-height: 1.6; }
    .why-rating { display: flex; align-items: center; justify-content: center; gap: 10px; }
    .stars-big { font-size: 1.2rem; color: var(--gold); }
    .rating-num { font-family: 'Playfair Display', serif; font-size: 1.4rem; font-weight: 900; color: var(--cream); }
    .rating-label { font-size: 0.75rem; color: rgba(255,255,255,0.4); }

    .floating-chips {
      position: absolute; inset: 0; pointer-events: none;
    }
    .chip {
      position: absolute;
      background: rgba(255,255,255,0.05);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 100px;
      padding: 8px 16px;
      font-size: 0.78rem;
      color: rgba(255,255,255,0.5);
      font-family: 'Syne', sans-serif;
      white-space: nowrap;
    }
    .chip:nth-child(1) { top: 10%; left: 0; animation: floatOrbit 4s 0s ease-in-out infinite; }
    .chip:nth-child(2) { top: 30%; right: 0; animation: floatOrbit 4s 1s ease-in-out infinite; }
    .chip:nth-child(3) { bottom: 20%; left: 5%; animation: floatOrbit 4s 2s ease-in-out infinite; }

    /* TESTIMONIALS */
    .testimonials-section { padding: 120px 6vw; background: var(--warm-white); }
    .testi-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; margin-top: 60px; }
    .testi-card {
      background: white;
      border-radius: 22px;
      padding: 32px;
      border: 1px solid rgba(26,10,0,0.06);
      transition: transform 0.3s, box-shadow 0.3s;
    }
    .testi-card:hover { transform: translateY(-6px); box-shadow: 0 20px 50px rgba(26,10,0,0.08); }
    .testi-card.highlight {
      background: var(--ember);
      color: white;
      border: none;
    }
    .testi-stars { font-size: 1rem; color: var(--gold); margin-bottom: 16px; }
    .testi-card.highlight .testi-stars { color: var(--cream); }
    .testi-text {
      font-family: 'Playfair Display', serif;
      font-style: italic;
      font-size: 1.05rem;
      line-height: 1.65;
      color: var(--charcoal);
      margin-bottom: 24px;
    }
    .testi-card.highlight .testi-text { color: white; }
    .testi-author { display: flex; align-items: center; gap: 12px; }
    .testi-avatar {
      width: 44px; height: 44px; border-radius: 50%;
      background: linear-gradient(135deg, var(--gold), var(--ember));
      display: flex; align-items: center; justify-content: center;
      font-size: 1.1rem;
    }
    .testi-name { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.9rem; color: var(--deep); }
    .testi-card.highlight .testi-name { color: white; }
    .testi-role { font-size: 0.75rem; opacity: 0.5; }

    /* NEWSLETTER */
    .newsletter-section {
      padding: 100px 6vw;
      background: var(--cream);
      text-align: center;
    }
    .newsletter-inner {
      max-width: 600px; margin: 0 auto;
    }
    .newsletter-section .section-title { margin: 0 auto 20px; text-align: center; max-width: 100%; }
    .newsletter-sub { font-size: 1rem; color: var(--charcoal); opacity: 0.6; margin-bottom: 40px; line-height: 1.7; }
    .newsletter-form {
      display: flex; gap: 12px;
      background: white;
      border: 1.5px solid rgba(26,10,0,0.1);
      border-radius: 100px;
      padding: 6px 6px 6px 24px;
      box-shadow: 0 8px 32px rgba(26,10,0,0.07);
    }
    .newsletter-form input {
      flex: 1; border: none; outline: none;
      font-family: 'DM Sans', sans-serif;
      font-size: 0.95rem;
      background: transparent;
      color: var(--deep);
    }
    .newsletter-form input::placeholder { opacity: 0.4; }
    .newsletter-form button {
      font-family: 'Syne', sans-serif;
      font-size: 0.82rem;
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      background: var(--ember);
      color: white;
      border: none;
      padding: 14px 28px;
      border-radius: 100px;
      cursor: none;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .newsletter-form button:hover { transform: scale(1.04); box-shadow: 0 8px 24px rgba(232,74,12,0.3); }

    /* FOOTER */
    footer {
      background: var(--deep);
      color: var(--cream);
      padding: 80px 6vw 40px;
    }
    .footer-grid {
      display: grid;
      grid-template-columns: 2fr 1fr 1fr 1fr;
      gap: 60px;
      margin-bottom: 60px;
    }
    .footer-brand .logo { color: var(--cream); display: block; margin-bottom: 16px; }
    .footer-desc { font-size: 0.88rem; opacity: 0.5; line-height: 1.7; margin-bottom: 28px; max-width: 280px; }
    .social-links { display: flex; gap: 12px; }
    .social-btn {
      width: 40px; height: 40px;
      border-radius: 50%;
      border: 1px solid rgba(255,255,255,0.15);
      display: flex; align-items: center; justify-content: center;
      font-size: 0.9rem;
      text-decoration: none;
      transition: background 0.2s, border-color 0.2s;
    }
    .social-btn:hover { background: var(--ember); border-color: var(--ember); }
    .footer-col h4 {
      font-family: 'Syne', sans-serif;
      font-size: 0.72rem;
      font-weight: 700;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--gold);
      margin-bottom: 20px;
    }
    .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
    .footer-col a {
      font-size: 0.88rem;
      color: rgba(255,255,255,0.5);
      text-decoration: none;
      transition: color 0.2s, opacity 0.2s;
    }
    .footer-col a:hover { color: var(--cream); }
    .footer-bottom {
      border-top: 1px solid rgba(255,255,255,0.07);
      padding-top: 28px;
      display: flex; align-items: center; justify-content: space-between;
    }
    .footer-bottom p { font-size: 0.8rem; opacity: 0.35; }
    .footer-bottom a { color: var(--gold); text-decoration: none; }

    /* SCROLL ANIM */
    .reveal {
      opacity: 0;
      transform: translateY(32px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .reveal.visible { opacity: 1; transform: translateY(0); }

    @media (max-width: 900px) {
      .hero { grid-template-columns: 1fr; text-align: center; padding-top: 120px; }
      .hero-right { display: none; }
      .hero-actions { justify-content: center; }
      .hero-stats { justify-content: center; }
      .hero-sub { margin: 0 auto 44px; }
      .menu-grid { grid-template-columns: 1fr 1fr; }
      .why-grid { grid-template-columns: 1fr; }
      .why-visual { display: none; }
      .testi-grid { grid-template-columns: 1fr; }
      .footer-grid { grid-template-columns: 1fr 1fr; gap: 40px; }
      .nav-links { display: none; }
    }
    @media (max-width: 600px) {
      .menu-grid { grid-template-columns: 1fr; }
      .footer-grid { grid-template-columns: 1fr; }
      .newsletter-form { flex-direction: column; border-radius: 20px; padding: 16px; }
      .newsletter-form button { border-radius: 14px; }
    }
  </style>
</head>
<body>

  <!-- CURSOR -->
  <div class="cursor" id="cursor"></div>
  <div class="cursor-ring" id="cursorRing"></div>

  <!-- NAV -->
  <nav id="navbar">
    <a href="#" class="logo">Food<span>Munch</span></a>
    <ul class="nav-links">
      <li><a href="#menu">Menu</a></li>
      <li><a href="#why">Why Us</a></li>
      <li><a href="#reviews">Reviews</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <button class="nav-cta">Order Now</button>
  </nav>

  <!-- HERO -->
  <section class="hero">
    <div class="hero-bg-circle"></div>
    <div class="hero-noise"></div>
    <div class="hero-left">
      <div class="hero-tag">🔥 Freshly Made Daily</div>
      <h1 class="hero-title">
        Bold Flavours.<br><em>Unforgettable</em><br>Moments.
      </h1>
      <p class="hero-sub">
        From sizzling street bites to decadent desserts — FoodMunch delivers joy on every plate. Real ingredients. Real passion. No compromises.
      </p>
      <div class="hero-actions">
        <button class="btn-primary"><span>Explore Menu</span></button>
        <a href="#why" class="btn-outline">Our Story</a>
      </div>
      <div class="hero-stats">
        <div>
          <div class="stat-num">200+</div>
          <div class="stat-label">Dishes</div>
        </div>
        <div>
          <div class="stat-num">4.9★</div>
          <div class="stat-label">Rating</div>
        </div>
        <div>
          <div class="stat-num">50k+</div>
          <div class="stat-label">Happy Munchers</div>
        </div>
      </div>
    </div>
    <div class="hero-right">
      <div class="hero-plate">
        <div class="plate-ring"></div>
        <div class="plate-ring-2"></div>
        <div class="plate-circle"></div>
        <div class="food-orbits">
          <div class="orbit-item">🌮</div>
          <div class="orbit-item">🍜</div>
          <div class="orbit-item">🍰</div>
          <div class="orbit-item">🥗</div>
        </div>
        <div class="food-emoji-main">🍔</div>
        <div class="hero-badge">
          <div class="badge-icon">⚡</div>
          <div>
            <div class="badge-text-top">Delivery</div>
            <div class="badge-text-main">30 min or free</div>
          </div>
        </div>
        <div class="hero-badge-2">
          <div class="badge-icon">🏆</div>
          <div>
            <div class="badge-text-top">Best of 2025</div>
            <div class="badge-text-main">Food Awards</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- MARQUEE -->
  <div class="marquee-section">
    <div class="marquee-track">
      <span class="marquee-item"><span class="marquee-dot">✦</span> Handcrafted Recipes</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> Farm Fresh Ingredients</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> Free Delivery Over ₹499</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> 200+ Menu Items</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> Live Order Tracking</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> 30-Minute Guarantee</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> Handcrafted Recipes</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> Farm Fresh Ingredients</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> Free Delivery Over ₹499</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> 200+ Menu Items</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> Live Order Tracking</span>
      <span class="marquee-item"><span class="marquee-dot">✦</span> 30-Minute Guarantee</span>
    </div>
  </div>

  <!-- MENU -->
  <section class="menu-section" id="menu">
    <div class="section-label">Our Specialties</div>
    <h2 class="section-title">Dishes that make you <em>come back</em></h2>
    <div class="menu-filter">
      <button class="filter-btn active">All</button>
      <button class="filter-btn">🍔 Burgers</button>
      <button class="filter-btn">🍕 Pizza</button>
      <button class="filter-btn">🌮 Tacos</button>
      <button class="filter-btn">🍜 Noodles</button>
      <button class="filter-btn">🍰 Desserts</button>
    </div>
    <div class="menu-grid">
      <div class="menu-card featured reveal">
        <div class="card-img">
          🍔
          <div class="card-badge">🔥 Chef's Pick</div>
        </div>
        <div class="card-body">
          <div class="card-category">Signature</div>
          <div class="card-stars">★★★★★</div>
          <div class="card-name">The Munch Classic</div>
          <div class="card-desc">Double smash patty, secret sauce, caramelised onions & aged cheddar on a brioche bun.</div>
          <div class="card-footer">
            <div class="card-price">₹349</div>
            <button class="add-btn">+</button>
          </div>
        </div>
      </div>
      <div class="menu-card reveal">
        <div class="card-img">🍕</div>
        <div class="card-body">
          <div class="card-category">Pizza</div>
          <div class="card-stars">★★★★★</div>
          <div class="card-name">Fire & Basil Margherita</div>
          <div class="card-desc">Wood-fired crust, San Marzano tomatoes, buffalo mozzarella, fresh basil.</div>
          <div class="card-footer">
            <div class="card-price">₹449</div>
            <button class="add-btn">+</button>
          </div>
        </div>
      </div>
      <div class="menu-card reveal">
        <div class="card-img">
          🌮
          <div class="card-badge">New</div>
        </div>
        <div class="card-body">
          <div class="card-category">Street</div>
          <div class="card-stars">★★★★☆</div>
          <div class="card-name">Smoky BBQ Tacos</div>
          <div class="card-desc">Pulled jackfruit or chicken, chipotle crema, pickled jalapeños, lime slaw.</div>
          <div class="card-footer">
            <div class="card-price">₹279</div>
            <button class="add-btn">+</button>
          </div>
        </div>
      </div>
      <div class="menu-card reveal">
        <div class="card-img">🍜</div>
        <div class="card-body">
          <div class="card-category">Noodles</div>
          <div class="card-stars">★★★★★</div>
          <div class="card-name">Spicy Miso Ramen</div>
          <div class="card-desc">Rich pork or veg broth, soft-boiled egg, nori, spring onions, chilli oil.</div>
          <div class="card-footer">
            <div class="card-price">₹389</div>
            <button class="add-btn">+</button>
          </div>
        </div>
      </div>
      <div class="menu-card reveal">
        <div class="card-img">🥗</div>
        <div class="card-body">
          <div class="card-category">Healthy</div>
          <div class="card-stars">★★★★☆</div>
          <div class="card-name">Mediterranean Bowl</div>
          <div class="card-desc">Quinoa, roasted veggies, feta, olives, hummus & tahini drizzle.</div>
          <div class="card-footer">
            <div class="card-price">₹329</div>
            <button class="add-btn">+</button>
          </div>
        </div>
      </div>
      <div class="menu-card reveal">
        <div class="card-img">
          🍰
          <div class="card-badge">🍫 Sweet</div>
        </div>
        <div class="card-body">
          <div class="card-category">Dessert</div>
          <div class="card-stars">★★★★★</div>
          <div class="card-name">Molten Choco Lava</div>
          <div class="card-desc">Warm dark chocolate cake, liquid centre, vanilla bean gelato, gold dust.</div>
          <div class="card-footer">
            <div class="card-price">₹219</div>
            <button class="add-btn">+</button>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- WHY US -->
  <section class="why-section" id="why">
    <div class="why-bg"></div>
    <div class="section-label">Why FoodMunch</div>
    <h2 class="section-title" style="max-width:460px;">Every bite tells a <em>story</em></h2>
    <div class="why-grid">
      <div class="why-features reveal">
        <div class="why-feat">
          <div class="feat-icon">🌿</div>
          <div>
            <div class="feat-title">100% Fresh Sourcing</div>
            <div class="feat-desc">Partnered with 40+ local farms. Every ingredient arrives within 24 hours of harvest — no frozen shortcuts, ever.</div>
          </div>
        </div>
        <div class="why-feat">
          <div class="feat-icon">👨‍🍳</div>
          <div>
            <div class="feat-title">Master Chefs</div>
            <div class="feat-desc">Our culinary team brings 60+ years of combined experience across Michelin-starred kitchens and beloved street stalls.</div>
          </div>
        </div>
        <div class="why-feat">
          <div class="feat-icon">⚡</div>
          <div>
            <div class="feat-title">Lightning Delivery</div>
            <div class="feat-desc">30 minutes or your next order is free. Real-time GPS tracking so you know exactly when to set the table.</div>
          </div>
        </div>
        <div class="why-feat">
          <div class="feat-icon">♻️</div>
          <div>
            <div class="feat-title">Zero Waste Packaging</div>
            <div class="feat-desc">100% compostable containers. Because great food shouldn't cost the planet anything extra.</div>
          </div>
        </div>
      </div>
      <div class="why-visual reveal">
        <div class="floating-chips">
          <div class="chip">🌱 Organic Certified</div>
          <div class="chip">⭐ 4.9 / 5 Average</div>
          <div class="chip">🚀 30-min Delivery</div>
        </div>
        <div class="why-card-big">
          <span class="big-emoji">🍽️</span>
          <h3>Made with Love</h3>
          <p>From prep to plating, every dish gets the attention it deserves. No rush, no compromise.</p>
          <div class="why-rating">
            <div class="stars-big">★★★★★</div>
            <div>
              <div class="rating-num">4.9</div>
              <div class="rating-label">50,000+ reviews</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- TESTIMONIALS -->
  <section class="testimonials-section" id="reviews">
    <div class="section-label">Happy Munchers</div>
    <h2 class="section-title">People <em>love</em> us</h2>
    <div class="testi-grid">
      <div class="testi-card highlight reveal">
        <div class="testi-stars">★★★★★</div>
        <p class="testi-text">"The Munch Classic burger is genuinely life-changing. I've tried everything in the city and nothing even comes close. This is my weekly ritual now."</p>
        <div class="testi-author">
          <div class="testi-avatar">😋</div>
          <div>
            <div class="testi-name">Priya Menon</div>
            <div class="testi-role" style="color:rgba(255,255,255,0.6);">Food Blogger, Hyderabad</div>
          </div>
        </div>
      </div>
      <div class="testi-card reveal">
        <div class="testi-stars">★★★★★</div>
        <p class="testi-text">"Ordered at 11pm, delivered in 28 minutes — piping hot. The packaging was fully compostable too. This is the future of food delivery."</p>
        <div class="testi-author">
          <div class="testi-avatar">🧑‍💻</div>
          <div>
            <div class="testi-name">Arjun Sharma</div>
            <div class="testi-role">Software Engineer</div>
          </div>
        </div>
      </div>
      <div class="testi-card reveal">
        <div class="testi-stars">★★★★★</div>
        <p class="testi-text">"As someone who eats out 5 days a week, finding FoodMunch was a revelation. The Mediterranean Bowl is my daily lunch and I never get bored."</p>
        <div class="testi-author">
          <div class="testi-avatar">👩‍⚕️</div>
          <div>
            <div class="testi-name">Dr. Sneha Reddy</div>
            <div class="testi-role">Nutritionist</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- NEWSLETTER -->
  <section class="newsletter-section" id="contact">
    <div class="newsletter-inner reveal">
      <div class="section-label" style="text-align:center;">Stay in the Loop</div>
      <h2 class="section-title">Get exclusive <em>deals</em> & new drops</h2>
      <p class="newsletter-sub">Join 20,000+ food lovers who get early access to new dishes, flash sales & chef's specials. No spam — just good food news.</p>
      <div class="newsletter-form">
        <input type="email" placeholder="your@email.com" />
        <button>Subscribe</button>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="footer-grid">
      <div class="footer-brand">
        <a href="#" class="logo">Food<span>Munch</span></a>
        <p class="footer-desc">Serving joy since 2022. From Hyderabad to everywhere — real food, real fast, real good.</p>
        <div class="social-links">
          <a href="#" class="social-btn">𝕏</a>
          <a href="#" class="social-btn">📸</a>
          <a href="#" class="social-btn">in</a>
          <a href="#" class="social-btn">▶</a>
        </div>
      </div>
      <div class="footer-col">
        <h4>Menu</h4>
        <ul>
          <li><a href="#">Burgers</a></li>
          <li><a href="#">Pizza</a></li>
          <li><a href="#">Noodles</a></li>
          <li><a href="#">Salads</a></li>
          <li><a href="#">Desserts</a></li>
          <li><a href="#">Beverages</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Company</h4>
        <ul>
          <li><a href="#">About Us</a></li>
          <li><a href="#">Our Chefs</a></li>
          <li><a href="#">Sustainability</a></li>
          <li><a href="#">Careers</a></li>
          <li><a href="#">Press</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Help</h4>
        <ul>
          <li><a href="#">Track Order</a></li>
          <li><a href="#">FAQ</a></li>
          <li><a href="#">Contact</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Terms</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2025 FoodMunch. All rights reserved. Made with ❤️ in Hyderabad.</p>
      <p>Built by <a href="#">@yourgithub</a></p>
    </div>
  </footer>

  <script>
    // CURSOR
    const cursor = document.getElementById('cursor');
    const ring = document.getElementById('cursorRing');
    let mx = 0, my = 0, rx = 0, ry = 0;
    document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; cursor.style.left = mx+'px'; cursor.style.top = my+'px'; });
    function animRing() {
      rx += (mx - rx) * 0.12;
      ry += (my - ry) * 0.12;
      ring.style.left = rx+'px';
      ring.style.top = ry+'px';
      requestAnimationFrame(animRing);
    }
    animRing();
    document.querySelectorAll('a,button,.menu-card,.testi-card,.why-feat').forEach(el => {
      el.addEventListener('mouseenter', () => { cursor.style.width='20px'; cursor.style.height='20px'; ring.style.width='60px'; ring.style.height='60px'; ring.style.opacity='0.3'; });
      el.addEventListener('mouseleave', () => { cursor.style.width='12px'; cursor.style.height='12px'; ring.style.width='36px'; ring.style.height='36px'; ring.style.opacity='0.6'; });
    });

    // NAV SCROLL
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => { navbar.classList.toggle('scrolled', window.scrollY > 60); });

    // REVEAL ON SCROLL
    const reveals = document.querySelectorAll('.reveal');
    const obs = new IntersectionObserver((entries) => {
      entries.forEach((e, i) => {
        if (e.isIntersecting) {
          setTimeout(() => e.target.classList.add('visible'), i * 80);
        }
      });
    }, { threshold: 0.1 });
    reveals.forEach(r => obs.observe(r));

    // FILTER BUTTONS
    document.querySelectorAll('.filter-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
      });
    });

    // ADD TO CART BOUNCE
    document.querySelectorAll('.add-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        btn.style.transform = 'scale(1.4)';
        btn.textContent = '✓';
        setTimeout(() => { btn.style.transform = 'scale(1)'; btn.textContent = '+'; }, 600);
      });
    });
  </script>
</body>
</html>

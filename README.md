<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>AR Designing Studio</title>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300&family=Jost:wght@300;400;500;600&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --gold: #A8895A;
      --gold-light: #C9A96E;
      --black: #111111;
      --off-white: #F9F7F4;
      --mid: #666666;
      --border: #E0D8CE;
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Jost', sans-serif;
      background: var(--off-white);
      color: var(--black);
      font-weight: 300;
      overflow-x: hidden;
    }

    /* NAV */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 18px 60px;
      background: rgba(249,247,244,0.92);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
      transition: padding 0.3s;
    }
    .nav-logo { height: 48px; }
    .nav-links { display: flex; gap: 40px; list-style: none; }
    .nav-links a {
      font-family: 'Jost', sans-serif;
      font-size: 12px; font-weight: 500; letter-spacing: 0.18em;
      text-transform: uppercase; text-decoration: none;
      color: var(--black); transition: color 0.2s;
    }
    .nav-links a:hover { color: var(--gold); }
    .nav-cta {
      font-size: 11px; font-weight: 500; letter-spacing: 0.18em;
      text-transform: uppercase; text-decoration: none;
      padding: 10px 24px; border: 1px solid var(--gold);
      color: var(--gold); transition: all 0.25s;
    }
    .nav-cta:hover { background: var(--gold); color: white; }

    /* HERO */
    .hero {
      min-height: 100vh;
      display: flex; flex-direction: column; align-items: center; justify-content: center;
      padding: 120px 60px 80px;
      position: relative; overflow: hidden; text-align: center;
    }
    .hero::before {
      content: '';
      position: absolute; inset: 0;
      background: radial-gradient(ellipse 70% 60% at 50% 40%, rgba(168,137,90,0.07) 0%, transparent 70%);
      pointer-events: none;
    }
    .hero-logo {
      width: min(320px, 60vw);
      margin-bottom: 40px;
      animation: fadeUp 1s ease both;
    }
    .hero-tagline {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(32px, 5vw, 64px);
      font-weight: 300; font-style: italic;
      letter-spacing: 0.02em; line-height: 1.2;
      color: var(--black);
      animation: fadeUp 1s 0.2s ease both;
    }
    .hero-tagline span { color: var(--gold); }
    .hero-sub {
      margin-top: 20px;
      font-size: 13px; font-weight: 400; letter-spacing: 0.2em;
      text-transform: uppercase; color: var(--mid);
      animation: fadeUp 1s 0.35s ease both;
    }
    .hero-actions {
      margin-top: 50px; display: flex; gap: 20px; flex-wrap: wrap; justify-content: center;
      animation: fadeUp 1s 0.5s ease both;
    }
    .btn-primary {
      padding: 14px 40px; background: var(--gold); color: white;
      font-size: 11px; font-weight: 500; letter-spacing: 0.2em;
      text-transform: uppercase; text-decoration: none;
      border: 1px solid var(--gold); transition: all 0.3s;
    }
    .btn-primary:hover { background: #8a6f44; border-color: #8a6f44; }
    .btn-outline {
      padding: 14px 40px; background: transparent; color: var(--black);
      font-size: 11px; font-weight: 500; letter-spacing: 0.2em;
      text-transform: uppercase; text-decoration: none;
      border: 1px solid var(--black); transition: all 0.3s;
    }
    .btn-outline:hover { background: var(--black); color: white; }
    .scroll-hint {
      position: absolute; bottom: 36px; left: 50%; transform: translateX(-50%);
      display: flex; flex-direction: column; align-items: center; gap: 8px;
      font-size: 10px; letter-spacing: 0.2em; text-transform: uppercase; color: var(--mid);
      animation: fadeUp 1s 0.8s ease both;
    }
    .scroll-line {
      width: 1px; height: 40px; background: linear-gradient(to bottom, var(--gold), transparent);
      animation: scrollPulse 2s infinite;
    }

    /* DIVIDER */
    .gold-rule {
      display: flex; align-items: center; gap: 16px;
      margin: 0 auto 60px; max-width: 200px;
    }
    .gold-rule::before, .gold-rule::after {
      content: ''; flex: 1; height: 1px; background: var(--gold-light);
    }
    .gold-rule-icon { color: var(--gold); font-size: 16px; }

    /* SECTIONS */
    section { padding: 100px 60px; }

    .section-label {
      font-size: 10px; font-weight: 500; letter-spacing: 0.3em;
      text-transform: uppercase; color: var(--gold); margin-bottom: 16px;
    }
    .section-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(30px, 4vw, 52px);
      font-weight: 300; line-height: 1.15;
    }
    .section-body {
      font-size: 15px; line-height: 1.85; color: #555; max-width: 560px; margin-top: 20px;
    }

    /* ABOUT */
    .about {
      background: white;
      display: grid; grid-template-columns: 1fr 1fr; gap: 80px;
      align-items: center;
    }
    .about-visual {
      position: relative; aspect-ratio: 4/5;
      background: linear-gradient(135deg, #f0ebe3 0%, #e6ddd0 100%);
      overflow: hidden;
    }
    .about-visual::after {
      content: '';
      position: absolute; inset: 0;
      background: linear-gradient(135deg, transparent 60%, rgba(168,137,90,0.15));
    }
    .about-grid-lines {
      position: absolute; inset: 0;
      background-image: 
        linear-gradient(rgba(168,137,90,0.12) 1px, transparent 1px),
        linear-gradient(90deg, rgba(168,137,90,0.12) 1px, transparent 1px);
      background-size: 40px 40px;
    }
    .about-arch {
      position: absolute; bottom: 0; left: 50%; transform: translateX(-50%);
      width: 160px; height: 220px;
      border: 2px solid rgba(168,137,90,0.4);
      border-bottom: none;
      border-radius: 80px 80px 0 0;
    }

    /* SERVICES */
    .services { background: var(--off-white); }
    .services-header { text-align: center; margin-bottom: 70px; }
    .services-header .section-body { margin: 20px auto 0; text-align: center; }
    .services-grid {
      display: grid; grid-template-columns: repeat(3, 1fr); gap: 2px;
      max-width: 1100px; margin: 0 auto;
    }
    .service-card {
      background: white; padding: 50px 36px;
      position: relative; overflow: hidden;
      transition: transform 0.3s, box-shadow 0.3s;
    }
    .service-card:hover { transform: translateY(-6px); box-shadow: 0 24px 60px rgba(0,0,0,0.08); }
    .service-card::before {
      content: ''; position: absolute; top: 0; left: 0;
      width: 3px; height: 0; background: var(--gold);
      transition: height 0.4s ease;
    }
    .service-card:hover::before { height: 100%; }
    .service-num {
      font-family: 'Cormorant Garamond', serif;
      font-size: 48px; font-weight: 300; color: var(--border);
      line-height: 1; margin-bottom: 24px;
    }
    .service-name {
      font-family: 'Cormorant Garamond', serif;
      font-size: 22px; font-weight: 600; margin-bottom: 14px;
    }
    .service-desc { font-size: 13px; line-height: 1.8; color: var(--mid); }

    /* PROCESS */
    .process { background: var(--black); color: white; }
    .process .section-title { color: white; }
    .process .section-body { color: #aaa; }
    .process-steps {
      display: grid; grid-template-columns: repeat(4, 1fr); gap: 0;
      margin-top: 60px; border-top: 1px solid #333;
    }
    .process-step { padding: 40px 30px; border-right: 1px solid #333; }
    .process-step:last-child { border-right: none; }
    .step-num {
      font-family: 'Cormorant Garamond', serif;
      font-size: 60px; font-weight: 300;
      color: var(--gold); opacity: 0.4; line-height: 1;
    }
    .step-title {
      font-size: 13px; font-weight: 500; letter-spacing: 0.15em;
      text-transform: uppercase; margin: 16px 0 12px;
    }
    .step-desc { font-size: 13px; line-height: 1.75; color: #888; }

    /* CONTACT */
    .contact {
      background: white;
      display: grid; grid-template-columns: 1fr 1fr; gap: 80px;
      align-items: start;
    }
    .contact-info { padding-top: 8px; }
    .contact-detail {
      display: flex; align-items: flex-start; gap: 16px;
      margin-top: 36px; padding-top: 36px;
      border-top: 1px solid var(--border);
    }
    .contact-detail:first-of-type { margin-top: 40px; }
    .contact-icon { font-size: 18px; color: var(--gold); margin-top: 2px; }
    .contact-label {
      font-size: 10px; letter-spacing: 0.25em; text-transform: uppercase;
      color: var(--mid); margin-bottom: 6px;
    }
    .contact-value { font-size: 15px; font-weight: 400; }
    .contact-value a { color: var(--black); text-decoration: none; }
    .contact-value a:hover { color: var(--gold); }

    /* FORM */
    .contact-form { display: flex; flex-direction: column; gap: 20px; }
    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
    .form-group { display: flex; flex-direction: column; gap: 8px; }
    .form-group label {
      font-size: 10px; letter-spacing: 0.2em; text-transform: uppercase; color: var(--mid);
    }
    .form-group input, .form-group textarea, .form-group select {
      padding: 14px 18px;
      border: 1px solid var(--border);
      background: var(--off-white);
      font-family: 'Jost', sans-serif; font-size: 14px; font-weight: 300;
      color: var(--black); outline: none;
      transition: border-color 0.2s;
      -webkit-appearance: none;
    }
    .form-group input:focus, .form-group textarea:focus, .form-group select:focus {
      border-color: var(--gold);
    }
    .form-group textarea { resize: vertical; min-height: 120px; }
    .form-submit {
      display: inline-flex; align-items: center; gap: 12px;
      padding: 16px 44px; background: var(--gold); color: white;
      font-family: 'Jost', sans-serif; font-size: 11px; font-weight: 500;
      letter-spacing: 0.2em; text-transform: uppercase;
      border: none; cursor: pointer; transition: background 0.3s;
      align-self: flex-start;
    }
    .form-submit:hover { background: #8a6f44; }
    .form-success {
      display: none; padding: 16px 20px;
      background: #f0ede6; border-left: 3px solid var(--gold);
      font-size: 13px; color: var(--black); letter-spacing: 0.05em;
    }

    /* FOOTER */
    footer {
      background: var(--black); color: white;
      padding: 60px; text-align: center;
    }
    .footer-logo { height: 60px; filter: brightness(0) invert(1); margin-bottom: 28px; opacity: 0.85; }
    .footer-tagline {
      font-family: 'Cormorant Garamond', serif;
      font-size: 16px; font-style: italic; color: #888; margin-bottom: 32px;
    }
    .footer-links { display: flex; justify-content: center; gap: 36px; margin-bottom: 36px; flex-wrap: wrap; }
    .footer-links a {
      font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
      color: #666; text-decoration: none; transition: color 0.2s;
    }
    .footer-links a:hover { color: var(--gold); }
    .footer-rule { width: 60px; height: 1px; background: #333; margin: 0 auto 24px; }
    .footer-copy { font-size: 11px; color: #555; letter-spacing: 0.08em; }

    /* ANIMATIONS */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes scrollPulse {
      0%, 100% { opacity: 1; } 50% { opacity: 0.3; }
    }

    .reveal {
      opacity: 0; transform: translateY(30px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .reveal.visible { opacity: 1; transform: none; }

    /* MOBILE */
    @media (max-width: 900px) {
      nav { padding: 16px 24px; }
      .nav-links { display: none; }
      section { padding: 70px 24px; }
      .about { grid-template-columns: 1fr; gap: 40px; }
      .about-visual { aspect-ratio: 16/9; }
      .services-grid { grid-template-columns: 1fr; gap: 2px; }
      .process-steps { grid-template-columns: 1fr 1fr; }
      .process-step { border-right: none; border-bottom: 1px solid #333; }
      .contact { grid-template-columns: 1fr; gap: 50px; }
      .form-row { grid-template-columns: 1fr; }
      footer { padding: 50px 24px; }
    }
  </style>
</head>
<body>

<!-- NAV -->
<nav>
  <img class="nav-logo" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABOYAAATmCAIAAAAKnjl9AABxn2NhQlgAAHGfanVtYgAAAB5qdW1kYzJwYQARABCAAACqADibcQNjMnBhAAAAcXlqdW1iAAAAR2p1bWRjMm1hABEAEIAAAKoAOJtxA3VybjpjMnBhOjI1NjZkMjZlLTlmODEtNDQ2YS04MzkyLTRjODY1MWU2ZWE3OAAAACFVanVtYgAAAClqdW1kYzJhcwARABCAAACqADibcQNjMnBhLmFzc2VydGlvbnMAAAAJ0Wp1bWIAAAA7anVtZEDLDDK7ikidpwsq1vR/Q2kTYzJwYS5pY29uAAAAABhjMnNofkJPk7gP+LBQ0Ij+3LFGxgAAABdiZmRiAGltYWdlL3N2Zyt4bWwAAAAJd2JpZGI8c3ZnIHdpZHRoPSI3MTYiIGhlaWdodD0iNzE2IiB2aWV3Qm94PSIwIDAgNzE2IDcxNiIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTUwOC43NDkgMzE3LjM5OUM1MTYuNzc3IDI4Ny4zMTQgNTA4Ljk5MSAyNTMuODg0IDQ4NS4zODkgMjMwLjI4MkM0NjEuNzg4IDIwNi42ODEgNDI4LjM2IDE5OC44OTUgMzk4LjI3MyAyMDYuOTIzQzM3Ni4yMzEgMTg0LjkyOCAzNDMuMzkgMTc0Ljk1NiAzMTEuMTQ4IDE4My41OTZDMjc4LjkwNiAxOTIuMjM0IDI1NS40NSAyMTcuMjkyIDI0Ny4zNiAyNDcuMzYxQzIxNy4yOTEgMjU1LjQ1MSAxOTIuMjMzIDI3OC45MSAxODMuNTk1IDMxMS4xNDlDMTc0Ljk1NyAzNDMuMzkxIDE4NC45MjcgMzc2LjIzMiAyMDYuOTI0IDM5OC4yNzRDMTk4Ljg5NiA0MjguMzU5IDIwNi42ODMgNDYxLjc4OSAyMzAuMjg0IDQ4NS4zOTFDMjUzLjg4NSA1MDguOTkyIDI4Ny4zMTMgNTE2Ljc3OSAzMTcuNDAxIDUwOC43NUMzMzkuNDQyIDUzMC43NDUgMzcyLjI4NiA1NDAuNzE3IDQwNC41MjUgNTMyLjA3OUM0MzYuNzY3IDUyMy40NDEgNDYwLjIyMyA0OTguMzg0IDQ2OC4zMTMgNDY4LjMxNUM0OTguMzgzIDQ2MC4yMjQgNTIzLjQ0IDQzNi43NjYgNTMyLjA3OCA0MDQuNTI2QzU0MC43MTYgMzcyLjI4NSA1MzAuNzQ3IDMzOS40NDMgNTA4Ljc0OSAzMTcuNDAyVjMxNy4zOTlaTTQ3MC44OTkgMjQ0Ljc3NkM0ODYuODkyIDI2MC43NyA0OTMuNDg4IDI4Mi42MDEgNDkwLjY4NyAzMDMuNDEyTDQxNS41NzcgMjYwLjA0NkM0MTIuNDExIDI1OC4yMTggNDA4LjUwOSAyNTguMjE4IDQwNS4zNDUgMjYwLjA0NkwzMTcuNDAxIDMxMC44MlYyNzcuNTI2QzMxNy40MDEgMjc1LjE5MSAzMTguNjUyIDI3My4wMDUgMzIwLjY3NiAyNzEuODM3TDM4Ny42NDQgMjMzLjE3NEM0MTQuMTc4IDIxOC4zNTMgNDQ4LjM0NiAyMjIuMjIzIDQ3MC45MDEgMjQ0Ljc3Nkg0NzAuODk5Wk0zNTcuODM3IDMxMS4xNDRMMzk4LjI3NSAzMzQuNDkxVjM4MS4xODVMMzU3LjgzNyA0MDQuNTMyTDMxNy4zOTggMzgxLjE4NVYzMzQuNDkxTDM1Ny44MzcgMzExLjE0NFpNMjY0Ljc3NiAyNjkuNjkzQzI2NS4yMDcgMjM5LjMwNSAyODUuNjQ0IDIxMS42NDkgMzE2LjQ1MyAyMDMuMzkzQzMzOC4zIDE5Ny41NCAzNjAuNTA1IDIwMi43NDQgMzc3LjEyNyAyMTUuNTczTDMwMi4wMTQgMjU4LjkzN0MyOTguODQ4IDI2MC43NjQgMjk2Ljg5OCAyNjQuMTQ0IDI5Ni44OTggMjY3Ljc5OFYzNjkuMzQ2TDI2OC4wNjUgMzUyLjY5OUMyNjYuMDQzIDM1MS41MzEgMjY0Ljc3NiAzNDkuMzUzIDI2NC43NzYgMzQ3LjAxN1YyNjkuNjkxVjI2OS42OTNaTTIwMy4zOTEgMzE2LjQ1NEMyMDkuMjQ0IDI5NC42MDggMjI0Ljg1NCAyNzcuOTc4IDI0NC4yNzYgMjY5Ljk5OVYzNTYuNzNDMjQ0LjI3NiAzNjAuMzg0IDI0Ni4yMjYgMzYzLjc2MyAyNDkuMzkyIDM2NS41OTFMMzM3LjMzNyA0MTYuMzY1TDMwOC41MDMgNDMzLjAxM0MzMDYuNDgxIDQzNC4xODEgMzAzLjk2MSA0MzQuMTg4IDMwMS45MzkgNDMzLjAyTDIzNC45NzEgMzk0LjM1N0MyMDguODY4IDM3OC43ODkgMTk1LjEzOCAzNDcuMjYxIDIwMy4zOTEgMzE2LjQ1NFpNMjQ0Ljc3NSA0NzAuOUMyMjguNzgxIDQ1NC45MDYgMjIyLjE4NiA0MzMuMDc1IDIyNC45ODYgNDEyLjI2NEwzMDAuMDk2IDQ1NS42M0MzMDMuMjYzIDQ1Ny40NTcgMzA3LjE2NCA0NTcuNDU3IDMxMC4zMjggNDU1LjYzTDM5OC4yNzMgNDA0Ljg1NlY0MzguMTQ5QzM5OC4yNzMgNDQwLjQ4NSAzOTcuMDIyIDQ0Mi42NzEgMzk0Ljk5NyA0NDMuODM5TDMyOC4wMjkgNDgyLjUwMkMzMDEuNDk1IDQ5Ny4zMjIgMjY3LjMyNyA0OTMuNDUyIDI0NC43NzIgNDcwLjlIMjQ0Ljc3NVpNNDUwLjg5NyA0NDUuOTgyQzQ1MC40NjYgNDc2LjM3MSA0MzAuMDI5IDUwNC4wMjcgMzk5LjIyIDUxMi4yODNDMzc3LjM3MyA1MTguMTM2IDM1NS4xNjggNTEyLjkzMiAzMzguNTQ3IDUwMC4xMDJMNDEzLjY1OSA0NTYuNzM4QzQxNi44MjYgNDU0LjkxMSA0MTguNzc1IDQ1MS41MzIgNDE4Ljc3NSA0NDcuODc3VjM0Ni4zMjlMNDQ3LjYwOSAzNjIuOTc3QzQ0OS42MzEgMzY0LjE0NSA0NTAuODk3IDM2Ni4zMjMgNDUwLjg5NyAzNjguNjU5VjQ0NS45ODVWNDQ1Ljk4MlpNNTEyLjI4MiAzOTkuMjIxQzUwNi40MjkgNDIxLjA2OCA0OTAuODE5IDQzNy42OTcgNDcxLjM5NyA0NDUuNjc2VjM1OC45NDZDNDcxLjM5NyAzNTUuMjkyIDQ2OS40NDggMzUxLjkxMiA0NjYuMjgxIDM1MC4wODVMMzc4LjMzNiAyOTkuMzExTDQwNy4xNyAyODIuNjYzQzQwOS4xOTIgMjgxLjQ5NSA0MTEuNzEyIDI4MS40ODcgNDEzLjczNCAyODIuNjU1TDQ4MC43MDIgMzIxLjMxOEM1MDYuODA1IDMzNi44ODcgNTIwLjUzNiAzNjguNDE1IDUxMi4yODIgMzk5LjIyMVoiIGZpbGw9ImJsYWNrIi8+Cjwvc3ZnPgoAAAF+anVtYgAAAEFqdW1kY2JvcgARABCAAACqADibcRNjMnBhLmFjdGlvbnMudjIAAAAAGGMyc2j5NpPocancK9jMjo5lDrF5AAABNWNib3KhZ2FjdGlvbnODpGZhY3Rpb25sYzJwYS5jcmVhdGVkZHdoZW7AdDIwMjYtMDYtMThUMDA6MDA6MDBabXNvZnR3YXJlQWdlbnSiZG5hbWVpZ3B0LWltYWdlZ3ZlcnNpb25jMi4wcWRpZ2l0YWxTb3VyY2VUeXBleEZodHRwOi8vY3YuaXB0Yy5vcmcvbmV3c2NvZGVzL2RpZ2l0YWxzb3VyY2V0eXBlL3RyYWluZWRBbGdvcml0aG1pY01lZGlhomZhY3Rpb25uYzJwYS5jb252ZXJ0ZWRkd2hlbsB0MjAyNi0wNi0xOFQwMDowMDowMFqiZmFjdGlvbngYYzJwYS53YXRlcm1hcmtlZC51bmJvdW5kZHdoZW7AdDIwMjYtMDYtMThUMDA6MDA6MDBaAAAVEmp1bWIAAABJanVtZGNib3IAEQAQgAAAqgA4m3ETYzJwYS5jZXJ0aWZpY2F0ZS1zdGF0dXMAAAAAGGMyc2hoDOIpIpvruGPflOF59kpjAAAUwWNib3KhaG9jc3BWYWxzgnkKdE1JSUgwd29CQUtDQ0I4d3dnZ2ZJQmdrckJnRUZCUWN3QVFFRWdnZTVNSUlIdFRDQjZhSVdCQlE5cXFwNGp2cjJUUHBlYXRGQVRRN2xWUElmcmhnUE1qQXlOakEyTVRZeU1qTXpORE5hTUlHWU1JR1ZNRWt3Q1FZRkt3NERBaG9GQUFRVTM0STNVMTVUMkRPeDRBUTlKRFh4ZGViaENoa0VGRGs5RUVmY2w0K3ZpSHROY3hnZHplWHVwS1VxQWhBTHBmenBEbkNNOGdXQU1lNUVIR1J6Z0FBWUR6SXdNall3TmpFMk1qSXpNelF6V3FBUkdBOHlNREkyTURZeU16SXlNek0wTWxxaElqQWdNQjRHQ1NzR0FRVUZCekFCQmdRUkdBOHlNREUyTURZeE9ESXlNek0wTTFxaEl6QWhNQjhHQ1NzR0FRVUZCekFCQWdRU0JCQnJsRU1RR1JFT2Jidk95a0ZpeHhyMU1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQmdRQkR0NkJ0N3VwdjRpQncyZ1lmRjFMc3F5MWtOWDYwUkNHUDFuUWkwNkd1MmhDZ0h0dGk0OGhTYWpzQkdvVjFCUFNqUVRsTVlnWnlTd2UzaDAxQ1VaWHc5L2Q2SUpkeGpYRDFJbTNOZk4yYWZsZ2M2a3ZnY3dFbUNpdkZWTy9lekJxZ2YyVk12THFZNUxjN0hYT2w5SC92dC9DdlFPZ0loT0JDRXlPWkpiZHNJMkpaQVJCNnJMK0oxRm9IZlBXNHlPd1NwaTFSWnkwWGp1TVk3UGRuTlFxLzlUZURib2tpZGdRb3c3by9MSWpkUkUvT0hnS0lrMzlLbHhZOG40ZXpZRlJyd1ZmVlJ0VWZOY3V6eU1KTlNTSXpwOTlMcENiT2wzVUJTZVRUZDZpYURuU212WFpNZ0x4TFQvK3RmZmVXbjZ3MVR6TnhaV3hUZFF3dGNUT3UvTGVibDZlUFgzbXpibXBsYzRVRElGUGFHbHNra3ZDWnMyQ2phTE03eHZBRjgxM2ZEZm9pZG1uYUFLaVZjYU9lb2U0WllsZ3ZNbFZwSEF4U01PMXJ1R08rWTRVTzVnNmd5b3ZocE8xK0ViTGR6VVE3Q3dVWjBqRU9vb3B5Yi9CemN6RWZoeFdubGtDZyt6Z3Zsa25IQXVPN3FZWW1FZkxHckxWcEtRMkV4TlhYOURhZ2dnVXhNSUlGTFRDQ0JTa3dnZ01Sb0FNQ0FRSUNFRnBLc2ovUUtNYitTN00vYmozako3b3dEUVlKS29aSWh2Y05BUUVMQlFBd1NqRWhNQjhHQTFVRUF3d1lVMU5NTG1OdmJTQkRNbEJCSUVsRFFTQlNNU0F5TURJMU1SZ3dGZ1lEVlFRS0RBOVRVMHdnUTI5eWNHOXlZWFJwYjI0eEN6QUpCZ05WQkFZVEFsVlRNQjRYRFRJMk1ERXdNakl3TVRReE5Wb1hEVEkzTURFd01qSXdNVFF4TkZvd1RURUxNQWtHQTFVRUJoTUNWVk14RVRBUEJnTlZCQW9NQ0ZOVFRDQkRiM0p3TVNzd0tRWURWUVFERENKVFUwd3VZMjl0SUVNeVVFRWdTVU5CSUZJeElFOURVMUFnVW1WemNHOXVaR1Z5TUlJQm9qQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FZOEFNSUlCaWdLQ0FZRUFvbENUUWVaS1M5NExtNmFWZENaWVBPeFMvTHVVSFRMTkZNUEdVTi9Rdlp6R2JuQ0xJNWZYak83TUNIeFc3bWUrK1pyQWtyRHJ1cVV6LzIxcEZKQ0RMd2lJTFJYdHNFdGRIeXlidWJobEZ5Umo3aE93SkdDTkN1Z0YrSGtmeHROaE5WdU1CSmRZbjdPTVhOamt4cWJRUS9DenA5TlUyV3lJOXhpbnVNVFlidjB4S040T0NTNlFKL1Z6MlhlbTFWQ2FJTm04eXpMRlJybjhvbFVGVGU2Z202eG9hc0ViUHpncWVnYlkwMTI2dExNZTY1MVZLZTdzMGpjVW42N0ZOcW1jc0xmZVJDcUw2RkNuRVNBSWdBdDVleVhQMlRueW5rV2JkN29IZUFtZ3BrNTdRSTR4L2VvaWFJY1ZnTVNDSWVSUFd2SVI4NGdQcEV1SktuNU1KQUVtcWFDYUJNbWRmQVh1YTJLRklqSUI3dGJjSzlMZjFrWTBkcUNDS0hpT3ZpcmREaFRrMW1vcWQ5dDBlalVucG9jV0Y4RzRIdkE2VTRHcW10WXJrNi9qSDV1M1pkSW1NRXFsSEE2K3l2R0xmMW8wQWFhaDBnRUloWEk0V0RuRTdENHlIUitFM3pjVWVkWXcwemNiZU9ib3paTHBiaXNOYnV3dzZ6STRMcWs4MGkzbEFnTUJBQUdqZ1ljd2dZUXdEQVlEVlIwVEFRSC9CQUl3QURBZkJnTlZIU01FR0RBV2dCUTVQUkJIM0plUHI0aDdUWE1ZSGMzbDdxU2xLakFQQmdrckJnRUZCUWN3QVFVRUFnVUFNQk1HQTFVZEpRUU1NQW9HQ0NzR0FRVUZCd01KTUIwR0ExVWREZ1FXQkJROXFxcDRqdnIyVFBwZWF0RkFUUTdsVlBJZnJqQU9CZ05WSFE4QkFmOEVCQU1DQjRBd0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dJQkFMdHpwbFdFbzJoUTZ4RHhvR3pYeVNtRW5UNm9MKzBLdXc2ZzY2dkx3UjY0QVlZRnR6QWxTRzN6RGVHOW9VMG8waXRsWUVUY3RvMnJWVC9YM1lVZS92Q1hXeVFzN0sxTEgwdjB1d242bnJEZ3NMRDlqa1J5dEk4TWF0MWo2T3V5MWd2VXgvSG5pdzdmMzJ6RUNhTDlQUjl6R3hGWXdTZ3BvbXRnYVRBcE8xVzBqS21rQ0pDcEVuQStibkxFZGh3d2FZSlBKYlJQVmM3cFNNOWZpd2QvemZCV2E5L2Nub1lmTnZBMWpzRTNsWE80N2JZWXFFUys5cGZlU1ErOGo2RStjaWZRUFNGOFVseFFxY2NWM0tuNzkyMndLZ2NtRUJTZ2xOOFZaSVdNcHoyS09qRUdkSkVoNFJqc1N0K0ZFV2pPWWFta2F6SXowMmpteWIrei9QK1Y4UnpYd2dWbFNteE9SLzZvWUpSM2FFSE9UaWhFcGNhWWg2ZzE4bzRHWnFva3ZXckJFcTRZSUd2ZWRLTjNKbVducGNJb0hTWDlQcW5sRkVt

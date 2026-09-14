
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FIREFORT · Дашборд — 3 слайда</title>
<style>
  :root {
    --red: #E53935;
    --red-dark: #B71C1C;
    --orange: #FF6F00;
    --orange-light: #FFA726;
    --orange-soft: #FFF3E0;
    --orange-line: #FFE0B2;
    --gray-bg: #F4F5F7;
    --gray-card: #FFFFFF;
    --gray-line: #E0E0E0;
    --gray-text: #4A4A4A;
    --gray-light: #9E9E9E;
    --green: #2E7D32;
    --green-light: #66BB6A;
    --blue: #1565C0;
    --blue-light: #42A5F5;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  html, body { height: 100%; }
  body {
    font-family: 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
    background: var(--gray-bg);
    color: var(--gray-text);
    line-height: 1.5;
    overflow: hidden;
  }

  .slider { position: relative; width: 100%; height: 100vh; overflow: hidden; }
  .slides { display: flex; height: 100%; transition: transform 0.45s cubic-bezier(0.65, 0, 0.35, 1); }
  .slide { flex: 0 0 100%; height: 100%; overflow-y: auto; padding: 24px; }
  .slide-inner { max-width: 1200px; margin: 0 auto; padding-bottom: 90px; }

  /* ==== НАВИГАЦИЯ ==== */
  .nav {
    position: fixed; bottom: 20px; left: 50%;
    transform: translateX(-50%);
    display: flex; align-items: center; gap: 14px;
    background: rgba(255,255,255,0.97);
    padding: 10px 20px; border-radius: 50px;
    box-shadow: 0 6px 24px rgba(0,0,0,0.15);
    z-index: 100; backdrop-filter: blur(8px);
    border: 1px solid var(--orange-line);
  }
  .nav-logo-ff {
    display: flex; align-items: center; gap: 6px;
    padding-right: 14px;
    border-right: 1px solid var(--orange-line);
    margin-right: 4px;
  }
  .nav-logo-ff svg { display: block; }
  .nav-logo-ff .nav-logo-text {
    font-size: 12px; font-weight: 900;
    color: var(--red-dark);
    letter-spacing: 1.2px;
  }
  .nav-btn {
    width: 42px; height: 42px; border-radius: 50%;
    border: none;
    background: linear-gradient(135deg, var(--red) 0%, var(--orange) 100%);
    color: #fff; font-size: 20px; font-weight: 800;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: transform 0.2s, box-shadow 0.2s;
    box-shadow: 0 3px 10px rgba(229,57,53,0.3);
  }
  .nav-btn:hover:not(:disabled) { transform: scale(1.08); box-shadow: 0 5px 16px rgba(229,57,53,0.45); }
  .nav-btn:disabled { opacity: 0.35; cursor: not-allowed; box-shadow: none; }
  .dots { display: flex; gap: 8px; align-items: center; }
  .dot-nav {
    width: 10px; height: 10px; border-radius: 50%;
    background: var(--orange-line); border: none;
    cursor: pointer; transition: all 0.25s; padding: 0;
  }
  .dot-nav.active {
    width: 28px; border-radius: 6px;
    background: linear-gradient(135deg, var(--red) 0%, var(--orange) 100%);
  }
  .slide-counter {
    font-size: 13px; font-weight: 800;
    color: var(--red-dark); min-width: 42px; text-align: center;
  }

  /* ==== ШАПКА ==== */
  header {
    background: linear-gradient(135deg, #B71C1C 0%, #E53935 55%, #FF6F00 130%);
    color: #fff; padding: 36px 40px;
    border-radius: 16px; margin-bottom: 24px;
    box-shadow: 0 10px 32px rgba(183,28,28,0.35);
    position: relative; overflow: hidden;
  }
  header::before {
    content: ""; position: absolute;
    top: -60px; right: -60px;
    width: 260px; height: 260px;
    background: radial-gradient(circle, rgba(255,255,255,0.14) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  header::after {
    content: ""; position: absolute;
    bottom: -80px; left: -40px;
    width: 200px; height: 200px;
    background: radial-gradient(circle, rgba(255,255,255,0.08) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  .header-grid {
    display: grid; grid-template-columns: 1.15fr 1fr;
    gap: 32px; align-items: center;
    position: relative; z-index: 1;
  }
  .header-left { display: flex; flex-direction: column; gap: 10px; }

  .brand-line {
    display: flex; align-items: center; gap: 14px;
    margin-bottom: 8px;
  }
  .brand-logo-ff {
    width: 62px; height: 62px;
    display: flex; align-items: center; justify-content: center;
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 4px 14px rgba(0,0,0,0.18);
    flex-shrink: 0;
  }
  .brand-logo-ff svg { display: block; }
  .brand-badge {
    display: inline-block;
    background: #fff; color: var(--red-dark);
    font-size: 20px; font-weight: 900;
    letter-spacing: 3px; padding: 8px 18px;
    border-radius: 8px;
    box-shadow: 0 4px 14px rgba(0,0,0,0.18);
  }
  header h1 { font-size: 30px; font-weight: 900; line-height: 1.15; letter-spacing: -0.5px; }
  .brand-sub { font-size: 14.5px; opacity: 0.95; line-height: 1.5; }
  .brand-sub b { font-weight: 800; }
  .brand-tagline {
    display: inline-block; margin-top: 8px;
    background: rgba(255,255,255,0.16);
    border-left: 4px solid #FFD54F;
    padding: 10px 16px; border-radius: 8px;
    font-size: 14.5px; font-weight: 600; align-self: flex-start;
  }
  .brand-tagline b { color: #FFD54F; font-weight: 900; }
  .header-right {
    display: flex; align-items: center; justify-content: flex-end;
    gap: 22px; background: rgba(0,0,0,0.18);
    border-radius: 14px; padding: 22px 26px;
    backdrop-filter: blur(2px);
  }
  .anchor { text-align: left; }
  .anchor-label {
    font-size: 11px; text-transform: uppercase;
    letter-spacing: 1.2px; font-weight: 700;
    opacity: 0.85; margin-bottom: 6px;
  }
  .anchor-value {
    font-size: 46px; font-weight: 900;
    line-height: 1; letter-spacing: -1.5px;
    color: #FFD54F; text-shadow: 0 3px 12px rgba(0,0,0,0.25);
  }
  .anchor-sub { font-size: 12px; opacity: 0.85; margin-top: 8px; }
  .anchor-divider { width: 1px; height: 70px; background: rgba(255,255,255,0.28); }

  /* ==== KPI ==== */
  .kpi-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 18px; margin-bottom: 24px;
  }
  .kpi {
    background: var(--gray-card);
    border-radius: 12px; padding: 22px 20px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.06);
    border-left: 5px solid var(--gray-line);
    transition: transform 0.2s, box-shadow 0.2s;
    position: relative; overflow: hidden;
  }
  .kpi::after {
    content: ""; position: absolute;
    top: 0; right: 0; width: 90px; height: 100%;
    background: linear-gradient(90deg, transparent 0%, rgba(255,111,0,0.05) 100%);
    pointer-events: none;
  }
  .kpi:hover { transform: translateY(-3px); box-shadow: 0 6px 20px rgba(0,0,0,0.1); }
  .kpi.red { border-left-color: var(--red); background: linear-gradient(135deg, #fff 60%, #FFF3E0 100%); }
  .kpi.green { border-left-color: var(--green); }
  .kpi.blue { border-left-color: var(--blue); background: linear-gradient(135deg, #fff 60%, #E3F2FD 100%); }
  .kpi.orange { border-left-color: var(--orange); background: linear-gradient(135deg, #fff 60%, var(--orange-soft) 100%); }
  .kpi .label { font-size: 12px; text-transform: uppercase; letter-spacing: 0.5px; color: var(--gray-light); margin-bottom: 8px; font-weight: 600; }
  .kpi .value { font-size: 30px; font-weight: 800; color: var(--gray-text); }
  .kpi .value.red { color: var(--red); }
  .kpi .value.green { color: var(--green); }
  .kpi .value.blue { color: var(--blue); }
  .kpi .value.orange { color: var(--orange); }
  .kpi .sub { font-size: 12px; color: var(--gray-light); margin-top: 6px; }

  /* ==== SECTIONS ==== */
  .section {
    background: var(--gray-card);
    border-radius: 12px; padding: 24px 28px;
    margin-bottom: 24px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.06);
    position: relative; overflow: hidden;
  }
  .section::before {
    content: ""; position: absolute;
    top: 0; left: 0; height: 4px; width: 100%;
    background: linear-gradient(90deg, var(--red) 0%, var(--orange) 50%, var(--orange-light) 100%);
    pointer-events: none;
  }
  .section h2 {
    font-size: 18px; font-weight: 700;
    color: var(--gray-text);
    margin-bottom: 18px; padding-bottom: 12px;
    border-bottom: 2px solid var(--orange-line);
    display: flex; align-items: center; gap: 10px;
  }
  .section h2 .dot {
    width: 10px; height: 10px; border-radius: 50%;
    background: linear-gradient(135deg, var(--red), var(--orange));
    display: inline-block;
  }

  /* ==== HERO ==== */
  .hero-benefit {
    background: linear-gradient(135deg, #FFF3E0 0%, #FFE0B2 55%, #FFCC80 100%);
    border: 3px solid var(--orange);
    border-radius: 14px; padding: 32px 36px;
    margin-bottom: 24px; text-align: center;
    position: relative; overflow: hidden;
  }
  .hero-benefit::before {
    content: ""; position: absolute;
    top: -50px; right: -50px;
    width: 200px; height: 200px;
    background: radial-gradient(circle, rgba(255,111,0,0.15) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  .hero-benefit .label {
    font-size: 14px; text-transform: uppercase;
    letter-spacing: 1px; color: var(--red-dark);
    font-weight: 700; margin-bottom: 10px;
  }
  .hero-benefit .big-number {
    font-size: 64px; font-weight: 900;
    background: linear-gradient(135deg, var(--red-dark) 0%, var(--red) 40%, var(--orange) 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    line-height: 1; margin-bottom: 10px;
  }
  .hero-benefit .sub { font-size: 17px; color: var(--gray-text); font-weight: 600; }
  .hero-benefit .desc {
    font-size: 14px; color: var(--gray-text);
    margin-top: 12px; max-width: 760px;
    margin-left: auto; margin-right: auto;
  }

  /* ==== TABLES ==== */
  table { width: 100%; border-collapse: collapse; font-size: 13.5px; }
  thead th {
    background: linear-gradient(135deg, var(--orange-soft) 0%, var(--orange-line) 100%);
    color: var(--gray-text); text-align: left;
    padding: 12px 14px; font-weight: 700; font-size: 12px;
    text-transform: uppercase; letter-spacing: 0.4px;
    border-bottom: 2px solid var(--orange-light);
  }
  tbody td { padding: 11px 14px; border-bottom: 1px solid var(--gray-line); }
  tbody tr:hover { background: var(--orange-soft); }
  .td-green { color: var(--green); font-weight: 700; }
  .td-red { color: var(--red); font-weight: 700; }
  .td-blue { color: var(--blue); font-weight: 700; }
  .td-orange { color: var(--orange); font-weight: 700; }
  .td-gray { color: var(--gray-light); }
  .tag {
    display: inline-block; padding: 3px 10px; border-radius: 20px;
    font-size: 11px; font-weight: 700;
  }
  .tag.green { background: #E8F5E9; color: var(--green); }
  .tag.red { background: #FFEBEE; color: var(--red); }
  .tag.blue { background: #E3F2FD; color: var(--blue); }
  .tag.orange { background: var(--orange-soft); color: var(--orange); }

  /* ==== ПЛАШКА СС / ЗАКУПКА ==== */
  .cost-banner {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 16px; margin-bottom: 20px; padding: 18px 20px;
    background: linear-gradient(135deg, #FFF3E0 0%, #FFE0B2 100%);
    border-radius: 12px;
    border-left: 5px solid var(--orange);
    position: relative; overflow: hidden;
  }
  .cost-banner::after {
    content: ""; position: absolute;
    top: -40px; right: -40px;
    width: 160px; height: 160px;
    background: radial-gradient(circle, rgba(229,57,53,0.10) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  .cost-banner .item { text-align: left; position: relative; z-index: 1; }
  .cost-banner .item .lbl {
    font-size: 11px; text-transform: uppercase;
    letter-spacing: 0.5px; color: var(--gray-text);
    font-weight: 700; margin-bottom: 6px;
  }
  .cost-banner .item .val { font-size: 24px; font-weight: 900; line-height: 1; }
  .cost-banner .item .val.blue { color: var(--blue); }
  .cost-banner .item .val.red { color: var(--red); }
  .cost-banner .item .val.green { color: var(--green); }
  .cost-banner .item .sub { font-size: 11.5px; color: var(--gray-light); margin-top: 6px; }

  /* ==== КОМПОНЕНТЫ ==== */
  .components-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-bottom: 24px;
  }
  .comp-card {
    background: linear-gradient(135deg, #FFFFFF 0%, #FAFAFA 100%);
    border-radius: 12px;
    padding: 20px 18px;
    border-left: 5px solid var(--orange);
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
    position: relative;
    overflow: hidden;
    transition: transform 0.2s, box-shadow 0.2s;
  }
  .comp-card:hover { transform: translateY(-3px); box-shadow: 0 6px 20px rgba(0,0,0,0.08); }
  .comp-card::after {
    content: ""; position: absolute;
    bottom: -30px; right: -30px;
    width: 100px; height: 100px;
    background: radial-gradient(circle, rgba(255,111,0,0.10) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  .comp-card:nth-child(1) { border-left-color: var(--orange); background: linear-gradient(135deg, #fff 55%, var(--orange-soft) 100%); }
  .comp-card:nth-child(2) { border-left-color: var(--red); background: linear-gradient(135deg, #fff 55%, #FFEBEE 100%); }
  .comp-card:nth-child(3) { border-left-color: var(--blue); background: linear-gradient(135deg, #fff 55%, #E3F2FD 100%); }
  .comp-card:nth-child(4) { border-left-color: var(--green); background: linear-gradient(135deg, #fff 55%, #E8F5E9 100%); }

  .comp-icon { font-size: 24px; line-height: 1; margin-bottom: 10px; position: relative; z-index: 1; }
  .comp-name {
    font-size: 13px; font-weight: 800;
    color: var(--gray-text);
    text-transform: uppercase;
    letter-spacing: 0.4px;
    margin-bottom: 4px;
    position: relative; z-index: 1;
  }
  .comp-supplier {
    font-size: 11.5px;
    color: var(--gray-light);
    margin-bottom: 12px;
    position: relative; z-index: 1;
  }
  .comp-price {
    font-size: 28px;
    font-weight: 900;
    line-height: 1;
    color: var(--orange);
    letter-spacing: -0.5px;
    position: relative; z-index: 1;
  }
  .comp-card:nth-child(2) .comp-price { color: var(--red); }
  .comp-card:nth-child(3) .comp-price { color: var(--blue); }
  .comp-card:nth-child(4) .comp-price { color: var(--green); }
  .comp-price .unit {
    font-size: 14px;
    font-weight: 700;
    color: var(--gray-light);
    margin-left: 4px;
  }
  .comp-share {
    margin-top: 10px;
    font-size: 11.5px;
    font-weight: 700;
    color: var(--gray-light);
    position: relative; z-index: 1;
  }
  .comp-share b { color: var(--gray-text); }

  .comp-total {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 18px 24px;
    background: linear-gradient(135deg, var(--red-dark) 0%, var(--red) 55%, var(--orange) 130%);
    border-radius: 12px;
    color: #fff;
    box-shadow: 0 6px 20px rgba(229,57,53,0.3);
    position: relative;
    overflow: hidden;
  }
  .comp-total::before {
    content: ""; position: absolute;
    top: -40px; right: -40px;
    width: 160px; height: 160px;
    background: radial-gradient(circle, rgba(255,255,255,0.12) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  .comp-total .lbl {
    font-size: 13px; font-weight: 700;
    letter-spacing: 1px;
    text-transform: uppercase;
    opacity: 0.95;
    position: relative; z-index: 1;
  }
  .comp-total .val {
    font-size: 32px;
    font-weight: 900;
    letter-spacing: -0.5px;
    color: #FFD54F;
    position: relative; z-index: 1;
  }

  /* ==== АРГУМЕНТЫ ==== */
  .arg-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; }
  .arg {
    padding: 24px 22px; border-radius: 12px;
    background: linear-gradient(135deg, #FFFFFF 0%, #FAFAFA 100%);
    border-left: 5px solid var(--blue);
    display: flex; flex-direction: column; gap: 10px;
    transition: transform 0.2s, box-shadow 0.2s;
    position: relative; overflow: hidden;
  }
  .arg::after {
    content: ""; position: absolute;
    bottom: -30px; right: -30px;
    width: 100px; height: 100px;
    background: radial-gradient(circle, rgba(255,111,0,0.08) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  .arg:hover { transform: translateY(-3px); box-shadow: 0 6px 20px rgba(0,0,0,0.08); }
  .arg:nth-child(3n+1) { border-left-color: var(--red); background: linear-gradient(135deg, #fff 55%, #FFEBEE 100%); }
  .arg:nth-child(3n+2) { border-left-color: var(--green); background: linear-gradient(135deg, #fff 55%, #E8F5E9 100%); }
  .arg:nth-child(3n+3) { border-left-color: var(--orange); background: linear-gradient(135deg, #fff 55%, var(--orange-soft) 100%); }
  .arg .arg-icon { font-size: 22px; line-height: 1; position: relative; z-index: 1; }
  .arg .arg-number {
    font-size: 34px; font-weight: 900;
    line-height: 1; color: var(--red);
    letter-spacing: -0.5px; position: relative; z-index: 1;
  }
  .arg:nth-child(3n+2) .arg-number { color: var(--green); }
  .arg:nth-child(3n+3) .arg-number { color: var(--orange); }
  .arg .arg-title { font-size: 14px; font-weight: 700; color: var(--gray-text); margin-top: 4px; position: relative; z-index: 1; }
  .arg .arg-desc { font-size: 12.5px; color: var(--gray-text); line-height: 1.5; position: relative; z-index: 1; }
  .arg .arg-desc b { color: var(--gray-text); font-weight: 800; }

  /* ==== ЗАГОЛОВОК СЛАЙДА ==== */
  .slide-title {
    display: flex; align-items: center; gap: 14px;
    margin-bottom: 18px; padding: 14px 22px;
    background: linear-gradient(135deg, #fff 0%, var(--orange-soft) 100%);
    border-radius: 12px;
    border-left: 5px solid var(--orange);
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
  }
  .slide-title .num {
    width: 40px; height: 40px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    background: linear-gradient(135deg, var(--red) 0%, var(--orange) 100%);
    color: #fff; font-weight: 900; font-size: 17px;
    box-shadow: 0 3px 10px rgba(229,57,53,0.3);
  }
  .slide-title .text {
    font-size: 20px; font-weight: 900;
    color: var(--red-dark); letter-spacing: -0.3px;
  }
  .slide-title .sub-text {
    font-size: 13px; color: var(--gray-light);
    margin-left: auto; font-weight: 600;
  }

  footer {
    text-align: center; font-size: 12px; color: var(--gray-light);
    padding: 20px 0 8px;
    display: flex; align-items: center; justify-content: center; gap: 12px;
    flex-wrap: wrap;
  }
  footer svg { display: block; opacity: 0.7; }

  /* ==== АДАПТИВ ==== */
  @media (max-width: 1000px) {
    .components-grid { grid-template-columns: repeat(2, 1fr); }
  }
  @media (max-width: 900px) {
    .header-grid { grid-template-columns: 1fr; gap: 22px; }
    .header-right { justify-content: flex-start; }
    .arg-grid { grid-template-columns: repeat(2, 1fr); }
    .cost-banner { grid-template-columns: 1fr; }
  }
  @media (max-width: 640px) {
    .slide { padding: 12px; }
    header { padding: 24px 20px; }
    header h1 { font-size: 22px; }
    .brand-logo-ff { width: 48px; height: 48px; }
    .brand-badge { font-size: 16px; letter-spacing: 2px; padding: 6px 14px; }
    .anchor-value { font-size: 34px; }
    .header-right { padding: 18px; gap: 16px; }
    .hero-benefit { padding: 22px 18px; }
    .hero-benefit .big-number { font-size: 42px; }
    .section { padding: 18px; }
    .kpi .value { font-size: 22px; }
    .arg-grid { grid-template-columns: 1fr; }
    .components-grid { grid-template-columns: 1fr; }
    .arg .arg-number { font-size: 28px; }
    .cost-banner .item .val { font-size: 20px; }
    .comp-total .val { font-size: 24px; }
    table { font-size: 12px; }
    thead th, tbody td { padding: 8px 8px; }
    .nav { bottom: 12px; padding: 8px 14px; gap: 10px; }
    .nav-btn { width: 36px; height: 36px; font-size: 16px; }
    .nav-logo-ff .nav-logo-text { display: none; }
  }
</style>
</head>
<body>

<div class="slider">
  <div class="slides" id="slides">

    <!-- ================= СЛАЙД 1: ЦЕННОСТЬ ================= -->
    <div class="slide">
      <div class="slide-inner">

        <header>
          <div class="header-grid">
            <div class="header-left">
              <div class="brand-line">
                <div class="brand-logo-ff">
                  <svg width="46" height="46" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg">
                    <defs>
                      <linearGradient id="shieldGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                        <stop offset="0%" stop-color="#B71C1C"/>
                        <stop offset="55%" stop-color="#E53935"/>
                        <stop offset="100%" stop-color="#FF6F00"/>
                      </linearGradient>
                      <linearGradient id="flameGrad" x1="50%" y1="100%" x2="50%" y2="0%">
                        <stop offset="0%" stop-color="#FFD54F"/>
                        <stop offset="50%" stop-color="#FFA726"/>
                        <stop offset="100%" stop-color="#FF6F00"/>
                      </linearGradient>
                    </defs>
                    <path d="M32 2 L58 12 L58 32 C58 46 46 56 32 62 C18 56 6 46 6 32 L6 12 Z" fill="url(#shieldGrad)"/>
                    <path d="M32 8 L52 16 L52 32 C52 43 42 51 32 56 C22 51 12 43 12 32 L12 16 Z" fill="#fff" opacity="0.12"/>
                    <path d="M32 18 C32 18 24 28 24 36 C24 41 27.5 45 32 45 C36.5 45 40 41 40 36 C40 32 38 29 36 26 C36 30 34 32 32 32 C32 32 34 26 32 18 Z" fill="url(#flameGrad)"/>
                    <circle cx="32" cy="37" r="3" fill="#fff" opacity="0.85"/>
                  </svg>
                </div>
                <div class="brand-badge">FIREFORT</div>
              </div>
              <h1>Огнестойкие распределительные коробки</h1>
              <p class="brand-sub">Серия <b>FIREFORT</b> · 11 артикулов · Корпус 100×100×50, оранжевый, IP54</p>
              <div class="brand-tagline">
                Собственная сборка · Себестоимость ниже в <b>2,4 раза</b>
              </div>
            </div>
            <div class="header-right">
              <div class="anchor">
                <div class="anchor-label">Цена для клиента</div>
                <div class="anchor-value">−20%</div>
                <div class="anchor-sub">от уровня ПроСистемс</div>
              </div>
              <div class="anchor-divider"></div>
              <div class="anchor">
                <div class="anchor-label">Маржинальность</div>
                <div class="anchor-value">58–72%</div>
                <div class="anchor-sub">на всех уровнях цены</div>
              </div>
            </div>
          </div>
        </header>

        <div class="hero-benefit">
          <div class="label">Главное конкурентное преимущество</div>
          <div class="big-number">−20%</div>
          <div class="sub">цена для клиента относительно уровня ПроСистемс</div>
          <div class="desc">
            Собственная сборка снижает себестоимость на <b>55%</b>. Это позволяет установить цену
            на <b>20% ниже рынка</b> и одновременно сохранить маржинальность <b>58–72%</b> — выгодно и клиенту, и компании.
          </div>
        </div>

        <div class="kpi-grid">
          <div class="kpi blue">
            <div class="label">Цена для клиента</div>
            <div class="value blue">−20%</div>
            <div class="sub">к уровню ПроСистемс</div>
          </div>
          <div class="kpi orange">
            <div class="label">Себестоимость ниже в</div>
            <div class="value orange">2,4 раза</div>
            <div class="sub">основа для гибкой цены</div>
          </div>
          <div class="kpi red">
            <div class="label">Маржинальность</div>
            <div class="value red">58–72%</div>
            <div class="sub">на всех уровнях цены</div>
          </div>
          <div class="kpi orange">
            <div class="label">Окупаемость вложений</div>
            <div class="value orange">~2 мес.</div>
            <div class="sub">старт 990 000 ₽</div>
          </div>
        </div>

        <div class="section" style="border: 2px solid var(--orange);">
          <h2 style="color:var(--red-dark);"><span class="dot"></span>Аргументы для отдела продаж</h2>
          <div class="arg-grid">

            <div class="arg">
              <div class="arg-icon">💰</div>
              <div class="arg-number">−20%</div>
              <div class="arg-title">Цена ниже рынка</div>
              <div class="arg-desc">Сильный аргумент в тендерах, проектных спецификациях и переговорах с дистрибьюторами.</div>
            </div>

            <div class="arg">
              <div class="arg-icon">📉</div>
              <div class="arg-number">2,4×</div>
              <div class="arg-title">Себестоимость ниже</div>
              <div class="arg-desc"><b>265,65 ₽</b> против <b>642,85 ₽</b> — основа для гибкой ценовой политики без потери прибыли.</div>
            </div>

            <div class="arg">
              <div class="arg-icon">📈</div>
              <div class="arg-number">58–72%</div>
              <div class="arg-title">Маржинальность</div>
              <div class="arg-desc">Снижение цены для клиента не снижает прибыль компании — сделки остаются выгодными.</div>
            </div>

            <div class="arg">
              <div class="arg-icon">🔓</div>
              <div class="arg-number">100%</div>
              <div class="arg-title">Независимость от поставщика</div>
              <div class="arg-desc">Контроль сроков, объёмов и артикулов без привязки к ПроСистемс.</div>
            </div>

            <div class="arg">
              <div class="arg-icon">🎯</div>
              <div class="arg-number">13 млн ₽</div>
              <div class="arg-title">Цель 2027</div>
              <div class="arg-desc">Рост выручки на <b>25%</b> и количества на <b>37%</b> — до <b>~13 700 шт.</b> при цене −20%.</div>
            </div>

            <div class="arg">
              <div class="arg-icon">🧩</div>
              <div class="arg-number">0 ₽</div>
              <div class="arg-title">Доп. вложений в инфраструктуру</div>
              <div class="arg-desc">Каналы, сертификаты, отдел продаж — уже готовы. Старт без дополнительных затрат.</div>
            </div>

          </div>
        </div>

      </div>
    </div>

    <!-- ================= СЛАЙД 2: ЦИФРЫ ================= -->
    <div class="slide">
      <div class="slide-inner">

        <div class="slide-title">
          <div class="num">2</div>
          <div class="text">Цифры и ценообразование</div>
          <div class="sub-text">Слайд 2 из 3</div>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Стоимость компонентов ОРК</h2>

          <div class="components-grid">

            <div class="comp-card">
              <div class="comp-icon">📦</div>
              <div class="comp-name">Корпус</div>
              <div class="comp-supplier">УралПласт · ПП, оранжевый</div>
              <div class="comp-price">94<span class="unit">₽</span></div>
              <div class="comp-share">Доля в СС: <b>~38%</b></div>
            </div>

            <div class="comp-card">
              <div class="comp-icon">🔌</div>
              <div class="comp-name">Клеммы</div>
              <div class="comp-supplier">ONKA · керамика, стеатит</div>
              <div class="comp-price">49,5<span class="unit">₽</span></div>
              <div class="comp-share">Доля в СС: <b>~20%</b></div>
            </div>

            <div class="comp-card">
              <div class="comp-icon">🔩</div>
              <div class="comp-name">Пластина</div>
              <div class="comp-supplier">Собственное производство · сталь</div>
              <div class="comp-price">97<span class="unit">₽</span></div>
              <div class="comp-share">Доля в СС: <b>~39%</b></div>
            </div>

            <div class="comp-card">
              <div class="comp-icon">🔧</div>
              <div class="comp-name">Метизы</div>
              <div class="comp-supplier">Китай · 2 гайки + 2 болта</div>
              <div class="comp-price">~5<span class="unit">₽</span></div>
              <div class="comp-share">Доля в СС: <b>~2%</b></div>
            </div>

          </div>

          <div class="comp-total">
            <div class="lbl">Итого себестоимость</div>
            <div class="val">~245,5 ₽</div>
          </div>

          <p style="font-size:12.5px;color:var(--gray-light);margin-top:14px;">
            ⓘ Расчёт на базе артикула <b>FRJB-KM-P1-2.5-02-FF-IP54</b> (2-полюсный, 2.5 мм²). Стоимость клемм и метизов варьируется в зависимости от количества полюсов. Разница с СС 265,65 ₽ — упаковка, маркировка, сборка (~20 ₽).
          </p>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Ценовая политика: FRJB-KM-P1-2.5-02-FF-IP54</h2>

          <div class="cost-banner">
            <div class="item">
              <div class="lbl">Наша себестоимость</div>
              <div class="val blue">265,65 ₽</div>
              <div class="sub">собственная сборка</div>
            </div>
            <div class="item">
              <div class="lbl">Закупка у ПроСистемс</div>
              <div class="val red">642,85 ₽</div>
              <div class="sub">текущая база</div>
            </div>
            <div class="item">
              <div class="lbl">Снижение себестоимости</div>
              <div class="val green">−377,20 ₽</div>
              <div class="sub">−58,7% против закупки</div>
            </div>
          </div>

          <p style="font-size:13.5px;color:var(--gray-text);margin-bottom:16px;">
            Входная цена для дистра по ПроСистемс — <b>800 ₽</b> (по данным об отгрузках). Наша цена — на <b>20% ниже</b> на каждом уровне.
          </p>

          <table>
            <thead>
              <tr>
                <th>Уровень цены</th>
                <th>ПроСистемс (рынок), ₽</th>
                <th>Наша цена (−20%), ₽</th>
                <th>Выгода клиенту</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><b>Вход для дистра</b></td>
                <td>800</td>
                <td class="td-green"><b>640</b></td>
                <td><span class="tag orange">−160 ₽ (−20%)</span></td>
              </tr>
              <tr>
                <td><b>МРЦ</b></td>
                <td>1 143 <span style="color:var(--gray-light);font-size:11px;">(800 ÷ 0,7)</span></td>
                <td class="td-green"><b>914</b></td>
                <td><span class="tag orange">−229 ₽ (−20%)</span></td>
              </tr>
              <tr>
                <td><b>РРЦ</b></td>
                <td>~1 200</td>
                <td class="td-green"><b>960</b></td>
                <td><span class="tag orange">−240 ₽ (−20%)</span></td>
              </tr>
            </tbody>
          </table>

          <p style="font-size:13px;color:var(--gray-text);margin-top:14px;">
            <b>Для отдела продаж:</b> цена ниже рынка на <b>160–240 ₽</b> на каждом уровне. Маржинальность <b>58–72%</b> — сделки выгодны компании.
          </p>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Целевые показатели 2027</h2>
          <div class="kpi-grid" style="margin-bottom:0;">
            <div class="kpi blue">
              <div class="label">База 2026</div>
              <div class="value blue">10,4 млн ₽</div>
              <div class="sub">9 990 шт.</div>
            </div>
            <div class="kpi orange">
              <div class="label">Цель 2027</div>
              <div class="value orange">13,0 млн ₽</div>
              <div class="sub">+25% к выручке</div>
            </div>
            <div class="kpi red">
              <div class="label">Плановое количество</div>
              <div class="value red">~13 700 шт.</div>
              <div class="sub">+37% к количеству</div>
            </div>
            <div class="kpi orange">
              <div class="label">Валовая прибыль</div>
              <div class="value orange">~8,7 млн ₽</div>
              <div class="sub">рост маржинальности</div>
            </div>
          </div>
        </div>

      </div>
    </div>

    <!-- ================= СЛАЙД 3: РЕСУРСЫ ================= -->
    <div class="slide">
      <div class="slide-inner">

        <div class="slide-title">
          <div class="num">3</div>
          <div class="text">Старт, расходы и ресурсы</div>
          <div class="sub-text">Слайд 3 из 3</div>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Стартовые вложения</h2>
          <table>
            <thead>
              <tr><th>Статья</th><th>Сумма, ₽</th><th>Комментарий</th></tr>
            </thead>
            <tbody>
              <tr><td>Комплектующие (стартовая партия)</td><td class="td-orange">940 000</td><td>~3 000 изделий</td></tr>
              <tr><td>Доставка</td><td class="td-orange">50 000</td><td>комплектующие на склад</td></tr>
              <tr style="background:var(--orange-soft);font-weight:800;">
                <td>ИТОГО старт</td><td class="td-red">990 000</td><td>окупаемость ~2 мес.</td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Расходы на сборку и маркировку</h2>
          <table>
            <thead>
              <tr><th>Статья</th><th>Сумма, ₽ / мес.</th><th>Комментарий</th></tr>
            </thead>
            <tbody>
              <tr><td>Оплата труда сборщиков (2 чел. × 3 ч/день)</td><td class="td-orange">~45 000</td><td>совмещение с основной работой</td></tr>
              <tr><td>Маркировка, упаковка, расходники</td><td class="td-orange">~15 000</td><td>на партию ~1 300 шт.</td></tr>
              <tr style="background:var(--orange-soft);font-weight:800;">
                <td>ИТОГО в месяц</td><td class="td-red">~60 000</td><td>при плановом объёме</td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Ресурсы: люди и смены</h2>
          <div class="kpi-grid" style="margin-bottom:0;">
            <div class="kpi orange">
              <div class="label">Время на 1 изделие</div>
              <div class="value orange">6 мин</div>
              <div class="sub">6 операций</div>
            </div>
            <div class="kpi blue">
              <div class="label">1 сотрудник за 3 часа</div>
              <div class="value blue">30 шт.</div>
              <div class="sub">180 мин / 6 мин</div>
            </div>
            <div class="kpi red">
              <div class="label">2 сотрудника за 3 часа</div>
              <div class="value red">60 шт./день</div>
              <div class="sub">совмещение</div>
            </div>
            <div class="kpi orange">
              <div class="label">2 700 изделий — 2 чел.</div>
              <div class="value orange">45 раб. дней</div>
              <div class="sub">~2 месяца при 3 ч/день</div>
            </div>
          </div>
          <table style="margin-top:20px;">
            <thead>
              <tr><th>Занятость на сборке</th><th>2 сотрудника, шт./день</th><th>Срок на 2 700 шт.</th></tr>
            </thead>
            <tbody>
              <tr style="background:var(--orange-soft);">
                <td><b>3 часа/день</b></td>
                <td class="td-green"><b>60</b></td>
                <td class="td-green"><b>45 раб. дней (~2 мес.) ✅</b></td>
              </tr>
              <tr><td>4 часа/день</td><td>80</td><td>34 раб. дня (~1,5 мес.)</td></tr>
              <tr><td>6 часов/день</td><td>120</td><td>22,5 раб. дня (~1 мес.)</td></tr>
            </tbody>
          </table>

          <p style="font-size:13px;color:var(--gray-text);margin-top:16px;">
            <b>Инфраструктура готова:</b> каналы продаж налажены (Русский Свет, ЭТМ + 40 дистрибьюторов), сертификаты получены, отдел продаж работает. Дополнительных вложений не требуется.
          </p>
        </div>

        <footer>
          <svg width="20" height="20" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg">
            <path d="M32 2 L58 12 L58 32 C58 46 46 56 32 62 C18 56 6 46 6 32 L6 12 Z" fill="#E53935"/>
            <path d="M32 18 C32 18 24 28 24 36 C24 41 27.5 45 32 45 C36.5 45 40 41 40 36 C40 32 38 29 36 26 C36 30 34 32 32 32 C32 32 34 26 32 18 Z" fill="#FFA726"/>
          </svg>
          Дашборд подготовлен для отдела продаж и руководства · FIREFORT · 2026
        </footer>

      </div>
    </div>

  </div>
</div>

<!-- ==== НАВИГАЦИЯ ==== -->
<div class="nav">
  <div class="nav-logo-ff">
    <svg width="22" height="22" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <linearGradient id="navShield" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#B71C1C"/>
          <stop offset="100%" stop-color="#FF6F00"/>
        </linearGradient>
      </defs>
      <path d="M32 2 L58 12 L58 32 C58 46 46 56 32 62 C18 56 6 46 6 32 L6 12 Z" fill="url(#navShield)"/>
      <path d="M32 18 C32 18 24 28 24 36 C24 41 27.5 45 32 45 C36.5 45 40 41 40 36 C40 32 38 29 36 26 C36 30 34 32 32 32 C32 32 34 26 32 18 Z" fill="#FFD54F"/>
    </svg>
    <span class="nav-logo-text">FIREFORT</span>
  </div>
  <button class="nav-btn" id="prevBtn" aria-label="Назад">‹</button>
  <div class="dots" id="dots">
    <button class="dot-nav active" data-slide="0" aria-label="Слайд 1"></button>
    <button class="dot-nav" data-slide="1" aria-label="Слайд 2"></button>
    <button class="dot-nav" data-slide="2" aria-label="Слайд 3"></button>
  </div>
  <div class="slide-counter" id="counter">1 / 3</div>
  <button class="nav-btn" id="nextBtn" aria-label="Вперёд">›</button>
</div>

<script>
  const slidesEl = document.getElementById('slides');
  const dots = document.querySelectorAll('.dot-nav');
  const prevBtn = document.getElementById('prevBtn');
  const nextBtn = document.getElementById('nextBtn');
  const counter = document.getElementById('counter');
  const total = dots.length;
  let current = 0;

  function goTo(index) {
    if (index < 0) index = 0;
    if (index > total - 1) index = total - 1;
    current = index;
    slidesEl.style.transform = `translateX(-${current * 100}%)`;
    dots.forEach((d, i) => d.classList.toggle('active', i === current));
    counter.textContent = `${current + 1} / ${total}`;
    prevBtn.disabled = current === 0;
    nextBtn.disabled = current === total - 1;
    document.querySelectorAll('.slide')[current].scrollTop = 0;
  }

  prevBtn.addEventListener('click', () => goTo(current - 1));
  nextBtn.addEventListener('click', () => goTo(current + 1));
  dots.forEach((d, i) => d.addEventListener('click', () => goTo(i)));

  document.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowLeft') goTo(current - 1);
    if (e.key === 'ArrowRight') goTo(current + 1);
  });

  let touchStartX = 0;
  const slider = document.querySelector('.slider');
  slider.addEventListener('touchstart', (e) => { touchStartX = e.changedTouches[0].screenX; }, { passive: true });
  slider.addEventListener('touchend', (e) => {
    const diff = touchStartX - e.changedTouches[0].screenX;
    if (Math.abs(diff) > 50) {
      if (diff > 0) goTo(current + 1);
      else goTo(current - 1);
    }
  }, { passive: true });

  goTo(0);
</script>

</body>
</html>

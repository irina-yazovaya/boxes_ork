<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FIREFORT · Дашборд для технического директора</title>
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
    --gray-text: #3A3A3A;
    --gray-light: #9E9E9E;
    --green: #2E7D32;
    --blue: #1565C0;
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
  .slide-inner { max-width: 1280px; margin: 0 auto; padding-bottom: 90px; }

  /* ==== НАВИГАЦИЯ ==== */
  .nav {
    position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
    display: flex; align-items: center; gap: 16px;
    background: rgba(255,255,255,0.97); padding: 10px 20px;
    border-radius: 50px; box-shadow: 0 6px 24px rgba(0,0,0,0.15);
    z-index: 100; backdrop-filter: blur(8px); border: 1px solid var(--orange-line);
  }
  .nav-btn {
    width: 42px; height: 42px; border-radius: 50%; border: none;
    background: linear-gradient(135deg, var(--red) 0%, var(--orange) 100%);
    color: #fff; font-size: 20px; font-weight: 800; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: transform 0.2s, box-shadow 0.2s;
    box-shadow: 0 3px 10px rgba(229,57,53,0.3);
  }
  .nav-btn:hover:not(:disabled) { transform: scale(1.08); box-shadow: 0 5px 16px rgba(229,57,53,0.45); }
  .nav-btn:disabled { opacity: 0.35; cursor: not-allowed; box-shadow: none; }
  .dots { display: flex; gap: 8px; align-items: center; }
  .dot-nav {
    width: 10px; height: 10px; border-radius: 50%; background: var(--orange-line);
    border: none; cursor: pointer; transition: all 0.25s; padding: 0;
  }
  .dot-nav.active { width: 28px; border-radius: 6px; background: linear-gradient(135deg, var(--red) 0%, var(--orange) 100%); }
  .slide-counter { font-size: 13px; font-weight: 800; color: var(--red-dark); min-width: 42px; text-align: center; }

  /* ==== ШАПКА ==== */
  header {
    background: linear-gradient(135deg, #B71C1C 0%, #E53935 55%, #FF6F00 130%);
    color: #fff; padding: 34px 38px; border-radius: 16px; margin-bottom: 24px;
    box-shadow: 0 10px 32px rgba(183,28,28,0.35);
    position: relative; overflow: hidden;
  }
  header::before {
    content: ""; position: absolute; top: -60px; right: -60px;
    width: 260px; height: 260px;
    background: radial-gradient(circle, rgba(255,255,255,0.14) 0%, transparent 70%);
    border-radius: 50%; pointer-events: none;
  }
  .header-grid {
    display: grid; grid-template-columns: 1.2fr 1fr; gap: 32px;
    align-items: center; position: relative; z-index: 1;
  }
  .header-left { display: flex; flex-direction: column; gap: 10px; }
  .brand-badge {
    display: inline-block; align-self: flex-start; background: #fff;
    color: var(--red-dark); font-size: 20px; font-weight: 900;
    letter-spacing: 3px; padding: 8px 18px; border-radius: 8px;
    box-shadow: 0 4px 14px rgba(0,0,0,0.18); margin-bottom: 4px;
  }
  header h1 { font-size: 28px; font-weight: 900; line-height: 1.15; letter-spacing: -0.5px; }
  .brand-sub { font-size: 14px; opacity: 0.95; line-height: 1.5; }
  .brand-sub b { font-weight: 800; }
  .brand-tagline {
    display: inline-block; margin-top: 8px;
    background: rgba(255,255,255,0.16); border-left: 4px solid #FFD54F;
    padding: 10px 16px; border-radius: 8px; font-size: 14px;
    font-weight: 600; align-self: flex-start;
  }
  .brand-tagline b { color: #FFD54F; font-weight: 900; }
  .header-right {
    display: flex; align-items: center; justify-content: flex-end; gap: 20px;
    background: rgba(0,0,0,0.18); border-radius: 14px;
    padding: 20px 24px; backdrop-filter: blur(2px);
  }
  .anchor { text-align: left; }
  .anchor-label {
    font-size: 11px; text-transform: uppercase; letter-spacing: 1.2px;
    font-weight: 700; opacity: 0.85; margin-bottom: 6px;
  }
  .anchor-value {
    font-size: 38px; font-weight: 900; line-height: 1; letter-spacing: -1.5px;
    color: #FFD54F; text-shadow: 0 3px 12px rgba(0,0,0,0.25);
  }
  .anchor-sub { font-size: 11.5px; opacity: 0.85; margin-top: 8px; }
  .anchor-divider { width: 1px; height: 70px; background: rgba(255,255,255,0.28); }

  /* ==== KPI ==== */
  .kpi-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 16px; margin-bottom: 22px;
  }
  .kpi {
    background: var(--gray-card); border-radius: 12px; padding: 20px 18px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.06);
    border-left: 5px solid var(--gray-line);
    transition: transform 0.2s, box-shadow 0.2s;
    position: relative; overflow: hidden;
  }
  .kpi:hover { transform: translateY(-3px); box-shadow: 0 6px 20px rgba(0,0,0,0.1); }
  .kpi.red { border-left-color: var(--red); background: linear-gradient(135deg, #fff 60%, #FFEBEE 100%); }
  .kpi.green { border-left-color: var(--green); background: linear-gradient(135deg, #fff 60%, #E8F5E9 100%); }
  .kpi.blue { border-left-color: var(--blue); background: linear-gradient(135deg, #fff 60%, #E3F2FD 100%); }
  .kpi.orange { border-left-color: var(--orange); background: linear-gradient(135deg, #fff 60%, var(--orange-soft) 100%); }
  .kpi .label { font-size: 11.5px; text-transform: uppercase; letter-spacing: 0.5px; color: var(--gray-light); margin-bottom: 8px; font-weight: 700; }
  .kpi .value { font-size: 26px; font-weight: 800; color: var(--gray-text); line-height: 1.1; }
  .kpi .value.red { color: var(--red); }
  .kpi .value.green { color: var(--green); }
  .kpi .value.blue { color: var(--blue); }
  .kpi .value.orange { color: var(--orange); }
  .kpi .sub { font-size: 11.5px; color: var(--gray-light); margin-top: 6px; }

  /* ==== SECTIONS ==== */
  .section {
    background: var(--gray-card); border-radius: 12px;
    padding: 22px 26px; margin-bottom: 22px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.06);
    position: relative; overflow: hidden;
  }
  .section::before {
    content: ""; position: absolute; top: 0; left: 0; height: 4px; width: 100%;
    background: linear-gradient(90deg, var(--red) 0%, var(--orange) 50%, var(--orange-light) 100%);
    pointer-events: none;
  }
  .section h2 {
    font-size: 17px; font-weight: 700; color: var(--gray-text);
    margin-bottom: 16px; padding-bottom: 12px;
    border-bottom: 2px solid var(--orange-line);
    display: flex; align-items: center; gap: 10px;
  }
  .section h2 .dot {
    width: 10px; height: 10px; border-radius: 50%;
    background: linear-gradient(135deg, var(--red), var(--orange)); display: inline-block;
  }

  /* ==== ЗАГОЛОВОК СЛАЙДА ==== */
  .slide-title {
    display: flex; align-items: center; gap: 14px; margin-bottom: 18px;
    padding: 14px 22px; background: linear-gradient(135deg, #fff 0%, var(--orange-soft) 100%);
    border-radius: 12px; border-left: 5px solid var(--orange);
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
  }
  .slide-title .num {
    width: 40px; height: 40px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    background: linear-gradient(135deg, var(--red) 0%, var(--orange) 100%);
    color: #fff; font-weight: 900; font-size: 17px;
    box-shadow: 0 3px 10px rgba(229,57,53,0.3);
  }
  .slide-title .text { font-size: 19px; font-weight: 900; color: var(--red-dark); letter-spacing: -0.3px; }
  .slide-title .sub-text { font-size: 13px; color: var(--gray-light); margin-left: auto; font-weight: 600; }

  /* ==== ТАБЛИЦЫ ==== */
  .tbl-wrap { overflow-x: auto; }
  table { width: 100%; border-collapse: collapse; font-size: 13px; min-width: 720px; }
  thead th {
    background: linear-gradient(135deg, var(--orange-soft) 0%, var(--orange-line) 100%);
    color: var(--gray-text); text-align: left;
    padding: 11px 12px; font-weight: 700; font-size: 11.5px;
    text-transform: uppercase; letter-spacing: 0.4px;
    border-bottom: 2px solid var(--orange-light);
    white-space: nowrap;
  }
  tbody td { padding: 10px 12px; border-bottom: 1px solid var(--gray-line); }
  tbody tr:hover { background: var(--orange-soft); }
  .td-green { color: var(--green); font-weight: 700; }
  .td-red { color: var(--red); font-weight: 700; }
  .td-blue { color: var(--blue); font-weight: 700; }
  .td-orange { color: var(--orange); font-weight: 700; }
  .td-gray { color: var(--gray-light); }
  .td-mono { font-family: 'Consolas', 'Courier New', monospace; font-weight: 700; }
  .row-total { background: var(--orange-soft) !important; font-weight: 800; }
  .row-total td { border-bottom: 2px solid var(--orange-light); }
  .art-code { font-family: 'Consolas', monospace; font-size: 11.5px; font-weight: 700; color: var(--blue); white-space: nowrap; }

  .tag {
    display: inline-block; padding: 3px 9px; border-radius: 20px;
    font-size: 11px; font-weight: 700; white-space: nowrap;
  }
  .tag.green { background: #E8F5E9; color: var(--green); }
  .tag.red { background: #FFEBEE; color: var(--red); }
  .tag.blue { background: #E3F2FD; color: var(--blue); }
  .tag.orange { background: var(--orange-soft); color: var(--orange); }

  /* ==== ФОРМУЛА СЕБЕСТОИМОСТИ ==== */
  .formula {
    display: grid; grid-template-columns: repeat(6, 1fr);
    gap: 12px; margin-bottom: 18px;
  }
  .formula .item {
    background: linear-gradient(135deg, #fff 0%, var(--orange-soft) 100%);
    border: 2px solid var(--orange-line); border-radius: 10px;
    padding: 14px 12px; text-align: center;
  }
  .formula .item.highlight {
    border-color: var(--orange); background: linear-gradient(135deg, #fff 0%, #FFE0B2 100%);
  }
  .formula .item .lbl {
    font-size: 10.5px; text-transform: uppercase; letter-spacing: 0.4px;
    color: var(--gray-text); font-weight: 700; margin-bottom: 6px;
  }
  .formula .item .val { font-size: 20px; font-weight: 900; color: var(--blue); line-height: 1; }
  .formula .item.highlight .val { color: var(--red); }
  .formula .item .sub { font-size: 10.5px; color: var(--gray-light); margin-top: 6px; }

  footer { text-align: center; font-size: 12px; color: var(--gray-light); padding: 20px 0 8px; }

  /* ==== АДАПТИВ ==== */
  @media (max-width: 1000px) {
    .header-grid { grid-template-columns: 1fr; gap: 20px; }
    .header-right { justify-content: flex-start; }
    .formula { grid-template-columns: repeat(3, 1fr); }
  }
  @media (max-width: 640px) {
    .slide { padding: 12px; }
    header { padding: 24px 20px; }
    header h1 { font-size: 20px; }
    .brand-badge { font-size: 16px; letter-spacing: 2px; padding: 6px 14px; }
    .anchor-value { font-size: 30px; }
    .header-right { padding: 16px; gap: 12px; flex-wrap: wrap; }
    .section { padding: 16px; }
    .kpi .value { font-size: 20px; }
    .formula { grid-template-columns: repeat(2, 1fr); }
    .formula .item .val { font-size: 17px; }
    .nav { bottom: 12px; padding: 8px 14px; gap: 10px; }
    .nav-btn { width: 36px; height: 36px; font-size: 16px; }
  }
</style>
</head>
<body>

<div class="slider">
  <div class="slides" id="slides">

    <!-- ================= СЛАЙД 1: ЭКОНОМИКА ПРОДУКТА ================= -->
    <div class="slide">
      <div class="slide-inner">

        <header>
          <div class="header-grid">
            <div class="header-left">
              <div class="brand-badge">FIREFORT</div>
              <h1>Себестоимость и маржинальность по 11 артикулам</h1>
              <p class="brand-sub">
                Серия <b>FIREFORT-П1</b> · IP54 · 100×100×50 мм · корпус 030-014нг (97 ₽) ·
                клеммы ONKA (арт. 1070002–1070007) · пластина 95 ₽ · метизы и сборка 20 ₽/шт.
              </p>
              <div class="brand-tagline">
                Средняя себестоимость <b>252,25 ₽</b> · средняя маржа <b>68,5%</b>
              </div>
            </div>
            <div class="header-right">
              <div class="anchor">
                <div class="anchor-label">Себестоимость</div>
                <div class="anchor-value">252 ₽</div>
                <div class="anchor-sub">средняя по 11 артикулам</div>
              </div>
              <div class="anchor-divider"></div>
              <div class="anchor">
                <div class="anchor-label">Маржа (при 800 ₽)</div>
                <div class="anchor-value">68,5%</div>
                <div class="anchor-sub">диапазон 65,4–72,6%</div>
              </div>
            </div>
          </div>
        </header>

        <div class="section">
          <h2><span class="dot"></span>Формула себестоимости одного изделия</h2>
          <div class="formula">
            <div class="item">
              <div class="lbl">Корпус</div>
              <div class="val">97,00</div>
              <div class="sub">030-014нг УПрк 100×100/50</div>
            </div>
            <div class="item">
              <div class="lbl">Клеммы ONKA</div>
              <div class="val">49,5–356,4</div>
              <div class="sub">1–2 шт. по типу</div>
            </div>
            <div class="item">
              <div class="lbl">Пластина</div>
              <div class="val">95,00</div>
              <div class="sub">монтажная</div>
            </div>
            <div class="item">
              <div class="lbl">Метизы</div>
              <div class="val">~10,00</div>
              <div class="sub">оценка</div>
            </div>
            <div class="item">
              <div class="lbl">Сборка</div>
              <div class="val">~10,00</div>
              <div class="sub">6 мин/шт.</div>
            </div>
            <div class="item highlight">
              <div class="lbl">ИТОГО база</div>
              <div class="val">261,50+</div>
              <div class="sub">+ клеммы</div>
            </div>
          </div>
          <p style="font-size:13px;color:var(--gray-text);">
            <b>Формула:</b> Себестоимость = Корпус (97 ₽) + Клеммы (по типу × шт.) + Пластина (95 ₽) +
            <b>Метизы и сборка (20 ₽)</b>. Минимум — <b>261,50 ₽</b> (2 клеммы 49,5 ₽), максимум — <b>568,40 ₽</b> (10 мм², 4 полюса).
          </p>
        </div>

        <div class="kpi-grid">
          <div class="kpi blue">
            <div class="label">Минимум себестоимости</div>
            <div class="value blue">261,50 ₽</div>
            <div class="sub">2,5 мм² · 2 клеммы</div>
          </div>
          <div class="kpi orange">
            <div class="label">Средняя себестоимость</div>
            <div class="value orange">359,32 ₽</div>
            <div class="sub">по всем 11 артикулам</div>
          </div>
          <div class="kpi red">
            <div class="label">Максимум себестоимости</div>
            <div class="value red">568,40 ₽</div>
            <div class="sub">10 мм² · 4 клеммы</div>
          </div>
          <div class="kpi green">
            <div class="label">Средняя маржа @800 ₽</div>
            <div class="value green">55,1%</div>
            <div class="sub">валовая по портфелю</div>
          </div>
        </div>

      </div>
    </div>

    <!-- ================= СЛАЙД 2: ТАБЛИЦА ПО АРТИКУЛАМ ================= -->
    <div class="slide">
      <div class="slide-inner">

        <div class="slide-title">
          <div class="num">2</div>
          <div class="text">Себестоимость по 11 артикулам</div>
          <div class="sub-text">Слайд 2 из 3</div>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Расчёт: комплектующие + метизы/сборка (20 ₽) = полная себестоимость</h2>
          <div class="tbl-wrap">
            <table>
              <thead>
                <tr>
                  <th>Артикул</th>
                  <th>Сечение</th>
                  <th>Клемм</th>
                  <th>Корпус, ₽</th>
                  <th>Клеммы, ₽</th>
                  <th>Пластина, ₽</th>
                  <th>Метизы+сборка, ₽</th>
                  <th>Себест-ть, ₽</th>
                  <th>Маржа @800 ₽</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td class="art-code">…-2.5-02-…</td><td>2,5 мм²</td><td>2</td>
                  <td>97,00</td><td>49,50</td><td>95,00</td><td>20,00</td>
                  <td class="td-green td-mono">261,50</td><td><span class="tag green">67,3%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-2.5-04-…</td><td>2,5 мм²</td><td>4</td>
                  <td>97,00</td><td>99,00</td><td>95,00</td><td>20,00</td>
                  <td class="td-green td-mono">311,00</td><td><span class="tag green">61,1%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-2.5-06-…</td><td>2,5 мм²</td><td>6</td>
                  <td>97,00</td><td>138,60</td><td>95,00</td><td>20,00</td>
                  <td class="td-green td-mono">350,60</td><td><span class="tag green">56,2%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-4-02-…</td><td>4 мм²</td><td>2</td>
                  <td>97,00</td><td>49,50</td><td>95,00</td><td>20,00</td>
                  <td class="td-green td-mono">261,50</td><td><span class="tag green">67,3%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-4-04-…</td><td>4 мм²</td><td>4</td>
                  <td>97,00</td><td>99,00</td><td>95,00</td><td>20,00</td>
                  <td class="td-green td-mono">311,00</td><td><span class="tag green">61,1%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-4-06-…</td><td>4 мм²</td><td>6</td>
                  <td>97,00</td><td>184,80</td><td>95,00</td><td>20,00</td>
                  <td class="td-orange td-mono">396,80</td><td><span class="tag orange">50,4%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-6-02-…</td><td>6 мм²</td><td>2</td>
                  <td>97,00</td><td>69,30</td><td>95,00</td><td>20,00</td>
                  <td class="td-green td-mono">281,30</td><td><span class="tag green">64,8%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-6-04-…</td><td>6 мм²</td><td>4</td>
                  <td>97,00</td><td>138,60</td><td>95,00</td><td>20,00</td>
                  <td class="td-green td-mono">350,60</td><td><span class="tag green">56,2%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-6-06-…</td><td>6 мм²</td><td>6</td>
                  <td>97,00</td><td>190,80</td><td>95,00</td><td>20,00</td>
                  <td class="td-orange td-mono">402,80</td><td><span class="tag orange">49,7%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-10-03-…</td><td>10 мм²</td><td>3</td>
                  <td>97,00</td><td>178,20</td><td>95,00</td><td>20,00</td>
                  <td class="td-orange td-mono">390,20</td><td><span class="tag orange">51,2%</span></td>
                </tr>
                <tr>
                  <td class="art-code">…-10-04-…</td><td>10 мм²</td><td>4</td>
                  <td>97,00</td><td>257,40</td><td>95,00</td><td>20,00</td>
                  <td class="td-red td-mono">469,40</td><td><span class="tag red">41,3%</span></td>
                </tr>
                <tr class="row-total">
                  <td colspan="6">ИТОГО / Среднее по 11 артикулам</td>
                  <td class="td-mono">220,00</td>
                  <td class="td-red td-mono">353,40</td>
                  <td><span class="tag orange">55,8%</span></td>
                </tr>
              </tbody>
            </table>
          </div>
          <p style="font-size:12.5px;color:var(--gray-text);margin-top:14px;">
            <b>Источник данных:</b> корпус 030-014нг — 97 ₽; клеммы ONKA по артикулам 1070002–1070007 (49,5 / 69,3 / 92,4 / 95,4 / 128,7 / 178,2 ₽); пластина — 95 ₽; метизы и сборка — 20 ₽/шт.
          </p>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Ключевые выводы для техдиректора</h2>
          <div class="kpi-grid" style="margin-bottom:0;">
            <div class="kpi green">
              <div class="label">Самая маржинальная позиция</div>
              <div class="value green">2,5/4 мм² · 2 кл.</div>
              <div class="sub">себест. 261,50 ₽ · маржа 67,3%</div>
            </div>
            <div class="kpi red">
              <div class="label">Наименее маржинальная</div>
              <div class="value red">10 мм² · 4 кл.</div>
              <div class="sub">себест. 469,40 ₽ · маржа 41,3%</div>
            </div>
            <div class="kpi blue">
              <div class="label">Метизы + сборка</div>
              <div class="value blue">20 ₽</div>
              <div class="sub">+7,6% к базовой себестоимости</div>
            </div>
            <div class="kpi orange">
              <div class="label">Разброс себестоимости</div>
              <div class="value orange">2,2×</div>
              <div class="sub">261,5 → 568,4 ₽ (с 4 кл. 10 мм²)</div>
            </div>
          </div>
        </div>

      </div>
    </div>

    <!-- ================= СЛАЙД 3: РЕСУРСЫ И ЗАПАС ================= -->
    <div class="slide">
      <div class="slide-inner">

        <div class="slide-title">
          <div class="num">3</div>
          <div class="text">Ресурсы, запас прочности и точки внимания</div>
          <div class="sub-text">Слайд 3 из 3</div>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Запас прочности по цене</h2>
          <div class="tbl-wrap">
            <table>
              <thead>
                <tr>
                  <th>Сценарий цены</th>
                  <th>Средняя себест., ₽</th>
                  <th>Цена, ₽</th>
                  <th>Валовая маржа, ₽</th>
                  <th>Маржинальность</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>Себестоимость (нулевая маржа)</td>
                  <td class="td-mono">353,40</td>
                  <td class="td-mono">353,40</td>
                  <td class="td-mono">0</td>
                  <td><span class="tag red">0%</span></td>
                </tr>
                <tr>
                  <td>Агрессивная цена</td>
                  <td class="td-mono">353,40</td>
                  <td class="td-mono">640,00</td>
                  <td class="td-green td-mono">286,60</td>
                  <td><span class="tag orange">44,8%</span></td>
                </tr>
                <tr style="background:var(--orange-soft);font-weight:700;">
                  <td>Целевая цена (дистр)</td>
                  <td class="td-mono">353,40</td>
                  <td class="td-mono">800,00</td>
                  <td class="td-green td-mono">446,60</td>
                  <td><span class="tag green">55,8%</span></td>
                </tr>
                <tr>
                  <td>МРЦ</td>
                  <td class="td-mono">353,40</td>
                  <td class="td-mono">1 143,00</td>
                  <td class="td-green td-mono">789,60</td>
                  <td><span class="tag green">69,1%</span></td>
                </tr>
                <tr>
                  <td>РРЦ</td>
                  <td class="td-mono">353,40</td>
                  <td class="td-mono">1 200,00</td>
                  <td class="td-green td-mono">846,60</td>
                  <td><span class="tag green">70,6%</span></td>
                </tr>
              </tbody>
            </table>
          </div>
          <p style="font-size:13px;color:var(--gray-text);margin-top:14px;">
            <b>Точка безубыточности:</b> при средней себестоимости 353,40 ₽ и цене входа 800 ₽ компания зарабатывает
            <b>446,60 ₽</b> валовой прибыли с изделия. Даже при снижении цены до 640 ₽ маржа остаётся положительной (<b>44,8%</b>).
          </p>
        </div>

        <div class="section">
          <h2><span class="dot"></span>Ресурсы на сборку (11 артикулов, план 2027)</h2>
          <div class="kpi-grid">
            <div class="kpi orange">
              <div class="label">Время на 1 изделие</div>
              <div class="value orange">6 мин</div>
              <div class="sub">6 операций сборки</div>
            </div>
            <div class="kpi blue">
              <div class="label">1 сборщик за смену (8 ч)</div>
              <div class="value blue">80 шт.</div>
              <div class="sub">при полной загрузке</div>
            </div>
            <div class="kpi red">
              <div class="label">План 2027</div>
              <div class="value red">13 700 шт.</div>
              <div class="sub">+37% к 2026</div>
            </div>
            <div class="kpi green">
              <div class="label">Нужно сборщиков</div>
              <div class="value green">~1,5 FTE</div>
              <div class="sub">при 8 ч/день, 250 дней</div>
            </div>
          </div>
          <div class="tbl-wrap" style="margin-top:18px;">
            <table>
              <thead>
                <tr><th>Статья</th><th>Расчёт</th><th>Сумма, ₽/мес.</th></tr>
              </thead>
              <tbody>
                <tr><td>Оплата труда сборщиков</td><td>1,5 FTE × 45 000 ₽</td><td class="td-orange">~67 500</td></tr>
                <tr><td>Метизы и расходники</td><td>~1 100 шт./мес. × 10 ₽</td><td class="td-orange">~11 000</td></tr>
                <tr><td>Упаковка и маркировка</td><td>~1 100 шт./мес.</td><td class="td-orange">~15 000</td></tr>
                <tr class="row-total"><td>ИТОГО в месяц</td><td>при плановом объёме</td><td class="td-red">~93 500</td></tr>
              </tbody>
            </table>
          </div>
        </div>

        <div class="section" style="border:2px solid var(--orange);">
          <h2 style="color:var(--red-dark);"><span class="dot"></span>Точки внимания для технического директора</h2>
          <div class="tbl-wrap">
            <table>
              <thead>
                <tr><th>Позиция</th><th>Проблема</th><th>Рекомендация</th></tr>
              </thead>
              <tbody>
                <tr>
                  <td><b>10 мм² · 4 клеммы</b></td>
                  <td class="td-red">Маржа всего 41,3% — самая низкая в линейке</td>
                  <td>Пересмотреть цену или найти клеммы дешевле</td>
                </tr>
                <tr>
                  <td><b>6 мм² · 6 клемм</b></td>
                  <td class="td-orange">Маржа 49,7% — ниже средней</td>
                  <td>Проверить альтернативных поставщиков клемм</td>
                </tr>
                <tr>
                  <td><b>2,5 и 4 мм² · 2 клеммы</b></td>
                  <td class="td-green">Лидеры по марже — 67,3%</td>
                  <td>Сделать флагманами продаж</td>
                </tr>
                <tr>
                  <td><b>Все 11 артикулов</b></td>
                  <td class="td-blue">Метизы+сборка 20 ₽ = 5,7% себестоимости</td>
                  <td>Контролировать норму расхода метизов</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <footer>
          Дашборд для технического директора · FIREFORT · Система КМ · 2026
        </footer>

      </div>
    </div>

  </div>
</div>

<!-- ==== НАВИГАЦИЯ ==== -->
<div class="nav">
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

  let touchStartX = 0, touchEndX = 0;
  const slider = document.querySelector('.slider');
  slider.addEventListener('touchstart', (e) => { touchStartX = e.changedTouches[0].screenX; }, { passive: true });
  slider.addEventListener('touchend', (e) => {
    touchEndX = e.changedTouches[0].screenX;
    const diff = touchStartX - touchEndX;
    if (Math.abs(diff) > 50) { if (diff > 0) goTo(current + 1); else goTo(current - 1); }
  }, { passive: true });

  goTo(0);
</script>

</body>
</html>

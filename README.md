<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>SPMB — Smart Power Management Board</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #0a0c10;
    --surface: #111318;
    --surface2: #181c24;
    --border: #1e2330;
    --accent: #f5a623;
    --accent2: #3de8a0;
    --accent3: #5b8fff;
    --text: #e8eaf0;
    --muted: #6b7280;
    --danger: #ff5f5f;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    line-height: 1.7;
    min-height: 100vh;
  }

  /* HERO */
  .hero {
    position: relative;
    overflow: hidden;
    padding: 80px 48px 64px;
    border-bottom: 1px solid var(--border);
    background: radial-gradient(ellipse 80% 60% at 60% -10%, rgba(245,166,35,0.12) 0%, transparent 70%),
                radial-gradient(ellipse 50% 40% at 90% 80%, rgba(61,232,160,0.06) 0%, transparent 60%);
  }

  .hero-grid {
    position: absolute; inset: 0; opacity: 0.04;
    background-image: linear-gradient(var(--accent) 1px, transparent 1px),
                      linear-gradient(90deg, var(--accent) 1px, transparent 1px);
    background-size: 40px 40px;
  }

  .badge-row {
    display: flex; gap: 10px; flex-wrap: wrap;
    margin-bottom: 28px;
  }

  .badge {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    padding: 4px 12px;
    border-radius: 4px;
    border: 1px solid;
    letter-spacing: 0.04em;
    font-weight: 700;
    text-transform: uppercase;
  }
  .badge-orange { border-color: var(--accent); color: var(--accent); background: rgba(245,166,35,0.08); }
  .badge-green  { border-color: var(--accent2); color: var(--accent2); background: rgba(61,232,160,0.08); }
  .badge-blue   { border-color: var(--accent3); color: var(--accent3); background: rgba(91,143,255,0.08); }

  .hero h1 {
    font-size: clamp(2.2rem, 5vw, 3.6rem);
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 1.1;
    max-width: 700px;
  }

  .hero h1 span { color: var(--accent); }

  .hero-sub {
    margin-top: 18px;
    font-size: 1.05rem;
    color: var(--muted);
    max-width: 560px;
  }

  .hero-meta {
    display: flex; gap: 32px; flex-wrap: wrap;
    margin-top: 36px;
    padding-top: 32px;
    border-top: 1px solid var(--border);
  }

  .meta-item { display: flex; flex-direction: column; gap: 4px; }
  .meta-label { font-size: 11px; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); font-family: 'JetBrains Mono', monospace; }
  .meta-value { font-size: 0.95rem; font-weight: 600; color: var(--text); }

  /* LAYOUT */
  .container { max-width: 1080px; margin: 0 auto; padding: 64px 48px; }

  /* SECTION */
  .section { margin-bottom: 72px; }

  .section-header {
    display: flex; align-items: center; gap: 14px;
    margin-bottom: 32px;
  }

  .section-icon {
    width: 36px; height: 36px;
    border-radius: 8px;
    display: grid; place-items: center;
    font-size: 16px;
    flex-shrink: 0;
  }
  .icon-orange { background: rgba(245,166,35,0.15); border: 1px solid rgba(245,166,35,0.3); }
  .icon-green  { background: rgba(61,232,160,0.12); border: 1px solid rgba(61,232,160,0.25); }
  .icon-blue   { background: rgba(91,143,255,0.12); border: 1px solid rgba(91,143,255,0.25); }
  .icon-red    { background: rgba(255,95,95,0.12);  border: 1px solid rgba(255,95,95,0.25); }

  .section-title {
    font-size: 1.3rem;
    font-weight: 700;
    letter-spacing: -0.01em;
  }

  /* OBJECTIVES */
  .objectives-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 16px;
  }

  .obj-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 22px 24px;
    display: flex; gap: 16px; align-items: flex-start;
    transition: border-color 0.2s, transform 0.2s;
  }
  .obj-card:hover { border-color: rgba(245,166,35,0.4); transform: translateY(-2px); }

  .obj-num {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    font-weight: 700;
    color: var(--accent);
    background: rgba(245,166,35,0.1);
    border: 1px solid rgba(245,166,35,0.2);
    border-radius: 4px;
    padding: 3px 7px;
    flex-shrink: 0;
    margin-top: 2px;
  }

  .obj-text { font-size: 0.9rem; color: var(--text); line-height: 1.5; }

  /* PIPELINE */
  .pipeline {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 36px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0;
  }

  .pipe-step {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    max-width: 360px;
  }

  .pipe-block {
    width: 100%;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 20px;
    display: flex; align-items: center; gap: 14px;
    transition: border-color 0.2s;
    position: relative;
  }
  .pipe-block:hover { border-color: var(--accent); }

  .pipe-icon { font-size: 20px; width: 36px; text-align: center; flex-shrink: 0; }
  .pipe-label { font-weight: 700; font-size: 0.9rem; }
  .pipe-sub { font-size: 0.75rem; color: var(--muted); font-family: 'JetBrains Mono', monospace; }

  .pipe-arrow {
    width: 2px;
    height: 28px;
    background: linear-gradient(to bottom, var(--border), var(--accent));
    position: relative;
    margin: 4px 0;
  }
  .pipe-arrow::after {
    content: '▼';
    position: absolute;
    bottom: -8px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 8px;
    color: var(--accent);
  }

  /* FEATURES */
  .features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 14px;
  }

  .feat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 22px 20px;
    transition: border-color 0.2s, background 0.2s;
  }
  .feat-card:hover { border-color: rgba(61,232,160,0.4); background: rgba(61,232,160,0.03); }

  .feat-header { display: flex; align-items: center; gap: 10px; margin-bottom: 10px; }
  .feat-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
  .dot-orange { background: var(--accent); box-shadow: 0 0 6px var(--accent); }
  .dot-green  { background: var(--accent2); box-shadow: 0 0 6px var(--accent2); }
  .dot-blue   { background: var(--accent3); box-shadow: 0 0 6px var(--accent3); }

  .feat-name { font-size: 0.88rem; font-weight: 700; }
  .feat-desc { font-size: 0.82rem; color: var(--muted); line-height: 1.5; }

  /* COMPONENTS TABLE */
  .comp-table {
    width: 100%;
    border-collapse: collapse;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
  }

  .comp-table th {
    background: var(--surface2);
    padding: 14px 20px;
    text-align: left;
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
    border-bottom: 1px solid var(--border);
  }

  .comp-table td {
    padding: 14px 20px;
    border-bottom: 1px solid var(--border);
    font-size: 0.88rem;
  }
  .comp-table tr:last-child td { border-bottom: none; }
  .comp-table tr:hover td { background: rgba(255,255,255,0.02); }

  .comp-block { font-weight: 600; color: var(--text); }
  .comp-part {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.82rem;
    color: var(--accent);
    background: rgba(245,166,35,0.08);
    padding: 3px 8px;
    border-radius: 4px;
    display: inline-block;
  }

  /* HIGHLIGHTS */
  .highlights-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 16px;
  }

  .hl-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 24px;
    transition: border-color 0.2s;
  }
  .hl-card:hover { border-color: rgba(91,143,255,0.4); }
  .hl-title {
    font-size: 0.88rem;
    font-weight: 700;
    color: var(--accent3);
    margin-bottom: 10px;
    display: flex; align-items: center; gap: 8px;
  }
  .hl-body { font-size: 0.85rem; color: var(--muted); line-height: 1.6; }

  /* LIMITATIONS */
  .limits-box {
    background: rgba(255,95,95,0.05);
    border: 1px solid rgba(255,95,95,0.25);
    border-radius: 12px;
    padding: 28px;
    display: flex; flex-direction: column; gap: 14px;
  }

  .limit-item { display: flex; gap: 12px; align-items: flex-start; }
  .limit-bullet {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: var(--danger);
    background: rgba(255,95,95,0.12);
    border-radius: 3px;
    padding: 2px 6px;
    flex-shrink: 0;
    margin-top: 2px;
    font-weight: 700;
  }
  .limit-text { font-size: 0.88rem; color: var(--text); line-height: 1.5; }

  /* FILE TREE */
  .tree-box {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 28px 32px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.85rem;
    line-height: 2;
    overflow-x: auto;
  }

  .tree-root { color: var(--accent); font-weight: 700; }
  .tree-dir  { color: var(--accent3); }
  .tree-file { color: var(--muted); }
  .tree-connector { color: var(--border); user-select: none; }

  /* FUTURE */
  .future-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 14px;
  }

  .future-item {
    background: var(--surface);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent2);
    border-radius: 0 10px 10px 0;
    padding: 16px 18px;
    font-size: 0.88rem;
    line-height: 1.5;
    color: var(--text);
    transition: background 0.2s;
  }
  .future-item:hover { background: rgba(61,232,160,0.04); }
  .future-tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    color: var(--accent2);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    display: block;
    margin-bottom: 6px;
    font-weight: 700;
  }

  /* DEMONSTRATES */
  .dem-grid {
    display: flex; flex-wrap: wrap; gap: 10px;
  }

  .dem-chip {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 100px;
    padding: 8px 18px;
    font-size: 0.85rem;
    font-weight: 600;
    color: var(--text);
    transition: all 0.2s;
    cursor: default;
    display: flex; align-items: center; gap: 8px;
  }
  .dem-chip:hover {
    background: rgba(245,166,35,0.1);
    border-color: var(--accent);
    color: var(--accent);
  }
  .dem-chip-dot { width: 6px; height: 6px; background: var(--accent); border-radius: 50%; }

  /* FOOTER */
  .footer {
    border-top: 1px solid var(--border);
    padding: 36px 48px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 16px;
  }

  .footer-left {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--muted);
  }

  .footer-left strong { color: var(--accent); }

  .footer-right {
    font-size: 12px;
    color: var(--muted);
  }

  @media (max-width: 640px) {
    .hero, .container, .footer { padding-left: 24px; padding-right: 24px; }
    .hero { padding-top: 48px; padding-bottom: 40px; }
    .pipeline { padding: 24px 16px; }
  }
</style>
</head>
<body>

<!-- ─── HERO ─── -->
<header class="hero">
  <div class="hero-grid"></div>
  <div class="badge-row">
    <span class="badge badge-orange">PCB Design</span>
    <span class="badge badge-green">Power Electronics</span>
    <span class="badge badge-blue">Embedded Systems</span>
  </div>
  <h1><span>SPMB</span> — Smart Power<br/>Management Board</h1>
  <p class="hero-sub">
    A power distribution and backup system that intelligently manages multiple power sources — handling input protection, voltage regulation, battery charging, and automatic switching.
  </p>
  <div class="hero-meta">
    <div class="meta-item">
      <span class="meta-label">Input Voltage</span>
      <span class="meta-value">12V DC</span>
    </div>
    <div class="meta-item">
      <span class="meta-label">Output Rail</span>
      <span class="meta-value">5V Regulated</span>
    </div>
    <div class="meta-item">
      <span class="meta-label">Battery</span>
      <span class="meta-value">18650 Li-ion</span>
    </div>
    <div class="meta-item">
      <span class="meta-label">Type</span>
      <span class="meta-value">Portfolio Project</span>
    </div>
  </div>
</header>

<main class="container">

  <!-- ─── OBJECTIVES ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-orange">🎯</div>
      <h2 class="section-title">Project Objectives</h2>
    </div>
    <div class="objectives-grid">
      <div class="obj-card">
        <span class="obj-num">01</span>
        <span class="obj-text">Design a safe DC input stage with fuse and reverse-polarity protection</span>
      </div>
      <div class="obj-card">
        <span class="obj-num">02</span>
        <span class="obj-text">Implement a regulated 5V power rail using a buck converter</span>
      </div>
      <div class="obj-card">
        <span class="obj-num">03</span>
        <span class="obj-text">Integrate a Li-ion battery charging system via TP4056</span>
      </div>
      <div class="obj-card">
        <span class="obj-num">04</span>
        <span class="obj-text">Enable automatic power path switching between adapter and battery</span>
      </div>
      <div class="obj-card">
        <span class="obj-num">05</span>
        <span class="obj-text">Provide measurable outputs and test points for embedded monitoring</span>
      </div>
    </div>
  </section>

  <!-- ─── ARCHITECTURE ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-blue">🧠</div>
      <h2 class="section-title">System Architecture</h2>
    </div>
    <div class="pipeline">
      <div class="pipe-step">
        <div class="pipe-block">
          <div class="pipe-icon">🔌</div>
          <div>
            <div class="pipe-label">12V DC Input</div>
            <div class="pipe-sub">External power supply</div>
          </div>
        </div>
        <div class="pipe-arrow"></div>
      </div>
      <div class="pipe-step">
        <div class="pipe-block">
          <div class="pipe-icon">🛡️</div>
          <div>
            <div class="pipe-label">Input Protection</div>
            <div class="pipe-sub">Fuse + P-MOSFET reverse polarity</div>
          </div>
        </div>
        <div class="pipe-arrow"></div>
      </div>
      <div class="pipe-step">
        <div class="pipe-block">
          <div class="pipe-icon">⚡</div>
          <div>
            <div class="pipe-label">Buck Converter</div>
            <div class="pipe-sub">LM2596 · 12V → 5V regulated</div>
          </div>
        </div>
        <div class="pipe-arrow"></div>
      </div>
      <div class="pipe-step">
        <div class="pipe-block">
          <div class="pipe-icon">🔋</div>
          <div>
            <div class="pipe-label">Battery Charger</div>
            <div class="pipe-sub">TP4056 → 18650 Li-ion</div>
          </div>
        </div>
        <div class="pipe-arrow"></div>
      </div>
      <div class="pipe-step">
        <div class="pipe-block">
          <div class="pipe-icon">🔄</div>
          <div>
            <div class="pipe-label">MOSFET Power Switch</div>
            <div class="pipe-sub">AO3401A · P-MOSFET high-side</div>
          </div>
        </div>
        <div class="pipe-arrow"></div>
      </div>
      <div class="pipe-step">
        <div class="pipe-block" style="border-color: rgba(61,232,160,0.5); background: rgba(61,232,160,0.05);">
          <div class="pipe-icon">💡</div>
          <div>
            <div class="pipe-label" style="color: var(--accent2);">5V Output Rail</div>
            <div class="pipe-sub">Stable regulated load</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ─── KEY FEATURES ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-green">🔧</div>
      <h2 class="section-title">Key Features</h2>
    </div>
    <div class="features-grid">
      <div class="feat-card">
        <div class="feat-header">
          <div class="feat-dot dot-orange"></div>
          <span class="feat-name">Input Protection</span>
        </div>
        <p class="feat-desc">Blade fuse for overcurrent protection + P-MOSFET for reverse polarity blocking with minimal voltage drop.</p>
      </div>
      <div class="feat-card">
        <div class="feat-header">
          <div class="feat-dot dot-orange"></div>
          <span class="feat-name">Voltage Regulation</span>
        </div>
        <p class="feat-desc">LM2596 buck converter steps 12V down to a stable 5V rail with high efficiency.</p>
      </div>
      <div class="feat-card">
        <div class="feat-header">
          <div class="feat-dot dot-green"></div>
          <span class="feat-name">Battery Management</span>
        </div>
        <p class="feat-desc">TP4056 handles constant current / constant voltage charging for a single 18650 Li-ion cell.</p>
      </div>
      <div class="feat-card">
        <div class="feat-header">
          <div class="feat-dot dot-green"></div>
          <span class="feat-name">Auto Power Switching</span>
        </div>
        <p class="feat-desc">P-MOSFET path controller automatically falls back to battery when the external adapter is removed.</p>
      </div>
      <div class="feat-card">
        <div class="feat-header">
          <div class="feat-dot dot-blue"></div>
          <span class="feat-name">ADC Monitoring</span>
        </div>
        <p class="feat-desc">Resistor voltage divider scales battery voltage to MCU ADC range for real-time sensing.</p>
      </div>
      <div class="feat-card">
        <div class="feat-header">
          <div class="feat-dot dot-blue"></div>
          <span class="feat-name">Test Points</span>
        </div>
        <p class="feat-desc">Exposed test points across the board for probing, debugging, and signal verification during development.</p>
      </div>
    </div>
  </section>

  <!-- ─── COMPONENTS ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-blue">🧩</div>
      <h2 class="section-title">Main Components</h2>
    </div>
    <table class="comp-table">
      <thead>
        <tr>
          <th>Function Block</th>
          <th>Component</th>
          <th>Notes</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="comp-block">Input Protection</td>
          <td><span class="comp-part">Fuse + AO3401A</span></td>
          <td style="color:var(--muted); font-size:0.82rem;">Overcurrent + reverse polarity guard</td>
        </tr>
        <tr>
          <td class="comp-block">Buck Converter</td>
          <td><span class="comp-part">LM2596</span></td>
          <td style="color:var(--muted); font-size:0.82rem;">12V → 5V, adjustable switching regulator</td>
        </tr>
        <tr>
          <td class="comp-block">Battery Charger</td>
          <td><span class="comp-part">TP4056</span></td>
          <td style="color:var(--muted); font-size:0.82rem;">CC/CV Li-ion charging IC</td>
        </tr>
        <tr>
          <td class="comp-block">Battery Cell</td>
          <td><span class="comp-part">18650 Li-ion</span></td>
          <td style="color:var(--muted); font-size:0.82rem;">Single cell, ~3.7V nominal</td>
        </tr>
        <tr>
          <td class="comp-block">Power Switching</td>
          <td><span class="comp-part">AO3401A</span></td>
          <td style="color:var(--muted); font-size:0.82rem;">P-MOSFET high-side switch</td>
        </tr>
        <tr>
          <td class="comp-block">Voltage Sensing</td>
          <td><span class="comp-part">R divider</span></td>
          <td style="color:var(--muted); font-size:0.82rem;">Scales Vbatt for ADC input</td>
        </tr>
      </tbody>
    </table>
  </section>

  <!-- ─── DESIGN HIGHLIGHTS ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-blue">⚙️</div>
      <h2 class="section-title">Design Highlights</h2>
    </div>
    <div class="highlights-grid">
      <div class="hl-card">
        <div class="hl-title">🔐 Reverse Polarity Protection</div>
        <div class="hl-body">A P-MOSFET is placed on the input stage to block incorrect polarity connections. Unlike a diode, the MOSFET's RDS(on) is very low, minimizing the voltage drop under normal forward operation.</div>
      </div>
      <div class="hl-card">
        <div class="hl-title">🔋 Charging System</div>
        <div class="hl-body">The TP4056 is fed directly from the regulated 5V buck output, ensuring the battery always receives a clean, stable charge voltage regardless of input fluctuations.</div>
      </div>
      <div class="hl-card">
        <div class="hl-title">🔄 Automatic Power Switching</div>
        <div class="hl-body">When adapter power is present, the MOSFET path keeps the battery isolated from the load. Upon loss of external supply, the gate logic allows battery current to flow automatically — no manual intervention required.</div>
      </div>
      <div class="hl-card">
        <div class="hl-title">📐 Voltage Monitoring</div>
        <div class="hl-body">A precision resistor divider network scales the 18650 battery voltage (0–4.2V) to a safe 0–3.3V window, compatible with most MCU ADC pins for real-time state-of-charge estimation.</div>
      </div>
    </div>
  </section>

  <!-- ─── LIMITATIONS ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-red">⚠️</div>
      <h2 class="section-title">Known Limitations</h2>
    </div>
    <div class="limits-box">
      <div class="limit-item">
        <span class="limit-bullet">LIM</span>
        <span class="limit-text">The <strong>TP4056 is not a full power-path IC</strong> — it cannot cleanly manage simultaneous charging and load driving, which may cause instability under heavy loads while charging.</span>
      </div>
      <div class="limit-item">
        <span class="limit-bullet">LIM</span>
        <span class="limit-text"><strong>No seamless load + charging optimization</strong> — the charger and load share the same rail without dedicated arbitration logic.</span>
      </div>
      <div class="limit-item">
        <span class="limit-bullet">REC</span>
        <span class="limit-text"><strong>Recommended future upgrade:</strong> replace TP4056 with a dedicated power-path management IC such as the IP5306 or BQ series (e.g. BQ24074) for proper load-sharing behavior.</span>
      </div>
    </div>
  </section>

  <!-- ─── PROJECT STRUCTURE ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-orange">📁</div>
      <h2 class="section-title">Project Structure</h2>
    </div>
    <div class="tree-box">
      <div><span class="tree-root">SPMB/</span></div>
      <div><span class="tree-connector">├── </span><span class="tree-dir">schematic/</span><span class="tree-file" style="margin-left:8px;font-size:11px;">— KiCad / EasyEDA source files</span></div>
      <div><span class="tree-connector">├── </span><span class="tree-dir">pcb/</span><span class="tree-file" style="margin-left:8px;font-size:11px;">— Layout files, copper pours, DRC reports</span></div>
      <div><span class="tree-connector">├── </span><span class="tree-dir">fabrication/</span><span class="tree-file" style="margin-left:8px;font-size:11px;">— Gerbers, drill files, BOM</span></div>
      <div><span class="tree-connector">├── </span><span class="tree-dir">docs/</span></div>
      <div><span class="tree-connector">│&nbsp;&nbsp; └── </span><span class="tree-file">README.md</span></div>
      <div><span class="tree-connector">└── </span><span class="tree-dir">images/</span><span class="tree-file" style="margin-left:8px;font-size:11px;">— 3D renders, board photos</span></div>
    </div>
  </section>

  <!-- ─── FUTURE IMPROVEMENTS ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-green">🚀</div>
      <h2 class="section-title">Future Improvements</h2>
    </div>
    <div class="future-grid">
      <div class="future-item">
        <span class="future-tag">Power IC</span>
        Replace TP4056 with a dedicated power-path IC — IP5306 or BQ series for proper load-sharing
      </div>
      <div class="future-item">
        <span class="future-tag">Sensing</span>
        Add current sensing via INA219 or ACS712 for precise power consumption tracking
      </div>
      <div class="future-item">
        <span class="future-tag">Controller</span>
        Integrate an MCU (STM32 / ESP32) for smart monitoring, alerts, and data logging
      </div>
      <div class="future-item">
        <span class="future-tag">Display</span>
        Add OLED display for real-time status — voltage, current, charge state
      </div>
      <div class="future-item">
        <span class="future-tag">PCB Stack</span>
        Upgrade to 4-layer PCB for improved power integrity and reduced EMI
      </div>
    </div>
  </section>

  <!-- ─── DEMONSTRATES ─── -->
  <section class="section">
    <div class="section-header">
      <div class="section-icon icon-orange">🧠</div>
      <h2 class="section-title">What This Project Demonstrates</h2>
    </div>
    <div class="dem-grid">
      <div class="dem-chip"><div class="dem-chip-dot"></div>Power Electronics Design</div>
      <div class="dem-chip"><div class="dem-chip-dot"></div>PCB Protection Strategies</div>
      <div class="dem-chip"><div class="dem-chip-dot"></div>Li-ion Battery Integration</div>
      <div class="dem-chip"><div class="dem-chip-dot"></div>Analog + Digital Interaction</div>
      <div class="dem-chip"><div class="dem-chip-dot"></div>Real-world Engineering Tradeoffs</div>
      <div class="dem-chip"><div class="dem-chip-dot"></div>Component Selection</div>
      <div class="dem-chip"><div class="dem-chip-dot"></div>PCB Layout Fundamentals</div>
    </div>
  </section>

</main>

<!-- ─── FOOTER ─── -->
<footer class="footer">
  <div class="footer-left">
    <strong>SPMB</strong> · Smart Power Management Board<br/>
    PCB Engineering Portfolio · Progressive Design Series
  </div>
  <div class="footer-right" style="font-family:'JetBrains Mono',monospace; font-size:11px; color: var(--muted);">
    v1.0 · 1-cell · 12V→5V · 18650
  </div>
</footer>

</body>
</html>

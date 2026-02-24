<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="color-scheme" content="dark" />
  <title>BIORECONSTRUCT™ — Renacer Tecnológico (Single File)</title>

  <!-- CSP (para archivo local). Si lo servís desde server, ajustá según tus needs -->
  <meta http-equiv="Content-Security-Policy"
        content="
          default-src 'self' 'unsafe-inline';
          img-src 'self' data:;
          connect-src 'self';
          object-src 'none';
          base-uri 'self';
          frame-ancestors 'none';
          form-action 'self';
        " />

  <style>
    :root{
      --bg: #07060c;
      --panel: rgba(15, 14, 24, 0.70);
      --panel2: rgba(10, 10, 18, 0.75);
      --stroke: rgba(255,255,255,0.10);
      --stroke2: rgba(255,255,255,0.16);
      --text: rgba(255,255,255,0.90);
      --muted: rgba(255,255,255,0.62);
      --neon-a: #00d4ff;
      --neon-b: #7f5cff;
      --neon-c: #46ff9a;
      --danger: #ff3b6b;
      --warn: #ffc14d;
      --ok: #46ff9a;
      --shadow: 0 18px 60px rgba(0,0,0,0.45);
      --radius: 16px;
      --radius2: 22px;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
      --sans: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans", "Liberation Sans", sans-serif;
    }

    *{ box-sizing: border-box; }
    html, body{ height:100%; }
    body{
      margin:0;
      background: var(--bg);
      color: var(--text);
      font-family: var(--sans);
      overflow-x:hidden;
    }

    /* Fondo */
    .bg{ position: fixed; inset: 0; z-index: -5; }
    #scene{ width: 100%; height: 100%; display:block; filter: saturate(1.05) contrast(1.05); }
    .scanlines{
      position: absolute; inset: 0;
      background: repeating-linear-gradient(to bottom,
        rgba(255,255,255,0.03),
        rgba(255,255,255,0.03) 1px,
        rgba(0,0,0,0) 3px,
        rgba(0,0,0,0) 6px
      );
      mix-blend-mode: overlay;
      opacity: 0.22;
      pointer-events:none;
    }
    .vignette{
      position:absolute; inset:0;
      background: radial-gradient(closest-side, rgba(0,0,0,0) 40%, rgba(0,0,0,0.55) 100%);
      pointer-events:none;
    }

    /* Topbar */
    .topbar{
      position: sticky; top:0; z-index: 50;
      display:flex; align-items:center; justify-content: space-between; gap: 12px;
      padding: 12px 14px;
      background: linear-gradient(to bottom, rgba(8,8,14,0.92), rgba(8,8,14,0.70));
      border-bottom: 1px solid var(--stroke);
      backdrop-filter: blur(10px);
    }

    .brand{ display:flex; align-items:center; gap: 10px; min-width: 260px; }
    .logo{
      width: 42px; height: 42px; display:grid; place-items:center;
      background: rgba(255,255,255,0.04);
      border: 1px solid var(--stroke);
      border-radius: 14px;
      box-shadow: var(--shadow);
    }
    .brandText{ display:flex; flex-direction:column; line-height: 1.1; }
    .brandName{ font-weight: 800; letter-spacing: 0.6px; }
    .tm{ font-size: 12px; opacity: 0.7; vertical-align: top; margin-left: 1px; }
    .brandTag{ font-size: 12px; color: var(--muted); }

    .nav{ display:flex; gap: 8px; flex-wrap: wrap; justify-content:center; }
    .navBtn{
      appearance:none;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,0.04);
      color: var(--text);
      padding: 10px 12px;
      border-radius: 14px;
      cursor:pointer;
      font-weight: 650;
      transition: transform 120ms ease, border-color 120ms ease, background 120ms ease;
    }
    .navBtn:hover{ transform: translateY(-1px); border-color: var(--stroke2); }
    .navBtn[aria-current="page"]{
      border-color: rgba(0,212,255,0.45);
      box-shadow: 0 0 0 1px rgba(0,212,255,0.2) inset;
    }
    .navBtn.glow{
      border-color: rgba(127,92,255,0.55);
      box-shadow: 0 0 22px rgba(127,92,255,0.18);
    }

    .right{ display:flex; gap: 10px; align-items:center; }
    .role{
      display:flex; align-items:center; gap: 8px;
      padding: 8px 10px;
      background: rgba(255,255,255,0.04);
      border: 1px solid var(--stroke);
      border-radius: 14px;
    }
    select{
      background: transparent;
      color: var(--text);
      border: 1px solid var(--stroke);
      border-radius: 12px;
      padding: 8px 10px;
      font-weight: 650;
    }
    option{ color: #000; }
    .panic{
      appearance:none;
      border: 1px solid rgba(255,59,107,0.35);
      background: rgba(255,59,107,0.10);
      color: var(--text);
      padding: 10px 12px;
      border-radius: 14px;
      cursor:pointer;
      font-weight: 750;
    }

    /* Layout */
    .main{
      display:grid;
      grid-template-columns: 360px 1fr;
      gap: 14px;
      padding: 14px;
      max-width: 1360px;
      margin: 0 auto;
    }
    .sidebar{ display:flex; flex-direction:column; gap: 14px; }
    .content{ min-height: calc(100vh - 92px); }

    .card{
      background: var(--panel);
      border: 1px solid var(--stroke);
      border-radius: var(--radius2);
      padding: 14px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(10px);
    }
    .cardTitle{
      margin: 0 0 10px 0;
      font-size: 14px;
      letter-spacing: 0.4px;
      text-transform: uppercase;
      color: rgba(255,255,255,0.85);
    }
    .kv{
      display:grid;
      grid-template-columns: 1fr auto;
      gap: 8px 10px;
      font-family: var(--mono);
      font-size: 12px;
    }
    .k{ color: var(--muted); }
    .v{ color: rgba(255,255,255,0.92); }
    .divider{ margin: 12px 0; height:1px; background: var(--stroke); }

    .muted{ color: var(--muted); }
    .small{ font-size: 12px; line-height: 1.35; }
    .row{ display:flex; gap: 10px; flex-wrap: wrap; }
    .btn{
      appearance:none;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,0.05);
      color: var(--text);
      padding: 10px 12px;
      border-radius: 14px;
      cursor:pointer;
      font-weight: 700;
    }
    .btn:hover{ border-color: var(--stroke2); }

    .app{
      background: var(--panel2);
      border: 1px solid var(--stroke);
      border-radius: var(--radius2);
      padding: 18px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(10px);
    }

    /* Typography */
    .h1{ margin: 0 0 10px; font-size: 26px; letter-spacing: 0.2px; }
    .lead{ margin: 0 0 16px; color: rgba(255,255,255,0.75); line-height: 1.55; }

    .glitch{
      position: relative;
      display:inline-block;
      text-shadow: 0 0 18px rgba(0,212,255,0.18);
    }
    .glitch::before, .glitch::after{
      content: attr(data-text);
      position:absolute; left:0; top:0;
      opacity: 0.55;
      pointer-events:none;
    }
    .glitch::before{ transform: translate(1px,-1px); color: rgba(127,92,255,0.75); }
    .glitch::after{ transform: translate(-1px,1px); color: rgba(70,255,154,0.55); }

    .chip{
      display:inline-block;
      padding: 3px 8px;
      border-radius: 999px;
      border: 1px solid rgba(0,212,255,0.25);
      background: rgba(0,212,255,0.08);
      font-family: var(--mono);
    }

    .trace{
      font-family: var(--mono);
      font-size: 12px;
      line-height: 1.35;
      background: rgba(255,255,255,0.03);
      border: 1px solid var(--stroke);
      border-radius: 14px;
      padding: 10px;
      max-height: 180px;
      overflow:auto;
    }
    .traceLine{ opacity: 0.9; }

    /* Components rendered by compiler */
    .grid{ display:grid; grid-template-columns: repeat(12, 1fr); gap: 12px; }
    .panel{
      grid-column: span 12;
      background: rgba(255,255,255,0.03);
      border: 1px solid var(--stroke);
      border-radius: var(--radius);
      padding: 14px;
    }
    @media(min-width: 980px){
      .panel.half{ grid-column: span 6; }
      .panel.third{ grid-column: span 4; }
    }
    .panelTitle{
      margin: 0 0 10px;
      font-size: 14px;
      letter-spacing: 0.4px;
      text-transform: uppercase;
      color: rgba(255,255,255,0.86);
    }

    .kpis{ display:flex; gap: 12px; flex-wrap: wrap; }
    .kpi{
      flex: 1 1 180px;
      padding: 12px;
      border-radius: 14px;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,0.03);
    }
    .kpiLabel{ color: var(--muted); font-size: 12px; }
    .kpiValue{ font-size: 22px; font-weight: 800; margin-top: 6px; }
    .kpiHint{ color: rgba(255,255,255,0.70); font-size: 12px; margin-top: 6px; font-family: var(--mono); }

    .table{
      width:100%;
      border-collapse: collapse;
      overflow:hidden;
      border-radius: 14px;
      border: 1px solid var(--stroke);
      background: rgba(0,0,0,0.20);
    }
    .table th, .table td{
      text-align:left;
      padding: 10px 10px;
      border-bottom: 1px solid rgba(255,255,255,0.08);
      font-size: 13px;
    }
    .table th{
      font-size: 12px;
      color: rgba(255,255,255,0.75);
      text-transform: uppercase;
      letter-spacing: 0.4px;
      background: rgba(255,255,255,0.04);
    }
    .table tr:hover td{ background: rgba(0,212,255,0.04); }

    .form{ display:flex; flex-direction:column; gap: 10px; }
    .label{ font-size: 12px; color: var(--muted); }
    .input, textarea{
      width:100%;
      background: rgba(255,255,255,0.04);
      border: 1px solid var(--stroke);
      border-radius: 14px;
      padding: 10px 12px;
      color: var(--text);
      font-family: var(--mono);
      outline: none;
    }
    textarea{ min-height: 120px; resize: vertical; }
    .help{ font-size: 12px; color: rgba(255,255,255,0.70); line-height: 1.4; }

    .badge{
      display:inline-flex;
      gap: 6px;
      align-items:center;
      padding: 4px 10px;
      border-radius: 999px;
      font-size: 12px;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,0.03);
    }
    .badge.ok{ border-color: rgba(70,255,154,0.35); background: rgba(70,255,154,0.08); }
    .badge.warn{ border-color: rgba(255,193,77,0.35); background: rgba(255,193,77,0.08); }
    .badge.danger{ border-color: rgba(255,59,107,0.35); background: rgba(255,59,107,0.10); }

    .hr{ height:1px; background: var(--stroke); margin: 12px 0; }

    .chat{ display:flex; flex-direction:column; gap: 10px; }
    .chatLog{
      height: 320px;
      overflow:auto;
      padding: 10px;
      border-radius: 14px;
      border: 1px solid var(--stroke);
      background: rgba(0,0,0,0.22);
    }
    .msg{
      padding: 10px 10px;
      border-radius: 14px;
      border: 1px solid rgba(255,255,255,0.08);
      margin-bottom: 10px;
    }
    .msg.user{ background: rgba(0,212,255,0.06); }
    .msg.ai{ background: rgba(127,92,255,0.07); }
    .msg .meta{ font-size: 12px; color: var(--muted); margin-bottom: 6px; font-family: var(--mono); }
    .msg .body{ font-size: 13px; line-height: 1.5; white-space: pre-wrap; }

    .footer{ margin-top: 12px; padding: 10px 4px; opacity: 0.92; }

    @media(max-width: 980px){
      .main{ grid-template-columns: 1fr; }
      .brand{ min-width: 0; }
    }

    /* Safe mode */
    body.safe *{ animation: none !important; transition: none !important; }
    body.safe #scene{ filter: none; }
  </style>
</head>

<body>
  <div class="bg">
    <canvas id="scene" aria-label="Animación de fondo cyberpunk"></canvas>
    <div class="scanlines" aria-hidden="true"></div>
    <div class="vignette" aria-hidden="true"></div>
  </div>

  <header class="topbar">
    <div class="brand">
      <div class="logo" aria-hidden="true">
        <svg viewBox="0 0 64 64" width="34" height="34" role="img" aria-label="BIORECONSTRUCT Logo">
          <defs>
            <linearGradient id="g" x1="0" y1="0" x2="1" y2="1">
              <stop offset="0" stop-color="#7f5cff"/>
              <stop offset="0.5" stop-color="#00d4ff"/>
              <stop offset="1" stop-color="#46ff9a"/>
            </linearGradient>
          </defs>
          <path d="M18 14c8-8 20-8 28 0" fill="none" stroke="url(#g)" stroke-width="3" stroke-linecap="round"/>
          <path d="M18 50c8 8 20 8 28 0" fill="none" stroke="url(#g)" stroke-width="3" stroke-linecap="round"/>
          <path d="M22 18c0 12 20 16 20 28" fill="none" stroke="url(#g)" stroke-width="3" stroke-linecap="round"/>
          <path d="M42 18c0 12-20 16-20 28" fill="none" stroke="url(#g)" stroke-width="3" stroke-linecap="round"/>
          <circle cx="32" cy="32" r="6" fill="none" stroke="url(#g)" stroke-width="3"/>
          <path d="M32 26v12M26 32h12" stroke="url(#g)" stroke-width="2" stroke-linecap="round"/>
        </svg>
      </div>
      <div class="brandText">
        <div class="brandName">BIORECONSTRUCT<span class="tm">™</span></div>
        <div class="brandTag">Renacer Tecnológico · Biotecnología · Soporte · Datos</div>
      </div>
    </div>

    <nav class="nav" aria-label="Navegación principal">
      <button class="navBtn" data-route="home" aria-current="page">Home</button>
      <button class="navBtn" data-route="fundamentos">Fundamentos</button>
      <button class="navBtn" data-route="datos">Laboratorio</button>
      <button class="navBtn" data-route="robotica">Robótica</button>
      <button class="navBtn" data-route="soporte">Soporte</button>
      <button class="navBtn glow" data-route="socrates">SOCRATES.AI</button>
    </nav>

    <div class="right">
      <div class="role">
        <label for="roleSelect" class="muted">Rol</label>
        <select id="roleSelect" aria-label="Seleccionar rol">
          <option>Visitor</option>
          <option>Researcher</option>
          <option>Support</option>
          <option>Admin</option>
        </select>
      </div>
      <button id="panicBtn" class="panic" title="Reduce animaciones y brillo">Modo Seguro</button>
    </div>
  </header>

  <main class="main">
    <aside class="sidebar" aria-label="Panel lateral">
      <section class="card">
        <h2 class="cardTitle">Estado del Sistema</h2>
        <div class="kv">
          <div class="k">Región</div><div class="v">AR-BA</div>
          <div class="k">Uptime</div><div class="v" id="uptime">00:00:00</div>
          <div class="k">Jobs</div><div class="v" id="jobCount">0</div>
          <div class="k">Tickets</div><div class="v" id="ticketCount">0</div>
        </div>
        <div class="divider"></div>
        <p class="muted small">
          Aviso: Demo sin backend. Datos y jobs son simulados para reproducir pipelines y soporte.
        </p>
      </section>

      <section class="card">
        <h2 class="cardTitle">Ribosomal Compiler</h2>
        <p class="muted small">
          JavaScript interpreta esquemas y genera UI/acciones:
          <span class="chip">schema → UI</span>
        </p>
        <div class="trace" id="trace">
          <div class="traceLine">· ready</div>
        </div>
      </section>

      <section class="card">
        <h2 class="cardTitle">Exportación</h2>
        <div class="row">
          <button id="exportJson" class="btn">Exportar JSON</button>
          <button id="exportCsv" class="btn">Exportar CSV</button>
        </div>
        <p class="muted small">Exporta datasets + métricas actuales (demo).</p>
      </section>
    </aside>

    <section class="content" aria-live="polite">
      <div id="app" class="app"></div>
      <footer class="footer">
        <div class="muted small">
          “La evolución fue accidental. El renacer es intencional. Pero la justicia… aún es una variable no resuelta.”
        </div>
      </footer>
    </section>
  </main>

  <script>
  'use strict';

  /**
   * BIORECONSTRUCT™ — Single File (HTML+CSS+JS)
   * Enfoque académico: separación de responsabilidades en módulos lógicos
   * - Utilidades puras
   * - Estado (in-memory)
   * - “API” simulada (fuentes/acciones)
   * - Validación (preflight)
   * - Motor UI Compiler (schema→UI)
   * - SOCRATES.AI (motor de respuesta basado en evidencia interna)
   * - Canvas (render loop)
   */

  /* ----------------------------- Utilidades ----------------------------- */
  const $ = (sel, root = document) => root.querySelector(sel);
  const $$ = (sel, root = document) => Array.from(root.querySelectorAll(sel));

  const clamp = (n, a, b) => Math.max(a, Math.min(b, n));
  const nowISO = () => new Date().toISOString();

  function safeText(s){
    return String(s ?? '').replace(/[<>&"]/g, (c) => ({
      '<':'&lt;','>':'&gt;','&':'&amp;','"':'&quot;'
    }[c]));
  }

  const formatPct = (x) => `${(x * 100).toFixed(1)}%`;

  function download(filename, text, mime='application/octet-stream'){
    const blob = new Blob([text], {type:mime});
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = filename;
    document.body.appendChild(a);
    a.click();
    a.remove();
    URL.revokeObjectURL(a.href);
  }

  function toCSV(rows){
    const esc = (v) => {
      const s = String(v ?? '');
      if (/[,"\n]/.test(s)) return `"${s.replace(/"/g, '""')}"`;
      return s;
    };
    const headers = Object.keys(rows[0] || {});
    const lines = [headers.map(esc).join(',')];
    for (const r of rows) lines.push(headers.map(h => esc(r[h])).join(','));
    return lines.join('\n');
  }

  /* ----------------------------- Estado global ----------------------------- */
  const state = {
    role: 'Visitor',
    route: 'home',
    safeMode: false,
    bootTime: Date.now(),

    datasets: [
      { id:'DS-ARBA-0007', owner:'lab.reconstruct', lineage:'human-trx-v2', created_at:'2026-02-11', hash:'b3a1f0e2', notes:'Transcriptómica urbana (muestras anonimizadas).' },
      { id:'DS-ARBA-0012', owner:'lab.reconstruct', lineage:'microbiome-env-v1', created_at:'2026-02-19', hash:'a81c9d11', notes:'Microbioma ambiental con presión industrial.' },
      { id:'DS-ARBA-0020', owner:'support.ops', lineage:'incident-telemetry-v3', created_at:'2026-02-22', hash:'9f2d7c60', notes:'Telemetría de drones médicos (sin PII).' },
    ],

    genomes: [
      { species:'Homo sapiens 2.0', mutation_index:0.87, adaptive_response:true, bio_memory:'ribosomal-linked' },
      { species:'Homo sapiens (baseline)', mutation_index:0.31, adaptive_response:true, bio_memory:'neural-biologic' },
      { species:'Urban microbiome cluster', mutation_index:0.62, adaptive_response:false, bio_memory:'distributed' },
    ],

    knowledgeBase: [
      {
        id:'KB-001',
        title:'Ribosoma: traducción ARNm → proteína',
        tags:['biología','ribosoma','fundamentos'],
        citation:'Manual interno BIORECONSTRUCT, Ed. 2026.2',
        body:
`El ribosoma traduce la secuencia del ARNm en una cadena polipeptídica usando ARNt.
En esta plataforma se usa como metáfora operativa: schema → UI/acciones ≈ ARNm → proteína (salida ejecutable).`
      },
      {
        id:'KB-002',
        title:'Selección natural (Darwin) y presión tecnológica',
        tags:['darwin','evolución','ética'],
        citation:'Evolución y Sociedad Técnica, 2025 (resumen operativo)',
        body:
`La selección natural actúa sobre variación heredable y diferencias de éxito.
La presión tecnológica puede alterar entornos, trayectorias adaptativas y desigualdades por acceso asimétrico.`
      },
      {
        id:'KB-003',
        title:'FASTA: formato de secuencias',
        tags:['datos','fasta','bioinformática'],
        citation:'Especificación FASTA (resumen operativo)',
        body:
`FASTA contiene cabecera ">" y líneas de secuencia.
Para ADN: A,C,G,T (a veces N). Para ARN: A,C,G,U.
Validar caracteres, calcular GC% y detectar motivos simples permite un QC básico.`
      }
    ],

    tickets: [
      { id:'TCK-1042', created_at:'2026-02-23', severity:'High', category:'Pipeline', subject:'Job atascado en etapa de normalización', steps:'Repro: iniciar job DS-ARBA-0012, observar progreso 63% > sin avance.', status:'Open' },
      { id:'TCK-1045', created_at:'2026-02-24', severity:'Medium', category:'UI', subject:'Tabla de genomes no ordena correctamente', steps:'Repro: ordenar por mutation_index, comparar con valores.', status:'Triaged' }
    ],

    jobs: []
  };

  const robotCatalog = [
    { unit:'DRN-MED-07', type:'Drone médico (triage)', sensors:'RGB, IR, LiDAR corto', power:'Batería 320Wh', limits:'Viento > 45km/h, lluvia extrema', safety:'Geofencing + kill-switch' },
    { unit:'RBX-BIO-12', type:'Brazo biomecánico (taller)', sensors:'Torque, EMG opcional', power:'Pack 600Wh', limits:'Ciclos térmicos, calibración semanal', safety:'Parada por sobrecarga' },
    { unit:'NPR-NEUR-03', type:'Neuroprótesis (conceptual)', sensors:'Electrodos multi-canal', power:'Inductiva', limits:'Interferencia EMI, latencia', safety:'Failsafe + perfiles' },
  ];

  /* ----------------------------- Trace UI ----------------------------- */
  function trace(line){
    const t = $('#trace');
    if (!t) return;
    const div = document.createElement('div');
    div.className = 'traceLine';
    div.textContent = `· ${line}`;
    t.appendChild(div);
    t.scrollTop = t.scrollHeight;
  }

  /* ----------------------------- Métricas ----------------------------- */
  function computeMetrics(){
    const mutAvg = state.genomes.reduce((a,g)=>a+g.mutation_index,0) / state.genomes.length;
    const diversity = clamp(0.45 + (state.datasets.length * 0.07), 0, 0.98);
    const pressure = clamp(0.38 + (state.jobs.length * 0.05) + (state.tickets.length * 0.03), 0, 0.99);

    const jobsActive = state.jobs.filter(j => j.status === 'Running').length;
    const ticketsOpen = state.tickets.filter(t => t.status === 'Open' || t.status === 'Triaged').length;

    return {
      mutation_avg: mutAvg,
      diversity,
      pressure,
      jobs_active: jobsActive,
      datasets: state.datasets.length,
      tickets: state.tickets.length,
      tickets_open: ticketsOpen,
      sla: 'High ≤ 4h / Medium ≤ 24h / Low ≤ 72h'
    };
  }

  /* ----------------------------- Validaciones (preflight) ----------------------------- */
  function validateJob(form){
    const errs = [];
    const dataset = (form.dataset_id || '').trim();
    const mode = (form.mode || '').trim();
    if (!dataset) errs.push('dataset_id requerido.');
    if (!mode) errs.push('mode requerido.');
    const okModes = ['batch','audit','fast'];
    if (mode && !okModes.includes(mode)) errs.push(`mode inválido. Usá: ${okModes.join(', ')}`);
    if (dataset && !state.datasets.some(d => d.id === dataset)) errs.push('dataset_id no existe en datasets (demo).');
    return errs;
  }

  function validateTicket(form){
    const errs = [];
    const sev = (form.severity || '').trim();
    const cat = (form.category || '').trim();
    const subj = (form.subject || '').trim();
    const steps = (form.steps || '').trim();

    const okSev = ['Low','Medium','High','Critical'];
    const okCat = ['UI','Pipeline','Data','Security'];

    if (!sev) errs.push('severity requerido.');
    if (sev && !okSev.includes(sev)) errs.push(`severity inválido. Usá: ${okSev.join(', ')}`);

    if (!cat) errs.push('category requerido.');
    if (cat && !okCat.includes(cat)) errs.push(`category inválida. Usá: ${okCat.join(', ')}`);

    if (!subj || subj.length < 6) errs.push('subject demasiado corto (≥ 6).');
    if (!steps || steps.length < 20) errs.push('steps demasiado corto (≥ 20).');

    return errs;
  }

  function parseFASTA(input){
    const raw = String(input || '').replace(/\r\n/g, '\n').trim();
    if (!raw) return { ok:false, error:'Entrada vacía.' };

    const lines = raw.split('\n');
    if (!lines[0].startsWith('>')) return { ok:false, error:'FASTA inválido: falta cabecera que comience con ">".' };

    const header = lines[0].slice(1).trim() || 'unnamed';
    const seq = lines.slice(1).join('').replace(/\s+/g,'').toUpperCase();
    if (!seq) return { ok:false, error:'FASTA inválido: secuencia vacía.' };

    const allowed = new Set(['A','C','G','T','U','N']);
    for (let i=0;i<seq.length;i++){
      const c = seq[i];
      if (!allowed.has(c)){
        return { ok:false, error:`Carácter inválido "${c}" en posición ${i+1}. Permitidos: A,C,G,T,U,N.` };
      }
    }
    return { ok:true, header, seq };
  }

  function calcGC(seq){
    let gc=0, total=0;
    for (const c of seq){
      if (c === 'N') continue;
      total++;
      if (c === 'G' || c === 'C') gc++;
    }
    return total ? gc/total : 0;
  }

  function findMotifs(seq, motif){
    const m = motif.toUpperCase().replace(/[^ACGTUN]/g,'');
    if (!m) return [];
    const hits = [];
    for (let i=0; i<=seq.length-m.length; i++){
      if (seq.slice(i, i+m.length) === m) hits.push(i+1);
    }
    return hits;
  }

  /* ----------------------------- Clasificación (soporte) ----------------------------- */
  function classifyTicket(form){
    const text = `${form.subject} ${form.steps}`.toLowerCase();
    let category = 'UI';
    if (/(job|pipeline|atasc|progreso|normaliz|qc)/.test(text)) category = 'Pipeline';
    if (/(dato|dataset|hash|export|csv|json)/.test(text)) category = 'Data';
    if (/(auth|token|xss|inyecc|csp|segur)/.test(text)) category = 'Security';

    let severity = 'Medium';
    if (/(cae|crash|bloquea|no funciona|critical)/.test(text)) severity = 'High';
    if (/(pérdida|brecha|exfil|leak)/.test(text)) severity = 'Critical';

    const suggestions = [];
    if (category === 'Pipeline'){
      suggestions.push('Adjuntar logs del job (stage, progress, últimos 20 eventos).');
      suggestions.push('Indicar dataset_id y modo (batch/audit/fast).');
    }
    if (category === 'UI'){
      suggestions.push('Indicar navegador y pasos exactos.');
      suggestions.push('Adjuntar captura y valores esperados vs observados.');
    }
    if (category === 'Security'){
      suggestions.push('No incluir PII. Adjuntar evidencia mínima reproducible.');
      suggestions.push('Indicar headers relevantes (CSP, auth) y endpoint afectado.');
    }
    if (category === 'Data'){
      suggestions.push('Adjuntar hash del dataset y formato (FASTA/JSON).');
      suggestions.push('Indicar si la validación falla y el mensaje exacto.');
    }
    return { category, severity, suggestions };
  }

  /* ----------------------------- Jobs (pipeline simulado) ----------------------------- */
  const stages = [
    { key:'Ingest', seconds: 2.5 },
    { key:'Normalize', seconds: 3.0 },
    { key:'QC', seconds: 2.2 },
    { key:'Analyze', seconds: 3.5 },
    { key:'Audit', seconds: 2.0 }
  ];

  function pushJobLog(job, severity, message){
    job.logs.push({
      at: nowISO(),
      severity,
      message,
      request_id: `req_${Math.random().toString(16).slice(2,10)}`
    });
  }

  function simulateJob(job){
    let stageIndex = 0;
    let stageStart = performance.now();
    const totalStages = stages.length;

    pushJobLog(job, 'INFO', `Job iniciado. dataset=${job.dataset_id} mode=${job.mode}`);

    function tick(){
      if (job.status !== 'Running') return;

      const st = stages[stageIndex];
      const elapsed = (performance.now() - stageStart) / 1000;
      const stageProgress = clamp(elapsed / st.seconds, 0, 1);

      job.stage = st.key;
      job.progress = Math.floor(((stageIndex + stageProgress) / totalStages) * 100);

      if (Math.random() < 0.03){
        pushJobLog(job, 'DEBUG', `Heartbeat: stage=${job.stage} progress=${job.progress}%`);
      }

      if (stageProgress >= 1){
        pushJobLog(job, 'INFO', `Etapa completada: ${st.key}`);
        stageIndex++;
        stageStart = performance.now();

        if (stageIndex >= totalStages){
          job.progress = 100;
          job.status = 'Done';
          pushJobLog(job, 'INFO', 'Job finalizado correctamente.');
          trace(`jobs:done ${job.id}`);
          renderRoute();
          refreshSidebarCounts();
          return;
        }
      }

      if (state.route === 'datos') renderRouteLight();
      requestAnimationFrame(tick);
    }

    requestAnimationFrame(tick);
  }

  /* ----------------------------- “API” simulada (fuentes + acciones) ----------------------------- */
  function startJob({dataset_id, mode}){
    const id = `JOB-${Math.floor(1000 + Math.random()*9000)}`;
    const job = {
      id,
      dataset_id,
      mode,
      stage: stages[0].key,
      progress: 0,
      status: 'Running',
      started_at: new Date().toISOString(),
      logs: []
    };
    state.jobs.unshift(job);
    trace(`jobs:start ${id} dataset=${dataset_id} mode=${mode}`);
    simulateJob(job);
    refreshSidebarCounts();
    return { ok:true, job };
  }

  function createTicket(payload){
    const id = `TCK-${Math.floor(1000 + Math.random()*9000)}`;
    const triage = classifyTicket(payload);

    const t = {
      id,
      created_at: new Date().toISOString().slice(0,10),
      severity: payload.severity,
      category: payload.category,
      subject: payload.subject,
      steps: payload.steps,
      status: 'Open'
    };

    state.tickets.unshift(t);
    trace(`tickets:create ${id} severity=${t.severity} category=${t.category}`);
    trace(`triage:suggest category=${triage.category} severity=${triage.severity}`);
    for (const s of triage.suggestions) trace(`triage:hint ${s}`);

    refreshSidebarCounts();
    return { ok:true, ticket:t, triage };
  }

  function socratesAnalyzeFASTA(fastaText){
    const parsed = parseFASTA(fastaText);
    const citations = socratesCite(['fasta','ribosoma']);
    if (!parsed.ok){
      return {
        ok:false,
        report:
`Resultado: ❌ FASTA inválido
Error: ${parsed.error}

Preguntas socráticas:
1) ¿Es ADN (T) o ARN (U)?
2) ¿La cabecera describe la muestra sin PII?

Evidencia / Citas:
${citations}`
      };
    }

    const seq = parsed.seq;
    const gc = calcGC(seq);
    const motif = 'ACG';
    const hits = findMotifs(seq, motif);

    const wrapped = seq.match(/.{1,60}/g).join('\n');

    const report =
`Resultado: ✅ FASTA válido
Header: ${parsed.header}
Longitud: ${seq.length}
GC% (sin contar N): ${formatPct(gc)}

Motif demo: "${motif}"
Hits (1-index): ${hits.length ? hits.slice(0,20).join(', ') + (hits.length>20 ? ' ...' : '') : 'sin coincidencias'}

Salida normalizada (60/line):
>${parsed.header}
${wrapped}

Ribosomal Compiler Trace (explicable):
1) Parse FASTA → (header, seq)
2) Validación caracteres → OK
3) Estadísticas → GC%, longitud
4) Motifs → búsqueda exacta (demo)
5) Reporte → evidencia + preguntas

Evidencia / Citas:
${citations}`;

    return { ok:true, report };
  }

  const api = {
    // métricas
    'metrics:mutation_avg': () => computeMetrics().mutation_avg,
    'metrics:diversity': () => computeMetrics().diversity,
    'metrics:pressure': () => computeMetrics().pressure,
    'metrics:jobs_active': () => computeMetrics().jobs_active,
    'metrics:datasets': () => computeMetrics().datasets,
    'metrics:tickets': () => computeMetrics().tickets,
    'metrics:tickets_open': () => computeMetrics().tickets_open,
    'metrics:sla': () => computeMetrics().sla,

    // listas
    'datasets:list': () => state.datasets,
    'jobs:list': () => state.jobs,
    'tickets:list': () => state.tickets,
    'kb:list': () => state.knowledgeBase.map(k => ({...k, tags:k.tags.join('|')})),
    'robots:list': () => robotCatalog,

    // acciones
    'jobs:start': (payload) => startJob(payload),
    'tickets:create': (payload) => createTicket(payload),
    'socrates:analyze_fasta': (payload) => socratesAnalyzeFASTA(payload.fasta),
  };

  /* ----------------------------- Schemas (UI Compiler) ----------------------------- */
  const schemas = {
    home: {
      page: 'home',
      rolesAllowed: ['Visitor','Researcher','Support','Admin'],
      title: 'El Renacer',
      components: [
        { type:'Hero', id:'hero', text:'La humanidad no evoluciona. Se reconstruye.' },
        { type:'Markdown', id:'intro', size:'half', title:'Propósito', body:
`BIORECONSTRUCT™ opera como plataforma técnico-científica: datos biológicos, trazabilidad y soporte operativo.
En este universo, la tecnología actúa como presión evolutiva moderna: no reemplaza a Darwin; reordena el entorno.` },
        { type:'Markdown', id:'metafora', size:'half', title:'Metáfora Ribosomal', body:
`Ribosoma (ARNm → proteína) ≈ Compilador (schema → UI/acciones).
El objetivo es convertir estructuras (datos) en resultados (función), con auditoría y control.` },
        { type:'CTA', id:'cta', actions:[
          { label:'Explorar Fundamentos', route:'fundamentos' },
          { label:'Abrir SOCRATES.AI', route:'socrates' },
          { label:'Reportar Incidente', route:'soporte' }
        ]},
        { type:'KPIGroup', id:'kpis', title:'Indicadores operativos (demo)', items:[
          { label:'Mutation Index (prom.)', source:'metrics:mutation_avg' },
          { label:'Diversity Score', source:'metrics:diversity' },
          { label:'Environmental Pressure', source:'metrics:pressure' }
        ]}
      ]
    },

    fundamentos: {
      page: 'fundamentos',
      rolesAllowed: ['Visitor','Researcher','Support','Admin'],
      title: 'Fundamentos Científicos',
      components: [
        { type:'Markdown', id:'bio', title:'Biología humana (resumen riguroso)', body:
`ADN y ARN almacenan y transportan información genética. El ribosoma traduce ARNm a proteína usando ARNt.
Mutaciones generan variación; la adaptación emerge cuando esa variación resulta ventajosa en un entorno dado.` },
        { type:'Markdown', id:'darwin', title:'Darwin y presión tecnológica', body:
`Selección natural: variación heredable + diferencias de éxito.
Presión tecnológica: cambios inducidos por infraestructura, salud, economía y ambiente que alteran qué rasgos son ventajosos.
La intervención puede salvar… o amplificar desigualdad si el acceso es asimétrico.` },
        { type:'Table', id:'kb', title:'Base de conocimiento (citas internas)', source:'kb:list', columns:['id','title','tags','citation'] }
      ]
    },

    datos: {
      page: 'datos',
      rolesAllowed: ['Researcher','Admin','Support'],
      title: 'Laboratorio de Datos',
      components: [
        { type:'KPIGroup', id:'kpis', title:'Métricas', items:[
          { label:'Jobs activos', source:'metrics:jobs_active' },
          { label:'Datasets', source:'metrics:datasets' },
          { label:'Tickets abiertos', source:'metrics:tickets_open' }
        ]},
        { type:'Table', id:'datasets', size:'half', title:'Datasets', source:'datasets:list', columns:['id','lineage','created_at','hash','notes'] },
        { type:'Table', id:'jobs', size:'half', title:'Jobs (pipeline simulado)', source:'jobs:list', columns:['id','dataset_id','stage','progress','status','started_at'] },
        { type:'Form', id:'startJob', title:'Disparar Job', submitTo:'jobs:start', validation:'job', fields:[
          { name:'dataset_id', label:'Dataset ID', placeholder:'DS-ARBA-0012', required:true },
          { name:'mode', label:'Modo', placeholder:'batch', required:true, hint:'batch | audit | fast' }
        ]},
        { type:'Markdown', id:'hint', title:'Notas de realismo', body:
`El pipeline simula etapas típicas: ingestión, normalización, QC, análisis y auditoría.
Los logs son estructurados y el progreso se actualiza por un loop de render (demo).` }
      ]
    },

    robotica: {
      page: 'robotica',
      rolesAllowed: ['Visitor','Researcher','Support','Admin'],
      title: 'Robótica y Reconstrucción',
      components: [
        { type:'Markdown', id:'catalogIntro', title:'Catálogo técnico (plausible)', body:
`Robots y drones se describen con límites: energía, sensores, seguridad operativa, mantenimiento.
La reconstrucción fisiológica se trata como ingeniería de tejidos y neuroprótesis (conceptual).` },
        { type:'Table', id:'robots', title:'Unidades (demo)', source:'robots:list', columns:['unit','type','sensors','power','limits','safety'] }
      ]
    },

    soporte: {
      page: 'soporte',
      rolesAllowed: ['Support','Admin','Researcher'],
      title: 'Soporte Técnico',
      components: [
        { type:'KPIGroup', id:'kpis', title:'Estado', items:[
          { label:'Tickets', source:'metrics:tickets' },
          { label:'Abiertos', source:'metrics:tickets_open' },
          { label:'SLA (objetivo)', source:'metrics:sla' }
        ]},
        { type:'Table', id:'tickets', title:'Tickets', source:'tickets:list', columns:['id','created_at','severity','category','subject','status'] },
        { type:'Form', id:'newTicket', title:'Crear Ticket', submitTo:'tickets:create', validation:'ticket', fields:[
          { name:'severity', label:'Severidad', placeholder:'Low | Medium | High | Critical', required:true },
          { name:'category', label:'Categoría', placeholder:'UI | Pipeline | Data | Security', required:true },
          { name:'subject', label:'Asunto', placeholder:'Describe el problema en 1 línea', required:true },
          { name:'steps', label:'Pasos para reproducir', placeholder:'1) ... 2) ... 3) ...', required:true, multiline:true }
        ]},
        { type:'Markdown', id:'sla', title:'SLA y auditoría', body:
`SLA demo: High ≤ 4h, Medium ≤ 24h, Low ≤ 72h.
Sugerencias automáticas se generan en frontend para reducir tiempo a resolución.` }
      ]
    },

    socrates: {
      page: 'socrates',
      rolesAllowed: ['Visitor','Researcher','Support','Admin'],
      title: 'SOCRATES.AI',
      components: [
        { type:'Chat', id:'chat', title:'Consola Holográfica', hint:
`Probá:
- "Analiza este FASTA" + pega secuencia
- "Calcula GC% de: ACGTTGCA..."
- "Detecta motif: ACG en ..." 
- "Ayudame con un ticket: job atascado"
- "Ciencia vs tecnología: debate"
`},
        { type:'Form', id:'fasta', title:'Analizador rápido (FASTA)', submitTo:'socrates:analyze_fasta', validation:'fasta', fields:[
          { name:'fasta', label:'FASTA', placeholder:'>sample\nACGTTGCA...', required:true, multiline:true }
        ]},
        { type:'Markdown', id:'kb', title:'Fuentes internas', body:
`SOCRATES.AI cita artículos internos (knowledge_base) y no “adivina”.
Si falta evidencia, pregunta antes de concluir (método socrático).` }
      ]
    }
  };

  /* ----------------------------- SOCRATES.AI (respuestas) ----------------------------- */
  function socratesCite(tags){
    const hits = state.knowledgeBase.filter(k => tags.some(t => k.tags.includes(t)));
    return hits.slice(0,2).map(k => `- ${k.id}: ${k.title} · ${k.citation}`).join('\n') || '- (sin citas disponibles en demo)';
  }

  function socratesDebate(){
    const citations = socratesCite(['darwin','ética']);
    return {
      title: 'SOCRATES.AI — Debate (Ciencia vs Tecnología)',
      body:
`Argumento (Ciencia):
- Descubre mecanismos: selección natural, mutación, adaptación.
- Reduce incertidumbre con evidencia y reproducibilidad.

Argumento (Tecnología):
- Interviene: convierte descubrimiento en acción (terapia, prótesis, infraestructura).
- Introduce nuevas presiones y riesgos: control, desigualdad, dependencia.

Preguntas socráticas:
1) ¿Quién controla el acceso a la reconstrucción?
2) ¿Qué auditoría existe sobre el cambio biológico?
3) ¿Qué métrica define “mejora” y quién la define?

Acciones sugeridas:
- Definir criterios de bioética: consentimiento, justicia, transparencia.
- Implementar trazabilidad: datasets, hashes, auditoría.

Evidencia / Citas:
${citations}`
    };
  }

  function socratesSupport(q){
    const triage = classifyTicket({subject:q, steps:q});
    const citations = socratesCite(['datos','ética']);
    return {
      title: 'SOCRATES.AI — Soporte técnico',
      body:
`Diagnóstico preliminar (sin afirmar sin evidencia):
- Posible categoría: ${triage.category}
- Severidad sugerida: ${triage.severity}

Preguntas socráticas:
1) ¿Cuál es el dataset_id (ej: DS-ARBA-0012)?
2) ¿En qué etapa se atasca (Ingest/Normalize/QC/Analyze/Audit)?
3) ¿Tenés logs del job y hora aproximada?

Acciones sugeridas:
${triage.suggestions.map(s => `- ${s}`).join('\n')}

Evidencia / Citas:
${citations}`
    };
  }

  function socratesBio(q){
    const maybeFASTA = q.includes('>') || /[ACGTUN]{12,}/i.test(q.replace(/\s+/g,''));
    if (maybeFASTA){
      let fastaText = q.trim();
      if (!fastaText.startsWith('>')){
        const seq = q.replace(/[^ACGTUN]/gi,'').toUpperCase();
        fastaText = `>sample\n${seq}`;
      }
      const res = socratesAnalyzeFASTA(fastaText);
      return { title:'SOCRATES.AI — Análisis (FASTA)', body: res.report };
    }

    const citations = socratesCite(['fasta','fundamentos']);
    return {
      title: 'SOCRATES.AI — Biología & Datos',
      body:
`Puedo validar FASTA, calcular GC% y detectar motifs.
Pegá un FASTA (con cabecera ">") o una secuencia.

Evidencia / Citas:
${citations}`
    };
  }

  function socratesGeneric(q){
    const citations = socratesCite(['ética','fundamentos']);
    return {
      title: 'SOCRATES.AI — Respuesta',
      body:
`(Método socrático) Antes de responder, necesito precisión:

Preguntas:
1) ¿Cuál es tu objetivo: soporte, análisis biológico o arquitectura?
2) ¿Qué tipo de dato: FASTA, JSON de muestras, o telemetría?
3) ¿Qué salida esperás: explicación, validación, pipeline reproducible?

Acciones sugeridas:
- Pegá un fragmento mínimo reproducible (sin datos sensibles).
- Indicá rol y contexto (Researcher/Support/Admin).

Evidencia / Citas:
${citations}`
    };
  }

  function socratesAnswer(userText){
    const q = String(userText || '').trim();
    const lower = q.toLowerCase();

    if (/debat|ciencia vs|tecnolog/.test(lower)) return socratesDebate();
    if (/ticket|incidente|soporte|job|atasc/.test(lower)) return socratesSupport(q);
    if (/fasta|secuencia|gc|motif|adn|arn|json/.test(lower)) return socratesBio(q);
    return socratesGeneric(q);
  }

  /* ----------------------------- UI Compiler ----------------------------- */
  function canAccess(schema){ return schema.rolesAllowed.includes(state.role); }

  function renderDenied(schema){
    return `
      <div class="panel">
        <h1 class="h1">Acceso restringido</h1>
        <p class="lead">Tu rol actual (<span class="chip">${safeText(state.role)}</span>) no tiene permisos para <b>${safeText(schema.title)}</b>.</p>
        <div class="hr"></div>
        <p class="muted">Probá cambiar el rol arriba a la derecha.</p>
      </div>
    `;
  }

  function resolveKpi(source, metrics){
    if (typeof source === 'string' && source.startsWith('metrics:')){
      const key = source.split(':')[1];
      const v = metrics[key];
      if (typeof v === 'number'){
        const display = key.includes('mutation') || key.includes('diversity') || key.includes('pressure')
          ? formatPct(v) : String(v);
        return { display, hint: `source=${source}` };
      }
      return { display: String(v), hint: `source=${source}` };
    }
    return { display: '-', hint: `source=${source}` };
  }

  function resolveSource(source){
    const fn = api[source];
    if (!fn) return [];
    const out = fn();
    return Array.isArray(out) ? out : [];
  }

  function renderTable(columns, rows){
    const cols = columns || [];
    const body = (rows || []).map(r => {
      return `<tr>${cols.map(c => `<td>${safeText(r[c])}</td>`).join('')}</tr>`;
    }).join('');

    return `
      <table class="table" role="table">
        <thead>
          <tr>${cols.map(c => `<th scope="col">${safeText(c)}</th>`).join('')}</tr>
        </thead>
        <tbody>${body || `<tr><td colspan="${cols.length}"><span class="muted">Sin datos</span></td></tr>`}</tbody>
      </table>
    `;
  }

  function renderField(f){
    const name = safeText(f.name);
    const label = safeText(f.label || f.name);
    const placeholder = safeText(f.placeholder || '');
    const hint = safeText(f.hint || '');
    const required = f.required ? 'required' : '';
    const multiline = !!f.multiline;

    return `
      <div>
        <div class="label">${label}${f.required ? ' <span class="muted">(requerido)</span>' : ''}</div>
        ${multiline
          ? `<textarea class="input" name="${name}" placeholder="${placeholder}" ${required}></textarea>`
          : `<input class="input" name="${name}" placeholder="${placeholder}" ${required} />`
        }
        ${hint ? `<div class="help">${hint}</div>` : ``}
      </div>
    `;
  }

  function compileComponent(comp){
    const sizeClass = comp.size === 'half' ? 'half' : (comp.size === 'third' ? 'third' : '');
    const panel = document.createElement('div');
    panel.className = `panel ${sizeClass}`;

    switch (comp.type){
      case 'Hero':
        panel.innerHTML = `
          <h2 class="panelTitle">Home / Manifiesto</h2>
          <p class="lead"><span class="glitch" data-text="${safeText(comp.text)}">${safeText(comp.text)}</span></p>
          <div class="row">
            <span class="badge ok">✔ Realismo técnico</span>
            <span class="badge warn">⚠ Bioética</span>
            <span class="badge">▣ Auditoría</span>
            <span class="badge">⌁ Datos</span>
          </div>
        `;
        break;

      case 'CTA':
        panel.innerHTML = `
          <h2 class="panelTitle">Acciones</h2>
          <div class="row">
            ${comp.actions.map((a,i)=>`<button class="btn" data-cta="${i}">${safeText(a.label)}</button>`).join('')}
          </div>
          <p class="muted small">Navegación interna generada por el motor.</p>
        `;
        panel._cta = comp.actions;
        break;

      case 'Markdown':
        panel.innerHTML = `
          <h2 class="panelTitle">${safeText(comp.title || 'Documento')}</h2>
          <div class="body" style="white-space:pre-wrap; line-height:1.55; font-size:13px; color:rgba(255,255,255,0.82)">${safeText(comp.body || '')}</div>
        `;
        break;

      case 'KPIGroup': {
        const items = comp.items || [];
        const metrics = computeMetrics();
        panel.innerHTML = `
          <h2 class="panelTitle">${safeText(comp.title || 'KPIs')}</h2>
          <div class="kpis">
            ${items.map(it => {
              const val = resolveKpi(it.source, metrics);
              return `
                <div class="kpi">
                  <div class="kpiLabel">${safeText(it.label)}</div>
                  <div class="kpiValue">${safeText(val.display)}</div>
                  <div class="kpiHint">${safeText(val.hint)}</div>
                </div>`;
            }).join('')}
          </div>
        `;
        break;
      }

      case 'Table': {
        const rows = resolveSource(comp.source);
        panel.innerHTML = `
          <h2 class="panelTitle">${safeText(comp.title || 'Tabla')}</h2>
          ${renderTable(comp.columns || [], rows)}
          ${comp.source === 'jobs:list' ? `<p class="muted small">Tip: creá un job para ver progreso y logs.</p>` : ''}
        `;
        break;
      }

      case 'Form': {
        const fields = comp.fields || [];
        panel.innerHTML = `
          <h2 class="panelTitle">${safeText(comp.title || 'Formulario')}</h2>
          <form class="form" data-submitto="${safeText(comp.submitTo)}" data-validation="${safeText(comp.validation || '')}">
            ${fields.map(f => renderField(f)).join('')}
            <div class="row">
              <button class="btn" type="submit">Enviar</button>
              <span class="muted small" data-formstatus></span>
            </div>
          </form>
        `;
        break;
      }

      case 'Chat':
        panel.innerHTML = `
          <h2 class="panelTitle">${safeText(comp.title || 'Chat')}</h2>
          <div class="chat">
            <div class="chatLog" id="chatLog" aria-label="Historial de chat"></div>
            <div class="row">
              <input class="input" id="chatInput" placeholder="Escribí tu consulta..." aria-label="Escribir consulta"/>
              <button class="btn" id="chatSend">Enviar</button>
            </div>
            <div class="help">${safeText(comp.hint || '')}</div>
          </div>
        `;
        break;

      default:
        panel.innerHTML = `<div class="muted">Componente no soportado: ${safeText(comp.type)}</div>`;
    }

    return panel;
  }

  function bindDynamicHandlers(){
    // CTAs
    $$('[data-cta]').forEach(btn => {
      btn.addEventListener('click', () => {
        const parentPanel = btn.closest('.panel');
        const actions = parentPanel?._cta || [];
        const idx = Number(btn.getAttribute('data-cta'));
        const a = actions[idx];
        if (a && a.route) navigate(a.route);
      }, { once:true });
    });

    // Forms
    $$('form[data-submitto]').forEach(form => {
      form.addEventListener('submit', (e) => {
        e.preventDefault();

        const submitTo = form.getAttribute('data-submitto');
        const validation = form.getAttribute('data-validation') || '';
        const statusEl = $('[data-formstatus]', form);

        const data = {};
        for (const el of Array.from(form.elements)){
          if (!el.name) continue;
          data[el.name] = el.value;
        }

        // Validación
        let errs = [];
        if (validation === 'job') errs = validateJob(data);
        if (validation === 'ticket') errs = validateTicket(data);
        if (validation === 'fasta'){
          const p = parseFASTA(data.fasta);
          if (!p.ok) errs = [p.error];
        }

        if (errs.length){
          if (statusEl) statusEl.textContent = `❌ ${errs[0]}`;
          trace(`form:error ${submitTo} ${errs[0]}`);
          return;
        }

        // “API call”
        const fn = api[submitTo];
        if (!fn){
          if (statusEl) statusEl.textContent = `❌ endpoint no existe: ${submitTo}`;
          trace(`api:missing ${submitTo}`);
          return;
        }

        const res = fn(data);

        if (submitTo === 'tickets:create'){
          if (statusEl) statusEl.textContent = `✅ Ticket creado: ${res.ticket.id}`;
          form.reset();
          renderRoute();
        } else if (submitTo === 'jobs:start'){
          if (statusEl) statusEl.textContent = `✅ Job iniciado: ${res.job.id}`;
          form.reset();
          renderRoute();
        } else if (submitTo === 'socrates:analyze_fasta'){
          if (statusEl) statusEl.textContent = res.ok ? '✅ Análisis completado' : '⚠ Revisá el formato';
          appendChat('user', 'Analiza este FASTA (form)');
          appendChat('ai', res.report);
        } else {
          if (statusEl) statusEl.textContent = '✅ Enviado';
        }

        refreshSidebarCounts();
      }, { once:true });
    });

    // Chat
    const chatSend = $('#chatSend');
    const chatInput = $('#chatInput');
    if (chatSend && chatInput){
      chatSend.addEventListener('click', () => {
        const text = chatInput.value.trim();
        if (!text) return;
        chatInput.value = '';
        appendChat('user', text);
        const ans = socratesAnswer(text);
        appendChat('ai', `${ans.title}\n\n${ans.body}`);
      });

      chatInput.addEventListener('keydown', (e) => {
        if (e.key === 'Enter'){
          e.preventDefault();
          chatSend.click();
        }
      });

      const log = $('#chatLog');
      if (log && !log.dataset.seeded){
        log.dataset.seeded = '1';
        appendChat('ai',
`SOCRATES.AI — inicializado
- No adivino: pido evidencia.
- Cito knowledge_base.
- Analizo FASTA (demo).
Escribí tu consulta o usá el analizador rápido.`);
      }
    }
  }

  function renderRoute(){
    const schema = schemas[state.route] || schemas.home;

    // nav current
    $$('.navBtn').forEach(b => {
      const r = b.getAttribute('data-route');
      b.setAttribute('aria-current', r === state.route ? 'page' : 'false');
    });

    if (!canAccess(schema)){
      trace(`access:denied route=${schema.page} role=${state.role}`);
      $('#app').innerHTML = renderDenied(schema);
      return;
    }

    trace(`compile:begin route=${schema.page}`);
    $('#app').innerHTML = '';

    const root = document.createElement('div');
    root.className = 'grid';

    const header = document.createElement('div');
    header.className = 'panel';
    header.innerHTML = `
      <h1 class="h1 glitch" data-text="${safeText(schema.title)}">${safeText(schema.title)}</h1>
      <p class="lead">Interfaz generada por esquema · rol: <span class="chip">${safeText(state.role)}</span></p>
    `;
    root.appendChild(header);

    for (const comp of schema.components){
      const node = compileComponent(comp);
      if (node) root.appendChild(node);
    }

    $('#app').appendChild(root);
    bindDynamicHandlers();
    trace(`compile:done route=${schema.page}`);
    refreshSidebarCounts();
  }

  function renderRouteLight(){ renderRoute(); }

  /* ----------------------------- Navegación y UI ----------------------------- */
  function navigate(route){
    if (!schemas[route]) route = 'home';
    state.route = route;
    renderRoute();
  }

  function refreshSidebarCounts(){
    $('#jobCount').textContent = String(state.jobs.length);
    $('#ticketCount').textContent = String(state.tickets.length);
  }

  function startUptime(){
    setInterval(() => {
      const s = Math.floor((Date.now() - state.bootTime)/1000);
      const hh = String(Math.floor(s/3600)).padStart(2,'0');
      const mm = String(Math.floor((s%3600)/60)).padStart(2,'0');
      const ss = String(s%60).padStart(2,'0');
      $('#uptime').textContent = `${hh}:${mm}:${ss}`;
    }, 250);
  }

  function exportJSON(){
    const metrics = computeMetrics();
    const out = {
      exported_at: nowISO(),
      role: state.role,
      metrics,
      datasets: state.datasets,
      genomes: state.genomes,
      tickets: state.tickets,
      jobs: state.jobs
    };
    download('bioreconstruct_export.json', JSON.stringify(out, null, 2), 'application/json');
    trace('export:json ok');
  }

  function exportCSV(){
    const rows = state.datasets.map(d => ({
      id: d.id,
      lineage: d.lineage,
      created_at: d.created_at,
      hash: d.hash,
      notes: d.notes
    }));
    download('bioreconstruct_datasets.csv', toCSV(rows), 'text/csv');
    trace('export:csv ok');
  }

  function appendChat(who, text){
    const log = $('#chatLog');
    if (!log) return;
    const msg = document.createElement('div');
    msg.className = `msg ${who === 'user' ? 'user' : 'ai'}`;

    const meta = who === 'user'
      ? `user@${state.role} · ${new Date().toLocaleTimeString()}`
      : `socrates.ai · ${new Date().toLocaleTimeString()}`;

    msg.innerHTML = `<div class="meta">${safeText(meta)}</div><div class="body">${safeText(text)}</div>`;
    log.appendChild(msg);
    log.scrollTop = log.scrollHeight;
  }

  /* ----------------------------- Canvas original ----------------------------- */
  function roundRect(ctx, x, y, w, h, r){
    const rr = Math.min(r, w/2, h/2);
    ctx.beginPath();
    ctx.moveTo(x+rr, y);
    ctx.arcTo(x+w, y, x+w, y+h, rr);
    ctx.arcTo(x+w, y+h, x, y+h, rr);
    ctx.arcTo(x, y+h, x, y, rr);
    ctx.arcTo(x, y, x+w, y, rr);
    ctx.closePath();
  }

  function drawSkyline(ctx, w, h, t){
    const baseY = h * 0.72;
    ctx.fillStyle = 'rgba(0,0,0,0.30)';
    ctx.fillRect(0, baseY, w, h-baseY);

    const n = 26;
    for (let i=0;i<n;i++){
      const bw = 40 + (i%5)*10;
      const bx = (i * (w/n)) - 10;
      const bh = 80 + (i%7)*28;
      ctx.fillStyle = 'rgba(0,0,0,0.50)';
      ctx.fillRect(bx, baseY - bh, bw, bh);

      const flick = 0.35 + 0.35*Math.sin((t/1000) + i);
      ctx.fillStyle = `rgba(127,92,255,${0.10 + 0.20*flick})`;
      for (let y=baseY-bh+10; y<baseY-8; y+=14){
        for (let x=bx+6; x<bx+bw-6; x+=10){
          if ((x+y+i) % 3 === 0) ctx.fillRect(x,y,4,6);
        }
      }
    }

    const haze = ctx.createLinearGradient(0, baseY-200, 0, baseY+120);
    haze.addColorStop(0,'rgba(0,212,255,0.00)');
    haze.addColorStop(1,'rgba(0,212,255,0.08)');
    ctx.fillStyle = haze;
    ctx.fillRect(0, baseY-240, w, 320);
  }

  function drawDrone(ctx, x, y){
    const glow = state.safeMode ? 0.08 : 0.18;
    ctx.save();
    ctx.translate(x, y);

    ctx.fillStyle = 'rgba(255,255,255,0.10)';
    roundRect(ctx, -18, -8, 36, 16, 8);
    ctx.fill();

    ctx.strokeStyle = `rgba(0,212,255,${glow})`;
    ctx.lineWidth = 2;
    ctx.beginPath();
    ctx.arc(0,0,18,0,Math.PI*2);
    ctx.stroke();

    ctx.fillStyle = `rgba(70,255,154,${glow})`;
    ctx.fillRect(-3,-2,6,4);

    ctx.strokeStyle = `rgba(127,92,255,${glow*0.7})`;
    ctx.beginPath();
    ctx.moveTo(-20,0); ctx.lineTo(-28,0);
    ctx.moveTo(20,0); ctx.lineTo(28,0);
    ctx.stroke();

    ctx.restore();
  }

  function drawRibosomeToChip(ctx, w, h, t){
    const cx = w*0.62, cy = h*0.40;
    const time = (t/1000) % 8;
    const k = time < 4 ? time/4 : 1 - (time-4)/4;
    const glow = state.safeMode ? 0.10 : 0.22;

    const rg = ctx.createRadialGradient(cx, cy, 10, cx, cy, 160);
    rg.addColorStop(0, `rgba(0,212,255,${glow})`);
    rg.addColorStop(0.55, `rgba(127,92,255,${glow*0.6})`);
    rg.addColorStop(1, 'rgba(0,0,0,0)');
    ctx.fillStyle = rg;
    ctx.fillRect(cx-180, cy-180, 360, 360);

    const ribR = 54;
    const chipS = 120;

    const ribAlpha = 1 - k;
    ctx.fillStyle = `rgba(255,255,255,${0.12*ribAlpha})`;
    ctx.strokeStyle = `rgba(70,255,154,${0.30*ribAlpha})`;
    ctx.lineWidth = 2;

    ctx.beginPath();
    ctx.ellipse(cx-12, cy-14, ribR*0.70, ribR*0.52, 0.3, 0, Math.PI*2);
    ctx.fill(); ctx.stroke();

    ctx.beginPath();
    ctx.ellipse(cx+10, cy+18, ribR*0.76, ribR*0.58, -0.25, 0, Math.PI*2);
    ctx.fill(); ctx.stroke();

    ctx.strokeStyle = `rgba(0,212,255,${0.22*ribAlpha})`;
    ctx.lineWidth = 3;
    ctx.beginPath();
    ctx.moveTo(cx-140, cy+34);
    ctx.bezierCurveTo(cx-90, cy+18, cx-40, cy+60, cx+140, cy+40);
    ctx.stroke();

    const chipAlpha = k;
    ctx.fillStyle = `rgba(255,255,255,${0.08*chipAlpha})`;
    ctx.strokeStyle = `rgba(0,212,255,${0.34*chipAlpha})`;
    ctx.lineWidth = 2;

    roundRect(ctx, cx-chipS/2, cy-chipS/2, chipS, chipS, 16);
    ctx.fill(); ctx.stroke();

    ctx.strokeStyle = `rgba(127,92,255,${0.30*chipAlpha})`;
    ctx.lineWidth = 2;
    for (let i=0;i<8;i++){
      const px = cx - chipS/2 + 14 + i*12;
      ctx.beginPath();
      ctx.moveTo(px, cy-chipS/2); ctx.lineTo(px, cy-chipS/2 - 10);
      ctx.moveTo(px, cy+chipS/2); ctx.lineTo(px, cy+chipS/2 + 10);
      ctx.stroke();
    }
    for (let i=0;i<8;i++){
      const py = cy - chipS/2 + 14 + i*12;
      ctx.beginPath();
      ctx.moveTo(cx-chipS/2, py); ctx.lineTo(cx-chipS/2 - 10, py);
      ctx.moveTo(cx+chipS/2, py); ctx.lineTo(cx+chipS/2 + 10, py);
      ctx.stroke();
    }

    ctx.fillStyle = `rgba(70,255,154,${0.20*chipAlpha})`;
    ctx.beginPath();
    ctx.arc(cx, cy, 12, 0, Math.PI*2);
    ctx.fill();

    ctx.fillStyle = `rgba(255,255,255,${0.35*(0.35+0.65*chipAlpha)})`;
    ctx.font = `12px ${getComputedStyle(document.documentElement).getPropertyValue('--mono')}`;
    ctx.fillText('RIBOSOME → COMPILER', cx-86, cy+78);
  }

  function startCanvas(){
    const canvas = $('#scene');
    const ctx = canvas.getContext('2d', { alpha: true });

    function resize(){
      const dpr = window.devicePixelRatio || 1;
      const w = Math.floor(window.innerWidth);
      const h = Math.floor(window.innerHeight);
      canvas.width = Math.floor(w * dpr);
      canvas.height = Math.floor(h * dpr);
      canvas.style.width = w+'px';
      canvas.style.height = h+'px';
      ctx.setTransform(dpr,0,0,dpr,0,0);
    }
    window.addEventListener('resize', resize);
    resize();

    const rain = Array.from({length: 140}, () => ({
      x: Math.random()*window.innerWidth,
      y: Math.random()*window.innerHeight,
      v: 220 + Math.random()*260,
      l: 10 + Math.random()*20
    }));

    const drones = Array.from({length: 6}, (_,i)=>({
      x: (i+1)*140 + Math.random()*80,
      y: 120 + Math.random()*120,
      vx: (Math.random()*0.6 + 0.2) * (Math.random()<0.5?-1:1),
      phase: Math.random()*Math.PI*2
    }));

    let t0 = performance.now();
    function loop(t){
      const dt = (t - t0)/1000;
      t0 = t;

      const w = window.innerWidth;
      const h = window.innerHeight;

      const g = ctx.createLinearGradient(0,0,0,h);
      g.addColorStop(0, 'rgba(6,6,14,1)');
      g.addColorStop(0.55, 'rgba(9,8,18,1)');
      g.addColorStop(1, 'rgba(4,4,10,1)');
      ctx.fillStyle = g;
      ctx.fillRect(0,0,w,h);

      drawSkyline(ctx, w, h, t);

      ctx.strokeStyle = state.safeMode ? 'rgba(255,255,255,0.10)' : 'rgba(0,212,255,0.16)';
      ctx.lineWidth = 1;
      ctx.beginPath();
      for (const r of rain){
        r.y += r.v*dt;
        r.x += 40*dt;
        if (r.y > h + 30){ r.y = -20; r.x = Math.random()*w; }
        if (r.x > w + 30){ r.x = -20; }
        ctx.moveTo(r.x, r.y);
        ctx.lineTo(r.x + 2, r.y + r.l);
      }
      ctx.stroke();

      drawRibosomeToChip(ctx, w, h, t);

      for (const d of drones){
        d.phase += dt;
        d.x += d.vx * 40 * dt;
        d.y += Math.sin(d.phase) * 10 * dt;
        if (d.x < -60) d.x = w + 60;
        if (d.x > w + 60) d.x = -60;
        drawDrone(ctx, d.x, d.y);
      }

      requestAnimationFrame(loop);
    }
    requestAnimationFrame(loop);
  }

  /* ----------------------------- Bind global ----------------------------- */
  function bindGlobal(){
    $$('.navBtn').forEach(btn => {
      btn.addEventListener('click', () => navigate(btn.getAttribute('data-route')));
    });

    $('#roleSelect').addEventListener('change', (e) => {
      state.role = e.target.value;
      trace(`role:set ${state.role}`);
      renderRoute();
    });

    $('#panicBtn').addEventListener('click', () => {
      state.safeMode = !state.safeMode;
      document.body.classList.toggle('safe', state.safeMode);
      trace(`safeMode:${state.safeMode ? 'on' : 'off'}`);
    });

    $('#exportJson').addEventListener('click', exportJSON);
    $('#exportCsv').addEventListener('click', exportCSV);
  }

  /* ----------------------------- Boot ----------------------------- */
  function boot(){
    bindGlobal();
    startUptime();
    startCanvas();
    refreshSidebarCounts();

    trace('boot:init ok');
    trace('canvas:ready ok');
    trace('compiler:ready ok');

    navigate('home');
  }

  boot();
  </script>
</body>
</html>

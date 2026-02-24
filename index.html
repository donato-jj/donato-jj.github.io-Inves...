<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="color-scheme" content="dark" />
  <title>BIORECONSTRUCT™ — Plataforma (Single File Pro)</title>

  <!--
    CSP para demo en archivo único.
    Nota: 'unsafe-inline' se usa porque CSS/JS están embebidos (single file).
    En producción: mover CSS/JS a archivos separados y eliminar unsafe-inline.
  -->
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
      --panel2: rgba(10, 10, 18, 0.78);
      --stroke: rgba(255,255,255,0.10);
      --stroke2: rgba(255,255,255,0.16);
      --text: rgba(255,255,255,0.92);
      --muted: rgba(255,255,255,0.62);
      --muted2: rgba(255,255,255,0.48);

      --neon-a: #00d4ff;
      --neon-b: #7f5cff;
      --neon-c: #46ff9a;

      --danger: #ff3b6b;
      --warn: #ffc14d;
      --ok: #46ff9a;

      --shadow: 0 18px 60px rgba(0,0,0,0.45);
      --shadow2: 0 12px 40px rgba(0,0,0,0.35);

      --radius: 16px;
      --radius2: 22px;
      --radius3: 28px;

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

    /* Background */
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
      box-shadow: var(--shadow2);
    }
    .brandText{ display:flex; flex-direction:column; line-height: 1.1; }
    .brandName{ font-weight: 900; letter-spacing: 0.6px; }
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
      font-weight: 700;
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
    .rolePill{
      display:flex; align-items:center; gap: 8px;
      padding: 8px 10px;
      background: rgba(255,255,255,0.04);
      border: 1px solid var(--stroke);
      border-radius: 14px;
      font-family: var(--mono);
      font-size: 12px;
      color: rgba(255,255,255,0.86);
    }
    .pillDot{
      width:8px; height:8px; border-radius:999px;
      background: rgba(70,255,154,0.8);
      box-shadow: 0 0 16px rgba(70,255,154,0.25);
    }
    .panic{
      appearance:none;
      border: 1px solid rgba(255,59,107,0.35);
      background: rgba(255,59,107,0.10);
      color: var(--text);
      padding: 10px 12px;
      border-radius: 14px;
      cursor:pointer;
      font-weight: 800;
    }
    .acctBtn{
      appearance:none;
      border: 1px solid rgba(0,212,255,0.25);
      background: rgba(0,212,255,0.06);
      color: var(--text);
      padding: 10px 12px;
      border-radius: 14px;
      cursor:pointer;
      font-weight: 800;
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
    .muted2{ color: var(--muted2); }
    .small{ font-size: 12px; line-height: 1.35; }
    .row{ display:flex; gap: 10px; flex-wrap: wrap; align-items:center; }
    .btn{
      appearance:none;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,0.05);
      color: var(--text);
      padding: 10px 12px;
      border-radius: 14px;
      cursor:pointer;
      font-weight: 800;
    }
    .btn:hover{ border-color: var(--stroke2); }
    .btn.primary{
      border-color: rgba(0,212,255,0.35);
      background: rgba(0,212,255,0.10);
    }
    .btn.ghost{
      border-color: rgba(255,255,255,0.10);
      background: rgba(255,255,255,0.02);
    }
    .btn.danger{
      border-color: rgba(255,59,107,0.35);
      background: rgba(255,59,107,0.10);
    }

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
      font-size: 12px;
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
    .kpiValue{ font-size: 22px; font-weight: 900; margin-top: 6px; }
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
      vertical-align: top;
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
    .label{ font-size: 12px; color: var(--muted); display:flex; align-items:center; justify-content:space-between; }
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
    .input:focus, textarea:focus{
      border-color: rgba(0,212,255,0.35);
      box-shadow: 0 0 0 2px rgba(0,212,255,0.12);
    }
    textarea{ min-height: 120px; resize: vertical; }
    .help{ font-size: 12px; color: rgba(255,255,255,0.70); line-height: 1.4; }
    .error{ font-size: 12px; color: rgba(255,59,107,0.95); font-family: var(--mono); }

    .badge{
      display:inline-flex;
      gap: 6px;
      align-items:center;
      padding: 4px 10px;
      border-radius: 999px;
      font-size: 12px;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,0.03);
      font-family: var(--mono);
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

    /* Auth overlay */
    .overlay{
      position: fixed; inset: 0;
      display:none;
      z-index: 100;
      align-items: center;
      justify-content: center;
      padding: 18px;
      background: rgba(0,0,0,0.60);
      backdrop-filter: blur(12px);
    }
    .overlay.show{ display:flex; }
    .modal{
      width: min(980px, 100%);
      border-radius: var(--radius3);
      border: 1px solid rgba(255,255,255,0.12);
      background: linear-gradient(180deg, rgba(16,16,26,0.92), rgba(10,10,18,0.88));
      box-shadow: var(--shadow);
      overflow:hidden;
    }
    .modalHead{
      display:flex;
      align-items:center;
      justify-content: space-between;
      gap: 10px;
      padding: 14px 16px;
      border-bottom: 1px solid rgba(255,255,255,0.10);
      background: rgba(255,255,255,0.03);
    }
    .modalTitle{
      display:flex;
      align-items:center;
      gap: 10px;
      font-weight: 900;
      letter-spacing: 0.3px;
    }
    .modalBody{
      display:grid;
      grid-template-columns: 1.1fr 1fr;
      gap: 14px;
      padding: 16px;
    }
    .authInfo{
      border: 1px solid rgba(255,255,255,0.10);
      background: rgba(255,255,255,0.02);
      border-radius: var(--radius2);
      padding: 14px;
    }
    .authInfo h3{ margin: 0 0 8px; font-size: 14px; letter-spacing:0.4px; text-transform: uppercase; }
    .authInfo p{ margin: 0 0 8px; color: rgba(255,255,255,0.78); line-height: 1.55; font-size: 13px; }
    .authInfo .note{ color: var(--muted); font-size: 12px; }
    .authTabs{
      display:flex;
      gap: 8px;
      padding: 8px;
      border: 1px solid rgba(255,255,255,0.10);
      border-radius: 999px;
      background: rgba(255,255,255,0.02);
      width: fit-content;
      margin-bottom: 10px;
    }
    .tab{
      appearance:none;
      border: 1px solid transparent;
      background: transparent;
      color: rgba(255,255,255,0.82);
      padding: 8px 10px;
      border-radius: 999px;
      cursor:pointer;
      font-weight: 800;
      font-family: var(--mono);
      font-size: 12px;
    }
    .tab.active{
      border-color: rgba(0,212,255,0.35);
      background: rgba(0,212,255,0.08);
      color: rgba(255,255,255,0.92);
    }
    .modalFoot{
      display:flex;
      align-items:center;
      justify-content: space-between;
      gap: 12px;
      padding: 12px 16px;
      border-top: 1px solid rgba(255,255,255,0.10);
      background: rgba(255,255,255,0.03);
    }
    .xBtn{
      appearance:none;
      border: 1px solid rgba(255,255,255,0.12);
      background: rgba(255,255,255,0.04);
      color: rgba(255,255,255,0.86);
      border-radius: 12px;
      padding: 8px 10px;
      cursor:pointer;
      font-weight: 900;
    }

    /* Toast */
    .toasts{
      position: fixed;
      right: 14px;
      bottom: 14px;
      z-index: 200;
      display:flex;
      flex-direction: column;
      gap: 10px;
      width: min(420px, calc(100vw - 28px));
      pointer-events:none;
    }
    .toast{
      pointer-events:none;
      border: 1px solid rgba(255,255,255,0.12);
      background: rgba(10,10,18,0.86);
      border-radius: 16px;
      padding: 10px 12px;
      box-shadow: var(--shadow2);
      backdrop-filter: blur(10px);
    }
    .toast .tTitle{
      font-weight: 900;
      font-size: 12px;
      letter-spacing: 0.4px;
      text-transform: uppercase;
      color: rgba(255,255,255,0.92);
    }
    .toast .tBody{
      margin-top: 6px;
      font-size: 13px;
      color: rgba(255,255,255,0.78);
      line-height: 1.4;
      white-space: pre-wrap;
    }
    .toast.ok{ border-color: rgba(70,255,154,0.22); }
    .toast.warn{ border-color: rgba(255,193,77,0.22); }
    .toast.err{ border-color: rgba(255,59,107,0.22); }

    /* Responsive */
    @media(max-width: 980px){
      .main{ grid-template-columns: 1fr; }
      .brand{ min-width: 0; }
      .modalBody{ grid-template-columns: 1fr; }
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
        <div class="brandTag">Plataforma · Biotecnología · Datos · Soporte · SOCRATES.AI</div>
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
      <div class="rolePill" title="Rol efectivo por sesión">
        <span class="pillDot" aria-hidden="true"></span>
        <span id="roleText">Visitor</span>
      </div>
      <button id="acctBtn" class="acctBtn" title="Cuenta y sesión">Cuenta</button>
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
          <div class="k">Sesión</div><div class="v" id="sessionState">—</div>
          <div class="k">Jobs</div><div class="v" id="jobCount">0</div>
          <div class="k">Tickets</div><div class="v" id="ticketCount">0</div>
        </div>
        <div class="divider"></div>
        <p class="muted small">
          Demo single-file sin backend. La autenticación es local (localStorage) y sirve para modelar permisos/roles.
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
        <div class

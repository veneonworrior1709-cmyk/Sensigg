
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>SENSI.GG — BGMI Sensitivity Calculator</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #070710;
  --surface: #0d0d1a;
  --surface2: #111120;
  --cyan: #00d4ff;
  --orange: #ff6b35;
  --purple: #a855f7;
  --gold: #ffd700;
  --text: #c8cfe0;
  --muted: #445566;
  --border: rgba(255,255,255,0.07);
}
*{box-sizing:border-box;margin:0;padding:0;}
html,body{background:var(--bg);color:var(--text);font-family:'Rajdhani',sans-serif;min-height:100vh;overflow-x:hidden;}
body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(0,212,255,0.018) 1px,transparent 1px),linear-gradient(90deg,rgba(0,212,255,0.018) 1px,transparent 1px);background-size:36px 36px;pointer-events:none;z-index:0;}
::-webkit-scrollbar{width:3px;}
::-webkit-scrollbar-track{background:#0a0a14;}
::-webkit-scrollbar-thumb{background:#00d4ff33;border-radius:2px;}

/* NAV */
nav{position:fixed;top:0;left:0;right:0;z-index:100;height:50px;background:rgba(7,7,16,0.95);backdrop-filter:blur(14px);border-bottom:1px solid rgba(0,212,255,0.12);display:flex;align-items:center;justify-content:space-between;padding:0 16px;}
.nav-logo{font-family:'Orbitron',monospace;font-size:17px;font-weight:900;background:linear-gradient(135deg,#fff,#00d4ff);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;cursor:pointer;border:none;}
.btn-primary{padding:8px 18px;font-size:10px;font-family:'Orbitron',monospace;letter-spacing:1px;background:linear-gradient(135deg,#00a8c8,#00d4ff);border:none;color:#000;font-weight:700;cursor:pointer;clip-path:polygon(6px 0%,100% 0%,calc(100% - 6px) 100%,0% 100%);}
.btn-ghost{padding:8px 16px;font-size:10px;font-family:'Orbitron',monospace;letter-spacing:1px;background:transparent;border:1px solid var(--border);color:var(--muted);cursor:pointer;}
.btn-ghost:hover{border-color:rgba(0,212,255,0.3);color:var(--cyan);}

/* PAGES */
.page{display:none;position:relative;z-index:1;padding-top:50px;}
.page.active{display:block;}

/* HOME */
.hero{min-height:calc(100vh - 50px);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:40px 20px;text-align:center;}
.hero-badge{font-size:9px;letter-spacing:4px;color:rgba(0,212,255,0.5);font-family:'Orbitron',monospace;margin-bottom:16px;padding:4px 14px;border:1px solid rgba(0,212,255,0.2);display:inline-block;}
.hero-title{font-family:'Orbitron',monospace;font-weight:900;font-size:clamp(56px,18vw,110px);letter-spacing:6px;line-height:0.88;background:linear-gradient(135deg,#ffffff 0%,#00d4ff 60%,#a855f7 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;filter:drop-shadow(0 0 40px rgba(0,212,255,0.18));}
.hero-sub{margin-top:20px;font-size:14px;color:var(--muted);letter-spacing:1px;line-height:1.7;max-width:340px;}
.hero-cta{margin-top:32px;padding:16px 36px;font-size:13px;font-family:'Orbitron',monospace;font-weight:700;letter-spacing:2px;background:linear-gradient(135deg,#00a8c8,#00d4ff);border:none;color:#000;cursor:pointer;clip-path:polygon(10px 0%,100% 0%,calc(100% - 10px) 100%,0% 100%);box-shadow:0 0 30px rgba(0,212,255,0.25);}

/* PRO SECTION */
.section-wrap{max-width:520px;margin:0 auto;padding:40px 16px;}
.section-eyebrow{font-size:9px;letter-spacing:3px;color:rgba(0,212,255,0.4);font-family:'Orbitron',monospace;margin-bottom:8px;}
.section-heading{font-family:'Orbitron',monospace;font-size:16px;color:#fff;margin-bottom:20px;}
.pro-row{display:flex;align-items:center;justify-content:space-between;padding:13px 16px;background:rgba(255,255,255,0.025);border:none;border-left:3px solid rgba(0,212,255,0.25);cursor:pointer;transition:all 0.15s;text-align:left;width:100%;margin-bottom:1px;}
.pro-row:hover{background:rgba(0,212,255,0.06);border-left-color:var(--cyan);}
.pro-name{font-family:'Orbitron',monospace;font-size:13px;color:#fff;font-weight:700;}
.pro-team{font-size:10px;color:var(--muted);letter-spacing:1px;margin-top:2px;}
.pro-stats{display:flex;gap:16px;align-items:center;}
.pro-stat{text-align:right;}
.pro-stat-label{font-size:9px;color:#334;letter-spacing:1px;margin-bottom:2px;}
.pro-stat-val{font-family:'Orbitron',monospace;font-size:13px;}
.arrow{color:#334;font-size:12px;margin-left:4px;}

/* GENERATOR */
.gen-wrap{max-width:520px;margin:0 auto;padding:16px;}
.progress-bar-row{display:flex;gap:4px;margin-bottom:6px;}
.progress-bar-seg{flex:1;height:2px;background:rgba(255,255,255,0.07);transition:background 0.3s;}
.progress-bar-seg.done{background:var(--cyan);}
.progress-labels{display:flex;justify-content:space-between;margin-bottom:20px;}
.progress-label{font-size:9px;letter-spacing:2px;text-transform:uppercase;font-family:'Orbitron',monospace;color:var(--muted);}
.progress-label.active{color:var(--cyan);}

.step-panel{background:var(--surface);border:1px solid var(--border);padding:20px 16px;margin-bottom:16px;}
.field-label{font-size:10px;letter-spacing:2px;color:var(--muted);text-transform:uppercase;font-family:'Orbitron',monospace;margin-bottom:10px;}
.field-group{margin-bottom:22px;}
.chip-row{display:flex;flex-wrap:wrap;gap:6px;}
.chip{padding:8px 13px;font-size:11px;font-family:'Orbitron',monospace;letter-spacing:0.5px;background:rgba(255,255,255,0.04);border:1px solid rgba(255,255,255,0.08);color:var(--muted);cursor:pointer;transition:all 0.15s;}
.chip.active-cyan{background:rgba(0,212,255,0.12);border-color:rgba(0,212,255,0.4);color:var(--cyan);}
.chip.active-orange{background:rgba(255,107,53,0.12);border-color:rgba(255,107,53,0.4);color:var(--orange);}
.chip.active-purple{background:rgba(168,85,247,0.12);border-color:rgba(168,85,247,0.4);color:var(--purple);}
.chip.active-gold{background:rgba(255,215,0,0.12);border-color:rgba(255,215,0,0.4);color:var(--gold);}
.issue-btn{width:100%;text-align:left;padding:10px 14px;background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.07);color:#778;font-size:12px;cursor:pointer;font-family:'Rajdhani',sans-serif;font-weight:500;transition:all 0.15s;margin-bottom:6px;}
.issue-btn.active{background:rgba(255,107,53,0.1);border-color:rgba(255,107,53,0.35);color:#ff9060;}

.btn-row{display:flex;gap:8px;}
.btn-back{flex:1;padding:12px;font-size:10px;font-family:'Orbitron',monospace;background:transparent;border:1px solid var(--border);color:var(--muted);cursor:pointer;letter-spacing:1px;}
.btn-next{flex:2;padding:12px;font-size:11px;font-family:'Orbitron',monospace;font-weight:700;letter-spacing:1px;background:linear-gradient(135deg,#00a8c8,#00d4ff);border:none;color:#000;cursor:pointer;clip-path:polygon(8px 0%,100% 0%,calc(100% - 8px) 100%,0% 100%);}

input[type=range]{-webkit-appearance:none;width:100%;height:3px;background:rgba(255,255,255,0.08);outline:none;cursor:pointer;border-radius:2px;}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:14px;height:14px;border-radius:50%;cursor:pointer;transition:transform 0.15s;}
input[type=range]::-webkit-slider-thumb:hover{transform:scale(1.35);}
#range-kd::-webkit-slider-thumb{background:var(--cyan);box-shadow:0 0 8px var(--cyan);}

/* RESULTS */
.results-wrap{max-width:520px;margin:0 auto;}
.results-topbar{display:flex;align-items:center;justify-content:space-between;padding:14px 16px;border-bottom:1px solid var(--border);}
.results-title-main{font-family:'Orbitron',monospace;font-size:13px;color:#fff;font-weight:700;}
.results-subtitle{font-size:10px;color:var(--muted);letter-spacing:1px;margin-top:2px;}
.results-actions{display:flex;gap:8px;}
.btn-edit{padding:6px 12px;font-size:10px;font-family:'Orbitron',monospace;letter-spacing:1px;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);color:var(--muted);cursor:pointer;}
.btn-edit.on{background:rgba(0,212,255,0.12);border-color:rgba(0,212,255,0.35);color:var(--cyan);}
.btn-copy-all{padding:6px 12px;font-size:10px;font-family:'Orbitron',monospace;letter-spacing:1px;background:rgba(255,215,0,0.1);border:1px solid rgba(255,215,0,0.3);color:var(--gold);cursor:pointer;}

.tab-bar{display:flex;background:rgba(0,0,0,0.3);border-bottom:1px solid var(--border);}
.tab-btn{flex:1;padding:11px 4px;font-size:10px;font-family:'Orbitron',monospace;letter-spacing:1px;text-transform:uppercase;background:transparent;border:none;border-bottom:2px solid transparent;color:var(--muted);cursor:pointer;transition:all 0.15s;}
.tab-btn.active-cyan{background:rgba(255,255,255,0.04);border-bottom-color:var(--cyan);color:var(--cyan);}
.tab-btn.active-orange{background:rgba(255,255,255,0.04);border-bottom-color:var(--orange);color:var(--orange);}
.tab-btn.active-purple{background:rgba(255,255,255,0.04);border-bottom-color:var(--purple);color:var(--purple);}
.tab-btn.active-gold{background:rgba(255,255,255,0.04);border-bottom-color:var(--gold);color:var(--gold);}

.tab-content{display:none;}
.tab-content.active{display:block;}

.section-block{margin-bottom:2px;}
.section-hdr{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background:rgba(255,255,255,0.03);border:none;border-left:3px solid var(--cyan);cursor:pointer;width:100%;transition:background 0.15s;}
.section-hdr:hover{background:rgba(255,255,255,0.055);}
.section-hdr-title{font-family:'Orbitron',monospace;font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;}
.section-hdr-sub{font-size:10px;color:var(--muted);margin-top:2px;letter-spacing:1px;}
.section-hdr-arrow{color:var(--muted);font-size:14px;transition:transform 0.2s;}
.section-hdr-arrow.open{transform:rotate(180deg);}
.section-body{background:rgba(0,0,0,0.18);}
.section-body.hidden{display:none;}

.sens-row{display:flex;align-items:center;gap:10px;padding:11px 14px;background:rgba(255,255,255,0.025);border-bottom:1px solid rgba(255,255,255,0.04);transition:background 0.12s;}
.sens-row:hover{background:rgba(255,255,255,0.045);}
.sens-row-icon{font-size:12px;width:16px;text-align:center;flex-shrink:0;}
.sens-row-label{flex:1;font-size:12px;color:#b0b8cc;font-family:'Rajdhani',sans-serif;font-weight:500;letter-spacing:0.3px;}
.sens-bar-wrap{width:80px;height:3px;background:rgba(255,255,255,0.08);border-radius:2px;flex-shrink:0;overflow:hidden;}
.sens-bar-fill{height:100%;border-radius:2px;transition:width 0.5s ease;}
.sens-val{font-family:'Orbitron',monospace;font-size:14px;font-weight:700;width:36px;text-align:right;flex-shrink:0;}
.sens-slider-wrap{display:flex;align-items:center;gap:6px;flex-shrink:0;}
.sens-slider-wrap input[type=range]{width:66px;}
.sens-edit-val{font-family:'Orbitron',monospace;font-size:13px;font-weight:700;width:32px;text-align:right;}
.disabled-row{opacity:0.3;pointer-events:none;}

.tip-box{padding:11px 16px;font-size:11px;color:var(--muted);line-height:1.7;border-top:1px solid var(--border);}

.results-bottom{display:flex;gap:8px;padding:16px;border-top:1px solid var(--border);}
.btn-regen{flex:1;padding:12px;font-size:10px;font-family:'Orbitron',monospace;letter-spacing:1px;background:transparent;border:1px solid var(--border);color:var(--muted);cursor:pointer;}
.btn-copy-big{flex:2;padding:12px;font-size:10px;font-family:'Orbitron',monospace;font-weight:700;letter-spacing:1px;background:linear-gradient(135deg,#00a8c8,#00d4ff);border:none;color:#000;cursor:pointer;clip-path:polygon(8px 0%,100% 0%,calc(100% - 8px) 100%,0% 100%);}

/* MODAL */
.modal-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.85);z-index:200;align-items:center;justify-content:center;padding:16px;}
.modal-overlay.open{display:flex;}
.modal-box{width:100%;max-width:480px;background:#0a0a12;border:1px solid rgba(0,212,255,0.2);max-height:85vh;overflow:auto;}
.modal-topbar{display:flex;align-items:center;justify-content:space-between;padding:14px 16px;border-bottom:1px solid var(--border);}
.modal-pro-name{font-family:'Orbitron',monospace;font-size:14px;color:#fff;font-weight:700;}
.modal-pro-team{font-size:10px;color:var(--muted);letter-spacing:1px;margin-top:2px;}
.modal-actions{display:flex;gap:8px;}
.btn-modal-copy{padding:6px 12px;font-size:10px;font-family:'Orbitron',monospace;background:rgba(255,215,0,0.1);border:1px solid rgba(255,215,0,0.3);color:var(--gold);cursor:pointer;}
.btn-modal-close{padding:6px 10px;background:transparent;border:1px solid var(--border);color:var(--muted);cursor:pointer;font-size:14px;}

/* Range thumb colors per section */
.cam-range::-webkit-slider-thumb{background:var(--cyan);box-shadow:0 0 8px var(--cyan);}
.ads-range::-webkit-slider-thumb{background:var(--orange);box-shadow:0 0 8px var(--orange);}
.gyro-range::-webkit-slider-thumb{background:var(--purple);box-shadow:0 0 8px var(--purple);}
.fl-range::-webkit-slider-thumb{background:var(--gold);box-shadow:0 0 8px var(--gold);}
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <button class="nav-logo" onclick="showPage('home')">SENSI.GG</button>
  <div style="display:flex;gap:8px;">
    <button class="btn-primary" onclick="showPage('gen')">GENERATE</button>
  </div>
</nav>

<!-- ══════════════ HOME PAGE ══════════════ -->
<div id="page-home" class="page active">
  <section class="hero">
    <div class="hero-badge">BGMI · PUBG MOBILE · SENSITIVITY CALCULATOR</div>
    <h1 class="hero-title">SENSI<br>.GG</h1>
    <p class="hero-sub">Generate your perfect BGMI sensitivity.<br>Every scope. Every tab. Exactly like in-game.</p>
    <button class="hero-cta" onclick="showPage('gen')">⚡ GENERATE MY SENSITIVITY</button>
    <div style="display:flex;gap:28px;margin-top:44px;flex-wrap:wrap;justify-content:center;">
      <div style="text-align:center;"><div style="font-family:'Orbitron',monospace;font-size:26px;font-weight:700;color:var(--cyan);">50K+</div><div style="font-size:10px;color:var(--muted);letter-spacing:2px;margin-top:3px;">PROFILES</div></div>
      <div style="text-align:center;"><div style="font-family:'Orbitron',monospace;font-size:26px;font-weight:700;color:var(--cyan);">7</div><div style="font-size:10px;color:var(--muted);letter-spacing:2px;margin-top:3px;">SCOPE ROWS</div></div>
      <div style="text-align:center;"><div style="font-family:'Orbitron',monospace;font-size:26px;font-weight:700;color:var(--cyan);">FREE</div><div style="font-size:10px;color:var(--muted);letter-spacing:2px;margin-top:3px;">ALWAYS</div></div>
    </div>
  </section>

  <!-- PRO PLAYERS -->
  <div class="section-wrap">
    <div class="section-eyebrow">PRO PLAYERS</div>
    <div class="section-heading">Copy Pro Settings</div>
    <div id="pro-list"></div>
  </div>

  <!-- GYRO COMPARISON -->
  <div class="section-wrap" style="padding-top:0;">
    <div class="section-eyebrow">GYRO GUIDE</div>
    <div class="section-heading">Gyro vs No Gyro</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;">
      <div style="background:rgba(255,255,255,0.025);border:1px solid rgba(255,60,60,0.2);padding:16px 14px;">
        <div style="font-family:'Orbitron',monospace;font-size:11px;color:#ff4444;margin-bottom:12px;letter-spacing:1px;">❌ NO GYRO</div>
        <div style="font-size:11px;color:var(--muted);line-height:1.8;">Easier to learn<br>Stable on shaky hands<br>Better for thumb players<br>Less recoil control<br>Limited at top tier</div>
      </div>
      <div style="background:rgba(255,255,255,0.025);border:1px solid rgba(0,212,255,0.2);padding:16px 14px;">
        <div style="font-family:'Orbitron',monospace;font-size:11px;color:var(--cyan);margin-bottom:12px;letter-spacing:1px;">✅ GYRO</div>
        <div style="font-size:11px;color:var(--muted);line-height:1.8;">Superior spray control<br>Faster target tracking<br>Used by all top pros<br>2–3 week learning curve<br>Requires wrist stability</div>
      </div>
    </div>
    <div style="font-size:11px;color:var(--muted);text-align:center;margin-top:12px;font-style:italic;">Tip: Start with Scope Only gyro. Move to Full after 2 weeks.</div>
  </div>

  <!-- FAQ -->
  <div class="section-wrap" style="padding-top:0;">
    <div class="section-eyebrow">FAQ</div>
    <div class="section-heading">Common Questions</div>
    <div id="faq-list"></div>
  </div>

  <div style="height:40px;"></div>
</div>

<!-- ══════════════ GENERATOR PAGE ══════════════ -->
<div id="page-gen" class="page">
  <div class="gen-wrap">
    <div class="progress-bar-row">
      <div class="progress-bar-seg" id="prog0"></div>
      <div class="progress-bar-seg" id="prog1"></div>
      <div class="progress-bar-seg" id="prog2"></div>
    </div>
    <div class="progress-labels">
      <span class="progress-label" id="plabel0">Device</span>
      <span class="progress-label" id="plabel1">Style</span>
      <span class="progress-label" id="plabel2">Profile</span>
    </div>

    <!-- STEP 0 -->
    <div id="step-0" class="step-panel">
      <div class="field-group">
        <div class="field-label">RAM</div>
        <div class="chip-row" id="chips-ram"></div>
      </div>
      <div class="field-group">
        <div class="field-label">Max FPS Support</div>
        <div class="chip-row" id="chips-fps"></div>
      </div>
      <div class="field-group" style="margin-bottom:0;">
        <div class="field-label">Gyroscope Mode</div>
        <div class="chip-row" id="chips-gyro"></div>
      </div>
    </div>

    <!-- STEP 1 -->
    <div id="step-1" class="step-panel" style="display:none;">
      <div class="field-group">
        <div class="field-label">Play Style</div>
        <div class="chip-row" id="chips-style"></div>
      </div>
      <div class="field-group">
        <div class="field-label">Control Layout</div>
        <div class="chip-row" id="chips-fingers"></div>
      </div>
      <div class="field-group" style="margin-bottom:0;">
        <div class="field-label">Recoil Issues (select all that apply)</div>
        <div id="issues-list"></div>
      </div>
    </div>

    <!-- STEP 2 -->
    <div id="step-2" class="step-panel" style="display:none;">
      <div class="field-group">
        <div class="field-label">KD Ratio: <span id="kd-display" style="color:var(--cyan);">1.5</span></div>
        <input type="range" id="range-kd" min="0.1" max="6" step="0.1" value="1.5" oninput="document.getElementById('kd-display').textContent=parseFloat(this.value).toFixed(1)">
        <div style="display:flex;justify-content:space-between;margin-top:4px;"><span style="font-size:10px;color:#334;">0.1 (New)</span><span style="font-size:10px;color:#334;">6.0 (Pro)</span></div>
      </div>
      <div class="field-group" style="margin-bottom:0;">
        <div class="field-label">Current Tier</div>
        <div class="chip-row" id="chips-tier"></div>
      </div>
    </div>

    <div class="btn-row">
      <button class="btn-back" id="btn-back" onclick="prevStep()" style="display:none;">← BACK</button>
      <button class="btn-next" id="btn-next" onclick="nextStep()">NEXT →</button>
    </div>
  </div>
</div>

<!-- ══════════════ RESULTS PAGE ══════════════ -->
<div id="page-results" class="page">
  <div class="results-wrap">
    <div class="results-topbar">
      <div>
        <div class="results-title-main">SENSITIVITY SETTINGS</div>
        <div class="results-subtitle">GENERATED · BGMI / PUBG MOBILE</div>
      </div>
      <div class="results-actions">
        <button class="btn-edit" id="btn-edit" onclick="toggleEdit()">✏️ EDIT</button>
        <button class="btn-copy-all" onclick="copyAll()">📋 COPY</button>
      </div>
    </div>

    <!-- TABS -->
    <div class="tab-bar">
      <button class="tab-btn active-cyan" id="tab-camera" onclick="switchTab('camera')">Camera</button>
      <button class="tab-btn" id="tab-ads" onclick="switchTab('ads')">ADS</button>
      <button class="tab-btn" id="tab-gyro" onclick="switchTab('gyro')">Gyroscope</button>
      <button class="tab-btn" id="tab-free" onclick="switchTab('free')">Free Look</button>
    </div>

    <!-- CAMERA TAB -->
    <div id="tab-content-camera" class="tab-content active">
      <div class="section-block">
        <button class="section-hdr" style="border-left-color:var(--cyan);" onclick="toggleSection('sec-tpp')">
          <div style="text-align:left;"><div class="section-hdr-title" style="color:var(--cyan);">TPP Camera</div><div class="section-hdr-sub">Third Person Perspective</div></div>
          <span class="section-hdr-arrow open" id="arrow-sec-tpp">▾</span>
        </button>
        <div class="section-body" id="sec-tpp">
          <div id="rows-cam-tpp"></div>
        </div>
      </div>
      <div class="section-block">
        <button class="section-hdr" style="border-left-color:#4dd9ff;" onclick="toggleSection('sec-fpp')">
          <div style="text-align:left;"><div class="section-hdr-title" style="color:#4dd9ff;">FPP Camera</div><div class="section-hdr-sub">First Person Perspective</div></div>
          <span class="section-hdr-arrow" id="arrow-sec-fpp">▾</span>
        </button>
        <div class="section-body hidden" id="sec-fpp">
          <div id="rows-cam-fpp"></div>
        </div>
      </div>
    </div>

    <!-- ADS TAB -->
    <div id="tab-content-ads" class="tab-content">
      <div class="section-block">
        <button class="section-hdr" style="border-left-color:var(--orange);" onclick="toggleSection('sec-ads')">
          <div style="text-align:left;"><div class="section-hdr-title" style="color:var(--orange);">ADS Sensitivity</div><div class="section-hdr-sub">Aim Down Sight — per scope</div></div>
          <span class="section-hdr-arrow open" id="arrow-sec-ads">▾</span>
        </button>
        <div class="section-body" id="sec-ads">
          <div id="rows-ads"></div>
        </div>
      </div>
      <div class="tip-box">💡 ADS values decrease as zoom increases — intentional. Lower zoom = fast tracking, higher zoom = precision.</div>
    </div>

    <!-- GYRO TAB -->
    <div id="tab-content-gyro" class="tab-content">
      <div id="gyro-scope-note" style="display:none;padding:10px 16px 4px;font-size:11px;color:rgba(168,85,247,0.5);letter-spacing:1px;">⚠ No Scope gyro is disabled (Scope Only mode)</div>
      <div class="section-block">
        <button class="section-hdr" style="border-left-color:var(--purple);" onclick="toggleSection('sec-gyro')">
          <div style="text-align:left;"><div class="section-hdr-title" style="color:var(--purple);">Gyroscope Sensitivity</div><div class="section-hdr-sub">Per-scope — same layout as ADS</div></div>
          <span class="section-hdr-arrow open" id="arrow-sec-gyro">▾</span>
        </button>
        <div class="section-body" id="sec-gyro">
          <div id="rows-gyro"></div>
        </div>
      </div>
      <div class="tip-box">🌀 Gyro values are higher than ADS — correct. Gyro compensates for physical tilt speed. Keep gyro 3–4× your ADS for the same scope.</div>
    </div>

    <!-- FREE LOOK TAB -->
    <div id="tab-content-free" class="tab-content">
      <div class="section-block">
        <button class="section-hdr" style="border-left-color:var(--gold);" onclick="toggleSection('sec-free')">
          <div style="text-align:left;"><div class="section-hdr-title" style="color:var(--gold);">Free Look Sensitivity</div><div class="section-hdr-sub">Camera pan without aiming</div></div>
          <span class="section-hdr-arrow open" id="arrow-sec-free">▾</span>
        </button>
        <div class="section-body" id="sec-free">
          <div id="rows-free"></div>
        </div>
      </div>
      <div class="tip-box">💡 Keep free look 20–30% lower than your TPP camera for control.</div>
    </div>

    <div class="results-bottom">
      <button class="btn-regen" onclick="showPage('gen')">🔄 REGENERATE</button>
      <button class="btn-copy-big" id="btn-copy-big" onclick="copyAll()">📋 COPY ALL SETTINGS</button>
    </div>
  </div>
</div>

<!-- ══════════════ PRO MODAL ══════════════ -->
<div class="modal-overlay" id="pro-modal" onclick="closeModal()">
  <div class="modal-box" onclick="event.stopPropagation()">
    <div class="modal-topbar">
      <div>
        <div class="modal-pro-name" id="modal-pro-name">—</div>
        <div class="modal-pro-team" id="modal-pro-team">—</div>
      </div>
      <div class="modal-actions">
        <button class="btn-modal-copy" onclick="copyProSettings()">📋 COPY</button>
        <button class="btn-modal-close" onclick="closeModal()">✕</button>
      </div>
    </div>
    <div class="tab-bar">
      <button class="tab-btn active-cyan" id="mtab-camera" onclick="switchModalTab('camera')">Camera</button>
      <button class="tab-btn" id="mtab-ads" onclick="switchModalTab('ads')">ADS</button>
      <button class="tab-btn" id="mtab-gyro" onclick="switchModalTab('gyro')">Gyro</button>
    </div>
    <div id="modal-tab-camera"><div id="modal-rows-cam"></div></div>
    <div id="modal-tab-ads" style="display:none;"><div id="modal-rows-ads"></div></div>
    <div id="modal-tab-gyro" style="display:none;"><div id="modal-rows-gyro"></div></div>
  </div>
</div>

<script>
// ─── DATA ─────────────────────────────────────────────────────────────────
const SCOPE_ROWS = [
  {key:"no_scope", label:"Camera (No Scope)",    icon:"👁"},
  {key:"red_dot",  label:"Red Dot / Holographic", icon:"🔴"},
  {key:"2x",       label:"2x Scope",              icon:"🔭"},
  {key:"3x",       label:"3x Scope",              icon:"🔭"},
  {key:"4x",       label:"4x Scope",              icon:"🔭"},
  {key:"6x",       label:"6x Scope",              icon:"🎯"},
  {key:"8x",       label:"8x / 15x Scope",        icon:"🎯"},
];

const PRO_PLAYERS = [
  {name:"Jonathan",team:"Team India",
   cam:{no_scope:95,red_dot:88,["2x"]:75,["3x"]:62,["4x"]:50,["6x"]:35,["8x"]:24},
   ads:{no_scope:68,red_dot:45,["2x"]:38,["3x"]:30,["4x"]:22,["6x"]:13,["8x"]:10},
   gyro:{no_scope:300,red_dot:240,["2x"]:200,["3x"]:165,["4x"]:140,["6x"]:100,["8x"]:78}},
  {name:"Scout",team:"OR Esports",
   cam:{no_scope:130,red_dot:118,["2x"]:100,["3x"]:82,["4x"]:65,["6x"]:45,["8x"]:30},
   ads:{no_scope:78,red_dot:60,["2x"]:48,["3x"]:38,["4x"]:28,["6x"]:18,["8x"]:12},
   gyro:{no_scope:350,red_dot:285,["2x"]:240,["3x"]:198,["4x"]:165,["6x"]:118,["8x"]:88}},
  {name:"Mortal",team:"Soul",
   cam:{no_scope:110,red_dot:100,["2x"]:85,["3x"]:70,["4x"]:55,["6x"]:38,["8x"]:26},
   ads:{no_scope:72,red_dot:55,["2x"]:42,["3x"]:35,["4x"]:25,["6x"]:15,["8x"]:10},
   gyro:{no_scope:0,red_dot:200,["2x"]:165,["3x"]:138,["4x"]:115,["6x"]:82,["8x"]:62}},
  {name:"Zgod",team:"XSpark",
   cam:{no_scope:100,red_dot:92,["2x"]:78,["3x"]:65,["4x"]:52,["6x"]:36,["8x"]:25},
   ads:{no_scope:65,red_dot:50,["2x"]:40,["3x"]:32,["4x"]:24,["6x"]:15,["8x"]:10},
   gyro:{no_scope:280,red_dot:225,["2x"]:188,["3x"]:155,["4x"]:130,["6x"]:92,["8x"]:70}},
];

const FAQS = [
  {q:"What sensitivity should I start with as a beginner?",a:"Start with medium values — TPP around 90–100%, ADS at 45–55% for red dot. Don't copy pro settings until you're Platinum+."},
  {q:"Should I use gyroscope in BGMI?",a:"Yes, if your device supports it. Gyro dramatically improves recoil control. Start with Scope Only before going full gyro. Takes 2–3 weeks."},
  {q:"Why does my 6x scope shake?",a:"Your 6x ADS sensitivity is too high. Drop it to 10–15% and increase gyro 6x if you use gyro. This is a sensitivity mismatch problem, not a skill problem."},
  {q:"How long should I test new settings?",a:"Minimum 3–5 days in TDM/Arena only. Your muscle memory needs 1000+ shots to adapt. Don't judge settings in the first 2 days."},
  {q:"What's the difference between camera and ADS sensitivity?",a:"Camera controls how fast you look around hipfiring. ADS controls speed when scoped. ADS should always be lower than camera sensitivity."},
];

// ─── FORM STATE ────────────────────────────────────────────────────────────
const form = {ram:8,fps:60,gyroMode:"scope",playstyle:"assaulter",fingers:"claw4",recoilIssues:[],kd:1.5,tier:"gold"};
let currentStep = 0;
let generatedResults = null;
let editMode = false;
let currentProIdx = 0;
let currentModalTab = "camera";

// ─── GENERATE LOGIC ────────────────────────────────────────────────────────
function clamp(v,a,b){return Math.round(Math.max(a,Math.min(b,v)));}

function generateSensitivity(){
  const {ram,fps,gyroMode,playstyle,fingers,recoilIssues,kd} = form;
  const fpsMod  = fps===120?-8:fps===90?-4:fps===60?0:6;
  const ramMod  = ram>=12?5:ram>=8?0:-8;
  const stMod   = playstyle==="rush"?18:playstyle==="sniper"?-18:playstyle==="assaulter"?5:0;
  const fgMod   = fingers==="claw6"?10:fingers==="claw5"?7:fingers==="claw4"?3:fingers==="thumb"?-8:0;
  const kdMod   = kd>3?8:kd>2?4:kd>1?0:-5;
  const rv = recoilIssues.includes("vertical");
  const rh = recoilIssues.includes("horizontal");
  const ss = recoilIssues.includes("scopeshake");

  const base = 95+fpsMod+ramMod+stMod+fgMod+kdMod;

  const cam_tpp = {
    no_scope: clamp(base,70,200),
    red_dot:  clamp(base-5,60,180),
    "2x":     clamp(base-12,50,150),
    "3x":     clamp(base-20,40,120),
    "4x":     clamp(base-30,30,100),
    "6x":     clamp(base-40,20,80),
    "8x":     clamp(base-50,12,60),
  };
  const cam_fpp = {
    no_scope: clamp(base+8,75,210),
    red_dot:  clamp(base+3,65,185),
    "2x":     clamp(base-4,52,155),
    "3x":     clamp(base-12,42,125),
    "4x":     clamp(base-22,32,105),
    "6x":     clamp(base-32,22,85),
    "8x":     clamp(base-42,14,65),
  };
  const adsBase = clamp(50+fpsMod+stMod*0.5+fgMod*0.6+kdMod,30,90);
  const ads = {
    no_scope: clamp(adsBase+20-(rv?5:0),40,110),
    red_dot:  clamp(adsBase+12-(rv?4:0),35,100),
    "2x":     clamp(adsBase+5-(rh?3:0),28,85),
    "3x":     clamp(adsBase-5,22,70),
    "4x":     clamp(adsBase-14-(ss?4:0),15,58),
    "6x":     clamp(adsBase-24-(ss?5:0),10,42),
    "8x":     clamp(adsBase-33-(ss?5:0),8,30),
  };
  const gyroBase = clamp(260+fpsMod*-3+ramMod*2+kdMod*4,140,420);
  const gyro = gyroMode==="none" ? null : {
    no_scope: gyroMode==="full"?clamp(gyroBase,180,420):0,
    red_dot:  clamp(gyroBase*0.82,120,340),
    "2x":     clamp(gyroBase*0.70,100,290),
    "3x":     clamp(gyroBase*0.58,80,235),
    "4x":     clamp(gyroBase*0.48-(ss?15:0),60,190),
    "6x":     clamp(gyroBase*0.36-(ss?12:0),40,145),
    "8x":     clamp(gyroBase*0.27-(ss?10:0),28,110),
  };
  const free = {
    tpp: clamp(cam_tpp.no_scope*0.72,45,140),
    fpp: clamp(cam_fpp.no_scope*0.68,42,135),
  };
  return {cam_tpp,cam_fpp,ads,gyro,free,gyroMode};
}

// ─── RENDER HELPERS ────────────────────────────────────────────────────────
function sensRowHTML(label, icon, value, min, max, color, rangeClass, dataKey, showEdit){
  const pct = Math.min(100,((value-min)/(max-min))*100);
  if(showEdit){
    return `<div class="sens-row">
      <span class="sens-row-icon">${icon}</span>
      <span class="sens-row-label">${label}</span>
      <div class="sens-bar-wrap"><div class="sens-bar-fill" style="width:${pct}%;background:linear-gradient(90deg,${color}88,${color});"></div></div>
      <div class="sens-slider-wrap">
        <input type="range" class="${rangeClass}" min="${min}" max="${max}" value="${value}" oninput="updateVal('${dataKey}',this.value,this)" style="--tc:${color}">
        <span class="sens-edit-val" style="color:${color};" id="ev-${dataKey}">${value}</span>
      </div>
    </div>`;
  }
  return `<div class="sens-row">
    <span class="sens-row-icon">${icon}</span>
    <span class="sens-row-label">${label}</span>
    <div class="sens-bar-wrap"><div class="sens-bar-fill" style="width:${pct}%;background:linear-gradient(90deg,${color}88,${color});"></div></div>
    <span class="sens-val" style="color:${color};">${value}</span>
  </div>`;
}

function updateVal(key, val, input){
  const v = parseInt(val);
  const parts = key.split("-");
  if(parts[0]==="cam_tpp") generatedResults.cam_tpp[parts[1]] = v;
  else if(parts[0]==="cam_fpp") generatedResults.cam_fpp[parts[1]] = v;
  else if(parts[0]==="ads") generatedResults.ads[parts[1]] = v;
  else if(parts[0]==="gyro" && generatedResults.gyro) generatedResults.gyro[parts[1]] = v;
  else if(parts[0]==="free_tpp") generatedResults.free.tpp = v;
  else if(parts[0]==="free_fpp") generatedResults.free.fpp = v;
  const el = document.getElementById("ev-"+key);
  if(el) el.textContent = v;
  // update bar
  const row = input.closest(".sens-row");
  if(row){
    const bar = row.querySelector(".sens-bar-fill");
    if(bar){
      const rng = input;
      const pct = Math.min(100,((v-parseInt(rng.min))/(parseInt(rng.max)-parseInt(rng.min)))*100);
      bar.style.width = pct+"%";
    }
  }
}

function renderRows(containerId, data, prefix, color, rangeClass, maxVal){
  const el = document.getElementById(containerId);
  if(!el) return;
  el.innerHTML = SCOPE_ROWS.map(r=>{
    const v = data[r.key]??0;
    return sensRowHTML(r.label, r.icon, v, 0, maxVal||200, color, rangeClass, prefix+"-"+r.key, editMode);
  }).join("");
}

function renderResults(){
  const r = generatedResults;
  renderRows("rows-cam-tpp", r.cam_tpp, "cam_tpp", "var(--cyan)", "cam-range", 200);
  renderRows("rows-cam-fpp", r.cam_fpp, "cam_fpp", "#4dd9ff", "cam-range", 210);
  renderRows("rows-ads",     r.ads,     "ads",     "var(--orange)", "ads-range", 110);
  renderRows("rows-free", {no_scope:r.free.tpp, red_dot:r.free.fpp}, "free_tpp", "var(--gold)", "fl-range", 150);
  // Free look only 2 rows
  document.getElementById("rows-free").innerHTML =
    sensRowHTML("TPP Free Look","👁",r.free.tpp,20,150,"var(--gold)","fl-range","free_tpp",editMode)+
    sensRowHTML("FPP Free Look","👁",r.free.fpp,20,150,"var(--gold)","fl-range","free_fpp",editMode);

  // Gyro
  const gyroTab = document.getElementById("tab-gyro");
  const gyroNote = document.getElementById("gyro-scope-note");
  if(r.gyro){
    gyroTab.style.display="";
    gyroNote.style.display = r.gyroMode==="scope" ? "" : "none";
    const rows = SCOPE_ROWS.map(row=>{
      const v = r.gyro[row.key]??0;
      const disabled = row.key==="no_scope" && r.gyroMode==="scope";
      const html = sensRowHTML(row.label, row.icon, v, 0, 420, "var(--purple)", "gyro-range", "gyro-"+row.key, editMode && !disabled);
      return disabled ? html.replace('class="sens-row"','class="sens-row disabled-row"') : html;
    }).join("");
    document.getElementById("rows-gyro").innerHTML = rows;
  } else {
    gyroTab.style.display="none";
    if(document.getElementById("tab-content-gyro").classList.contains("active")){
      switchTab("camera");
    }
  }
}

// ─── NAV & PAGES ───────────────────────────────────────────────────────────
function showPage(name){
  document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
  document.getElementById("page-"+name).classList.add("active");
  window.scrollTo(0,0);
  if(name==="gen") resetGen();
}

function toggleEdit(){
  editMode = !editMode;
  const btn = document.getElementById("btn-edit");
  btn.textContent = editMode ? "✏️ EDITING" : "✏️ EDIT";
  btn.className = editMode ? "btn-edit on" : "btn-edit";
  renderResults();
}

function switchTab(name){
  const colors = {camera:"cyan",ads:"orange",gyro:"purple",free:"gold"};
  ["camera","ads","gyro","free"].forEach(t=>{
    document.getElementById("tab-content-"+t).classList.remove("active");
    const btn = document.getElementById("tab-"+t);
    if(btn) btn.className = "tab-btn";
  });
  document.getElementById("tab-content-"+name).classList.add("active");
  const btn = document.getElementById("tab-"+name);
  if(btn) btn.className = "tab-btn active-"+colors[name];
}

function toggleSection(id){
  const body = document.getElementById(id);
  const arrow = document.getElementById("arrow-"+id);
  body.classList.toggle("hidden");
  arrow.classList.toggle("open");
}

// ─── GENERATOR STEPS ───────────────────────────────────────────────────────
function makeChips(containerId, options, formKey, colorClass){
  const el = document.getElementById(containerId);
  el.innerHTML = options.map(o=>`
    <button class="chip ${form[formKey]===o.v?"active-"+colorClass:""}" onclick="setForm('${formKey}','${o.v}','${colorClass}','${containerId}',this)">${o.l}</button>
  `).join("");
}

function setForm(key, val, colorClass, containerId, btn){
  form[key] = isNaN(val)?val:parseFloat(val)||val;
  // re-render chips
  document.querySelectorAll("#"+containerId+" .chip").forEach(c=>{
    c.className = "chip";
  });
  btn.className = "chip active-"+colorClass;
}

function toggleIssue(val, btn){
  if(form.recoilIssues.includes(val)){
    form.recoilIssues = form.recoilIssues.filter(x=>x!==val);
    btn.classList.remove("active");
  } else {
    form.recoilIssues.push(val);
    btn.classList.add("active");
  }
}

function resetGen(){
  currentStep=0;
  editMode=false;
  updateStepUI();
  buildStep0();
  buildStep1();
  buildStep2();
}

function buildStep0(){
  makeChips("chips-ram",[{v:4,l:"4 GB"},{v:6,l:"6 GB"},{v:8,l:"8 GB"},{v:12,l:"12 GB"},{v:16,l:"16 GB"}],"ram","cyan");
  makeChips("chips-fps",[{v:40,l:"40 FPS"},{v:60,l:"60 FPS"},{v:90,l:"90 FPS"},{v:120,l:"120 FPS"}],"fps","cyan");
  makeChips("chips-gyro",[{v:"none",l:"❌ No Gyro"},{v:"scope",l:"🔭 Scope Only"},{v:"full",l:"✅ Full Gyro"}],"gyroMode","purple");
}
function buildStep1(){
  makeChips("chips-style",[{v:"rush",l:"🔥 Rush"},{v:"assaulter",l:"⚔️ Assaulter"},{v:"sniper",l:"🎯 Sniper"},{v:"balanced",l:"⚖️ Balanced"}],"playstyle","orange");
  makeChips("chips-fingers",[{v:"thumb",l:"👍 Thumb"},{v:"claw3",l:"3-Finger"},{v:"claw4",l:"4-Finger"},{v:"claw5",l:"5-Finger"},{v:"claw6",l:"6-Finger"}],"fingers","orange");
  document.getElementById("issues-list").innerHTML = [
    {v:"vertical",l:"🔼 Vertical Recoil — gun pulls up when spraying"},
    {v:"horizontal",l:"↔️ Horizontal Drift — spray drifts left/right"},
    {v:"scopeshake",l:"📳 Scope Shake — 4x/6x/8x bounces"},
    {v:"tracking",l:"👁️ Bad Tracking — can't follow moving targets"},
  ].map(r=>`<button class="issue-btn${form.recoilIssues.includes(r.v)?" active":""}" onclick="toggleIssue('${r.v}',this)">${r.l}</button>`).join("");
}
function buildStep2(){
  makeChips("chips-tier",["Bronze","Silver","Gold","Platinum","Diamond","Crown","Ace","Conqueror"].map(t=>({v:t.toLowerCase(),l:t})),"tier","gold");
}

function updateStepUI(){
  [0,1,2].forEach(i=>{
    document.getElementById("step-"+i).style.display = i===currentStep?"block":"none";
    document.getElementById("prog"+i).className = "progress-bar-seg"+(i<=currentStep?" done":"");
    document.getElementById("plabel"+i).className = "progress-label"+(i===currentStep?" active":"");
  });
  document.getElementById("btn-back").style.display = currentStep>0?"block":"none";
  document.getElementById("btn-next").textContent = currentStep===2?"⚡ GENERATE SETTINGS":"NEXT →";
}

function nextStep(){
  if(currentStep<2){ currentStep++; updateStepUI(); return; }
  form.kd = parseFloat(document.getElementById("range-kd").value)||1.5;
  generatedResults = generateSensitivity();
  renderResults();
  switchTab("camera");
  showPage("results");
}
function prevStep(){ if(currentStep>0){currentStep--;updateStepUI();} }

// ─── COPY ──────────────────────────────────────────────────────────────────
function copyAll(){
  const r = generatedResults;
  const lines = ["=== SENSI.GG — BGMI SENSITIVITY SETTINGS ===",""];
  lines.push("📷 TPP CAMERA:");
  SCOPE_ROWS.forEach(row=>lines.push(`  ${row.label}: ${r.cam_tpp[row.key]}`));
  lines.push("","📷 FPP CAMERA:");
  SCOPE_ROWS.forEach(row=>lines.push(`  ${row.label}: ${r.cam_fpp[row.key]}`));
  lines.push("","🔭 ADS:");
  SCOPE_ROWS.forEach(row=>lines.push(`  ${row.label}: ${r.ads[row.key]}`));
  if(r.gyro){
    lines.push("","🌀 GYROSCOPE:");
    SCOPE_ROWS.forEach(row=>lines.push(`  ${row.label}: ${r.gyro[row.key]}`));
  }
  lines.push("","👁 FREE LOOK:");
  lines.push(`  TPP: ${r.free.tpp}`,`  FPP: ${r.free.fpp}`);
  lines.push("","Generated at sensi.gg");
  navigator.clipboard.writeText(lines.join("\n")).then(()=>{
    const btn = document.getElementById("btn-copy-big");
    btn.textContent="✅ COPIED!";
    setTimeout(()=>btn.textContent="📋 COPY ALL SETTINGS",2000);
    const btn2 = document.querySelector(".btn-copy-all");
    if(btn2){btn2.textContent="✅";setTimeout(()=>btn2.textContent="📋 COPY",2000);}
  });
}

// ─── PRO MODAL ──────────────────────────────────────────────────────────────
function openProModal(idx){
  currentProIdx = idx;
  const pro = PRO_PLAYERS[idx];
  document.getElementById("modal-pro-name").textContent = pro.name;
  document.getElementById("modal-pro-team").textContent = pro.team;
  switchModalTab("camera");
  document.getElementById("pro-modal").classList.add("open");
}
function closeModal(){
  document.getElementById("pro-modal").classList.remove("open");
}
function switchModalTab(name){
  currentModalTab = name;
  ["camera","ads","gyro"].forEach(t=>{
    document.getElementById("modal-tab-"+t).style.display = t===name?"block":"none";
    document.getElementById("mtab-"+t).className = "tab-btn"+(t===name?" active-"+(t==="camera"?"cyan":t==="ads"?"orange":"purple"):"");
  });
  const pro = PRO_PLAYERS[currentProIdx];
  const color = name==="camera"?"var(--cyan)":name==="ads"?"var(--orange)":"var(--purple)";
  const maxV = name==="gyro"?420:name==="ads"?110:200;
  const data = name==="camera"?pro.cam:name==="ads"?pro.ads:pro.gyro;
  const containerId = "modal-rows-"+name;
  if(!data){document.getElementById(containerId).innerHTML="<div style='padding:16px;font-size:12px;color:#445;'>No gyro data</div>";return;}
  document.getElementById(containerId).innerHTML = SCOPE_ROWS.map(r=>{
    const v = data[r.key]??0;
    return sensRowHTML(r.label,r.icon,v,0,maxV,color,"",""  ,false);
  }).join("");
}

function copyProSettings(){
  const pro = PRO_PLAYERS[currentProIdx];
  const lines = [`=== ${pro.name} (${pro.team}) — SENSI.GG ===`,"","📷 TPP CAMERA:"];
  SCOPE_ROWS.forEach(r=>lines.push(`  ${r.label}: ${pro.cam[r.key]}`));
  lines.push("","🔭 ADS:"); SCOPE_ROWS.forEach(r=>lines.push(`  ${r.label}: ${pro.ads[r.key]}`));
  if(pro.gyro){ lines.push("","🌀 GYROSCOPE:"); SCOPE_ROWS.forEach(r=>lines.push(`  ${r.label}: ${pro.gyro[r.key]||0}`)); }
  navigator.clipboard.writeText(lines.join("\n")).then(()=>{
    const btn = document.querySelector(".btn-modal-copy");
    btn.textContent="✅ COPIED";
    setTimeout(()=>btn.textContent="📋 COPY",2000);
  });
}

// ─── BUILD HOME ────────────────────────────────────────────────────────────
function buildHome(){
  // Pro list
  document.getElementById("pro-list").innerHTML = PRO_PLAYERS.map((pro,i)=>`
    <button class="pro-row" onclick="openProModal(${i})">
      <div><div class="pro-name">${pro.name}</div><div class="pro-team">${pro.team}</div></div>
      <div class="pro-stats">
        <div class="pro-stat"><div class="pro-stat-label">NO SCOPE</div><div class="pro-stat-val" style="color:var(--cyan);">${pro.cam.no_scope}</div></div>
        <div class="pro-stat"><div class="pro-stat-label">4x ADS</div><div class="pro-stat-val" style="color:var(--orange);">${pro.ads["4x"]}</div></div>
        <div class="pro-stat"><div class="pro-stat-label">4x GYRO</div><div class="pro-stat-val" style="color:var(--purple);">${pro.gyro["4x"]}</div></div>
        <span class="arrow">›</span>
      </div>
    </button>
  `).join("");

  // FAQ
  document.getElementById("faq-list").innerHTML = FAQS.map((f,i)=>`
    <div style="border-bottom:1px solid var(--border);">
      <button onclick="toggleFaq(${i})" style="width:100%;text-align:left;padding:14px 0;background:none;border:none;color:#aaa;font-family:'Rajdhani',sans-serif;font-size:14px;font-weight:600;cursor:pointer;display:flex;justify-content:space-between;align-items:center;">
        ${f.q}<span style="color:#445;font-size:16px;flex-shrink:0;margin-left:10px;" id="faq-arrow-${i}">+</span>
      </button>
      <div id="faq-ans-${i}" style="display:none;padding:0 0 14px;font-size:13px;color:var(--muted);line-height:1.7;">${f.a}</div>
    </div>
  `).join("");
}

function toggleFaq(i){
  const ans = document.getElementById("faq-ans-"+i);
  const arrow = document.getElementById("faq-arrow-"+i);
  const open = ans.style.display==="block";
  ans.style.display = open?"none":"block";
  arrow.textContent = open?"+":" ×";
  arrow.style.color = open?"#445":"var(--cyan)";
}

// ─── INIT ──────────────────────────────────────────────────────────────────
buildHome();
buildStep0();
buildStep1();
buildStep2();
updateStepUI();
</script>
</body>
</html>

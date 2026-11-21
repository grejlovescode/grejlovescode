<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>GREJ</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700;800&display=swap');

*{margin:0;padding:0;box-sizing:border-box;}

:root{
  --bg:#0a0a0a;
  --fg:#f0ede6;
  --dim:#888;
  --mid:#2a2a2a;
  --line:#333;
}

body{
  background:var(--bg);
  color:var(--fg);
  font-family:'JetBrains Mono',monospace;
  overflow-x:hidden;
}

/* halftone bg */
body::before{
  content:'';
  position:fixed;inset:0;
  background-image:radial-gradient(circle,#1e1e1e 1.2px,transparent 1.2px);
  background-size:16px 16px;
  pointer-events:none;z-index:0;
  opacity:.5;
}

.wrap{
  position:relative;z-index:1;
  max-width:880px;margin:0 auto;
  padding:0 20px 80px;
}

/* ── INK PANELS ── */
.panel{
  border:3px solid var(--fg);
  margin-bottom:0;
  position:relative;
  background:var(--bg);
  overflow:hidden;
}

/* ── SECTION LABEL ── */
.sec{
  display:flex;align-items:center;gap:12px;
  padding:7px 0 7px;
  font-size:10px;letter-spacing:3px;color:var(--dim);
  text-transform:uppercase;
}
.sec::before,.sec::after{content:'';flex:1;height:1px;background:var(--line);}

/* ══════════════════════════════════
   HERO
══════════════════════════════════ */
.hero{
  display:grid;
  grid-template-columns:1fr auto;
  min-height:260px;
  border:3px solid var(--fg);
  margin-bottom:0;
}

.hero-left{
  padding:36px 32px 28px;
  display:flex;flex-direction:column;justify-content:space-between;
  border-right:3px solid var(--fg);
}

.hero-title{
  font-size:clamp(56px,10vw,100px);
  font-weight:800;
  letter-spacing:.15em;
  line-height:1;
  position:relative;
}

/* manga ink drip effect on title */
.hero-title::after{
  content:'';
  position:absolute;
  bottom:-6px;left:0;right:0;
  height:3px;
  background:repeating-linear-gradient(90deg,var(--fg) 0,var(--fg) 12px,transparent 12px,transparent 18px);
}

.hero-meta{
  margin-top:18px;
}
.hero-meta p{
  font-size:12px;letter-spacing:2px;color:var(--dim);
  line-height:2.2;
}
.hero-meta p b{color:var(--fg);}

.hero-right{
  width:200px;
  position:relative;
  display:flex;align-items:flex-end;justify-content:center;
  overflow:hidden;
}

/* ── CHARACTER A: hero girl (ink illustration) ── */
.char-hero{
  position:absolute;bottom:0;
  width:180px;
}

/* ══════════════════════════════════
   MANGA PANEL ROW (3-col)
══════════════════════════════════ */
.row3{
  display:grid;
  grid-template-columns:1fr 1fr 1fr;
  border:3px solid var(--fg);
  border-top:none;
}

.cell{
  padding:22px 18px 18px;
  border-right:3px solid var(--fg);
  position:relative;
  overflow:hidden;
}
.cell:last-child{border-right:none;}

.cell-num{
  font-size:9px;color:var(--dim);letter-spacing:2px;
  margin-bottom:6px;
}
.cell-title{
  font-size:14px;font-weight:800;letter-spacing:2px;
  margin-bottom:8px;
}
.cell-body{
  font-size:11px;color:#aaa;line-height:1.8;
}
.cell-tag{
  margin-top:10px;font-size:9px;
  letter-spacing:2px;color:var(--dim);
  border-top:1px solid var(--line);
  padding-top:8px;
}

/* ── CHARACTER B: sitting coder ── */
.char-cell{
  position:absolute;
  bottom:10px;right:8px;
  opacity:.18;
  width:70px;
}

/* ══════════════════════════════════
   SKILLS
══════════════════════════════════ */
.skills-wrap{
  display:grid;
  grid-template-columns:1fr 220px;
  border:3px solid var(--fg);
  border-top:none;
}

.skills-left{
  padding:28px 28px;
  border-right:3px solid var(--fg);
}

.skill-row{
  display:grid;
  grid-template-columns:80px 1fr 38px;
  align-items:center;
  gap:14px;
  margin-bottom:14px;
}
.skill-name{font-size:11px;font-weight:700;letter-spacing:1px;}
.bar-track{
  height:8px;background:var(--mid);
  border:1px solid var(--line);
  position:relative;overflow:hidden;
}
.bar-fill{
  height:100%;background:var(--fg);
  width:0;
  animation:barfill 1.4s cubic-bezier(.4,0,.2,1) forwards;
  position:relative;
}
.bar-fill::after{
  content:'';position:absolute;inset:0;
  background:repeating-linear-gradient(-45deg,transparent,transparent 3px,rgba(0,0,0,.3) 3px,rgba(0,0,0,.3) 4px);
}
@keyframes barfill{to{width:var(--w);}}
.bar-pct{font-size:10px;color:var(--dim);text-align:right;}

.skills-right{
  display:flex;align-items:flex-end;justify-content:center;
  overflow:hidden;padding:0;
  position:relative;
}

/* ══════════════════════════════════
   CURRENTLY — ticker
══════════════════════════════════ */
.ticker-panel{
  border:3px solid var(--fg);
  border-top:none;
  overflow:hidden;
  padding:0;
}
.ticker-inner{
  display:flex;
  white-space:nowrap;
  animation:tick 24s linear infinite;
  font-size:11px;letter-spacing:2px;color:var(--dim);
  padding:14px 0;
  border-top:1px solid var(--line);
  border-bottom:1px solid var(--line);
}
.ticker-inner span{flex-shrink:0;padding:0 28px;}
.ticker-inner .dot{color:var(--fg);padding:0;}
@keyframes tick{from{transform:translateX(0);}to{transform:translateX(-50%);}}
.ticker-label{
  font-size:9px;letter-spacing:3px;color:var(--dim);
  padding:10px 18px 0;
}

/* ══════════════════════════════════
   THOUGHTS — speech panels
══════════════════════════════════ */
.thoughts-wrap{
  border:3px solid var(--fg);
  border-top:none;
  display:grid;
  grid-template-columns:auto 1fr;
}

.thoughts-char{
  width:150px;
  border-right:3px solid var(--fg);
  display:flex;align-items:flex-end;justify-content:center;
  overflow:hidden;padding-bottom:0;background:var(--bg);
  position:relative;
}

/* screentone on char panel */
.thoughts-char::before{
  content:'';position:absolute;inset:0;
  background-image:radial-gradient(circle,rgba(255,255,255,.07) 1px,transparent 1px);
  background-size:6px 6px;pointer-events:none;
}

.bubbles{
  padding:24px 20px 20px;
  display:flex;flex-direction:column;gap:14px;
}

.bub{
  border:2.5px solid var(--fg);
  padding:12px 16px;
  font-size:12px;line-height:1.7;
  position:relative;
  opacity:0;
  animation:bubin .4s ease both;
  max-width:360px;
}
.bub.r{
  align-self:flex-end;
  background:var(--fg);color:var(--bg);
}
.bub::after{content:'';position:absolute;bottom:-11px;width:0;height:0;}
.bub.l::after{left:16px;border-top:11px solid var(--fg);border-right:11px solid transparent;}
.bub.r::after{right:16px;border-top:11px solid var(--fg);border-left:11px solid transparent;}

.bub:nth-child(1){animation-delay:.1s;}
.bub:nth-child(2){animation-delay:.4s;}
.bub:nth-child(3){animation-delay:.7s;}
.bub:nth-child(4){animation-delay:1s;}
.bub:nth-child(5){animation-delay:1.3s;}

@keyframes bubin{
  from{opacity:0;transform:scale(.92) translateY(6px);}
  to{opacity:1;transform:none;}
}

/* ══════════════════════════════════
   STATS
══════════════════════════════════ */
.stats-panel{
  display:grid;grid-template-columns:1fr 1fr;
  border:3px solid var(--fg);border-top:none;
}
.stat-cell{
  padding:0;
  border-right:3px solid var(--fg);
  overflow:hidden;
}
.stat-cell:last-child{border-right:none;}
.stat-cell img{
  width:100%;display:block;
  filter:grayscale(1) contrast(1.1) brightness(.9);
}

.graph-panel{
  border:3px solid var(--fg);border-top:none;overflow:hidden;
}
.graph-panel img{
  width:100%;display:block;
  filter:grayscale(1) contrast(1.1);
}

/* ══════════════════════════════════
   SNAKE
══════════════════════════════════ */
.snake-panel{
  border:3px solid var(--fg);border-top:none;
  overflow:hidden;padding:16px 20px;
  position:relative;
}
.snake-panel img{
  width:100%;display:block;
  filter:grayscale(1) contrast(1.4) brightness(.85);
}
.snake-label{
  font-size:9px;letter-spacing:3px;color:var(--dim);
  margin-bottom:10px;
}

/* ── CHARACTER C: watching from corner ── */
.char-corner{
  position:absolute;
  bottom:10px;right:14px;
  width:90px;opacity:.22;
}

/* ══════════════════════════════════
   FOOTER
══════════════════════════════════ */
.footer{
  border:3px solid var(--fg);border-top:none;
  display:grid;grid-template-columns:auto 1fr;
}
.footer-char{
  width:120px;border-right:3px solid var(--fg);
  display:flex;align-items:flex-end;justify-content:center;
  overflow:hidden;
}
.footer-text{
  padding:28px 24px;
  display:flex;flex-direction:column;justify-content:center;
  gap:10px;
}
.footer-text p{font-size:11px;letter-spacing:2px;color:var(--dim);}
.footer-text .eof{
  font-size:22px;font-weight:800;letter-spacing:4px;
  color:var(--fg);
  animation:flicker 5s ease-in-out infinite;
}
@keyframes flicker{0%,94%,100%{opacity:1;}95%{opacity:.3;}97%{opacity:.8;}98%{opacity:.2;}99%{opacity:1;}}

/* ══════════════════════════════════
   TERMINAL HEADER STRIP
══════════════════════════════════ */
.term{
  padding:20px 24px 18px;
  font-size:12px;line-height:2.1;
  border:3px solid var(--fg);border-top:none;
}
.t-line{
  display:flex;align-items:center;gap:10px;
  opacity:0;animation:tin .3s ease both;
}
.t-line:nth-child(1){animation-delay:.1s;}
.t-line:nth-child(2){animation-delay:.5s;}
.t-line:nth-child(3){animation-delay:.9s;}
.t-line:nth-child(4){animation-delay:1.3s;}
.t-line:nth-child(5){animation-delay:1.7s;}
@keyframes tin{from{opacity:0;transform:translateX(-6px);}to{opacity:1;transform:none;}}
.t-p{color:var(--dim);}
.t-o{color:#ccc;padding-left:16px;}
.caret{
  display:inline-block;width:7px;height:13px;
  background:var(--fg);vertical-align:middle;margin-left:2px;
  animation:blink .85s step-end infinite;
}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:0;}}

/* responsive */
@media(max-width:620px){
  .hero{grid-template-columns:1fr;}
  .hero-right{display:none;}
  .row3{grid-template-columns:1fr;}
  .cell{border-right:none;border-bottom:3px solid var(--fg);}
  .skills-wrap{grid-template-columns:1fr;}
  .skills-right{height:180px;}
  .thoughts-wrap{grid-template-columns:1fr;}
  .thoughts-char{width:100%;height:140px;border-right:none;border-bottom:3px solid var(--fg);}
  .stats-panel{grid-template-columns:1fr;}
  .stat-cell:first-child{border-right:none;border-bottom:3px solid var(--fg);}
  .footer{grid-template-columns:1fr;}
  .footer-char{display:none;}
}
</style>
</head>
<body>
<div class="wrap">

<!-- ══ HERO ══ -->
<div class="hero">
  <div class="hero-left">
    <div>
      <div class="hero-title">G R E J</div>
      <div class="hero-meta" style="margin-top:20px;">
        <p><b>developer.</b> builder. observer.</p>
        <p style="color:var(--dim);margin-top:4px;">somewhere between silence and source code.</p>
      </div>
    </div>
    <div style="font-size:10px;letter-spacing:3px;color:var(--dim);margin-top:24px;">
      ◉ SYSTEM ONLINE &nbsp;·&nbsp; ⟳ CODE COMPILING &nbsp;·&nbsp; ⚠ BUGS EXISTING
    </div>
  </div>

  <!-- HERO CHARACTER: spiky-hair coder, arms crossed, intense gaze -->
  <div class="hero-right">
    <svg class="char-hero" viewBox="0 0 180 310" fill="none" xmlns="http://www.w3.org/2000/svg">
      <!-- body shadow/screentone -->
      <defs>
        <pattern id="ht" x="0" y="0" width="4" height="4" patternUnits="userSpaceOnUse">
          <circle cx="1" cy="1" r=".8" fill="white" opacity=".25"/>
        </pattern>
      </defs>
      <!-- legs -->
      <rect x="58" y="220" width="26" height="80" rx="3" fill="white"/>
      <rect x="92" y="220" width="26" height="80" rx="3" fill="white"/>
      <rect x="60" y="295" width="26" height="12" rx="2" fill="#ccc"/>
      <rect x="94" y="295" width="26" height="12" rx="2" fill="#ccc"/>
      <!-- pants crease lines -->
      <line x1="71" y1="230" x2="71" y2="295" stroke="#0a0a0a" stroke-width="1.5"/>
      <line x1="105" y1="230" x2="105" y2="295" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- torso / jacket -->
      <path d="M42 130 L40 225 H140 L138 130 Q110 118 90 122 Q70 118 42 130Z" fill="white"/>
      <!-- jacket lapels -->
      <path d="M90 122 L78 150 L65 148 L50 132 Q68 124 90 122Z" fill="#1a1a1a"/>
      <path d="M90 122 L102 150 L115 148 L130 132 Q112 124 90 122Z" fill="#1a1a1a"/>
      <!-- jacket collar line -->
      <line x1="90" y1="122" x2="82" y2="175" stroke="#0a0a0a" stroke-width="1.5"/>
      <line x1="90" y1="122" x2="98" y2="175" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- belt -->
      <rect x="40" y="218" width="100" height="8" rx="1" fill="#0a0a0a"/>
      <rect x="82" y="216" width="16" height="11" rx="1" fill="#555"/>
      <!-- arms crossed -->
      <path d="M42 138 Q20 150 18 180 Q16 200 38 205 L50 202 Q48 182 55 165Z" fill="white"/>
      <path d="M138 138 Q160 150 162 180 Q164 200 142 205 L130 202 Q132 182 125 165Z" fill="white"/>
      <!-- crossed forearms -->
      <path d="M38 190 Q60 185 100 192 Q120 195 142 190 L140 205 Q118 210 100 207 Q62 210 40 205Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <path d="M38 200 Q60 195 100 202 Q120 205 142 200" stroke="#0a0a0a" stroke-width="1" stroke-dasharray="3 2"/>
      <!-- hands -->
      <ellipse cx="36" cy="203" rx="10" ry="7" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <ellipse cx="144" cy="203" rx="10" ry="7" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- neck -->
      <rect x="78" y="108" width="24" height="20" rx="4" fill="white"/>
      <!-- HEAD -->
      <ellipse cx="90" cy="88" rx="38" ry="40" fill="white"/>
      <!-- jaw sharpening -->
      <path d="M60 100 Q62 128 90 132 Q118 128 120 100" fill="white"/>
      <!-- ear -->
      <ellipse cx="51" cy="88" rx="8" ry="11" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <ellipse cx="129" cy="88" rx="8" ry="11" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- inner ear -->
      <ellipse cx="51" cy="88" rx="4" ry="6" fill="#ccc"/>
      <ellipse cx="129" cy="88" rx="4" ry="6" fill="#ccc"/>
      <!-- EYES — sharp, intense manga eyes -->
      <path d="M62 82 Q70 76 80 80 Q78 90 70 92 Q62 90 62 82Z" fill="#0a0a0a"/>
      <path d="M100 80 Q110 76 118 82 Q118 90 110 92 Q102 90 100 80Z" fill="#0a0a0a"/>
      <!-- eye shine -->
      <circle cx="66" cy="82" r="2.5" fill="white"/>
      <circle cx="104" cy="80" r="2.5" fill="white"/>
      <!-- pupils -->
      <circle cx="72" cy="85" r="4" fill="#1a1a1a"/>
      <circle cx="108" cy="85" r="4" fill="#1a1a1a"/>
      <!-- eyelid lines -->
      <path d="M62 82 Q70 76 80 80" stroke="#0a0a0a" stroke-width="2" fill="none"/>
      <path d="M100 80 Q110 76 118 82" stroke="#0a0a0a" stroke-width="2" fill="none"/>
      <!-- BROWS — sharp angled, serious expression -->
      <path d="M60 73 Q72 66 82 70" stroke="#0a0a0a" stroke-width="3" fill="none" stroke-linecap="round"/>
      <path d="M98 70 Q108 66 120 73" stroke="#0a0a0a" stroke-width="3" fill="none" stroke-linecap="round"/>
      <!-- nose -->
      <path d="M88 94 Q90 100 92 94" stroke="#0a0a0a" stroke-width="1.5" fill="none"/>
      <!-- mouth — slight smirk -->
      <path d="M82 110 Q90 115 102 108" stroke="#0a0a0a" stroke-width="2" fill="none" stroke-linecap="round"/>
      <!-- HAIR — spiky manga hair -->
      <path d="M54 72 Q48 50 60 36 Q52 40 50 28 Q66 38 70 30 Q74 18 90 14 Q106 18 110 30 Q114 38 130 28 Q128 40 120 36 Q132 50 126 72" fill="#0a0a0a"/>
      <!-- hair detail spikes -->
      <path d="M54 72 Q50 58 56 44 Q58 56 62 60Z" fill="#0a0a0a"/>
      <path d="M126 72 Q130 58 124 44 Q122 56 118 60Z" fill="#0a0a0a"/>
      <path d="M68 24 Q72 36 78 32 Q76 42 90 40 Q104 42 102 32 Q108 36 112 24 Q108 38 90 38 Q72 38 68 24Z" fill="#1a1a1a"/>
      <!-- hair strands -->
      <line x1="80" y1="14" x2="78" y2="38" stroke="#555" stroke-width="1"/>
      <line x1="90" y1="12" x2="90" y2="38" stroke="#555" stroke-width="1"/>
      <line x1="100" y1="14" x2="102" y2="38" stroke="#555" stroke-width="1"/>
      <!-- screentone on face shadow -->
      <path d="M54 90 Q52 110 60 120 Q62 130 90 132" fill="url(#ht)" opacity=".6"/>
      <!-- small action lines around figure -->
      <line x1="8" y1="60" x2="30" y2="75" stroke="white" stroke-width="1" opacity=".3"/>
      <line x1="4" y1="90" x2="28" y2="92" stroke="white" stroke-width="1" opacity=".25"/>
      <line x1="8" y1="120" x2="28" y2="112" stroke="white" stroke-width="1" opacity=".2"/>
      <line x1="172" y1="60" x2="150" y2="75" stroke="white" stroke-width="1" opacity=".3"/>
      <line x1="176" y1="90" x2="152" y2="92" stroke="white" stroke-width="1" opacity=".25"/>
    </svg>
  </div>
</div>

<!-- ══ TERMINAL ══ -->
<div class="term">
  <div class="t-line"><span class="t-p">$</span> <span>whoami</span></div>
  <div class="t-line"><span class="t-o">GREJ</span></div>
  <div class="t-line"><span class="t-p">$</span> <span>cat status.txt</span></div>
  <div class="t-line"><span class="t-o">building things. breaking things. rewriting things at 3am.</span></div>
  <div class="t-line"><span class="t-p">$</span> <span>exit</span> &nbsp;<span style="color:var(--dim);font-size:11px;">// permission denied</span><span class="caret"></span></div>
</div>

<!-- ══ CURRENTLY ══ -->
<div class="ticker-panel">
  <div class="ticker-label">$ currently</div>
  <div class="ticker-inner">
    <span>designing interfaces</span><span class="dot"> ◆ </span>
    <span>writing C++</span><span class="dot"> ◆ </span>
    <span>building random projects</span><span class="dot"> ◆ </span>
    <span>fixing bugs i probably created</span><span class="dot"> ◆ </span>
    <span>trying not to rewrite everything</span><span class="dot"> ◆ </span>
    <span>designing interfaces</span><span class="dot"> ◆ </span>
    <span>writing C++</span><span class="dot"> ◆ </span>
    <span>building random projects</span><span class="dot"> ◆ </span>
    <span>fixing bugs i probably created</span><span class="dot"> ◆ </span>
    <span>trying not to rewrite everything</span><span class="dot"> ◆ </span>
  </div>
</div>

<!-- ══ SKILLS ══ -->
<div class="sec">$ stack</div>
<div class="skills-wrap">
  <div class="skills-left">
    <div class="skill-row" style="animation-delay:.05s">
      <div class="skill-name">C++</div>
      <div class="bar-track"><div class="bar-fill" style="--w:95%;animation-delay:.1s"></div></div>
      <div class="bar-pct">95</div>
    </div>
    <div class="skill-row">
      <div class="skill-name">ImGui</div>
      <div class="bar-track"><div class="bar-fill" style="--w:90%;animation-delay:.2s"></div></div>
      <div class="bar-pct">90</div>
    </div>
    <div class="skill-row">
      <div class="skill-name">UI / UX</div>
      <div class="bar-track"><div class="bar-fill" style="--w:85%;animation-delay:.3s"></div></div>
      <div class="bar-pct">85</div>
    </div>
    <div class="skill-row">
      <div class="skill-name">Systems</div>
      <div class="bar-track"><div class="bar-fill" style="--w:75%;animation-delay:.4s"></div></div>
      <div class="bar-pct">75</div>
    </div>
    <div class="skill-row">
      <div class="skill-name">Web</div>
      <div class="bar-track"><div class="bar-fill" style="--w:70%;animation-delay:.5s"></div></div>
      <div class="bar-pct">70</div>
    </div>
    <div style="border-top:1px solid var(--line);padding-top:12px;margin-top:4px;display:flex;flex-wrap:wrap;gap:8px;">
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">C++</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">C#</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">Python</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">React</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">Next.js</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">Node.js</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">ImGui</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">DX11</span>
      <span style="font-size:9px;letter-spacing:2px;color:var(--dim);border:1px solid var(--line);padding:3px 8px;">Win32</span>
    </div>
  </div>

  <!-- CHARACTER: girl with laptop, sitting cross-legged -->
  <div class="skills-right">
    <svg viewBox="0 0 220 280" fill="none" xmlns="http://www.w3.org/2000/svg" style="width:100%;height:100%;display:block;">
      <!-- floor shadow -->
      <ellipse cx="110" cy="268" rx="70" ry="8" fill="#1a1a1a"/>
      <!-- legs cross-legged -->
      <path d="M60 200 Q50 230 48 255 Q70 258 85 252 Q82 230 80 215Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <path d="M160 200 Q170 230 172 255 Q150 258 135 252 Q138 230 140 215Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- cross-leg overlap -->
      <path d="M75 230 Q110 220 145 230 Q148 248 110 252 Q72 248 75 230Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- laptop -->
      <rect x="62" y="198" width="96" height="60" rx="4" fill="#1a1a1a" stroke="white" stroke-width="2"/>
      <rect x="66" y="202" width="88" height="52" rx="2" fill="#111"/>
      <!-- code on screen -->
      <rect x="70" y="208" width="40" height="2.5" rx="1" fill="#555"/>
      <rect x="70" y="214" width="60" height="2.5" rx="1" fill="#444"/>
      <rect x="74" y="220" width="30" height="2.5" rx="1" fill="#555"/>
      <rect x="74" y="226" width="50" height="2.5" rx="1" fill="#444"/>
      <rect x="70" y="232" width="45" height="2.5" rx="1" fill="#555"/>
      <rect x="70" y="238" width="35" height="2.5" rx="1" fill="#444"/>
      <!-- cursor blink on screen -->
      <rect x="110" y="238" width="5" height="8" rx="1" fill="white" opacity=".8">
        <animate attributeName="opacity" values="0.8;0;0.8" dur="1s" repeatCount="indefinite"/>
      </rect>
      <!-- laptop hinge -->
      <rect x="62" y="256" width="96" height="6" rx="2" fill="#222" stroke="white" stroke-width="1.5"/>
      <!-- torso -->
      <path d="M68 150 L64 200 L156 200 L152 150 Q130 138 110 142 Q90 138 68 150Z" fill="white"/>
      <!-- hoodie pocket -->
      <rect x="90" y="175" width="40" height="22" rx="3" fill="#eee" stroke="#0a0a0a" stroke-width="1.5"/>
      <line x1="110" y1="175" x2="110" y2="197" stroke="#0a0a0a" stroke-width="1"/>
      <!-- hoodie drawstrings -->
      <line x1="102" y1="148" x2="99" y2="175" stroke="#888" stroke-width="1.5"/>
      <line x1="118" y1="148" x2="121" y2="175" stroke="#888" stroke-width="1.5"/>
      <!-- arms on laptop -->
      <path d="M68 158 Q44 165 42 185 Q40 200 55 205 L65 202 Q62 190 68 178Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <path d="M152 158 Q176 165 178 185 Q180 200 165 205 L155 202 Q158 190 152 178Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- hands on keyboard -->
      <ellipse cx="78" cy="206" rx="14" ry="8" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <ellipse cx="142" cy="206" rx="14" ry="8" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- fingers -->
      <path d="M68 203 Q65 198 68 195" stroke="#0a0a0a" stroke-width="1.2" fill="none"/>
      <path d="M73 201 Q70 195 73 192" stroke="#0a0a0a" stroke-width="1.2" fill="none"/>
      <path d="M148 203 Q151 198 148 195" stroke="#0a0a0a" stroke-width="1.2" fill="none"/>
      <path d="M143 201 Q146 195 143 192" stroke="#0a0a0a" stroke-width="1.2" fill="none"/>
      <!-- neck -->
      <rect x="98" y="130" width="24" height="18" rx="4" fill="white"/>
      <!-- HEAD -->
      <ellipse cx="110" cy="108" rx="36" ry="38" fill="white"/>
      <path d="M80 115 Q82 138 110 142 Q138 138 140 115" fill="white"/>
      <!-- ear -->
      <ellipse cx="73" cy="108" rx="7" ry="10" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <ellipse cx="147" cy="108" rx="7" ry="10" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- EYES — big, focused, slight bags (coder look) -->
      <path d="M82 102 Q92 96 100 100 Q99 110 92 112 Q84 110 82 102Z" fill="#0a0a0a"/>
      <path d="M120 100 Q128 96 138 102 Q138 110 130 112 Q122 110 120 100Z" fill="#0a0a0a"/>
      <circle cx="86" cy="102" r="2" fill="white"/>
      <circle cx="124" cy="100" r="2" fill="white"/>
      <circle cx="92" cy="105" r="4.5" fill="#1a1a1a"/>
      <circle cx="130" cy="105" r="4.5" fill="#1a1a1a"/>
      <!-- eyelashes (girl) -->
      <path d="M82 102 L80 98 M84 100 L82 95 M87 99 L85 94" stroke="#0a0a0a" stroke-width="1.5"/>
      <path d="M138 102 L140 98 M136 100 L138 95 M133 99 L135 94" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- eyebrows -->
      <path d="M80 94 Q92 88 102 92" stroke="#0a0a0a" stroke-width="2.5" fill="none" stroke-linecap="round"/>
      <path d="M118 92 Q128 88 140 94" stroke="#0a0a0a" stroke-width="2.5" fill="none" stroke-linecap="round"/>
      <!-- nose small -->
      <path d="M108 116 Q110 121 112 116" stroke="#0a0a0a" stroke-width="1.5" fill="none"/>
      <!-- mouth — focused pout -->
      <path d="M101 128 Q110 132 119 128" stroke="#0a0a0a" stroke-width="2" fill="none" stroke-linecap="round"/>
      <!-- HAIR — long, flowing side ponytail -->
      <path d="M74 90 Q68 60 80 42 Q72 48 68 34 Q84 42 86 28 Q94 16 110 14 Q126 16 128 28 Q136 24 148 34 Q142 48 136 42 Q148 60 142 90" fill="#0a0a0a"/>
      <!-- ponytail going down right -->
      <path d="M142 90 Q158 110 160 150 Q162 180 148 200 Q138 180 140 150 Q138 120 132 100Z" fill="#0a0a0a"/>
      <!-- hair shine streak -->
      <path d="M88 28 Q90 50 88 80" stroke="#888" stroke-width="2" fill="none" opacity=".6"/>
      <path d="M94 25 Q96 48 94 78" stroke="#666" stroke-width="1" fill="none" opacity=".4"/>
      <!-- hair band -->
      <ellipse cx="148" cy="108" rx="6" ry="10" fill="none" stroke="white" stroke-width="2"/>
      <!-- little sweat drop (focus) -->
      <path d="M150 75 Q152 68 148 72Z" fill="white" stroke="#0a0a0a" stroke-width="1"/>
    </svg>
  </div>
</div>

<!-- ══ PROJECTS ══ -->
<div class="sec">$ projects</div>
<div class="row3">
  <div class="cell">
    <div class="cell-num">01 /</div>
    <div class="cell-title">INTERFACES</div>
    <div class="cell-body">custom UI.<br>pixels → logic → motion.</div>
    <div class="cell-tag">C++ · ImGui · DX11</div>
    <!-- tiny decorative char silhouette -->
    <svg class="char-cell" viewBox="0 0 60 90" fill="none">
      <ellipse cx="30" cy="18" rx="12" ry="13" fill="white" opacity=".5"/>
      <path d="M18 32 L14 80 H46 L42 32 Q36 28 30 29 Q24 28 18 32Z" fill="white" opacity=".5"/>
      <path d="M20 20 Q14 10 20 4 Q22 8 24 6 Q26 2 30 0 Q34 2 36 6 Q38 8 40 4 Q46 10 40 20" fill="#0a0a0a" opacity=".6"/>
    </svg>
  </div>
  <div class="cell">
    <div class="cell-num">02 /</div>
    <div class="cell-title">SYSTEMS</div>
    <div class="cell-body">close to the machine.<br>exploring how it works.</div>
    <div class="cell-tag">C++ · Win32 · Native</div>
  </div>
  <div class="cell" style="border-right:none;">
    <div class="cell-num">03 /</div>
    <div class="cell-title">WEB</div>
    <div class="cell-body">ideas made accessible.<br>frontend → backend.</div>
    <div class="cell-tag">React · Next.js · Node</div>
  </div>
</div>
<div class="row3" style="border-top:3px solid var(--fg);">
  <div class="cell" style="grid-column:1/-1;border-right:none;display:flex;align-items:center;gap:24px;">
    <div>
      <div class="cell-num">04 /</div>
      <div class="cell-title">EXPERIMENTS</div>
      <div class="cell-body">/dev/null. ideas without a roadmap. still not deleting them.</div>
    </div>
  </div>
</div>

<!-- ══ THOUGHTS ══ -->
<div class="sec">$ thoughts.log</div>
<div class="thoughts-wrap">
  <!-- CHARACTER: leaning guy, contemplative -->
  <div class="thoughts-char">
    <svg viewBox="0 0 150 300" fill="none" xmlns="http://www.w3.org/2000/svg" style="width:100%;height:100%;display:block;">
      <defs>
        <pattern id="ht2" x="0" y="0" width="5" height="5" patternUnits="userSpaceOnUse">
          <circle cx="1" cy="1" r=".9" fill="white" opacity=".2"/>
        </pattern>
      </defs>
      <!-- legs -->
      <rect x="40" y="210" width="22" height="78" rx="3" fill="white"/>
      <rect x="88" y="210" width="22" height="78" rx="3" fill="white"/>
      <rect x="40" y="283" width="23" height="12" rx="2" fill="#ccc"/>
      <rect x="88" y="283" width="23" height="12" rx="2" fill="#ccc"/>
      <line x1="51" y1="218" x2="51" y2="282" stroke="#0a0a0a" stroke-width="1.2"/>
      <line x1="99" y1="218" x2="99" y2="282" stroke="#0a0a0a" stroke-width="1.2"/>
      <!-- body -->
      <path d="M28 125 L26 215 H124 L122 125 Q100 112 75 116 Q50 112 28 125Z" fill="white"/>
      <!-- hoodie -->
      <path d="M75 116 L65 142 L52 140 L38 127 Q55 118 75 116Z" fill="#1a1a1a"/>
      <path d="M75 116 L85 142 L98 140 L112 127 Q95 118 75 116Z" fill="#1a1a1a"/>
      <line x1="75" y1="116" x2="68" y2="170" stroke="#0a0a0a" stroke-width="1.5"/>
      <line x1="75" y1="116" x2="82" y2="170" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- belt -->
      <rect x="26" y="208" width="98" height="7" rx="1" fill="#0a0a0a"/>
      <!-- left arm leaning on something (elbow prop) -->
      <path d="M28 133 Q6 148 4 174 Q2 196 24 200 L36 197 Q34 177 40 160Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- right arm at side -->
      <path d="M122 133 Q144 145 146 168 Q148 188 130 195 L118 192 Q120 174 116 158Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- left hand (chin resting) -->
      <ellipse cx="22" cy="198" rx="10" ry="7" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- right hand -->
      <ellipse cx="132" cy="193" rx="10" ry="7" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- neck -->
      <rect x="62" y="103" width="24" height="18" rx="4" fill="white"/>
      <!-- HEAD tilted slightly -->
      <ellipse cx="75" cy="82" rx="34" ry="37" fill="white"/>
      <path d="M46 92 Q48 118 75 122 Q102 118 104 92" fill="white"/>
      <!-- ear -->
      <ellipse cx="40" cy="82" rx="7" ry="10" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <ellipse cx="110" cy="82" rx="7" ry="10" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- EYES — half-closed, tired but thoughtful -->
      <path d="M48 76 Q57 71 65 74" stroke="#0a0a0a" stroke-width="2.5" fill="none"/>
      <path d="M48 80 Q57 83 65 80" stroke="#0a0a0a" stroke-width="1.5" fill="none"/>
      <ellipse cx="56" cy="78" rx="6" ry="4.5" fill="#0a0a0a"/>
      <circle cx="52" cy="77" r="1.5" fill="white"/>
      <path d="M85 74 Q93 71 102 76" stroke="#0a0a0a" stroke-width="2.5" fill="none"/>
      <path d="M85 80 Q93 83 102 80" stroke="#0a0a0a" stroke-width="1.5" fill="none"/>
      <ellipse cx="93" cy="78" rx="6" ry="4.5" fill="#0a0a0a"/>
      <circle cx="90" cy="77" r="1.5" fill="white"/>
      <!-- eyebags (tired coder) -->
      <path d="M48 83 Q56 86 65 83" stroke="#aaa" stroke-width="1" fill="none"/>
      <path d="M85 83 Q93 86 102 83" stroke="#aaa" stroke-width="1" fill="none"/>
      <!-- brows — relaxed, slightly furrowed in thought -->
      <path d="M46 68 Q57 63 67 67" stroke="#0a0a0a" stroke-width="2.5" fill="none" stroke-linecap="round"/>
      <path d="M83 67 Q93 63 104 68" stroke="#0a0a0a" stroke-width="2.5" fill="none" stroke-linecap="round"/>
      <!-- nose -->
      <path d="M73 95 Q75 100 77 95" stroke="#0a0a0a" stroke-width="1.5" fill="none"/>
      <!-- mouth — neutral, pensive -->
      <path d="M65 108 Q75 112 85 110" stroke="#0a0a0a" stroke-width="2" fill="none" stroke-linecap="round"/>
      <!-- thought dot above head -->
      <circle cx="118" cy="48" r="4" fill="white" opacity=".6"/>
      <circle cx="128" cy="34" r="6" fill="white" opacity=".5"/>
      <circle cx="135" cy="18" r="9" fill="white" opacity=".4"/>
      <!-- HAIR -->
      <path d="M42 68 Q38 42 50 26 Q42 32 40 20 Q56 28 58 16 Q64 6 75 4 Q86 6 92 16 Q94 28 110 20 Q108 32 100 26 Q112 42 108 68" fill="#0a0a0a"/>
      <path d="M60 10 Q62 30 60 65" stroke="#555" stroke-width="1.5" fill="none"/>
      <path d="M75 6 Q76 28 75 65" stroke="#555" stroke-width="1" fill="none"/>
      <!-- screentone shadow on half face -->
      <path d="M42 70 Q40 92 46 112 Q48 122 75 122" fill="url(#ht2)" opacity=".8"/>
    </svg>
  </div>

  <div class="bubbles">
    <div class="bub l">The world is loud.</div>
    <div class="bub r">so i build things that make sense to me.</div>
    <div class="bub l">there's no perfect system.</div>
    <div class="bub r">only systems waiting for their next failure.</div>
    <div class="bub l" style="border-style:dashed;font-style:italic;color:var(--dim);">sometimes code is easier than explaining yourself.</div>
  </div>
</div>

<!-- ══ GITHUB STATS ══ -->
<div class="sec">$ github_activity</div>
<div class="stats-panel">
  <div class="stat-cell">
    <img src="https://github-readme-stats.vercel.app/api?username=grejlovescode&show_icons=true&hide_border=true&bg_color=0a0a0a&title_color=ffffff&text_color=d4d4d8&icon_color=aaaaaa" alt="stats" loading="lazy"/>
  </div>
  <div class="stat-cell">
    <img src="https://streak-stats.demolab.com?user=grejlovescode&hide_border=true&background=0a0a0a&ring=ffffff&fire=aaaaaa&currStreakLabel=ffffff&sideLabels=d4d4d8&dates=71717a&currStreakNum=f4f4f5&sideNums=f4f4f5" alt="streak" loading="lazy"/>
  </div>
</div>
<div class="graph-panel">
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=grejlovescode&bg_color=0a0a0a&color=d4d4d8&line=aaaaaa&point=ffffff&area=true&hide_border=true" alt="activity" loading="lazy"/>
</div>

<!-- ══ SNAKE ══ -->
<div class="snake-panel">
  <div class="snake-label">contribution protocol</div>
  <img src="https://raw.githubusercontent.com/Platane/snk/output/github-contribution-grid-snake-dark.svg" alt="snake"/>
  <!-- char peeking from corner -->
  <svg class="char-corner" viewBox="0 0 90 110" fill="none">
    <!-- peeking figure: just head + hands over edge -->
    <ellipse cx="45" cy="55" rx="28" ry="30" fill="white" opacity=".7"/>
    <ellipse cx="27" cy="58" rx="6" ry="8" fill="white" opacity=".7"/>
    <ellipse cx="63" cy="58" rx="6" ry="8" fill="white" opacity=".7"/>
    <!-- eyes wide with curiosity -->
    <circle cx="37" cy="52" r="5" fill="#0a0a0a" opacity=".9"/>
    <circle cx="53" cy="52" r="5" fill="#0a0a0a" opacity=".9"/>
    <circle cx="35" cy="50" r="1.8" fill="white" opacity=".9"/>
    <circle cx="51" cy="50" r="1.8" fill="white" opacity=".9"/>
    <!-- eyebrows raised (curious) -->
    <path d="M32 44 Q38 40 43 43" stroke="#0a0a0a" stroke-width="2" fill="none" opacity=".8"/>
    <path d="M47 43 Q52 40 58 44" stroke="#0a0a0a" stroke-width="2" fill="none" opacity=".8"/>
    <!-- mouth: open O of surprise -->
    <ellipse cx="45" cy="66" rx="5" ry="6" fill="#0a0a0a" opacity=".8"/>
    <!-- hair -->
    <path d="M18 48 Q16 30 28 20 Q22 24 20 14 Q32 20 34 10 Q38 2 45 0 Q52 2 56 10 Q58 20 70 14 Q68 24 62 20 Q74 30 72 48" fill="#0a0a0a" opacity=".7"/>
    <!-- hands gripping bottom -->
    <ellipse cx="27" cy="84" rx="12" ry="7" fill="white" opacity=".6"/>
    <ellipse cx="63" cy="84" rx="12" ry="7" fill="white" opacity=".6"/>
    <line x1="22" y1="80" x2="20" y2="90" stroke="#0a0a0a" stroke-width="1.5" opacity=".6"/>
    <line x1="27" y1="78" x2="25" y2="90" stroke="#0a0a0a" stroke-width="1.5" opacity=".6"/>
    <line x1="32" y1="80" x2="30" y2="90" stroke="#0a0a0a" stroke-width="1.5" opacity=".6"/>
    <line x1="58" y1="80" x2="60" y2="90" stroke="#0a0a0a" stroke-width="1.5" opacity=".6"/>
    <line x1="63" y1="78" x2="65" y2="90" stroke="#0a0a0a" stroke-width="1.5" opacity=".6"/>
    <line x1="68" y1="80" x2="70" y2="90" stroke="#0a0a0a" stroke-width="1.5" opacity=".6"/>
  </svg>
</div>

<!-- ══ FOOTER ══ -->
<div class="sec"></div>
<div class="footer">
  <!-- CHARACTER: tired, waving goodbye -->
  <div class="footer-char">
    <svg viewBox="0 0 120 220" fill="none" xmlns="http://www.w3.org/2000/svg" style="width:100%;display:block;">
      <!-- legs -->
      <rect x="34" y="158" width="18" height="52" rx="3" fill="white"/>
      <rect x="68" y="158" width="18" height="52" rx="3" fill="white"/>
      <!-- body -->
      <path d="M24 92 L22 162 H98 L96 92 Q80 82 60 86 Q40 82 24 92Z" fill="white"/>
      <!-- shirt design: simple stripes -->
      <line x1="40" y1="92" x2="40" y2="160" stroke="#ddd" stroke-width="1.5"/>
      <line x1="60" y1="90" x2="60" y2="160" stroke="#ddd" stroke-width="1.5"/>
      <line x1="80" y1="92" x2="80" y2="160" stroke="#ddd" stroke-width="1.5"/>
      <!-- belt -->
      <rect x="22" y="156" width="76" height="7" rx="1" fill="#0a0a0a"/>
      <!-- left arm waving up -->
      <path d="M24 100 Q-2 80 2 54 Q4 36 20 30 L28 38 Q18 50 20 68 Q22 84 30 94Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- waving hand -->
      <ellipse cx="20" cy="27" rx="12" ry="10" fill="white" stroke="#0a0a0a" stroke-width="1.5" transform="rotate(-20,20,27)"/>
      <line x1="12" y1="20" x2="8" y2="10" stroke="#0a0a0a" stroke-width="1.5"/>
      <line x1="17" y1="17" x2="14" y2="6" stroke="#0a0a0a" stroke-width="1.5"/>
      <line x1="22" y1="17" x2="22" y2="6" stroke="#0a0a0a" stroke-width="1.5"/>
      <line x1="27" y1="19" x2="29" y2="9" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- right arm at side -->
      <path d="M96 100 Q110 118 108 148 L96 152 Q94 128 92 108Z" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <ellipse cx="102" cy="156" rx="10" ry="7" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- neck -->
      <rect x="50" y="74" width="20" height="16" rx="4" fill="white"/>
      <!-- HEAD -->
      <ellipse cx="60" cy="56" rx="30" ry="32" fill="white"/>
      <path d="M34 65 Q36 85 60 88 Q84 85 86 65" fill="white"/>
      <!-- ear -->
      <ellipse cx="29" cy="56" rx="6" ry="9" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <ellipse cx="91" cy="56" rx="6" ry="9" fill="white" stroke="#0a0a0a" stroke-width="1.5"/>
      <!-- EYES — closed/squinting from smiling / tired -->
      <path d="M38 52 Q46 48 54 52 Q52 57 46 58 Q40 57 38 52Z" fill="#0a0a0a"/>
      <circle cx="41" cy="52" r="1.8" fill="white"/>
      <path d="M66 52 Q74 48 82 52 Q80 57 74 58 Q68 57 66 52Z" fill="#0a0a0a"/>
      <circle cx="69" cy="52" r="1.8" fill="white"/>
      <!-- sleepy/smile lines under eyes -->
      <path d="M38 60 Q46 63 54 60" stroke="#aaa" stroke-width="1" fill="none"/>
      <path d="M66 60 Q74 63 82 60" stroke="#aaa" stroke-width="1" fill="none"/>
      <!-- brows — relaxed -->
      <path d="M37 44 Q46 39 55 43" stroke="#0a0a0a" stroke-width="2.5" fill="none" stroke-linecap="round"/>
      <path d="M65 43 Q74 39 83 44" stroke="#0a0a0a" stroke-width="2.5" fill="none" stroke-linecap="round"/>
      <!-- nose -->
      <path d="M58 70 Q60 74 62 70" stroke="#0a0a0a" stroke-width="1.5" fill="none"/>
      <!-- mouth — tired smile -->
      <path d="M50 80 Q60 86 70 80" stroke="#0a0a0a" stroke-width="2" fill="none" stroke-linecap="round"/>
      <!-- HAIR -->
      <path d="M30 46 Q26 24 38 10 Q30 16 28 6 Q42 14 44 4 Q50 -2 60 -2 Q70 -2 76 4 Q78 14 92 6 Q90 16 82 10 Q94 24 90 46" fill="#0a0a0a"/>
      <!-- small z's (sleepy) -->
      <text x="96" y="22" font-family="monospace" font-size="12" fill="white" opacity=".5">z</text>
      <text x="104" y="12" font-family="monospace" font-size="9" fill="white" opacity=".35">z</text>
      <text x="110" y="5" font-family="monospace" font-size="7" fill="white" opacity=".2">z</text>
    </svg>
  </div>

  <div class="footer-text">
    <p style="font-size:9px;letter-spacing:3px;">// session ending</p>
    <div class="eof">EOF</div>
    <p>saving changes...</p>
    <p>compiling memories...</p>
    <p style="font-size:10px;letter-spacing:3px;">goodbye.</p>
    <p style="margin-top:8px;font-size:9px;color:#444;letter-spacing:2px;">grejlovescode · github</p>
  </div>
</div>

</div>
</body>
</html>

<!doctype html>
<html lang="cs">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>made by OFFON. (precise location)</title>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg1:#0c0f1a; --bg2:#1b1f2f; --accent:#ff4d4d; --muted:rgba(255,255,255,0.65);
  --green:#7CFC00;
}
*{box-sizing:border-box}
html,body{height:100%;margin:0;font-family:'Roboto Mono',monospace;background:linear-gradient(180deg,var(--bg1),var(--bg2));color:#fff;overflow:hidden}
#loginCard{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);width:380px;padding:28px;border-radius:12px;background:rgba(255,255,255,0.02);box-shadow:0 20px 60px rgba(0,0,0,0.7);text-align:center;z-index:12}
h2{margin:0 0 8px;font-weight:700}
.lead{color:var(--muted);font-size:14px;margin-bottom:12px}
input{width:88%;padding:10px 12px;margin:8px 0;border-radius:8px;border:none;background:rgba(255,255,255,0.03);color:#fff;outline:none}
button.primary{padding:10px 18px;border-radius:10px;border:none;background:linear-gradient(90deg,var(--accent),#b33);color:#fff;font-weight:700;cursor:pointer;box-shadow:0 8px 30px rgba(255,0,0,0.12)}
button.primary:hover{transform:translateY(-2px)}
#error{height:20px;color:#ff8b8b;margin-top:8px;font-weight:700}

/* secret */
#secretBox{position:fixed;width:64px;height:64px;border-radius:50%;background:#0b0b0f;border:2px solid rgba(255,255,255,0.04);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:20px;cursor:pointer;z-index:14;transition:transform .25s,opacity .3s}
#secretBox.revealed{width:220px;height:56px;border-radius:12px;background:rgba(255,255,255,0.03);font-size:16px;color:#fff;padding:6px 12px;}

/* toast */
#copiedToast{position:fixed;left:50%;top:12%;transform:translateX(-50%);padding:10px 16px;border-radius:10px;background:rgba(0,0,0,0.75);color:#fff;opacity:0;pointer-events:none;transition:opacity .35s;z-index:30}
#copiedToast.show{opacity:1}

/* overlay panel */
#overlay{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;z-index:20;pointer-events:none;opacity:0;transition:opacity .35s}
#overlay.active{opacity:1;pointer-events:auto}
#panel{width:92%;max-width:1000px;background:linear-gradient(180deg, rgba(0,0,0,0.76), rgba(0,0,0,0.66));border-radius:12px;padding:18px;box-shadow:0 30px 80px rgba(0,0,0,0.8);position:relative;overflow:hidden}

/* scan text (typewriter + fake lines) */
#scanArea{display:flex;gap:18px;flex-wrap:wrap;align-items:flex-start}
#scanText{flex:1;min-width:320px;max-width:640px;height:360px;overflow:auto;background:rgba(0,0,0,0.14);padding:12px;border-radius:8px;color:#ffb3b3;font-family:monospace;white-space:pre-wrap;font-size:13px;line-height:1.25;border:1px solid rgba(255,255,255,0.02)}
#leftCol{min-width:240px;max-width:320px}

/* info blocks */
.infoBlock{background:rgba(255,255,255,0.02);padding:12px;border-radius:8px;margin-bottom:10px;color:var(--muted);font-size:13px}
#ipBig{font-size:20px;font-weight:800;color:#ffdede}
.smallLabel{font-size:12px;color:#cfcfcf;margin-bottom:6px}

/* percent bar */
#percentWrap{margin-top:8px}
#percentBar{width:100%;height:12px;background:rgba(255,255,255,0.04);border-radius:8px;overflow:hidden}
#percentFill{height:100%;width:0%;background:linear-gradient(90deg,#ff6b6b,#ff1f1f);transition:width .25s linear}

/* blood full screen */
.blood-layer{position:fixed;inset:0;pointer-events:none;z-index:50;overflow:hidden}
.drip{position:absolute;top:-260px;background:linear-gradient(180deg,rgba(120,0,0,0.95),rgba(160,0,0,0.9));border-radius:10px;opacity:0.94;box-shadow:0 8px 20px rgba(120,0,0,0.45)}
@keyframes dripSlow{0%{transform:translateY(-260px);opacity:0}10%{opacity:1}90%{transform:translateY(100vh);opacity:1}100%{transform:translateY(100vh);opacity:0}}
.splat{position:absolute;border-radius:50%;background:radial-gradient(circle at 30% 30%,rgba(160,0,0,0.95),rgba(120,0,0,0.9));opacity:0.95;animation:splatFade 2.2s linear forwards}
@keyframes splatFade{0%{transform:scale(.6);opacity:1}100%{transform:scale(1.4);opacity:0}}

/* glitch overlay */
.glitch{position:absolute;inset:0;pointer-events:none;mix-blend-mode:screen;z-index:40}
.glitch .line{position:absolute;height:2px;background:linear-gradient(90deg,transparent,#ff6b6b,transparent);opacity:0.06;animation:glitchLine 3s linear infinite}
@keyframes glitchLine{0%{transform:translateX(-120%)}50%{transform:translateX(120%)}100%{transform:translateX(-120%)}}

/* spotlight for verified location */
.location-spot{border:2px solid rgba(255,30,30,0.9);box-shadow:0 0 30px rgba(255,20,20,0.06);border-radius:10px;padding:8px;animation:pulseRed 1.6s ease-in-out infinite}
@keyframes pulseRed{0%{box-shadow:0 0 6px rgba(255,50,50,0.06)}50%{box-shadow:0 0 30px rgba(255,30,30,0.18)}100%{box-shadow:0 0 6px rgba(255,50,50,0.06)}}

/* typewriter small */
.typewriter { font-family: monospace; white-space:pre-wrap; overflow-wrap: anywhere; }
.typewriter .ch{opacity:0;display:inline-block;animation:tw 0.02s forwards}
@keyframes tw{0%{opacity:0}100%{opacity:1}}

/* small utility */
.small{font-size:12px;color:var(--muted)}
.controls{display:flex;gap:8px;align-items:center;justify-content:flex-end}
footer{position:fixed;bottom:8px;width:100%;text-align:center;color:rgba(255,255,255,0.3);font-size:12px;z-index:5}
.map-links a{color:#ffdede;text-decoration:none;font-weight:700;margin-right:8px}
.muteBtn{background:#333;color:#fff;padding:8px 10px;border-radius:8px;border:none;cursor:pointer}
</style>
</head>
<body>

<!-- LOGIN CARD (no storing passwords) -->
<div id="loginCard" role="dialog" aria-modal="false">
  <h2>Vítej — OFFON</h2>
  <div class="lead"> login Žádné ukládání hesel.</div>
  <input id="username" placeholder="Uživatelské jméno (libovolné)">
  <input id="secretInput" placeholder="Tajné heslo">
  <div style="display:flex;gap:8px;justify-content:center;margin-top:8px">
    <button class="primary" onclick="login()">Přihlásit se</button>
    <button class="muteBtn" id="globalMute">Mute</button>
  </div>
  <div id="error" class="small" style="height:18px;margin-top:8px;color:#ff9b9b"></div>
</div>

<!-- SECRET BOX -->
<div id="secretBox" title="Klikni pro tajné heslo">?</div>
<div id="copiedToast">Zkopírováno do schránky!</div>

<!-- OVERLAY (SCAN) -->
<div id="overlay" aria-hidden="true">
  <div id="panel" role="dialog" aria-modal="true">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <div class="smallLabel">SCANNING MODULE — OFFON</div>
      <div class="controls small">
        <div id="scanStatus">Idle</div>
      </div>
    </div>

    <div id="scanArea" style="margin-top:12px">
      <div id="scanText" class="typewriter" aria-live="polite">Preparing scan...</div>

      <div id="leftCol">
        <div class="infoBlock">
          <div class="smallLabel">TVŮJE IP</div>
          <div id="ipBig">Načítám…</div>
          <div id="percentWrap" class="small" style="margin-top:8px">
            <div id="percentBar"><div id="percentFill"></div></div>
          </div>
        </div>

        <div class="infoBlock">
          <div class="smallLabel">Device info</div>
          <div id="deviceInfo">—</div>
        </div>

        <div class="infoBlock">
          <div class="smallLabel">Další</div>
          <div id="moreInfo" class="small">—</div>
        </div>

        <div class="infoBlock">
          <div class="smallLabel">Lokace (IP)</div>
          <div id="locationQuick" class="small">—</div>
          <div style="margin-top:8px">
            <button id="openLocationBtn" class="muteBtn">Získat přesnou polohu</button>
          </div>
        </div>

        <div style="text-align:right;margin-top:8px"><button id="backBtn" class="muteBtn">ZPĚT</button></div>
      </div>
    </div>

    <div style="margin-top:12px" class="map-links" id="mapLinksRow"></div>
  </div>

  <!-- glitch lines -->
  <div class="glitch" aria-hidden="true">
    <div class="line" style="top:20%;width:60%;left:-60%"></div>
    <div class="line" style="top:45%;width:80%;left:-80%;animation-duration:4s"></div>
    <div class="line" style="top:70%;width:70%;left:-70%;animation-duration:3.6s"></div>
  </div>
</div>

<!-- LOCATION PANEL -->
<div id="locationOverlay" aria-hidden="true" style="position:fixed;inset:0;display:flex;align-items:center;justify-content:center;z-index:30;pointer-events:none;opacity:0;transition:opacity .3s">
  <div id="locationPanel" style="width:80%;max-width:720px;background:rgba(10,10,10,0.95);padding:18px;border-radius:12px;color:#fff;border:1px solid rgba(255,255,255,0.03);pointer-events:auto">
    <h3 style="margin:0 0 8px">TVOJE LOKACE</h3>
    <div id="locationInfo" style="white-space:pre-wrap;font-family:monospace">Počkej na dokončení scanu nebo klikni 'Získat přesnou polohu'.</div>
    <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:12px">
      <button id="locBackBtn" class="muteBtn">ZPĚT</button>
    </div>
  </div>
</div>

<!-- BLOOD LAYER -->
<div class="blood-layer" id="bloodLayer" aria-hidden="true"></div>

<footer>© Copyright reserved OFFON</footer>

<script>
/* ------------------ Vars & Elements ------------------ */
const secretBox = document.getElementById('secretBox');
const copiedToast = document.getElementById('copiedToast');
const overlay = document.getElementById('overlay');
const scanTextEl = document.getElementById('scanText');
const ipBig = document.getElementById('ipBig');
const deviceInfo = document.getElementById('deviceInfo');
const moreInfo = document.getElementById('moreInfo');
const percentFill = document.getElementById('percentFill');
const scanStatus = document.getElementById('scanStatus');
const locationQuick = document.getElementById('locationQuick');
const openLocationBtn = document.getElementById('openLocationBtn');
const locationOverlay = document.getElementById('locationOverlay');
const locationInfo = document.getElementById('locationInfo');
const mapLinksRow = document.getElementById('mapLinksRow');
const backBtn = document.getElementById('backBtn');
const locBackBtn = document.getElementById('locBackBtn');
const loginCard = document.getElementById('loginCard');
const globalMuteBtn = document.getElementById('globalMute');

let revealed = false;
let publicIP = null;
let audioCtx = null;
let masterGain = null;
let isMuted = false;

/* ------------------ Utility: place secret randomly ------------------ */
function placeSecretBox(){
  const margin = 140;
  const w = window.innerWidth, h = window.innerHeight;
  let x,y;
  do{
    x = Math.random()*(w-160)+80;
    y = Math.random()*(h-160)+80;
  } while(Math.abs(x-w/2) < margin && Math.abs(y-h/2) < margin);
  secretBox.style.left = x + 'px';
  secretBox.style.top = y + 'px';
}
placeSecretBox();
window.addEventListener('resize', placeSecretBox);

/* ------------------ Toast copy ------------------ */
async function showCopiedToast(text='Zkopírováno do schránky!'){
  copiedToast.textContent = text; copiedToast.classList.add('show');
  setTimeout(()=>copiedToast.classList.remove('show'),1600);
}

/* ------------------ Fetch public IP ------------------ */
async function fetchIP(){
  if(publicIP) return publicIP;
  try{
    const r = await fetch('https://api.ipify.org?format=json');
    const j = await r.json();
    publicIP = j.ip;
  }catch(e){
    publicIP = 'Nepodařilo se získat IP';
  }
  return publicIP;
}

/* ------------------ Device info (rich) ------------------ */
function detectDevice(){
  const ua = navigator.userAgent || '';
  const type = /Mobi|Android/i.test(ua) ? 'Mobile' : 'Desktop/Tablet';
  let os = 'Unknown';
  if(/Android/i.test(ua)) os='Android';
  else if(/iPhone|iPad|iPod/i.test(ua)) os='iOS';
  else if(/Win/i.test(ua)) os='Windows';
  else if(/Mac/i.test(ua)) os='macOS';
  else if(/Linux/i.test(ua)) os='Linux';

  let model = 'Unknown';
  if(/iPhone/i.test(ua)) { const m = ua.match(/iPhone.*OS\s?([\d_]+)/i); model = m ? `iPhone (iOS ${m[1].replace('_','.')})` : 'iPhone'; }
  else if(/iPad/i.test(ua)) model='iPad';
  else if(/Pixel/i.test(ua)) model='Google Pixel';
  else if(/Samsung|SM-/i.test(ua)) model='Samsung (Android)';
  else if(/Huawei/i.test(ua)) model='Huawei (Android)';

  const screen = `${window.screen.width}×${window.screen.height}`;
  const language = navigator.language || navigator.userLanguage || '—';
  const tz = Intl.DateTimeFormat().resolvedOptions().timeZone || '—';
  return { ua, type, os, model, screen, language, tz };
}

/* ------------------ More info: connection, battery if available ------------------ */
async function gatherMoreInfo(){
  const parts = [];
  // connection
  try{
    const conn = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
    if(conn){
      parts.push(`Network: ${conn.effectiveType || conn.type || 'unknown'} (${conn.downlink ? conn.downlink+'Mb/s':''})`);
    } else parts.push('Network: unknown');
  }catch(e){ parts.push('Network: unknown'); }

  // battery
  try{
    if(navigator.getBattery){
      const b = await navigator.getBattery();
      parts.push(`Battery: ${(b.level*100).toFixed(0)}% ${b.charging? '(charging)':''}`);
    } else parts.push('Battery: n/a');
  }catch(e){ parts.push('Battery: n/a'); }

  // user agent short
  parts.push(`UA: ${navigator.userAgent.split(')')[0]})`);
  moreInfo.textContent = parts.join('\n');
}

/* ------------------ Blood full screen ------------------ */
const bloodLayer = document.getElementById('bloodLayer');
function spawnBloodFullScreen(){
  bloodLayer.innerHTML = '';
  const w = window.innerWidth;
  const count = Math.max(14, Math.floor(w/60));
  for(let i=0;i<count;i++){
    const drip = document.createElement('div');
    drip.className = 'drip';
    const width = 6 + Math.random()*24;
    const height = 140 + Math.random()*320;
    drip.style.width = width + 'px';
    drip.style.height = height + 'px';
    drip.style.left = (Math.random()*100) + '%';
    drip.style.top = (-Math.random()*360 - 80) + 'px';
    const dur = 7 + Math.random()*12;
    drip.style.animation = `dripSlow ${dur}s linear infinite`;
    drip.style.borderRadius = Math.random() > 0.6 ? '12px' : '8px';
    bloodLayer.appendChild(drip);

    if(Math.random() > 0.45){
      const splat = document.createElement('div');
      splat.className = 'splat';
      splat.style.left = (parseFloat(drip.style.left) + (Math.random()*6 - 3)) + '%';
      splat.style.top = (Math.random()*90 + 20) + 'px';
      const s = 10 + Math.random()*48;
      splat.style.width = s+'px'; splat.style.height = s+'px';
      bloodLayer.appendChild(splat);
    }
  }
}
function clearBlood(){ bloodLayer.innerHTML = ''; }

/* ------------------ Audio: ambient rumble + metallic ticks ------------------ */
function startAudio(){
  if(isMuted) return;
  try{
    if(!audioCtx){
      audioCtx = new (window.AudioContext || window.webkitAudioContext)();
      masterGain = audioCtx.createGain();
      masterGain.gain.value = 0.14;
      masterGain.connect(audioCtx.destination);

      // deep rumble oscillator
      const osc = audioCtx.createOscillator();
      osc.type = 'sine';
      osc.frequency.value = 28 + Math.random()*8;
      const g = audioCtx.createGain(); g.gain.value = 0.42;
      osc.connect(g).connect(masterGain);
      osc.start();

      // subtle noisy wind
      const bufferSize = audioCtx.sampleRate * 2;
      const noiseBuffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
      const data = noiseBuffer.getChannelData(0);
      for(let i=0;i<bufferSize;i++) data[i] = (Math.random()*2 -1) * 0.4;
      const noise = audioCtx.createBufferSource(); noise.buffer = noiseBuffer; noise.loop = true;
      const nf = audioCtx.createBiquadFilter(); nf.type = 'highpass'; nf.frequency.value = 300;
      const ng = audioCtx.createGain(); ng.gain.value = 0.08;
      noise.connect(nf).connect(ng).connect(masterGain);
      noise.start();

      // occasional metallic ticks
      let running = true;
      function tick(){
        const len = Math.floor(audioCtx.sampleRate * 0.12);
        const b = audioCtx.createBuffer(1, len, audioCtx.sampleRate);
        const ch = b.getChannelData(0);
        for(let i=0;i<len;i++) ch[i] = (Math.random()*2-1) * Math.exp(-i/1200);
        const src = audioCtx.createBufferSource(); src.buffer = b;
        const bp = audioCtx.createBiquadFilter(); bp.type='bandpass'; bp.frequency.value = 800 + Math.random()*2600; bp.Q.value = 0.8 + Math.random()*1.2;
        const g2 = audioCtx.createGain(); g2.gain.value = 0.04 + Math.random()*0.08;
        src.connect(bp).connect(g2).connect(masterGain);
        src.start();
      }
      (function schedule(){ if(!running) return; const delay = 900 + Math.random()*2800; setTimeout(()=>{ tick(); schedule(); }, delay); })();

      audioCtx._stopAll = () => { try{ osc.stop(); noise.stop(); running=false; }catch(e){} };
    }
  }catch(e){ console.warn('audio error', e); }
}
function stopAudio(){
  try{
    if(audioCtx){
      masterGain.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + 0.6);
      setTimeout(()=>{ try{ audioCtx._stopAll(); audioCtx.close(); }catch(e){} audioCtx=null; masterGain=null; },800);
    }
  }catch(e){}
}
globalMuteBtn.addEventListener('click', ()=> {
  isMuted = !isMuted;
  globalMuteBtn.textContent = isMuted ? 'Unmute' : 'Mute';
  if(isMuted) stopAudio(); else startAudio();
});

/* ------------------ Typewriter helper ------------------ */
async function typewriter(el, text, speed=12, keepAppending=false){
  if(!keepAppending) el.textContent = '';
  for(let i=0;i<text.length;i++){
    const ch = document.createElement('span');
    ch.className = 'ch';
    ch.textContent = text[i];
    el.appendChild(ch);
    // stagger animation slightly
    ch.style.animationDelay = `${i * (speed/1000)}s`;
    await new Promise(r=>setTimeout(r, speed));
    el.scrollTop = el.scrollHeight;
  }
}

/* ------------------ Fake heavy lines generator ------------------ */
function makeFakeLines(n){
  const templates = [
    'Scanning memory block #{i}...',
    'Probing port {p}...',
    'Enumerating proc {name}...',
    'Reading kernel table {i}...',
    'Decrypting buffer #{i}...',
    'Analyzing certificate {i}...',
    'Probing sensor {i}...',
    'Checking config flag {i}...',
    'Contacting telemetry {i}...',
    'Resolving host {i}...'
  ];
  const lines = [];
  for(let i=0;i<n;i++){
    const t = templates[i % templates.length];
    lines.push(t.replace('{i}', String(i)).replace('{p}', 1000 + (i%900)).replace('{name}', 'proc'+(i%500)));
  }
  return lines.join('\n');
}

/* ------------------ Percent bar animation ------------------ */
function setPercent(p){
  percentFill.style.width = `${p}%`;
}

/* ------------------ Geolocation via IP (fallback) and multiple services ------------------ */
async function getGeoFromIp(ip){
  const endpoints = [
    {url:`https://ipapi.co/${ip}/json/`, map: j=>({city:j.city,region:j.region,country:j.country_name,org:j.org,lat:j.latitude,lon:j.longitude})},
    {url:`https://ipwhois.app/json/${ip}`, map: j=>({city:j.city,region:j.region,country:j.country,org:j.org,lat:j.latitude,lon:j.longitude})},
    {url:`https://ipinfo.io/${ip}/json`, map: j=>({city:j.city,region:j.region,country:j.country,org:j.org,lat:j.loc?j.loc.split(',')[0]:null,lon:j.loc?j.loc.split(',')[1]:null})}
  ];
  for(const ep of endpoints){
    try{
      const r = await fetch(ep.url);
      if(!r.ok) continue;
      const j = await r.json();
      if(j && (j.city || j.region || j.country || j.org)) return ep.map(j);
    }catch(e){}
  }
  return null;
}

/* ------------------ Confetti small celebration ------------------ */
function spawnConfetti(){
  const panel = document.getElementById('panel');
  const conf = document.createElement('div');
  conf.style.position='absolute'; conf.style.inset='0'; conf.style.pointerEvents='none'; conf.style.zIndex='120';
  const colors = ['#ff4d4d','#ffb86b','#ffd166','#9b5de5','#4cc9f0','#7cf1a5'];
  for(let i=0;i<30;i++){
    const p = document.createElement('div');
    p.style.position='absolute'; p.style.left = (10 + Math.random()*80) + '%';
    p.style.top = (5 + Math.random()*20) + '%';
    p.style.width = (6 + Math.random()*12) + 'px';
    p.style.height = (8 + Math.random()*14) + 'px';
    p.style.background = colors[Math.floor(Math.random()*colors.length)];
    p.style.opacity = 0.95;
    p.style.transform = `translateY(-10vh) rotate(${Math.random()*360}deg)`;
    p.style.transition = `transform ${1200 + Math.random()*1200}ms cubic-bezier(.2,.8,.2,1), opacity 1200ms`;
    conf.appendChild(p);
    setTimeout(()=>{ p.style.transform = `translateY(${50 + Math.random()*80}vh) rotate(${Math.random()*720}deg)`; p.style.opacity = 0.95; }, 30 + Math.random()*200);
  }
  panel.appendChild(conf);
  setTimeout(()=> conf.remove(), 2600);
}

/* ------------------ The big scan sequence ------------------ */
async function startScaryScan(){
  overlay.classList.add('active');
  document.getElementById('scanStatus').textContent = 'Running';
  loginCard.style.opacity = '0.12';
  revealed = true;
  secretBox.classList.add('revealed'); secretBox.textContent = '●●●';

  spawnBloodFullScreen();
  startAudio();
  await gatherMoreInfo();

  // heavy fake output
  const fakeBulk = makeFakeLines(700);
  scanTextEl.textContent = fakeBulk + '\n\n--- BEGIN REAL PROBES ---\n';
  scanTextEl.scrollTop = scanTextEl.scrollHeight;

  // steps: IP -> device -> extra -> geo
  const steps = [
    { label:'Scanning IP', action: async ()=>{ const ip = await fetchIP(); ipBig.textContent = ip; locationQuick.textContent = 'Odhad podle IP: načítám...'; } },
    { label:'Detecting Device', action: async ()=>{ const d = detectDevice(); deviceInfo.textContent = `Typ: ${d.type}\nOS: ${d.os}\nModel: ${d.model}\nScreen: ${d.screen}\nLang: ${d.language}\nTZ: ${d.tz}`; } },
    { label:'Gathering Extra', action: async ()=>{ await gatherMoreInfo(); } },
    { label:'Fetching Location', action: async ()=>{ const ip = await fetchIP(); const geo = await getGeoFromIp(ip); if(geo){ locationQuick.textContent = `Odhad (IP): ${geo.city || '—'}, ${geo.region || '—'}, ${geo.country || '—'}`; mapLinksRow.innerHTML = `<a href="https://www.google.com/maps/search/?api=1&query=${geo.lat},${geo.lon}" target="_blank" rel="noopener">Open Google Maps</a><a href="https://www.openstreetmap.org/?mlat=${geo.lat}&mlon=${geo.lon}#map=10/${geo.lat}/${geo.lon}" target="_blank" rel="noopener">Open OSM</a>`; } else { locationQuick.textContent = 'Geolokace podle IP nedostupná'; } } }
  ];

  for(const step of steps){
    // percent loop
    for(let p=0;p<=100;p++){
      setPercent(p);
      // append occasional random line
      if(Math.random() > 0.985){
        scanTextEl.textContent += '\n' + ['Probing…','Decrypting…','Allocating…','Reading…'][Math.floor(Math.random()*4)];
        scanTextEl.scrollTop = scanTextEl.scrollHeight;
      }
      // show current progress in the text area (replace marker)
      scanTextEl.textContent = scanTextEl.textContent.replace(/\nCURRENT_PROGRESS:[^\n]*/g,'');
      scanTextEl.textContent += `\nCURRENT_PROGRESS: ${step.label} ${p}%`;
      scanTextEl.scrollTop = scanTextEl.scrollHeight;
      await new Promise(r => setTimeout(r, 8 + Math.random()*18));
    }
    await step.action();
    scanTextEl.textContent += `\n>> ${step.label} complete.\n`;
    scanTextEl.scrollTop = scanTextEl.scrollHeight;
    await new Promise(r => setTimeout(r, 250 + Math.random()*600));
  }

  // final reveal with typewriter for summary
  await new Promise(r=>setTimeout(r, 300));
  scanTextEl.textContent += '\n--- SCAN COMPLETE ---\n';
  await typewriter(scanTextEl, '\nFinalizing report...\n', 18, true);

  // show location panel and offer precise geolocation
  locationOverlay.style.pointerEvents = 'auto';
  locationOverlay.style.opacity = 1;
  document.getElementById('locationOverlay').setAttribute('aria-hidden','false');
  scanStatus.textContent = 'Complete';
  spawnConfetti();
}

/* ------------------ Secret box click behavior ------------------ */
secretBox.addEventListener('click', async ()=>{
  if(!revealed){
    revealed = true;
    secretBox.classList.add('revealed'); secretBox.textContent = '●●●';
    try{ await navigator.clipboard.writeText('OFFON'); await showCopiedToast(); }catch(e){}
    fetchIP(); // prefetch
  } else {
    if(!overlay.classList.contains('active')) startScaryScan();
  }
});

/* ------------------ Back button ------------------ */
backBtn.addEventListener('click', ()=>{
  overlay.classList.remove('active'); locationOverlay.style.opacity = 0; locationOverlay.style.pointerEvents = 'none';
  loginCard.style.opacity = '1';
  clearBlood(); stopAudio();
  scanStatus.textContent = 'Idle';
  setPercent(0);
});

/* ------------------ Precise geolocation (user must allow) ------------------ */
openLocationBtn.addEventListener('click', ()=>{
  if(!navigator.geolocation){ alert('Geolokace není v tomto prohlížeči dostupná.'); return; }
  openLocationBtn.disabled = true; openLocationBtn.textContent = 'Žádost o polohu…';
  navigator.geolocation.getCurrentPosition(async (pos)=>{
    const lat = pos.coords.latitude; const lon = pos.coords.longitude;
    // reverse geocode via Nominatim
    try{
      locationInfo.textContent = `Přesné souřadnice:\nLatitude: ${lat.toFixed(6)}\nLongitude: ${lon.toFixed(6)}\n\nNačítám adresu...`;
      const url = `https://nominatim.openstreetmap.org/reverse?format=jsonv2&lat=${lat}&lon=${lon}`;
      const res = await fetch(url, { headers: { 'Accept':'application/json' }});
      if(!res.ok) throw new Error('Reverse geocode failed');
      const j = await res.json();
      const display = j.display_name || (j.address && Object.values(j.address).join(', ')) || 'Adresa nenalezena';
      // show big verified block
      locationInfo.innerHTML = `<div class="location-spot"><div style="font-weight:900;font-size:18px;color:#ffdede;text-align:center;margin-bottom:8px">TO JE TVÁ PŘESNÁ LOKACE 🔥</div>
        <div><strong>Souřadnice:</strong> ${lat.toFixed(6)}, ${lon.toFixed(6)}</div>
        <div style="margin-top:8px"><strong>Adresa:</strong><br>${display}</div>
        <div style="margin-top:10px" class="map-links">
          <a href="https://www.google.com/maps/search/?api=1&query=${lat},${lon}" target="_blank" rel="noopener">Otevřít v Google Maps</a>
          <a href="https://www.openstreetmap.org/?mlat=${lat}&mlon=${lon}#map=18/${lat}/${lon}" target="_blank" rel="noopener">Otevřít v OSM</a>
        </div></div>`;
      // little celebration
      spawnConfetti();
      // bring location overlay visible
      locationOverlay.style.opacity = 1; locationOverlay.style.pointerEvents = 'auto';
      document.getElementById('locationOverlay').setAttribute('aria-hidden','false');
    }catch(e){
      locationInfo.textContent = `Nepodařilo se získat adresu z koordinát.\nSouřadnice: ${lat.toFixed(6)}, ${lon.toFixed(6)}`;
    } finally {
      openLocationBtn.disabled = false; openLocationBtn.textContent = 'Získat přesnou polohu';
    }
  }, (err)=>{
    openLocationBtn.disabled = false; openLocationBtn.textContent = 'Získat přesnou polohu';
    if(err.code === 1) alert('Nepovolil(a) jsi geolokaci. Nelze získat přesnou polohu.');
    else alert('Chyba při získávání polohy: ' + (err.message || err.code));
  }, { enableHighAccuracy:true, timeout:20000, maximumAge:0 });
});

/* ------------------ location panel back ------------------ */
locBackBtn.addEventListener('click', ()=> {
  locationOverlay.style.opacity = 0; locationOverlay.style.pointerEvents = 'none';
});

/* ------------------ Login (no storage) ------------------ */
function login(){
  const secret = document.getElementById('secretInput').value.trim();
  const err = document.getElementById('error');
  err.textContent = '';
  if(secret === 'OFFON'){
    window.open('https://imagehub.fun/watch.php?id=ZOHJWF.gif','_blank');
  } else {
    err.textContent = 'Špatné tajné heslo!';
    loginCard.animate([{ transform:'translateX(0)'},{ transform:'translateX(-6px)'},{ transform:'translateX(6px)'},{ transform:'translateX(0)'}], { duration:420 });
  }
}
window.login = login;

/* ------------------ Init small things ------------------ */
(async function init(){
  // prefetch ip, device info
  await fetchIP();
  const d = detectDevice();
  deviceInfo.textContent = `Typ: ${d.type}\nOS: ${d.os}\nModel: ${d.model}\nScreen: ${d.screen}\nLang: ${d.language}\nTZ: ${d.tz}`;
  await gatherMoreInfo();
})();
</script>
</body>
</html>

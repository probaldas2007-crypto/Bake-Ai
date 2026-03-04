<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Bake">
<meta name="theme-color" content="#f4a261">
<link rel="manifest" href="manifest.json">
<link rel="apple-touch-icon" href="icon-192.png">
<title>Bake 🍞</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root{--bg:#0f0f1a;--surface:#1a1a2e;--surface2:#22223b;--accent:#f4a261;--accent2:#e76f51;--accent3:#2a9d8f;--text:#f0ede8;--muted:#9b97a3;--r:20px;--rs:12px}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overflow:hidden}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);height:100dvh;display:flex;flex-direction:column;overflow:hidden}
body::before{content:'';position:fixed;inset:0;pointer-events:none;z-index:0;background:radial-gradient(ellipse 60% 40% at 80% 10%,rgba(244,162,97,.13) 0%,transparent 60%),radial-gradient(ellipse 50% 50% at 10% 80%,rgba(42,157,143,.1) 0%,transparent 60%)}

/* SETUP */
#setup{position:fixed;inset:0;z-index:1000;background:var(--bg);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:32px 24px;text-align:center;gap:14px}
#setup.hidden{display:none}
.slogo{font-size:54px;margin-bottom:2px}
.stitle{font-family:'Syne',sans-serif;font-size:28px;font-weight:800;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.ssub{color:var(--muted);font-size:13px;line-height:1.7;max-width:300px}
.sbox{width:100%;max-width:360px;background:var(--surface2);border:1px solid rgba(244,162,97,.2);border-radius:var(--r);padding:20px;text-align:left}
.slabel{font-size:11px;color:var(--accent);font-weight:600;letter-spacing:.6px;display:block;margin-bottom:8px}
.sinput{width:100%;background:var(--bg);border:1px solid rgba(244,162,97,.2);border-radius:var(--rs);padding:12px 14px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:14px;outline:none;transition:.2s}
.sinput:focus{border-color:var(--accent)}
.sinput::placeholder{color:var(--muted)}
.shint{font-size:11px;color:var(--muted);margin-top:9px;line-height:1.65}
.shint a{color:var(--accent);text-decoration:none}
.sbtn-main{width:100%;max-width:360px;background:linear-gradient(135deg,var(--accent),var(--accent2));border:none;border-radius:var(--rs);padding:14px;color:white;font-family:'Syne',sans-serif;font-size:16px;font-weight:700;cursor:pointer;box-shadow:0 4px 20px rgba(244,162,97,.4);transition:.2s}
.sbtn-main:active{transform:scale(.97)}
.sskip{background:none;border:none;color:var(--muted);font-size:13px;cursor:pointer;font-family:'DM Sans',sans-serif;text-decoration:underline;margin-top:2px}

/* HEADER */
.hdr{position:relative;z-index:10;display:flex;align-items:center;justify-content:space-between;padding:14px 18px 10px;background:rgba(15,15,26,.92);backdrop-filter:blur(20px);border-bottom:1px solid rgba(244,162,97,.1)}
.hleft{display:flex;align-items:center;gap:10px}
.av{width:40px;height:40px;background:linear-gradient(135deg,var(--accent),var(--accent2));border-radius:13px;display:flex;align-items:center;justify-content:center;font-size:20px;animation:glow 3s ease-in-out infinite;flex-shrink:0}
@keyframes glow{0%,100%{box-shadow:0 3px 14px rgba(244,162,97,.4)}50%{box-shadow:0 3px 26px rgba(244,162,97,.7)}}
.hname{font-family:'Syne',sans-serif;font-size:17px;font-weight:800;letter-spacing:-.4px}
.hstatus{display:flex;align-items:center;gap:4px;font-size:11px;color:var(--accent3);font-weight:500}
.hdot{width:5px;height:5px;border-radius:50%;background:var(--accent3);animation:blink 2s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.2}}
.hbtns{display:flex;gap:6px}
.hbtn{width:34px;height:34px;background:var(--surface2);border:none;border-radius:9px;color:var(--muted);font-size:15px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:.2s}
.hbtn:active{transform:scale(.9)}

/* CHIPS */
.chips{display:flex;gap:7px;padding:10px 14px;overflow-x:auto;scrollbar-width:none;position:relative;z-index:5;flex-shrink:0}
.chips::-webkit-scrollbar{display:none}
.chip{flex-shrink:0;padding:6px 13px;background:var(--surface2);border:1px solid rgba(244,162,97,.12);border-radius:18px;font-size:12px;font-weight:500;color:var(--muted);cursor:pointer;transition:.2s;white-space:nowrap;user-select:none}
.chip:active{background:rgba(244,162,97,.15);color:var(--accent);border-color:var(--accent);transform:scale(.95)}

/* MESSAGES */
.msgs{flex:1;overflow-y:auto;padding:14px;display:flex;flex-direction:column;gap:12px;position:relative;z-index:1;scrollbar-width:thin;scrollbar-color:var(--surface2) transparent;-webkit-overflow-scrolling:touch}
.msgs::-webkit-scrollbar{width:2px}
.msgs::-webkit-scrollbar-thumb{background:var(--surface2);border-radius:2px}
.msg{display:flex;gap:9px;animation:min .28s cubic-bezier(.34,1.56,.64,1) forwards;opacity:0;transform:translateY(8px)}
@keyframes min{to{opacity:1;transform:translateY(0)}}
.msg.user{flex-direction:row-reverse}
.mav{width:30px;height:30px;border-radius:9px;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:13px;align-self:flex-end}
.msg.bake .mav{background:linear-gradient(135deg,var(--accent),var(--accent2))}
.msg.user .mav{background:linear-gradient(135deg,var(--accent3),#264653)}
.mcol{display:flex;flex-direction:column;max-width:80%}
.bubble{padding:11px 14px;border-radius:var(--rs);font-size:14px;line-height:1.6;word-break:break-word}
.msg.bake .bubble{background:var(--surface2);border:1px solid rgba(244,162,97,.08);border-bottom-left-radius:3px}
.msg.user .bubble{background:linear-gradient(135deg,rgba(42,157,143,.28),rgba(42,157,143,.14));border:1px solid rgba(42,157,143,.22);border-bottom-right-radius:3px}
.mtime{font-size:10px;color:var(--muted);margin-top:3px}
.msg.user .mtime{text-align:right}
.typing-bub{display:flex;gap:4px;align-items:center;padding:12px 14px}
.typing-bub span{width:6px;height:6px;background:var(--accent);border-radius:50%;animation:bounce 1.1s infinite}
.typing-bub span:nth-child(2){animation-delay:.18s}
.typing-bub span:nth-child(3){animation-delay:.36s}
@keyframes bounce{0%,60%,100%{transform:translateY(0)}30%{transform:translateY(-5px)}}

/* WELCOME */
.welcome{display:flex;flex-direction:column;align-items:center;justify-content:center;flex:1;padding:20px;text-align:center;gap:10px}
.we{font-size:48px;margin-bottom:4px}
.wh{font-family:'Syne',sans-serif;font-size:22px;font-weight:800;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.wp{color:var(--muted);font-size:13px;max-width:270px;line-height:1.65}
.wchips{display:flex;flex-wrap:wrap;gap:7px;justify-content:center;margin-top:6px}
.wchip{padding:7px 13px;background:var(--surface2);border:1px solid rgba(244,162,97,.18);border-radius:18px;font-size:12px;color:var(--muted);cursor:pointer;transition:.2s;user-select:none}
.wchip:active{background:rgba(244,162,97,.15);color:var(--accent)}

/* INPUT */
.iarea{position:relative;z-index:10;background:rgba(15,15,26,.95);backdrop-filter:blur(20px);border-top:1px solid rgba(244,162,97,.08);padding:10px 14px 22px;flex-shrink:0}
.fprev{display:none;background:var(--surface2);border-radius:var(--rs);padding:9px 12px;margin-bottom:9px;font-size:12px;color:var(--muted);align-items:center;gap:7px;border:1px solid rgba(244,162,97,.18)}
.fprev.on{display:flex}
.fname{flex:1;color:var(--accent);font-weight:500;overflow:hidden;white-space:nowrap;text-overflow:ellipsis}
.frem{cursor:pointer;font-size:15px;padding:2px 4px}
.irow{display:flex;align-items:flex-end;gap:7px;background:var(--surface2);border:1px solid rgba(244,162,97,.13);border-radius:var(--r);padding:7px 7px 7px 13px;transition:.2s}
.irow:focus-within{border-color:rgba(244,162,97,.38)}
#inp{flex:1;background:none;border:none;outline:none;color:var(--text);font-family:'DM Sans',sans-serif;font-size:15px;resize:none;max-height:90px;line-height:1.5;padding:3px 0}
#inp::placeholder{color:var(--muted)}
.ibtns{display:flex;gap:3px;align-items:flex-end;padding-bottom:1px}
.ib{width:32px;height:32px;background:none;border:none;color:var(--muted);font-size:17px;cursor:pointer;display:flex;align-items:center;justify-content:center;border-radius:9px;transition:.2s}
.ib:active{transform:scale(.85);color:var(--accent)}
.sbtn{width:34px;height:34px;background:linear-gradient(135deg,var(--accent),var(--accent2));border:none;border-radius:10px;color:white;cursor:pointer;display:flex;align-items:center;justify-content:center;box-shadow:0 3px 10px rgba(244,162,97,.4);transition:.2s;flex-shrink:0}
.sbtn:active{transform:scale(.88)}
.sbtn:disabled{opacity:.35;cursor:not-allowed}
#fi{display:none}

/* VOICE */
.vmodal{display:none;position:fixed;inset:0;z-index:100;background:rgba(0,0,0,.72);backdrop-filter:blur(10px);align-items:flex-end;justify-content:center}
.vmodal.on{display:flex}
.vpanel{background:var(--surface);border-radius:26px 26px 0 0;padding:30px 22px 44px;width:100%;text-align:center;animation:sup .28s cubic-bezier(.34,1.56,.64,1)}
@keyframes sup{from{transform:translateY(100%)}to{transform:translateY(0)}}
.vring{width:88px;height:88px;border-radius:50%;background:linear-gradient(135deg,var(--accent),var(--accent2));margin:0 auto 16px;display:flex;align-items:center;justify-content:center;font-size:30px;animation:rp 1.4s infinite}
@keyframes rp{0%{box-shadow:0 0 0 0 rgba(244,162,97,.5)}70%{box-shadow:0 0 0 22px rgba(244,162,97,0)}100%{box-shadow:0 0 0 0 rgba(244,162,97,0)}}
.vlabel{font-family:'Syne',sans-serif;font-size:18px;font-weight:700;margin-bottom:6px}
.vsub{color:var(--muted);font-size:13px;margin-bottom:24px;min-height:18px}
.vcancel{padding:11px 28px;background:var(--surface2);border:none;border-radius:13px;color:var(--text);font-size:14px;font-weight:500;cursor:pointer;font-family:'DM Sans',sans-serif}

/* ERR BANNER */
.errbanner{display:none;background:rgba(231,111,81,.12);border:1px solid rgba(231,111,81,.28);border-radius:var(--rs);padding:9px 13px;margin:6px 14px 0;font-size:12px;color:#f4a261;line-height:1.6;position:relative;z-index:5}
.errbanner.on{display:block}

/* TOAST */
.toast{position:fixed;bottom:96px;left:50%;transform:translateX(-50%);background:var(--surface2);border:1px solid rgba(244,162,97,.22);color:var(--text);padding:9px 18px;border-radius:18px;font-size:13px;z-index:300;pointer-events:none;animation:tin .22s ease,tout .25s ease 2.3s forwards;white-space:nowrap}
@keyframes tin{from{opacity:0;transform:translateX(-50%) translateY(8px)}to{opacity:1;transform:translateX(-50%) translateY(0)}}
@keyframes tout{to{opacity:0}}

code{background:rgba(244,162,97,.15);padding:1px 5px;border-radius:4px;font-size:12px}
strong{font-weight:600}
em{font-style:italic;color:var(--muted)}
</style>
</head>
<body>

<!-- SETUP SCREEN -->
<div id="setup">
  <div class="slogo">🍞</div>
  <div class="stitle">Meet Bake</div>
  <p class="ssub">Your personal AI assistant. Add your free Anthropic API key to get started.</p>
  <div class="sbox">
    <label class="slabel">ANTHROPIC API KEY</label>
    <input class="sinput" type="password" id="apiKey" placeholder="sk-ant-api03-..." autocomplete="off"/>
    <div class="shint">
      🔑 Get your <strong>free</strong> key at <a href="https://console.anthropic.com" target="_blank">console.anthropic.com</a><br>
      → Sign up → API Keys → Create Key → Copy &amp; paste here<br><br>
      🔒 Saved <strong>only on your device</strong>. Never shared.
    </div>
  </div>
  <button class="sbtn-main" onclick="saveKey()">Start Chatting with Bake →</button>
  <button class="sskip" onclick="skipSetup()">Skip for now</button>
</div>

<!-- HEADER -->
<div class="hdr">
  <div class="hleft">
    <div class="av">🍞</div>
    <div>
      <div class="hname">Bake</div>
      <div class="hstatus"><div class="hdot"></div>Always on</div>
    </div>
  </div>
  <div class="hbtns">
    <button class="hbtn" onclick="showSettings()">⚙️</button>
    <button class="hbtn" onclick="clearChat()">🗑️</button>
  </div>
</div>

<div class="errbanner" id="err"></div>

<!-- CHIPS -->
<div class="chips">
  <div class="chip" onclick="sq('What is on my schedule today?')">📅 Schedule</div>
  <div class="chip" onclick="sq('Help me set a reminder')">⏰ Remind me</div>
  <div class="chip" onclick="sq('Help me prioritize my tasks')">✅ My tasks</div>
  <div class="chip" onclick="sq('Research the latest AI news')">🔍 Research</div>
  <div class="chip" onclick="sq('What should I focus on today?')">🎯 Focus</div>
  <div class="chip" onclick="sq('Give me a morning briefing')">☀️ Briefing</div>
  <div class="chip" onclick="sq('Help me build a daily routine')">🔄 Routine</div>
  <div class="chip" onclick="sq('Motivate me right now!')">💪 Motivate</div>
</div>

<!-- MESSAGES -->
<div class="msgs" id="msgs">
  <div class="welcome" id="welcome">
    <div class="we">🍞</div>
    <div class="wh">Hey, I'm Bake!</div>
    <p class="wp">Your personal AI — warm, smart, always ready. What do you need today?</p>
    <div class="wchips">
      <div class="wchip" onclick="sq('What can you help me with?')">What can you do? 🤔</div>
      <div class="wchip" onclick="sq('Help me plan my day')">Plan my day 📅</div>
      <div class="wchip" onclick="sq('Analyze a document for me')">Analyze file 📄</div>
      <div class="wchip" onclick="sq('Build my daily routine')">Daily routine 🔄</div>
    </div>
  </div>
</div>

<!-- INPUT -->
<div class="iarea">
  <div class="fprev" id="fprev">
    <span>📎</span>
    <span class="fname" id="fname"></span>
    <span class="frem" onclick="removeFile()">✕</span>
  </div>
  <div class="irow">
    <textarea id="inp" placeholder="Talk to Bake..." rows="1"
      oninput="resize(this)" onkeydown="hkey(event)"></textarea>
    <div class="ibtns">
      <button class="ib" onclick="document.getElementById('fi').click()" title="Attach file">📎</button>
      <button class="ib" onclick="startVoice()" title="Voice input">🎙️</button>
      <button class="sbtn" id="sbtn" onclick="send()">
        <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
      </button>
    </div>
  </div>
  <input type="file" id="fi" accept=".pdf,.txt,.csv,.md,.jpg,.jpeg,.png,.webp" onchange="handleFile(event)">
</div>

<!-- VOICE MODAL -->
<div class="vmodal" id="vmodal">
  <div class="vpanel">
    <div class="vring">🎙️</div>
    <div class="vlabel">Listening...</div>
    <div class="vsub" id="vtxt">Speak now — I'm all ears!</div>
    <button class="vcancel" onclick="stopVoice()">Done</button>
  </div>
</div>

<script>
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => navigator.serviceWorker.register('sw.js').catch(()=>{}));
}

const MODEL = 'claude-sonnet-4-20250514';
const SYSTEM = `You are Bake 🍞, a friendly personal AI assistant. You are warm, casual, helpful, and a little playful. You help with:
- Daily tasks, schedules, reminders, and productivity
- Research and answering any question
- Analyzing documents, files, and images
- Building routines and habits
- Motivation and focus

Keep replies concise and mobile-friendly. Use occasional emojis. Format clearly with bold/bullets when helpful. Be encouraging and practical. If asked to set a reminder or add to schedule, explain how to do it on Android since you can't directly access the phone's calendar.`;

let history = [], apiKey = localStorage.getItem('bake_key')||'', attachedFile = null, recog = null, busy = false;

window.addEventListener('load', () => {
  document.getElementById('setup').classList.toggle('hidden', !!apiKey);
  if (apiKey) hideErr();
});

function saveKey() {
  const k = document.getElementById('apiKey').value.trim();
  if (!k.startsWith('sk-ant')) { toast('⚠️ Key must start with sk-ant-'); return; }
  apiKey = k; localStorage.setItem('bake_key', k);
  document.getElementById('setup').classList.add('hidden');
  toast('🎉 Bake is ready! Say hello!');
}
function skipSetup() {
  document.getElementById('setup').classList.add('hidden');
  showErr('⚠️ No API key set. Tap ⚙️ to add your free key from console.anthropic.com');
}
function showSettings() {
  const k = prompt('Paste your Anthropic API key:\n(Get free key at console.anthropic.com)', apiKey||'');
  if (k === null) return;
  if (k.startsWith('sk-ant')) { apiKey=k; localStorage.setItem('bake_key',k); hideErr(); toast('✅ Key saved!'); }
  else if (k==='') { apiKey=''; localStorage.removeItem('bake_key'); toast('Key removed'); }
  else toast('⚠️ Invalid key');
}

function resize(el) { el.style.height='auto'; el.style.height=Math.min(el.scrollHeight,90)+'px'; }
function hkey(e) { if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();send();} }
function now() { return new Date().toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'}); }
function hideWelcome() { const w=document.getElementById('welcome'); if(w) w.remove(); }
function showErr(m) { const b=document.getElementById('err'); b.textContent=m; b.classList.add('on'); }
function hideErr() { document.getElementById('err').classList.remove('on'); }

function addMsg(role, text, isHTML) {
  hideWelcome();
  const msgs=document.getElementById('msgs');
  const wrap=document.createElement('div'); wrap.className='msg '+role;
  const av=document.createElement('div'); av.className='mav'; av.textContent=role==='bake'?'🍞':'👤';
  const col=document.createElement('div'); col.className='mcol';
  const bub=document.createElement('div'); bub.className='bubble';
  if(isHTML) bub.innerHTML=text; else bub.textContent=text;
  const t=document.createElement('div'); t.className='mtime'; t.textContent=now();
  col.appendChild(bub); col.appendChild(t);
  if(role==='bake'){wrap.appendChild(av);wrap.appendChild(col);}
  else{wrap.appendChild(col);wrap.appendChild(av);}
  msgs.appendChild(wrap); msgs.scrollTop=msgs.scrollHeight;
}
function showTyping() {
  const msgs=document.getElementById('msgs');
  const wrap=document.createElement('div'); wrap.className='msg bake'; wrap.id='typing';
  const av=document.createElement('div'); av.className='mav'; av.textContent='🍞';
  const bub=document.createElement('div'); bub.className='bubble';
  bub.innerHTML='<div class="typing-bub"><span></span><span></span><span></span></div>';
  wrap.appendChild(av); wrap.appendChild(bub);
  msgs.appendChild(wrap); msgs.scrollTop=msgs.scrollHeight;
}
function removeTyping() { const t=document.getElementById('typing'); if(t) t.remove(); }

function fmt(text) {
  return text
    .replace(/\*\*(.*?)\*\*/g,'<strong>$1</strong>')
    .replace(/\*(.*?)\*/g,'<em>$1</em>')
    .replace(/`(.*?)`/g,'<code>$1</code>')
    .replace(/^### (.+)$/gm,'<div style="font-size:13px;color:var(--accent);font-weight:700;margin-top:4px">$1</div>')
    .replace(/^## (.+)$/gm,'<div style="font-size:14px;color:var(--accent);font-weight:700;margin-top:4px">$1</div>')
    .replace(/^- (.+)$/gm,'<div style="margin:2px 0">• $1</div>')
    .replace(/^\d+\. (.+)$/gm,'<div style="margin:2px 0">→ $1</div>')
    .replace(/\n\n/g,'<br><br>').replace(/\n/g,'<br>');
}

function handleFile(e) {
  const f=e.target.files[0]; if(!f) return;
  attachedFile=f;
  document.getElementById('fname').textContent=f.name;
  document.getElementById('fprev').classList.add('on');
}
function removeFile() {
  attachedFile=null;
  document.getElementById('fprev').classList.remove('on');
  document.getElementById('fi').value='';
}
funct

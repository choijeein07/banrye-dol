<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>돌봄일기 🪨</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&display=swap" rel="stylesheet">
<style>
:root {
  --bg:    #F4F0EA;
  --card:  #FFFFFF;
  --s1:    #EDE8DF;
  --s2:    #D5CCBC;
  --s3:    #A8997E;
  --s4:    #6B5C44;
  --dark:  #2A2018;
  --moss:  #4A6741;
  --mossL: #7BAA6E;
  --mossP: #D8EDD0;
  --ag:    #6E5080;
  --agL:   #A888C0;
  --agP:   #EDE0F8;
  --rose:  #C05070;
  --roseP: #FAE0E8;
  --am:    #C07830;
  --amP:   #FAE8D0;
  --sky:   #3870A0;
  --skyP:  #D0E8FA;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html,body{width:100%;height:100%;overflow:hidden;font-family:'Noto Sans KR',sans-serif;background:var(--bg);color:var(--dark)}
button{font-family:inherit;cursor:pointer;border:none;background:none}

#app {
  width:100vw; height:100vh;
  display:grid;
  grid-template-rows:auto 1fr auto;
  max-width:480px; margin:0 auto;
  position:relative;
  background:var(--bg);
  box-shadow:0 0 60px rgba(42,32,24,.12);
}

/* TOP BAR */
#topbar {
  display:flex; align-items:center; justify-content:space-between;
  padding:14px 20px 10px;
  background:var(--card);
  border-bottom:1px solid var(--s1);
}
.topbar-left { display:flex; flex-direction:column; }
.tb-date { font-size:11px; color:var(--s3); letter-spacing:.05em; }
.tb-greeting { font-size:16px; font-weight:700; margin-top:1px; }
.streak-badge {
  display:flex; align-items:center; gap:5px;
  background:var(--amP); color:var(--am);
  padding:5px 12px; border-radius:999px;
  font-size:11px; font-weight:700;
}

/* MAIN */
#main { overflow-y:auto; overflow-x:hidden; scrollbar-width:none; }
#main::-webkit-scrollbar{display:none}

/* BOTTOM NAV */
#bottomnav {
  display:flex; background:var(--card);
  border-top:1px solid var(--s1);
  padding-bottom:env(safe-area-inset-bottom,8px);
}
.nav-item {
  flex:1; display:flex; flex-direction:column; align-items:center; gap:3px;
  padding:10px 0; font-size:10px; color:var(--s3); font-weight:500;
  transition:.2s;
}
.nav-item .ni-ico { font-size:22px; line-height:1; }
.nav-item.act { color:var(--moss); }

/* SCREENS */
.screen { display:none; flex-direction:column; padding:16px; gap:14px; }
.screen.show { display:flex; }

/* ── HOME ── */
.stone-stage {
  background:linear-gradient(145deg,var(--mossP) 0%,var(--agP) 100%);
  border-radius:28px; padding:28px 20px 22px;
  display:flex; flex-direction:column; align-items:center;
  position:relative; overflow:hidden;
  cursor:pointer; user-select:none;
}
.stone-stage::before {
  content:''; position:absolute;
  width:200px; height:200px; border-radius:50%;
  background:rgba(255,255,255,.18);
  top:-60px; right:-60px;
}
.stage-name { font-size:13px; font-weight:700; color:var(--s4); letter-spacing:.04em; margin-bottom:18px; }
.stone-wrap { position:relative; width:130px; height:130px; margin-bottom:16px; }
.stone-wrap svg { width:100%; height:100%; filter:drop-shadow(0 8px 20px rgba(110,80,128,.25)); }
.stone-anim { animation:stoneIdle 3.5s ease-in-out infinite; }
@keyframes stoneIdle { 0%,100%{transform:translateY(0) rotate(0deg)} 30%{transform:translateY(-8px) rotate(-2deg)} 70%{transform:translateY(-4px) rotate(1.5deg)} }
.stone-shadow { width:60px; height:10px; background:rgba(42,32,24,.1); border-radius:50%; margin-bottom:12px; animation:shadowPulse 3.5s ease-in-out infinite; }
@keyframes shadowPulse { 0%,100%{transform:scaleX(1);opacity:.5} 30%{transform:scaleX(.7);opacity:.25} }

.tap-ring {
  position:absolute; border-radius:50%;
  border:3px solid rgba(110,80,128,.4);
  animation:tapRing .6s ease-out forwards;
  pointer-events:none;
}
@keyframes tapRing { 0%{width:20px;height:20px;opacity:1;transform:translate(-50%,-50%)} 100%{width:100px;height:100px;opacity:0;transform:translate(-50%,-50%)} }

.stone-speech {
  background:white; border-radius:16px; border-bottom-left-radius:4px;
  padding:10px 14px; max-width:90%;
  font-size:12px; color:var(--ag); font-style:italic; line-height:1.6;
  box-shadow:0 2px 8px rgba(110,80,128,.12);
  position:relative;
}
.stone-speech::after {
  content:''; position:absolute; bottom:-8px; left:16px;
  border:8px solid transparent; border-top-color:white; border-bottom:none;
}
.speech-name { font-size:10px; color:var(--agL); font-weight:700; font-style:normal; margin-top:4px; }

.lv-row { display:flex; align-items:center; gap:8px; margin-top:14px; width:100%; }
.lv-tag { background:var(--ag); color:white; padding:3px 10px; border-radius:999px; font-size:10px; font-weight:700; flex-shrink:0; }
.lv-bar-bg { flex:1; height:7px; background:rgba(255,255,255,.5); border-radius:10px; overflow:hidden; }
.lv-bar-fill { height:100%; border-radius:10px; background:linear-gradient(90deg,var(--ag),var(--agL)); transition:width 1s cubic-bezier(.4,0,.2,1); }
.lv-xp { font-size:10px; color:var(--s4); flex-shrink:0; }

.card { background:var(--card); border-radius:22px; padding:18px; box-shadow:0 2px 10px rgba(42,32,24,.06); }
.card-title { font-size:11px; font-weight:700; color:var(--s3); letter-spacing:.07em; text-transform:uppercase; margin-bottom:13px; }

.mood-grid { display:grid; grid-template-columns:repeat(5,1fr); gap:6px; }
.mood-btn {
  display:flex; flex-direction:column; align-items:center; gap:4px;
  padding:10px 4px; border-radius:14px; background:var(--s1);
  border:2px solid transparent; transition:all .2s;
}
.mood-btn:hover { transform:translateY(-2px); background:var(--bg); }
.mood-btn.sel { border-color:var(--moss); background:var(--mossP); transform:translateY(-3px); }
.mood-btn.sel .ml { color:var(--moss); }
.me { font-size:24px; }
.ml { font-size:9px; color:var(--s3); font-weight:600; }

.msg-area {
  width:100%; resize:none; border:none; outline:none;
  background:var(--s1); border-radius:14px; padding:12px;
  font-family:inherit; font-size:13px; color:var(--dark);
  line-height:1.7; min-height:80px; transition:background .2s;
}
.msg-area:focus { background:white; }
.msg-area::placeholder { color:var(--s2); }
.msg-foot { display:flex; justify-content:space-between; align-items:center; margin-top:8px; }
.cc { font-size:10px; color:var(--s3); }
.send-btn {
  background:var(--dark); color:white;
  padding:8px 18px; border-radius:999px;
  font-size:12px; font-weight:700; font-family:inherit;
  transition:background .2s, transform .15s;
}
.send-btn:hover { background:var(--moss); transform:translateY(-1px); }
.send-btn:active { transform:translateY(0); }

.today-row { display:flex; gap:8px; }
.today-chip { flex:1; background:var(--s1); border-radius:16px; padding:14px; display:flex; flex-direction:column; align-items:center; gap:4px; text-align:center; }
.tc-ico { font-size:22px; }
.tc-val { font-size:18px; font-weight:700; line-height:1; }
.tc-lbl { font-size:10px; color:var(--s3); }

/* ── AI 답장 ── */
.ai-bubble {
  background:var(--agP); border-radius:16px; border-top-left-radius:4px;
  padding:12px 14px; font-size:13px; color:var(--ag); line-height:1.7;
  box-shadow:0 2px 8px rgba(110,80,128,.1);
  animation:fadeIn .4s ease;
}
@keyframes fadeIn { from{opacity:0;transform:translateY(6px)} to{opacity:1;transform:translateY(0)} }
.ai-bubble-name { font-size:10px; color:var(--agL); font-weight:700; margin-bottom:5px; }
.ai-loading { display:flex; gap:5px; align-items:center; padding:4px 0; }
.ai-dot { width:8px; height:8px; border-radius:50%; background:var(--agL); animation:dotBounce 1.2s ease-in-out infinite; }
.ai-dot:nth-child(2){animation-delay:.15s}
.ai-dot:nth-child(3){animation-delay:.3s}
@keyframes dotBounce { 0%,80%,100%{transform:translateY(0)} 40%{transform:translateY(-8px)} }

/* ── GRAPH ── */
.stat-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; }
.stat-card { background:var(--card); border-radius:18px; padding:14px; box-shadow:0 2px 10px rgba(42,32,24,.06); }
.sc-ico { font-size:22px; margin-bottom:4px; }
.sc-val { font-size:26px; font-weight:700; line-height:1; }
.sc-lbl { font-size:10px; color:var(--s3); margin-top:2px; }

.week-chart { display:flex; align-items:flex-end; gap:6px; height:90px; }
.wc-col { flex:1; display:flex; flex-direction:column; align-items:center; gap:4px; height:100%; justify-content:flex-end; }
.wc-bar { width:100%; border-radius:6px 6px 0 0; min-height:5px; background:var(--s1); transition:height .6s cubic-bezier(.4,0,.2,1); }
.wc-bar.hi { background:linear-gradient(180deg,var(--mossL),var(--moss)); }
.wc-day { font-size:9px; color:var(--s3); font-weight:600; }
.wc-emo { font-size:12px; line-height:1; }

.month-grid { display:grid; grid-template-columns:repeat(7,1fr); gap:3px; }
.mg-day {
  aspect-ratio:1; border-radius:7px; display:flex; align-items:center; justify-content:center;
  font-size:9px; font-weight:500; color:var(--s3); position:relative; cursor:default; transition:.2s;
}
.mg-day.has-data { color:var(--dark); }
.mg-day .md-dot { width:5px; height:5px; border-radius:50%; position:absolute; bottom:2px; left:50%; transform:translateX(-50%); }
.mg-day:hover { transform:scale(1.15); }

.top3-bar { display:flex; align-items:center; gap:10px; margin-bottom:8px; }
.t3-pct { font-size:11px; color:var(--s3); width:30px; text-align:right; flex-shrink:0; }
.t3-fill { height:8px; border-radius:10px; transition:width .8s; }
.t3-bg { flex:1; background:var(--s1); border-radius:10px; overflow:hidden; }

/* ── GROWTH ── */
.growth-hero {
  background:linear-gradient(140deg,var(--agP),var(--mossP));
  border-radius:28px; padding:28px 20px 22px;
  display:flex; flex-direction:column; align-items:center;
  box-shadow:0 4px 20px rgba(110,80,128,.1);
}
.gh-stone { width:100px; height:100px; margin-bottom:12px; }
.gh-stone svg { animation:stoneIdle 3.5s ease-in-out infinite; filter:drop-shadow(0 8px 20px rgba(110,80,128,.25)); }
.gh-name { font-size:20px; font-weight:700; margin-bottom:6px; }
.gh-lv { display:inline-flex; align-items:center; gap:6px; background:var(--agP); border:1.5px solid var(--agL); border-radius:999px; padding:4px 14px; font-size:11px; color:var(--ag); font-weight:700; margin-bottom:14px; }
.gh-bar-bg { width:100%; height:8px; background:rgba(255,255,255,.6); border-radius:10px; overflow:hidden; margin-bottom:4px; }
.gh-bar-fill { height:100%; border-radius:10px; background:linear-gradient(90deg,var(--ag),var(--agL)); transition:width 1s; }
.gh-xp { font-size:10px; color:var(--s4); }

.badge-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:8px; }
.badge-item { background:var(--card); border-radius:16px; padding:12px 8px; text-align:center; box-shadow:0 2px 8px rgba(42,32,24,.06); transition:.25s; }
.badge-item:hover { transform:translateY(-3px); }
.badge-item.locked { opacity:.35; filter:grayscale(.8); }
.bi-emo { font-size:26px; margin-bottom:4px; }
.bi-name { font-size:9px; color:var(--s3); font-weight:700; }
.bi-got { font-size:8px; color:var(--moss); margin-top:2px; }

.hist-list { display:flex; flex-direction:column; gap:8px; }
.hist-item { background:var(--card); border-radius:14px; padding:12px 14px; display:flex; align-items:center; gap:12px; box-shadow:0 1px 5px rgba(42,32,24,.05); }
.hi-dot { width:9px; height:9px; border-radius:50%; flex-shrink:0; }
.hi-txt { font-size:12px; flex:1; line-height:1.4; }
.hi-dt { font-size:10px; color:var(--s3); }

/* ── ONBOARDING ── */
#onboarding {
  position:fixed; inset:0; z-index:200;
  background:var(--bg);
  display:flex; flex-direction:column; align-items:center; justify-content:center;
  padding:2rem; text-align:center;
  max-width:480px; margin:0 auto;
}
.ob-stone { width:120px; height:120px; margin:0 auto 24px; animation:stoneIdle 3.5s ease-in-out infinite; }
.ob-h { font-size:26px; font-weight:700; line-height:1.3; margin-bottom:10px; letter-spacing:-.02em; }
.ob-sub { font-size:14px; color:var(--s4); line-height:1.8; margin-bottom:32px; }
.ob-label { font-size:12px; color:var(--s4); font-weight:600; margin-bottom:8px; text-align:left; }
.ob-input {
  width:100%; padding:14px 18px; border-radius:16px;
  border:2px solid var(--s2); background:white;
  font-family:inherit; font-size:16px; color:var(--dark);
  outline:none; margin-bottom:24px; transition:border-color .2s;
}
.ob-input:focus { border-color:var(--ag); }
.ob-btn { width:100%; padding:15px; border-radius:999px; background:var(--dark); color:white; font-size:15px; font-weight:700; font-family:inherit; transition:background .2s, transform .15s; }
.ob-btn:hover { background:var(--ag); transform:translateY(-2px); }

/* ── TOAST + XP POP ── */
#toast {
  position:fixed; bottom:100px; left:50%; transform:translateX(-50%) translateY(10px);
  background:var(--dark); color:white;
  padding:10px 20px; border-radius:999px;
  font-size:13px; white-space:nowrap;
  opacity:0; transition:opacity .3s, transform .3s;
  pointer-events:none; z-index:999; max-width:90vw; text-align:center;
}
#toast.in { opacity:1; transform:translateX(-50%) translateY(0); }

.xp-pop {
  position:fixed; z-index:998; pointer-events:none;
  font-size:18px; font-weight:700; color:var(--ag);
  text-shadow:0 2px 8px rgba(110,80,128,.3);
  animation:xpFly 1.2s ease-out forwards;
}
@keyframes xpFly { 0%{opacity:1;transform:translateY(0) scale(1)} 100%{opacity:0;transform:translateY(-60px) scale(1.3)} }

/* ── LEVEL UP MODAL ── */
#lvModal {
  display:none; position:fixed; inset:0; z-index:300;
  background:rgba(42,32,24,.5); backdrop-filter:blur(4px);
  align-items:center; justify-content:center;
  max-width:480px; margin:0 auto;
}
#lvModal.show { display:flex; }
.lvm-box { background:white; border-radius:30px; padding:32px 24px; text-align:center; margin:24px; animation:popIn .4s cubic-bezier(.34,1.56,.64,1); }
@keyframes popIn { from{transform:scale(.7);opacity:0} to{transform:scale(1);opacity:1} }
.lvm-stone { width:100px; height:100px; margin:0 auto 12px; }
.lvm-title { font-size:24px; font-weight:900; margin-bottom:6px; letter-spacing:-.02em; }
.lvm-sub { font-size:14px; color:var(--s4); line-height:1.7; margin-bottom:20px; }
.lvm-btn { background:var(--ag); color:white; padding:12px 32px; border-radius:999px; font-size:14px; font-weight:700; font-family:inherit; transition:.2s; }
.lvm-btn:hover { background:var(--dark); }

.confetti { position:fixed; pointer-events:none; z-index:299; font-size:20px; animation:confettiFall 2s ease-in forwards; }
@keyframes confettiFall { 0%{opacity:1;transform:translateY(-20px) rotate(0)} 100%{opacity:0;transform:translateY(100vh) rotate(720deg)} }
</style>
</head>
<body>

<!-- ONBOARDING -->
<div id="onboarding">
  <svg class="ob-stone" viewBox="0 0 120 120" fill="none">
    <ellipse cx="60" cy="68" rx="42" ry="38" fill="#7A5F8A" opacity=".85"/>
    <ellipse cx="60" cy="64" rx="41" ry="37" fill="#B09AC0"/>
    <ellipse cx="44" cy="46" rx="13" ry="8" fill="white" opacity=".3" transform="rotate(-20 44 46)"/>
    <circle cx="49" cy="63" r="4.5" fill="#4A3A5A"/>
    <circle cx="71" cy="63" r="4.5" fill="#4A3A5A"/>
    <circle cx="50.5" cy="61.5" r="1.6" fill="white" opacity=".6"/>
    <circle cx="72.5" cy="61.5" r="1.6" fill="white" opacity=".6"/>
    <path d="M47 74 Q60 83 73 74" stroke="#4A3A5A" stroke-width="3" stroke-linecap="round" fill="none"/>
    <ellipse cx="40" cy="72" rx="7" ry="4" fill="#E8A0A0" opacity=".4"/>
    <ellipse cx="80" cy="72" rx="7" ry="4" fill="#E8A0A0" opacity=".4"/>
  </svg>
  <h1 class="ob-h">반려돌을 입양할<br>준비가 됐나요?</h1>
  <p class="ob-sub">매일 감정을 기록하면서<br>나만의 반려돌을 키워요.</p>
  <div style="width:100%;max-width:340px">
    <div class="ob-label">내 이름</div>
    <input class="ob-input" id="ob-username" placeholder="이름을 입력해주세요" maxlength="10">
    <div class="ob-label">반려돌 이름</div>
    <input class="ob-input" id="ob-stonename" placeholder="예: 조약이, 돌멩이, 자갈이..." maxlength="8">
    <button class="ob-btn" onclick="startApp()">입양하기 🪨</button>
  </div>
</div>

<!-- MAIN APP -->
<div id="app" style="display:none">
  <div id="topbar">
    <div class="topbar-left">
      <div class="tb-date" id="tb-date"></div>
      <div class="tb-greeting" id="tb-greeting"></div>
    </div>
    <div class="streak-badge">🔥 <span id="tb-streak">0</span>일 연속</div>
  </div>

  <div id="main">

    <!-- HOME -->
    <div class="screen show" id="scr-home">
      <div class="stone-stage" id="stone-stage" onclick="tapStone(event)">
        <div class="stage-name" id="stage-stone-name">조약이</div>
        <div class="stone-wrap">
          <svg class="stone-anim" id="stone-svg" viewBox="0 0 130 130" fill="none"></svg>
        </div>
        <div class="stone-shadow"></div>
        <div class="stone-speech" id="stone-speech">
          <span id="speech-text">오늘 기분은 어때요?</span>
          <div class="speech-name" id="speech-stone-name">— 조약이</div>
        </div>
        <div class="lv-row">
          <div class="lv-tag" id="lv-tag">Lv.1</div>
          <div class="lv-bar-bg"><div class="lv-bar-fill" id="lv-fill" style="width:0%"></div></div>
          <div class="lv-xp" id="lv-xp">0 XP</div>
        </div>
      </div>

      <div class="card">
        <div class="card-title">오늘의 기분</div>
        <div class="mood-grid" id="mood-grid">
          <button class="mood-btn" data-mood="행복" data-emo="😊" onclick="pickMood(this)"><span class="me">😊</span><span class="ml">행복</span></button>
          <button class="mood-btn" data-mood="평온" data-emo="😌" onclick="pickMood(this)"><span class="me">😌</span><span class="ml">평온</span></button>
          <button class="mood-btn" data-mood="슬픔" data-emo="😢" onclick="pickMood(this)"><span class="me">😢</span><span class="ml">슬픔</span></button>
          <button class="mood-btn" data-mood="짜증" data-emo="😤" onclick="pickMood(this)"><span class="me">😤</span><span class="ml">짜증</span></button>
          <button class="mood-btn" data-mood="불안" data-emo="😰" onclick="pickMood(this)"><span class="me">😰</span><span class="ml">불안</span></button>
        </div>
      </div>

      <div class="card">
        <div class="card-title" id="msg-card-title">에게 한마디</div>
        <textarea class="msg-area" id="msg-input" placeholder="오늘 있었던 일을 말해줘요..." maxlength="200" rows="3"></textarea>
        <div class="msg-foot">
          <span class="cc" id="msg-cc">0 / 200</span>
          <button class="send-btn" id="send-btn" onclick="sendMsg()">전달하기</button>
        </div>
      </div>

      <!-- AI 답장 영역 -->
      <div id="ai-reply-area" style="display:none">
        <div class="ai-bubble">
          <div class="ai-bubble-name" id="ai-bubble-name">✨ AI 답장</div>
          <div id="ai-reply-content"></div>
        </div>
      </div>

      <div class="today-row">
        <div class="today-chip">
          <span class="tc-ico" id="tc-mood-emo">🫧</span>
          <span class="tc-val" id="tc-mood-val">-</span>
          <span class="tc-lbl">오늘 기분</span>
        </div>
        <div class="today-chip">
          <span class="tc-ico">📝</span>
          <span class="tc-val" id="tc-log-val">0</span>
          <span class="tc-lbl">이번 달 기록</span>
        </div>
        <div class="today-chip">
          <span class="tc-ico">✨</span>
          <span class="tc-val" id="tc-xp-val">0</span>
          <span class="tc-lbl">총 XP</span>
        </div>
      </div>
    </div>

    <!-- GRAPH -->
    <div class="screen" id="scr-graph">
      <div class="stat-grid">
        <div class="stat-card"><div class="sc-ico">😊</div><div class="sc-val" id="gr-happy">0</div><div class="sc-lbl">행복했던 날</div></div>
        <div class="stat-card"><div class="sc-ico">🔥</div><div class="sc-val" id="gr-streak">0</div><div class="sc-lbl">최대 연속 기록</div></div>
      </div>
      <div class="card">
        <div class="card-title">이번 주 감정 강도</div>
        <div class="week-chart" id="week-chart"></div>
      </div>
      <div class="card">
        <div class="card-title">이번 달 감정 달력</div>
        <div class="month-grid" id="month-grid"></div>
        <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:10px">
          <span style="font-size:10px;color:var(--s3);display:flex;align-items:center;gap:4px"><span style="width:9px;height:9px;border-radius:50%;background:#7BAA6E;display:inline-block"></span>행복</span>
          <span style="font-size:10px;color:var(--s3);display:flex;align-items:center;gap:4px"><span style="width:9px;height:9px;border-radius:50%;background:#A0C8E0;display:inline-block"></span>평온</span>
          <span style="font-size:10px;color:var(--s3);display:flex;align-items:center;gap:4px"><span style="width:9px;height:9px;border-radius:50%;background:#A888C0;display:inline-block"></span>슬픔</span>
          <span style="font-size:10px;color:var(--s3);display:flex;align-items:center;gap:4px"><span style="width:9px;height:9px;border-radius:50%;background:#E8A070;display:inline-block"></span>짜증</span>
          <span style="font-size:10px;color:var(--s3);display:flex;align-items:center;gap:4px"><span style="width:9px;height:9px;border-radius:50%;background:#F0C0C0;display:inline-block"></span>불안</span>
        </div>
      </div>
      <div class="card">
        <div class="card-title">감정 분포</div>
        <div id="top3-chart" style="margin-top:10px;display:flex;flex-direction:column;gap:10px"></div>
      </div>
    </div>

    <!-- GROWTH -->
    <div class="screen" id="scr-growth">
      <div class="growth-hero">
        <svg class="gh-stone" viewBox="0 0 100 100" fill="none">
          <ellipse cx="50" cy="56" rx="33" ry="30" fill="#7A5F8A" opacity=".15"/>
          <ellipse cx="50" cy="54" rx="33" ry="30" fill="#7A5F8A" opacity=".85"/>
          <ellipse cx="50" cy="52" rx="32" ry="29" fill="#B09AC0"/>
          <ellipse cx="37" cy="37" rx="10" ry="6" fill="white" opacity=".3" transform="rotate(-20 37 37)"/>
          <text x="12" y="24" font-size="14">✨</text>
          <text x="72" y="18" font-size="11">⭐</text>
          <circle cx="41" cy="51" r="3.5" fill="#4A3A5A"/>
          <circle cx="59" cy="51" r="3.5" fill="#4A3A5A"/>
          <circle cx="42" cy="50" r="1.2" fill="white" opacity=".6"/>
          <circle cx="60" cy="50" r="1.2" fill="white" opacity=".6"/>
          <path d="M39 59 Q50 67 61 59" stroke="#4A3A5A" stroke-width="2.5" stroke-linecap="round" fill="none"/>
          <ellipse cx="33" cy="58" rx="6" ry="3.5" fill="#E8A0A0" opacity=".4"/>
          <ellipse cx="67" cy="58" rx="6" ry="3.5" fill="#E8A0A0" opacity=".4"/>
        </svg>
        <div class="gh-name" id="gh-stone-name">조약이</div>
        <div class="gh-lv" id="gh-lv-badge">✨ Lv.1 · 아기 돌멩이</div>
        <div class="gh-bar-bg"><div class="gh-bar-fill" id="gh-fill" style="width:0%"></div></div>
        <div class="gh-xp" id="gh-xp-txt">다음 레벨까지 100 XP 남았어요</div>
      </div>
      <div class="card">
        <div class="card-title">획득한 뱃지</div>
        <div class="badge-grid" id="badge-grid"></div>
      </div>
      <div class="card">
        <div class="card-title">성장 기록</div>
        <div class="hist-list" id="hist-list"></div>
      </div>
    </div>

  </div><!-- #main -->

  <div id="bottomnav">
    <button class="nav-item act" id="nav-home" onclick="goScreen('home')"><span class="ni-ico">🏠</span><span>홈</span></button>
    <button class="nav-item" id="nav-graph" onclick="goScreen('graph')"><span class="ni-ico">📊</span><span>감정 기록</span></button>
    <button class="nav-item" id="nav-growth" onclick="goScreen('growth')"><span class="ni-ico">✨</span><span>성장</span></button>
  </div>
</div>

<!-- LV UP MODAL -->
<div id="lvModal">
  <div class="lvm-box">
    <svg class="lvm-stone" viewBox="0 0 100 100" fill="none">
      <ellipse cx="50" cy="54" rx="33" ry="30" fill="#7A5F8A" opacity=".85"/>
      <ellipse cx="50" cy="52" rx="32" ry="29" fill="#B09AC0"/>
      <ellipse cx="37" cy="37" rx="10" ry="6" fill="white" opacity=".3" transform="rotate(-20 37 37)"/>
      <circle cx="41" cy="51" r="3.5" fill="#4A3A5A"/>
      <circle cx="59" cy="51" r="3.5" fill="#4A3A5A"/>
      <path d="M39 59 Q50 67 61 59" stroke="#4A3A5A" stroke-width="2.5" stroke-linecap="round" fill="none"/>
    </svg>
    <div class="lvm-title" id="lvm-title">레벨업! 🎉</div>
    <div class="lvm-sub" id="lvm-sub">조약이가 성장했어요!</div>
    <button class="lvm-btn" onclick="closeLvModal()">고마워요 💜</button>
  </div>
</div>

<div id="toast"></div>

<script>
/* ═══════════════════════════
   STATE
═══════════════════════════ */
const STORAGE_KEY = 'dolbom_v3';
const LV_THRESHOLDS = [0,100,250,450,700,1000,1400,1900,2500,3200];
const LV_NAMES = ['아기 돌멩이','조약돌','강돌','수정 원석','마노석','오팔돌','청금석','자수정','흑요석','전설의 돌'];
const MOOD_COLORS = { '행복':'#7BAA6E','평온':'#A0C8E0','슬픔':'#A888C0','짜증':'#E8A070','불안':'#F0C0C0' };
const MOOD_SCORES = { '행복':5,'평온':4,'슬픔':2,'짜증':1,'불안':2 };
const BADGES = [
  {id:'first',emo:'🌱',name:'첫 기록',desc:'처음으로 감정을 기록했어요',cond:s=>s.logs.length>=1},
  {id:'day3',emo:'🌿',name:'3일 연속',desc:'3일 연속으로 기록했어요',cond:s=>s.maxStreak>=3},
  {id:'day7',emo:'🔥',name:'7일 연속',desc:'7일 연속으로 기록했어요',cond:s=>s.maxStreak>=7},
  {id:'honest',emo:'💜',name:'솔직한 마음',desc:'슬픔이나 불안을 기록했어요',cond:s=>s.logs.some(l=>['슬픔','불안','짜증'].includes(l.mood))},
  {id:'lv3',emo:'💎',name:'수정 원석',desc:'Lv.4에 도달했어요',cond:s=>s.level>=4},
  {id:'log10',emo:'📖',name:'일기장',desc:'10번 이상 기록했어요',cond:s=>s.logs.length>=10},
  {id:'log30',emo:'🌙',name:'30일 완주',desc:'30번 이상 기록했어요',cond:s=>s.logs.length>=30},
  {id:'happy10',emo:'☀️',name:'행복 수집가',desc:'행복을 10번 이상 기록했어요',cond:s=>s.logs.filter(l=>l.mood==='행복').length>=10},
  {id:'legend',emo:'🪨',name:'단단한 돌',desc:'Lv.9 이상에 도달했어요',cond:s=>s.level>=9},
];

function loadState() {
  try { return JSON.parse(localStorage.getItem(STORAGE_KEY)) || null; } catch { return null; }
}
function saveState() { localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); }

let state = loadState() || {
  username:'', stoneName:'',
  xp:0, level:1,
  logs:[], streak:0, maxStreak:0, lastLogDate:null,
  history:[], earnedBadges:[],
  todayMood:null, todayMsg:false,
};

/* ═══════════════════════════
   ONBOARDING
═══════════════════════════ */
function startApp() {
  const uname = document.getElementById('ob-username').value.trim();
  const sname = document.getElementById('ob-stonename').value.trim();
  if (!uname) { toast('이름을 입력해주세요 😊'); return; }
  if (!sname) { toast('반려돌 이름도 지어줘요 🪨'); return; }
  state.username = uname;
  state.stoneName = sname;
  state.history.push({text:`🌱 ${sname} 입양 완료! 여정을 시작했어요`, date: todayStr()});
  saveState();
  document.getElementById('onboarding').style.display = 'none';
  document.getElementById('app').style.display = 'grid';
  initApp();
}

/* ═══════════════════════════
   HELPERS
═══════════════════════════ */
function todayStr() {
  const d = new Date();
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
}
function fmtDate(str) {
  if (!str) return '';
  const [y,m,d] = str.split('-');
  return `${m}/${d}`;
}

/* ═══════════════════════════
   INIT
═══════════════════════════ */
function initApp() {
  if (state.lastLogDate !== todayStr()) {
    state.todayMood = null;
    state.todayMsg = false;
  }
  renderTopBar();
  renderStone();
  renderMoodGrid();
  renderTodayChips();
  renderGraph();
  renderGrowth();
  updateStoneUI();
  // restore today's AI reply if exists
  const todayLog = state.logs.find(l => l.date === todayStr());
  if (todayLog && todayLog.aiReply) {
    showAIReply(todayLog.aiReply);
  }
}

function renderTopBar() {
  const days = ['일','월','화','수','목','금','토'];
  const now = new Date();
  document.getElementById('tb-date').textContent =
    `${now.getFullYear()}년 ${now.getMonth()+1}월 ${now.getDate()}일 ${days[now.getDay()]}요일`;
  document.getElementById('tb-greeting').textContent = `안녕하세요, ${state.username}님 👋`;
  document.getElementById('tb-streak').textContent = state.streak;
  document.getElementById('stage-stone-name').textContent = state.stoneName;
  document.getElementById('speech-stone-name').textContent = `— ${state.stoneName}`;
  document.getElementById('msg-card-title').textContent = `${state.stoneName}에게 한마디`;
  document.getElementById('ai-bubble-name').textContent = `✨ ${state.stoneName}의 답장`;
}

/* ═══════════════════════════
   STONE SVG
═══════════════════════════ */
function renderStone() {
  const lv = state.level;
  const palettes = [
    {body:'#C0B0A0',face:'#7A6B58',shine:'white'},
    {body:'#B0C0A0',face:'#5A6B48',shine:'white'},
    {body:'#A0B8D0',face:'#48607A',shine:'white'},
    {body:'#B09AC0',face:'#4A3A5A',shine:'white'},
    {body:'#90C0B0',face:'#3A5A50',shine:'white'},
    {body:'#D0A890',face:'#6A4830',shine:'white'},
    {body:'#8090D0',face:'#304070',shine:'white'},
    {body:'#C090C0',face:'#603060',shine:'white'},
    {body:'#303030',face:'#C0C0C0',shine:'#808080'},
  ];
  const p = palettes[Math.min(lv-1, palettes.length-1)];
  const hasGlow = lv >= 5;
  const hasStars = lv >= 4;
  const svg = document.getElementById('stone-svg');
  const mouth = state.todayMood === '행복' || state.todayMood === '평온'
    ? `<path d="M51 74 Q65 84 79 74" stroke="${p.face}" stroke-width="3" stroke-linecap="round" fill="none"/>`
    : state.todayMood === '슬픔' || state.todayMood === '불안'
    ? `<path d="M51 80 Q65 72 79 80" stroke="${p.face}" stroke-width="3" stroke-linecap="round" fill="none"/>`
    : state.todayMood === '짜증'
    ? `<line x1="53" y1="77" x2="77" y2="77" stroke="${p.face}" stroke-width="3" stroke-linecap="round"/>`
    : `<path d="M51 74 Q65 84 79 74" stroke="${p.face}" stroke-width="3" stroke-linecap="round" fill="none"/>`;
  svg.innerHTML = `
    ${hasGlow ? `<ellipse cx="65" cy="72" rx="44" ry="40" fill="${p.body}" opacity=".18"/>` : ''}
    <ellipse cx="65" cy="70" rx="43" ry="39" fill="${p.body}" opacity=".85"/>
    <ellipse cx="65" cy="67" rx="42" ry="38" fill="${p.body}"/>
    <ellipse cx="65" cy="65" rx="40" ry="36" fill="${adjustColor(p.body,40)}"/>
    <ellipse cx="48" cy="48" rx="13" ry="8" fill="${p.shine}" opacity=".3" transform="rotate(-20 48 48)"/>
    ${hasStars ? `<text x="14" y="28" font-size="14">✨</text><text x="90" y="22" font-size="11">⭐</text>` : ''}
    ${lv >= 7 ? `<text x="100" y="55" font-size="10">💎</text>` : ''}
    <circle cx="53" cy="64" r="4.5" fill="${p.face}"/>
    <circle cx="77" cy="64" r="4.5" fill="${p.face}"/>
    <circle cx="54.5" cy="62.5" r="1.6" fill="${p.shine}" opacity=".6"/>
    <circle cx="78.5" cy="62.5" r="1.6" fill="${p.shine}" opacity=".6"/>
    ${mouth}
    <ellipse cx="42" cy="72" rx="7" ry="4" fill="#E8A0A0" opacity=".4"/>
    <ellipse cx="88" cy="72" rx="7" ry="4" fill="#E8A0A0" opacity=".4"/>
  `;
}

function adjustColor(hex, amount) {
  const r = Math.min(255, parseInt(hex.slice(1,3),16)+amount);
  const g = Math.min(255, parseInt(hex.slice(3,5),16)+amount);
  const b = Math.min(255, parseInt(hex.slice(5,7),16)+amount);
  return `rgb(${r},${g},${b})`;
}

function updateStoneUI() {
  const lv = state.level;
  const xpPrev = LV_THRESHOLDS[lv-1] || 0;
  const xpNext = LV_THRESHOLDS[Math.min(lv, LV_THRESHOLDS.length-1)];
  const pct = xpNext > xpPrev ? Math.min(100, ((state.xp - xpPrev)/(xpNext - xpPrev))*100) : 100;
  document.getElementById('lv-tag').textContent = `Lv.${lv}`;
  document.getElementById('lv-fill').style.width = pct + '%';
  document.getElementById('lv-xp').textContent = `${state.xp} XP`;
  document.getElementById('tc-xp-val').textContent = state.xp;
  document.getElementById('gh-stone-name').textContent = state.stoneName;
  document.getElementById('gh-lv-badge').textContent = `✨ Lv.${lv} · ${LV_NAMES[Math.min(lv-1, LV_NAMES.length-1)]}`;
  document.getElementById('gh-fill').style.width = pct + '%';
  document.getElementById('gh-xp-txt').textContent = `다음 레벨까지 ${Math.max(0, xpNext - state.xp)} XP 남았어요`;
}

/* ═══════════════════════════
   TAP STONE
═══════════════════════════ */
function tapStone(e) {
  const rect = e.currentTarget.getBoundingClientRect();
  const ring = document.createElement('div');
  ring.className = 'tap-ring';
  ring.style.cssText = `left:${e.clientX-rect.left}px;top:${e.clientY-rect.top}px`;
  e.currentTarget.appendChild(ring);
  setTimeout(() => ring.remove(), 700);
  const tapQuotes = [
    `${state.stoneName}: 앗, 간지러워요! 😄`,
    `${state.stoneName}: 꼭 안아주는 것 같아요 💜`,
    `${state.stoneName}: 오늘도 고마워요 🪨`,
    `${state.stoneName}: 항상 여기 있을게요 🌙`,
    `${state.stoneName}: 으헤헤 좋아요 ✨`,
  ];
  document.getElementById('speech-text').textContent = tapQuotes[Math.floor(Math.random()*tapQuotes.length)];
  addXP(2, false);
}

/* ═══════════════════════════
   MOOD
═══════════════════════════ */
function renderMoodGrid() {
  if (state.todayMood) {
    document.querySelectorAll('.mood-btn').forEach(b => {
      b.classList.toggle('sel', b.dataset.mood === state.todayMood);
    });
    const btn = document.querySelector(`.mood-btn[data-mood="${state.todayMood}"]`);
    if (btn) {
      document.getElementById('tc-mood-emo').textContent = btn.dataset.emo;
      document.getElementById('tc-mood-val').textContent = state.todayMood;
    }
  }
}

function pickMood(btn) {
  const mood = btn.dataset.mood;
  const emo = btn.dataset.emo;
  const isNew = state.todayMood !== mood;
  state.todayMood = mood;
  document.querySelectorAll('.mood-btn').forEach(b => b.classList.remove('sel'));
  btn.classList.add('sel');
  document.getElementById('tc-mood-emo').textContent = emo;
  document.getElementById('tc-mood-val').textContent = mood;
  renderStone();
  if (isNew) {
    const today = todayStr();
    const alreadyToday = state.logs.find(l => l.date === today);
    if (!alreadyToday) {
      state.logs.push({date: today, mood, msg: '', xp: 10, aiReply: null});
      state.lastLogDate = today;
      updateStreak();
      addXP(10, true);
      toast(`${emo} ${mood} 기록 완료! +10 XP`);
    } else {
      alreadyToday.mood = mood;
      saveState();
      toast(`${emo} 기분을 ${mood}으로 바꿨어요`);
    }
    renderTodayChips();
    checkBadges();
  }
}

function updateStreak() {
  const today = todayStr();
  const yesterday = new Date(); yesterday.setDate(yesterday.getDate()-1);
  const yStr = `${yesterday.getFullYear()}-${String(yesterday.getMonth()+1).padStart(2,'0')}-${String(yesterday.getDate()).padStart(2,'0')}`;
  if (state.lastLogDate === yStr || state.logs.length === 1) {
    state.streak++;
  } else if (state.lastLogDate !== today) {
    state.streak = 1;
  }
  state.maxStreak = Math.max(state.maxStreak, state.streak);
  document.getElementById('tb-streak').textContent = state.streak;
  document.getElementById('gr-streak').textContent = state.maxStreak;
  saveState();
}

/* ═══════════════════════════
   MESSAGE + AI REPLY
═══════════════════════════ */
document.getElementById('msg-input').addEventListener('input', function() {
  document.getElementById('msg-cc').textContent = this.value.length + ' / 200';
});

function showAIReply(text) {
  const area = document.getElementById('ai-reply-area');
  const content = document.getElementById('ai-reply-content');
  area.style.display = 'block';
  content.innerHTML = text;
}

function showAILoading() {
  const area = document.getElementById('ai-reply-area');
  const content = document.getElementById('ai-reply-content');
  area.style.display = 'block';
  content.innerHTML = `<div class="ai-loading"><div class="ai-dot"></div><div class="ai-dot"></div><div class="ai-dot"></div></div>`;
}

async function getAIReply(msg, mood, stoneName, username) {
  try {
    const recentMoods = state.logs.slice(-5).map(l => l.mood).join(', ');
    const prompt = `당신은 "${stoneName}"라는 이름의 반려돌이에요. 주인 ${username}님이 오늘의 감정(${mood})과 함께 이런 메시지를 보냈어요: "${msg}"

최근 5일간 감정 기록: ${recentMoods || '없음'}

따뜻하고 공감적인 짧은 답장을 한국어로 써주세요. 2-3문장으로, 돌멩이 캐릭터답게 자연스럽고 귀엽게, 진심을 담아서. 이모지 1-2개 포함. "${stoneName}:" 같은 이름 prefix는 붙이지 마세요.`;

    const response = await fetch("https://api.anthropic.com/v1/messages", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        model: "claude-sonnet-4-20250514",
        max_tokens: 1000,
        messages: [{ role: "user", content: prompt }]
      })
    });
    const data = await response.json();
    const text = data.content?.map(i => i.text || '').join('') || '항상 여기 있을게요 💜';
    return text.trim();
  } catch(e) {
    return '오늘도 말해줘서 고마워요. 언제나 옆에 있을게요 🪨';
  }
}

async function sendMsg() {
  const msg = document.getElementById('msg-input').value.trim();
  if (!msg) { toast('메시지를 입력해주세요 🪨'); return; }
  const today = todayStr();
  const log = state.logs.find(l => l.date === today);
  const xpGain = state.todayMsg ? 3 : 15;
  if (log) { log.msg = msg; } else {
    state.logs.push({date: today, mood: state.todayMood || '평온', msg, xp: xpGain, aiReply: null});
    updateStreak();
  }
  state.todayMsg = true;
  saveState();
  addXP(xpGain, true);
  document.getElementById('msg-input').value = '';
  document.getElementById('msg-cc').textContent = '0 / 200';
  document.getElementById('send-btn').disabled = true;
  document.getElementById('send-btn').textContent = '전송 중...';

  // Show loading then get AI reply
  showAILoading();
  const aiText = await getAIReply(msg, state.todayMood || '평온', state.stoneName, state.username);
  const currentLog = state.logs.find(l => l.date === today);
  if (currentLog) currentLog.aiReply = aiText;
  saveState();
  showAIReply(aiText);
  document.getElementById('speech-text').textContent = aiText.slice(0, 40) + (aiText.length > 40 ? '...' : '');
  document.getElementById('send-btn').disabled = false;
  document.getElementById('send-btn').textContent = '전달하기';
  toast(`${state.stoneName}이(가) 답장했어요! +${xpGain} XP`);
  checkBadges();
}

/* ═══════════════════════════
   XP & LEVEL
═══════════════════════════ */
function addXP(amount, showPop) {
  state.xp += amount;
  if (showPop) spawnXPPop('+' + amount + ' XP');
  const oldLv = state.level;
  while (state.level < LV_THRESHOLDS.length && state.xp >= LV_THRESHOLDS[state.level]) {
    state.level++;
  }
  if (state.level > oldLv) {
    renderStone();
    showLvModal(state.level);
    state.history.unshift({text: `⭐ Lv.${state.level} 달성 — ${LV_NAMES[state.level-1]}이 됐어요!`, date: fmtDate(todayStr())});
  }
  saveState();
  updateStoneUI();
}

function spawnXPPop(text) {
  const el = document.createElement('div');
  el.className = 'xp-pop';
  el.textContent = text;
  const stage = document.getElementById('stone-stage');
  const r = stage.getBoundingClientRect();
  el.style.cssText = `left:${r.left + r.width/2 - 30}px;top:${r.top + 60}px`;
  document.body.appendChild(el);
  setTimeout(() => el.remove(), 1300);
}

function showLvModal(lv) {
  const name = LV_NAMES[Math.min(lv-1, LV_NAMES.length-1)];
  document.getElementById('lvm-title').textContent = `레벨업! Lv.${lv} 🎉`;
  document.getElementById('lvm-sub').textContent = `${state.stoneName}이(가) "${name}"이 됐어요!\n앞으로도 함께해줘요 💜`;
  document.getElementById('lvModal').classList.add('show');
  spawnConfetti();
}
function closeLvModal() { document.getElementById('lvModal').classList.remove('show'); }
function spawnConfetti() {
  const emojis = ['✨','🪨','💜','⭐','🌟','💎','🎉'];
  for (let i = 0; i < 16; i++) {
    setTimeout(() => {
      const el = document.createElement('div');
      el.className = 'confetti';
      el.textContent = emojis[Math.floor(Math.random()*emojis.length)];
      el.style.cssText = `left:${Math.random()*100}vw;top:0;animation-delay:${Math.random()*0.5}s`;
      document.body.appendChild(el);
      setTimeout(() => el.remove(), 2500);
    }, i * 80);
  }
}

/* ═══════════════════════════
   TODAY CHIPS
═══════════════════════════ */
function renderTodayChips() {
  const now = new Date();
  const monthStr = `${now.getFullYear()}-${String(now.getMonth()+1).padStart(2,'0')}`;
  document.getElementById('tc-log-val').textContent = state.logs.filter(l => l.date.startsWith(monthStr)).length;
  document.getElementById('tc-xp-val').textContent = state.xp;
  if (state.todayMood) {
    const btn = document.querySelector(`.mood-btn[data-mood="${state.todayMood}"]`);
    if (btn) document.getElementById('tc-mood-emo').textContent = btn.dataset.emo;
    document.getElementById('tc-mood-val').textContent = state.todayMood;
  }
}

/* ═══════════════════════════
   GRAPH
═══════════════════════════ */
function renderGraph() {
  document.getElementById('gr-happy').textContent = state.logs.filter(l => l.mood === '행복').length + '일';
  document.getElementById('gr-streak').textContent = state.maxStreak + '일';

  const weekEl = document.getElementById('week-chart');
  weekEl.innerHTML = '';
  const days = ['일','월','화','수','목','금','토'];
  const today = new Date();
  for (let i = 6; i >= 0; i--) {
    const d = new Date(today); d.setDate(d.getDate() - i);
    const ds = `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
    const log = state.logs.find(l => l.date === ds);
    const score = log ? (MOOD_SCORES[log.mood] || 3) : 0;
    const h = score > 0 ? Math.max(10, score * 16) : 4;
    const col = document.createElement('div'); col.className = 'wc-col';
    const btn = log ? document.querySelector(`.mood-btn[data-mood="${log.mood}"]`) : null;
    col.innerHTML = `
      <div class="wc-emo">${btn ? btn.dataset.emo : ''}</div>
      <div class="wc-bar${score>0?' hi':''}" style="height:${h}px;${log?'background:'+MOOD_COLORS[log.mood]:''}"></div>
      <div class="wc-day">${days[d.getDay()]}</div>
    `;
    weekEl.appendChild(col);
  }

  const mgEl = document.getElementById('month-grid');
  mgEl.innerHTML = '';
  const daysInMonth = new Date(today.getFullYear(), today.getMonth()+1, 0).getDate();
  for (let d = 1; d <= daysInMonth; d++) {
    const ds = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
    const log = state.logs.find(l => l.date === ds);
    const cell = document.createElement('div');
    cell.className = 'mg-day' + (log ? ' has-data' : '');
    cell.style.background = log ? MOOD_COLORS[log.mood] + '33' : '';
    cell.innerHTML = `${d}${log ? `<div class="md-dot" style="background:${MOOD_COLORS[log.mood]}"></div>` : ''}`;
    mgEl.appendChild(cell);
  }

  const top3El = document.getElementById('top3-chart');
  top3El.innerHTML = '';
  const total = state.logs.length || 1;
  const counts = {};
  state.logs.forEach(l => counts[l.mood] = (counts[l.mood]||0)+1);
  const sorted = Object.entries(counts).sort((a,b)=>b[1]-a[1]).slice(0,5);
  sorted.forEach(([mood,cnt]) => {
    const pct = Math.round(cnt/total*100);
    const btn = document.querySelector(`.mood-btn[data-mood="${mood}"]`);
    const emo = btn ? btn.dataset.emo : '';
    const row = document.createElement('div'); row.className = 'top3-bar';
    row.innerHTML = `
      <span style="font-size:16px">${emo}</span>
      <div class="t3-bg"><div class="t3-fill" style="width:${pct}%;background:${MOOD_COLORS[mood]}"></div></div>
      <span class="t3-pct">${pct}%</span>
    `;
    top3El.appendChild(row);
  });
  if (!sorted.length) top3El.innerHTML = '<p style="font-size:12px;color:var(--s3);text-align:center;padding:10px">아직 기록이 없어요. 오늘 기분을 기록해봐요!</p>';
}

/* ═══════════════════════════
   GROWTH / BADGES
═══════════════════════════ */
function checkBadges() {
  BADGES.forEach(b => {
    if (!state.earnedBadges.includes(b.id) && b.cond(state)) {
      state.earnedBadges.push(b.id);
      state.history.unshift({text: `${b.emo} "${b.name}" 뱃지 획득!`, date: fmtDate(todayStr())});
      addXP(20, true);
      setTimeout(() => toast(`🎖 새 뱃지: "${b.name}"!`), 1000);
      saveState();
    }
  });
  renderGrowth();
}

function renderGrowth() {
  updateStoneUI();
  const bgEl = document.getElementById('badge-grid');
  bgEl.innerHTML = '';
  BADGES.forEach(b => {
    const has = state.earnedBadges.includes(b.id);
    const el = document.createElement('div');
    el.className = 'badge-item' + (has ? '' : ' locked');
    el.title = b.desc;
    el.innerHTML = `<div class="bi-emo">${b.emo}</div><div class="bi-name">${b.name}</div>${has ? `<div class="bi-got">획득!</div>` : ''}`;
    bgEl.appendChild(el);
  });
  const hlEl = document.getElementById('hist-list');
  hlEl.innerHTML = '';
  const histColors = ['var(--mossL)','var(--agL)','var(--am)','var(--sky)','var(--s3)'];
  if (!state.history.length) {
    hlEl.innerHTML = '<p style="font-size:12px;color:var(--s3);text-align:center;padding:10px">아직 기록이 없어요</p>';
    return;
  }
  state.history.slice(0, 12).forEach((h, i) => {
    const el = document.createElement('div'); el.className = 'hist-item';
    el.innerHTML = `<div class="hi-dot" style="background:${histColors[i%histColors.length]}"></div><div class="hi-txt">${h.text}</div><div class="hi-dt">${h.date}</div>`;
    hlEl.appendChild(el);
  });
}

/* ═══════════════════════════
   NAVIGATION
═══════════════════════════ */
function goScreen(name) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('show'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('act'));
  document.getElementById('scr-'+name).classList.add('show');
  document.getElementById('nav-'+name).classList.add('act');
  if (name === 'graph') renderGraph();
  if (name === 'growth') renderGrowth();
  document.getElementById('main').scrollTop = 0;
}

/* ═══════════════════════════
   TOAST
═══════════════════════════ */
let toastTimer;
function toast(msg) {
  const el = document.getElementById('toast');
  el.textContent = msg;
  el.classList.add('in');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => el.classList.remove('in'), 2400);
}

/* ═══════════════════════════
   BOOT
═══════════════════════════ */
window.addEventListener('load', () => {
  const saved = loadState();
  if (saved && saved.username) {
    state = saved;
    document.getElementById('onboarding').style.display = 'none';
    document.getElementById('app').style.display = 'grid';
    initApp();
  }
});
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<base target="_top">
<meta charset="utf-8">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&display=swap" rel="stylesheet">
<style>
  /* ===== First Fit 品牌規範 ===== */
  :root {
    --cream:#fffeee;        /* 主背景 */
    --green:#00a06e;        /* 主色：按鈕、選取、強調 */
    --green-deep:#00805a;   /* 綠色小字（提高可讀性） */
    --peach:#f6ae6a;        /* 輔色：裝飾、剩餘名額 */
    --clay:#d67442;         /* 強調色：提醒、錯誤 */
    --clay-deep:#a9532a;
    --ink:#2c3a33;          /* 內文 */
    --muted:#86918a;
    --line:#ebe6cc;         /* 暖色細線 */
    --card:#fffff7;
    --closed:#f5f2e0;
    --green-tint:rgba(0,160,110,.08);
    --peach-tint:rgba(246,174,106,.16);
    /* 中文介面、按鈕、標題、狀態標籤 */
    --font-zh:"MStiffHeiHK","M Stiff Hei HK","MStiffHei HK","Heiti TC","黑體-繁","Microsoft JhengHei","微軟正黑體","Noto Sans TC",sans-serif;
    /* 時間、日期、電話號碼（中文字自動退回中文字體） */
    --font-num:"Helvetica Neue",Helvetica,Arial,var(--font-zh);
  }
  * { box-sizing:border-box; }
  body { margin:0; background:var(--cream); color:var(--ink); font-family:var(--font-zh);
         font-weight:400; line-height:1.6; -webkit-font-smoothing:antialiased; }
  .num { font-family:var(--font-num); font-variant-numeric:tabular-nums; letter-spacing:.02em; }
  .hidden { display:none !important; }

  /* Hero */
  .hero { position:relative; overflow:hidden; padding:36px 24px 0; text-align:center; }
  .hero svg.deco { position:absolute; inset:0; width:100%; height:100%; pointer-events:none; }
  .hero > *:not(.deco) { position:relative; }
  .logo { height:72px; max-width:220px; object-fit:contain; display:block; margin:0 auto 18px; }
  .wordmark { font-family:"Helvetica Neue",Helvetica,Arial,var(--font-zh); font-weight:300; font-size:30px;
              letter-spacing:.32em; color:var(--green); margin:0 0 6px .32em; }
  .zh-name { font-size:15px; letter-spacing:.42em; margin:0 0 22px .42em; }
  .zh-name:empty { display:none; }
  .logo:not(.hidden) ~ .wordmark.hidden + .zh-name { margin-top:-4px; }
  .hero h1 { margin:0; font-size:22px; font-weight:500; letter-spacing:.18em; }
  .hero p { margin:8px 0 0; color:var(--muted); font-size:14px; letter-spacing:.04em; }

  /* 分頁 */
  .tabs { display:flex; justify-content:center; gap:28px; margin-top:22px; border-bottom:1px solid var(--line); position:relative; }
  .tabs button { border:0; background:none; font-family:var(--font-zh); font-size:15px; letter-spacing:.16em; color:var(--muted);
                 padding:10px 2px 12px; cursor:pointer; border-bottom:1.5px solid transparent; margin-bottom:-1px; }
  .tabs button.on { color:var(--green-deep); border-color:var(--green); font-weight:500; }
  .badge { display:inline-block; min-width:18px; height:18px; padding:0 5px; border-radius:9px; background:var(--peach);
           color:#fff; font-size:11px; line-height:18px; letter-spacing:0; margin-left:4px; vertical-align:1px; }

  main { max-width:560px; margin:0 auto; padding:24px 18px 40px; }
  .card { background:var(--card); border:1px solid var(--line); border-radius:24px; padding:22px 20px; margin-bottom:18px; }
  .card h2 { margin:0 0 16px; font-size:16px; font-weight:500; letter-spacing:.12em; display:flex; align-items:center; gap:12px; }
  .step { font-family:"Helvetica Neue",Helvetica,Arial,sans-serif; font-weight:300; font-size:13px; color:var(--green);
          border:1px solid var(--green); border-radius:50%; width:30px; height:30px; display:inline-flex;
          align-items:center; justify-content:center; letter-spacing:0; flex:none; }

  /* 場館照片 */
  .gallery { margin:0 -18px 18px; }
  .strip { display:flex; gap:12px; overflow-x:auto; scroll-snap-type:x mandatory; padding:0 18px; scrollbar-width:none; }
  .strip::-webkit-scrollbar { display:none; }
  .strip figure { margin:0; flex:0 0 86%; scroll-snap-align:center; position:relative; }
  .strip figure:only-child { flex-basis:100%; }
  .strip img { width:100%; aspect-ratio:4/3; object-fit:cover; border-radius:22px; display:block; background:var(--closed); }
  .strip figcaption { position:absolute; left:12px; bottom:12px; background:rgba(255,254,238,.92); color:var(--ink);
                      font-size:12px; letter-spacing:.08em; padding:4px 12px; border-radius:999px; }
  .dots { display:flex; justify-content:center; gap:6px; margin-top:12px; }
  .dots i { width:6px; height:6px; border-radius:3px; background:var(--line); transition:.25s; }
  .dots i.on { width:18px; background:var(--green); }

  /* 關於 */
  .intro { display:flex; flex-direction:column; gap:10px; }
  .intro p { margin:0; font-size:14px; line-height:1.95; letter-spacing:.04em; }
  .intro p.lead { font-size:17px; line-height:1.75; font-weight:500; color:var(--green-deep); letter-spacing:.06em;
                  padding-bottom:12px; border-bottom:1px solid var(--line); text-wrap:balance; }
  .place { display:flex; align-items:flex-start; gap:10px; margin-top:16px; padding:14px 16px; border-radius:18px;
           background:var(--green-tint); font-size:14px; line-height:1.7; }
  .place svg { color:var(--green); flex:none; margin-top:3px; }
  .place-text { flex:1; min-width:0; }
  .place-map { flex:none; color:#fff; background:var(--green); border-radius:999px; padding:4px 14px; font-size:13px;
               text-decoration:none; letter-spacing:.06em; white-space:nowrap; }
  .place-map:hover { background:var(--green-deep); }
  .contact { display:flex; gap:10px; margin-top:16px; flex-wrap:wrap; }
  .chip { display:inline-flex; align-items:center; gap:8px; border:1px solid var(--line); border-radius:999px; padding:8px 16px;
          font-size:14px; color:var(--ink); text-decoration:none; background:var(--cream); }
  .chip:hover { border-color:var(--green); }
  .chip svg { color:var(--green); flex:none; }

  /* 日期 */
  .dates { display:flex; gap:10px; overflow-x:auto; padding:2px 2px 8px; scrollbar-width:none; }
  .dates::-webkit-scrollbar { display:none; }
  .date { flex:0 0 66px; border:1px solid var(--line); border-radius:999px; background:var(--cream);
          padding:12px 0 10px; text-align:center; cursor:pointer; font:inherit; color:inherit; transition:.2s; }
  .date .w { font-size:12px; color:var(--muted); letter-spacing:.08em; }
  .date .d { font-size:19px; font-weight:400; margin:2px 0; }
  .date .n { font-size:11px; color:var(--clay); }
  .date:disabled { opacity:.32; cursor:not-allowed; }
  .date:not(:disabled):hover { border-color:var(--green); }
  .date.sel { background:var(--green); border-color:var(--green); color:#fff; }
  .date.sel .w, .date.sel .n { color:rgba(255,255,255,.85); }

  /* 時段 */
  .group + .group { margin-top:14px; }
  .group-title { font-size:12px; color:var(--muted); letter-spacing:.24em; margin:4px 0 10px;
                 display:flex; align-items:center; gap:10px; }
  .group-title::after { content:""; flex:1; height:1px; background:var(--line); }
  .slots { display:grid; grid-template-columns:repeat(auto-fill,minmax(96px,1fr)); gap:10px; }
  .slot { border:1px solid var(--line); border-radius:999px; background:var(--cream); padding:10px 4px 8px;
          cursor:pointer; font:inherit; color:inherit; text-align:center; transition:.2s; }
  .slot:hover { border-color:var(--green); }
  .slot b { display:block; font-size:16px; font-weight:400; }
  .slot small { color:var(--clay); font-size:11px; }
  .slot.sel { background:var(--green); border-color:var(--green); color:#fff; }
  .slot.sel small { color:rgba(255,255,255,.85); }

  /* 表單 */
  label.f { display:block; font-size:13px; color:var(--muted); letter-spacing:.08em; margin:16px 0 6px; }
  label.f .opt { color:#b0b7ad; }
  input, textarea { width:100%; padding:12px 16px; border:1px solid var(--line); border-radius:16px;
                    font-family:var(--font-zh); font-size:16px; color:var(--ink); background:var(--cream); transition:.2s; }
  input[type=tel] { font-family:var(--font-num); letter-spacing:.04em; }
  input::placeholder, textarea::placeholder { color:#b9bfb0; }
  input:focus, textarea:focus { outline:none; border-color:var(--green); background:#fff; box-shadow:0 0 0 3px var(--green-tint); }
  .req { color:var(--clay); }
  .chosen { background:var(--green-tint); color:var(--green-deep); border-radius:16px; padding:12px 16px; font-size:14px; letter-spacing:.04em; }
  .choices { display:flex; flex-wrap:wrap; gap:8px; }
  .choices label { cursor:pointer; }
  .choices input { position:absolute; opacity:0; width:1px; height:1px; }
  .choices span { display:inline-block; border:1px solid var(--line); border-radius:999px; padding:9px 20px; background:var(--cream);
                  font-size:15px; letter-spacing:.08em; transition:.2s; }
  .choices input:checked + span { background:var(--green); border-color:var(--green); color:#fff; }
  .choices input:focus-visible + span { box-shadow:0 0 0 3px var(--green-tint); }

  .btn { display:block; width:100%; border:1px solid var(--green); border-radius:999px; padding:14px;
         font-family:var(--font-zh); font-size:16px; font-weight:500; letter-spacing:.24em;
         background:var(--green); color:#fff; cursor:pointer; margin-top:22px; text-align:center; text-decoration:none; transition:.2s; }
  .btn:hover { background:var(--green-deep); border-color:var(--green-deep); }
  .btn:disabled { opacity:.5; cursor:wait; }
  .btn.outline { background:transparent; color:var(--green-deep); }
  .btn.outline:hover { background:var(--green-tint); }
  .btn.ghost { background:transparent; color:var(--muted); border-color:var(--line); letter-spacing:.12em; }
  .btn + .btn { margin-top:10px; }
  .btn.small { display:inline-block; width:auto; padding:8px 18px; font-size:13px; letter-spacing:.1em; margin:0; }

  .msg { padding:12px 16px; border-radius:16px; font-size:14px; margin:12px 0 0; }
  .msg.err { background:var(--peach-tint); color:var(--clay-deep); border:1px solid rgba(214,116,66,.25); }
  .empty { color:var(--muted); font-size:14px; padding:6px 0; }

  /* 完成 */
  .done { text-align:center; padding-top:34px; }
  .check { width:58px; height:58px; border-radius:50%; border:1px solid var(--green); color:var(--green);
           display:flex; align-items:center; justify-content:center; margin:0 auto 14px; }
  .done h2 { justify-content:center; font-size:20px; }
  .done .label { color:var(--muted); font-size:13px; letter-spacing:.12em; }
  .done .code { font-size:36px; font-weight:300; letter-spacing:.36em; margin:6px 0 6px .36em; color:var(--green-deep); }
  .done .when { font-size:15px; }
  .done .hint { color:var(--muted); font-size:14px; margin:14px 0 0; line-height:1.8; }
  .line-box { background:var(--peach-tint); border-radius:20px; padding:18px 18px 20px; margin-top:22px; text-align:left; }
  .line-box b { font-weight:500; letter-spacing:.08em; }
  .line-box ol { font-size:14px; line-height:1.9; padding-left:20px; margin:8px 0 0; }

  /* 我的預約 */
  .bk { border:1px solid var(--line); border-radius:20px; padding:16px 18px; background:var(--cream); }
  .bk + .bk { margin-top:12px; }
  .bk-top { display:flex; justify-content:space-between; align-items:center; gap:10px; }
  .bk-when { font-size:17px; }
  .bk-code { color:var(--muted); font-size:12px; margin-top:2px; }
  .tag { display:inline-block; border-radius:999px; padding:3px 12px; font-size:12px; letter-spacing:.1em; white-space:nowrap; }
  .tag.待確認 { background:var(--peach-tint); color:var(--clay-deep); }
  .tag.已確認 { background:var(--green); color:#fff; }
  .tag.已到場 { background:var(--green-tint); color:var(--green-deep); }
  .tag.已婉拒, .tag.已取消, .tag.未到 { background:var(--closed); color:var(--muted); }
  .bk-body { margin-top:12px; padding-top:12px; border-top:1px dashed var(--line); font-size:14px; line-height:1.8; }
  .bk-body .addr { display:flex; gap:8px; align-items:flex-start; }
  .bk-body .addr svg { color:var(--green); margin-top:4px; flex:none; }
  .bk-body a { color:var(--green-deep); }
  .bk-actions { margin-top:12px; display:flex; gap:8px; flex-wrap:wrap; }
  .lookup { display:grid; grid-template-columns:1fr; gap:10px; }

  .spinner { width:24px; height:24px; border:2px solid var(--line); border-top-color:var(--green); border-radius:50%;
             animation:spin 1s linear infinite; margin:10px auto; }
  @keyframes spin { to { transform:rotate(360deg); } }
  footer { text-align:center; color:var(--muted); font-size:12px; letter-spacing:.12em; padding-bottom:32px; }
  /* 確認視窗 */
  .ask { position:fixed; inset:0; background:rgba(44,58,51,.32); display:flex; align-items:center; justify-content:center;
         padding:16px; z-index:20; }
  .ask-box { background:var(--card); border:1px solid var(--line); border-radius:22px; padding:22px 22px 18px; width:100%; max-width:360px;
             box-shadow:0 18px 40px rgba(44,58,51,.18); }
  .ask-box p { margin:0 0 18px; font-size:15px; line-height:1.8; letter-spacing:.04em; }
  .ask-btns { display:flex; justify-content:flex-end; gap:8px; }
  .btn.clay { background:transparent; color:var(--clay-deep); border-color:rgba(214,116,66,.45); }
  .btn.clay:hover { background:var(--peach-tint); }
</style>
</head>
<body>
<header class="hero">
  <svg class="deco" viewBox="0 0 400 260" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
    <circle cx="370" cy="-10" r="90" fill="none" stroke="#f6ae6a" stroke-width="1" opacity=".55"/>
    <circle cx="370" cy="-10" r="118" fill="none" stroke="#f6ae6a" stroke-width="1" opacity=".3"/>
    <path d="M-20 262 C 50 226, 110 226, 170 256" fill="none" stroke="#00a06e" stroke-width="1" opacity=".35"/>
    <circle cx="28" cy="40" r="5" fill="#d67442" opacity=".5"/>
  </svg>
  <img class="logo hidden" id="logo" alt="">
  <div class="wordmark" id="gymName"></div>
  <div class="zh-name" id="gymNameZh"></div>
  <h1>預約參觀</h1>
  <p>每次約 <span class="num" id="mins"></span> 分鐘，由教練帶您認識空間與課程</p>
  <nav class="tabs">
    <button type="button" class="on" data-view="book">預約參觀</button>
    <button type="button" data-view="mine">我的預約<span class="badge num hidden" id="mineCount"></span></button>
  </nav>
</header>

<main>
  <!-- ===== 預約參觀 ===== -->
  <div id="bookView">
    <div class="gallery hidden" id="gallery">
      <div class="strip" id="strip"></div>
      <div class="dots" id="dots"></div>
    </div>

    <section class="card about hidden" id="about">
      <div id="intro" class="intro"></div>
      <div class="place hidden" id="place"></div>
      <div class="contact" id="contact"></div>
    </section>

    <div id="bookingSteps">
      <section class="card">
        <h2><span class="step">01</span>選擇日期</h2>
        <div id="dates" class="dates"><div class="spinner"></div></div>
      </section>

      <section class="card hidden" id="slotCard">
        <h2><span class="step">02</span>選擇時段</h2>
        <div id="slots"></div>
      </section>

      <section class="card hidden" id="formCard">
        <h2><span class="step">03</span>填寫資料</h2>
        <div class="chosen" id="chosen"></div>
        <form id="form" autocomplete="on" novalidate>
          <div id="fields"></div>
          <button class="btn" id="submitBtn" type="submit">送出預約</button>
          <div id="formMsg"></div>
        </form>
      </section>
    </div>

    <section class="card done hidden" id="doneView">
      <div class="check"><svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M5 12.5l4.5 4.5L19 7.5"/></svg></div>
      <h2>已送出預約申請</h2>
      <div class="label">預約編號</div>
      <div class="code num" id="doneCode"></div>
      <div class="when num" id="doneLabel"></div>
      <p class="hint">店家確認後，可在「我的預約」查看狀態。</p>
      <div class="line-box hidden" id="lineBox">
        <b>以 LINE 接收確認與提醒</b>
        <ol>
          <li>加入官方帳號好友</li>
          <li>點「傳送預約編號」，送出已帶入的編號</li>
          <li>店家確認後會通知您，參觀前 <span class="num" id="remindH"></span> 小時再提醒</li>
        </ol>
        <a class="btn" id="lineAdd" target="_blank" rel="noopener">加入官方帳號</a>
        <a class="btn outline" id="lineSend" target="_blank" rel="noopener">傳送預約編號</a>
      </div>
      <button class="btn outline" type="button" onclick="showView('mine')">查看我的預約</button>
      <button class="btn ghost" type="button" onclick="restart()">再預約一個時段</button>
    </section>
  </div>

  <!-- ===== 我的預約 ===== -->
  <div id="mineView" class="hidden">
    <section class="card">
      <h2>我的預約</h2>
      <div id="mineList"><div class="spinner"></div></div>
    </section>
    <section class="card">
      <h2>查詢預約</h2>
      <form id="lookupForm" class="lookup">
        <input name="code" placeholder="預約編號（6 碼）" maxlength="6" autocapitalize="characters" class="num" style="letter-spacing:.2em">
        <input name="key" placeholder="預約時填寫的手機或姓名">
        <button class="btn" style="margin-top:4px">查詢</button>
        <div id="lookupMsg"></div>
      </form>
    </section>
  </div>
</main>
<footer id="foot"></footer>

<script>
const CFG = <?!= JSON.stringify(cfg) ?>;
const WEEK = ['日','一','二','三','四','五','六'];
const STORE_KEY = 'firstfit.myBookings';
let DATA = null, STORE = {}, FIELDS = {}, selDate = null, selSlot = null, slotNotice = '';

const $ = id => document.getElementById(id);
/** 頁內確認視窗（取代瀏覽器的 confirm） */
function ask(message, okText, danger) {
  return new Promise(resolve => {
    const prev = document.activeElement;
    const w = document.createElement('div');
    w.className = 'ask';
    w.innerHTML = '<div class="ask-box" role="dialog" aria-modal="true"><p></p><div class="ask-btns">' +
      '<button type="button" class="btn ghost small" data-v="0">返回</button>' +
      '<button type="button" class="btn small' + (danger ? ' clay' : '') + '" data-v="1"></button></div></div>';
    w.querySelector('p').textContent = message;
    w.querySelector('[data-v="1"]').textContent = okText || '確定';
    const close = v => { w.remove(); document.removeEventListener('keydown', onKey); if (prev && prev.focus) prev.focus(); resolve(v); };
    const onKey = e => { if (e.key === 'Escape') close(false); };
    w.addEventListener('click', e => {
      if (e.target === w) return close(false);
      const v = e.target.closest('[data-v]');
      if (v) close(v.dataset.v === '1');
    });
    document.addEventListener('keydown', onKey);
    document.body.appendChild(w);
    w.querySelector('[data-v="1"]').focus();
  });
}

$('gymName').textContent = CFG.gymNameEn || CFG.gymName;
$('gymNameZh').textContent = CFG.gymNameEn ? CFG.gymName : '';
$('mins').textContent = CFG.slotMinutes;
$('remindH').textContent = CFG.remindHours;

function el(tag, cls, html) { const e = document.createElement(tag); if (cls) e.className = cls; if (html != null) e.innerHTML = html; return e; }
function esc(s) { return String(s == null ? '' : s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
function num(s) { return '<span class="num">' + esc(s) + '</span>'; }
function dow(d) { return new Date(d + 'T12:00:00+08:00').getUTCDay(); }
function addDays(d, n) { const x = new Date(d + 'T12:00:00Z'); x.setUTCDate(x.getUTCDate() + n); return x.toISOString().slice(0, 10); }
function mmdd(d) { return Number(d.slice(5,7)) + '/' + Number(d.slice(8)); }
function errText(err) { return String(err && err.message || err).replace(/^Error:\s*/, ''); }
function run(fn, ...args) {
  return new Promise((ok, fail) => google.script.run.withSuccessHandler(ok).withFailureHandler(fail)[fn](...args));
}
/** 圖片：主要網址載入失敗時改用備用網址 */
function img(urls, alt) {
  const i = new Image();
  i.alt = alt || ''; i.loading = 'lazy'; i.src = urls.src;
  i.onerror = () => { if (urls.fallback && i.src !== urls.fallback) i.src = urls.fallback; };
  return i;
}
const ICON = {
  phone: '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M5 4h4l2 5-2.5 1.5a11 11 0 005 5L15 13l5 2v4a2 2 0 01-2 2A16 16 0 013 6a2 2 0 012-2"/></svg>',
  line: '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 4C7 4 3 7.2 3 11.2c0 3.5 3.1 6.4 7.3 7l-.5 2.6 3.4-2.5c4.6-.4 7.8-3.3 7.8-7.1C21 7.2 17 4 12 4z"/></svg>',
  pin: '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 21s-7-6.2-7-11.5a7 7 0 0114 0C19 14.8 12 21 12 21z"/><circle cx="12" cy="9.5" r="2.5"/></svg>',
};

// ---------- 分頁 ----------
document.querySelectorAll('.tabs button').forEach(b => b.onclick = () => showView(b.dataset.view));
function showView(v) {
  document.querySelectorAll('.tabs button').forEach(b => b.classList.toggle('on', b.dataset.view === v));
  $('bookView').classList.toggle('hidden', v !== 'book');
  $('mineView').classList.toggle('hidden', v !== 'mine');
  if (v === 'mine') loadMine();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

// ---------- 店家資料與照片 ----------
function renderStore() {
  const s = STORE;
  // 英文名稱當字標、中文名稱在下方；上傳 LOGO 後以 LOGO 取代字標
  $('gymName').textContent = s.nameEn || s.name;
  $('gymNameZh').textContent = (s.nameEn || s.logo) ? s.name : '';
  $('foot').textContent = s.nameEn ? s.name + '  ' + s.nameEn : s.name;
  if (s.logo) { const l = $('logo'); l.src = s.logo.src; l.onerror = () => { if (l.src !== s.logo.fallback) l.src = s.logo.fallback; }; l.alt = s.name; l.classList.remove('hidden'); }
  $('gymName').classList.toggle('hidden', !!s.logo);

  const photos = s.photos || [];
  $('gallery').classList.toggle('hidden', !photos.length);
  $('strip').innerHTML = ''; $('dots').innerHTML = '';
  photos.forEach((p, i) => {
    const fig = el('figure');
    fig.appendChild(img(p, p.caption || (s.name + ' 場館照片 ' + (i + 1))));
    if (p.caption) fig.appendChild(el('figcaption', '', esc(p.caption)));
    $('strip').appendChild(fig);
    if (photos.length > 1) $('dots').appendChild(el('i', i === 0 ? 'on' : ''));
  });
  $('strip').onscroll = () => {
    const st = $('strip'), figs = st.children; if (!figs.length) return;
    const i = Math.round(st.scrollLeft / (figs[0].offsetWidth + 12));
    [...$('dots').children].forEach((d, k) => d.classList.toggle('on', k === i));
  };

  const contact = [];
  // 地址與地圖：公開顯示
  $('place').innerHTML = s.address ? ICON.pin + '<span class="place-text">' + esc(s.address) + '</span>' +
    (s.mapUrl ? '<a class="place-map" target="_blank" rel="noopener" href="' + esc(s.mapUrl) + '">Google 地圖</a>' : '') : '';
  $('place').classList.toggle('hidden', !s.address);
  if (s.phone) contact.push('<a class="chip" href="tel:' + esc(s.phone.replace(/[^\d+]/g, '')) + '">' + ICON.phone + num(s.phone) + '</a>');
  if (s.lineAddUrl) contact.push('<a class="chip" target="_blank" rel="noopener" href="' + esc(s.lineAddUrl) + '">' + ICON.line + 'LINE 官方帳號</a>');
  const paras = String(s.intro || '').split(/\n+/).map(t => t.trim()).filter(Boolean);
  $('intro').innerHTML = paras.map((t, i) => '<p' + (i === 0 && paras.length > 1 ? ' class="lead"' : '') + '>' + esc(t) + '</p>').join('');
  $('intro').classList.toggle('hidden', !s.intro);
  $('contact').innerHTML = contact.join('');
  $('contact').style.marginTop = s.intro ? '' : '0';
  $('about').classList.toggle('hidden', !s.intro && !contact.length && !s.address);
}

// ---------- 預約表單欄位 ----------
function renderFields() {
  const f = FIELDS, box = $('fields');
  const lab = (text, required) => '<label class="f">' + esc(text) + (required ? ' <span class="req">*</span>' : ' <span class="opt">（選填）</span>') + '</label>';
  let h = lab('姓名', true) + '<input name="name" maxlength="30" autocomplete="name">';
  if (f.phone.enabled) h += lab(f.phone.label, f.phone.required) + '<input name="phone" type="tel" inputmode="numeric" placeholder="0912 345 678" autocomplete="tel">';
  if (f.gender.enabled) h += lab(f.gender.label, f.gender.required) + '<div class="choices">' +
    f.gender.options.map(o => '<label><input type="radio" name="gender" value="' + esc(o) + '"><span>' + esc(o) + '</span></label>').join('') + '</div>';
  if (f.email.enabled) h += lab(f.email.label, f.email.required) + '<input name="email" type="email" autocomplete="email">';
  if (f.note.enabled) h += lab(f.note.label, f.note.required) + '<textarea name="note" rows="3" maxlength="200" placeholder="例：器械皮拉提斯、一對一課程、方案價格"></textarea>';
  box.innerHTML = h;
}
function formValues() {
  const f = $('form'), v = k => f.elements[k] ? f.elements[k].value.trim() : '';
  const g = f.querySelector('input[name=gender]:checked');
  return { name: v('name'), phone: v('phone'), email: v('email'), note: v('note'), gender: g ? g.value : '' };
}
function checkForm(v) {
  const f = FIELDS;
  if (!v.name) return '請填寫姓名';
  if (f.phone.enabled && f.phone.required && !v.phone) return '請填寫' + f.phone.label;
  if (f.gender.enabled && f.gender.required && !v.gender) return '請選擇' + f.gender.label;
  if (f.email.enabled && f.email.required && !v.email) return '請填寫' + f.email.label;
  if (f.note.enabled && f.note.required && !v.note) return '請填寫' + f.note.label;
  return '';
}

// ---------- 載入 ----------
function load(onlySlots) {
  run(onlySlots ? 'getPublicSlots' : 'getPublicData').then(d => {
    if (onlySlots) { DATA = d; }
    else { DATA = d.booking; STORE = d.store; FIELDS = d.fields; renderStore(); renderFields(); }
    renderDates();
  }).catch(err => { $('dates').innerHTML = '<div class="msg err">' + esc(errText(err)) + '</div>'; });
}

function renderDates() {
  const box = $('dates');
  box.innerHTML = '';
  let first = null;
  for (let d = DATA.today; d <= DATA.lastDay; d = addDays(d, 1)) {
    const list = DATA.days[d] || [];
    const b = el('button', 'date',
      '<div class="w">' + (d === DATA.today ? '今天' : '週' + WEEK[dow(d)]) + '</div>' +
      '<div class="d num">' + mmdd(d) + '</div>' +
      '<div class="n">' + (list.length ? num(list.length) + ' 時段' : '額滿') + '</div>');
    b.type = 'button';
    b.disabled = !list.length;
    b.dataset.date = d;
    b.onclick = () => selectDate(d);
    box.appendChild(b);
    if (list.length && !first) first = d;
  }
  if (!first) box.innerHTML = '<div class="empty">近期暫無可預約時段，歡迎透過 LINE 與我們聯繫。</div>';
  else selectDate(selDate && DATA.days[selDate] ? selDate : first);
}

function selectDate(d) {
  selDate = d; selSlot = null;
  document.querySelectorAll('.date').forEach(b => b.classList.toggle('sel', b.dataset.date === d));
  $('formCard').classList.add('hidden');
  const box = $('slots');
  box.innerHTML = '';
  const groups = [['上午', s => s.start < '12:00'], ['下午', s => s.start >= '12:00' && s.start < '18:00'], ['晚上', s => s.start >= '18:00']];
  groups.forEach(([title, fn]) => {
    const list = (DATA.days[d] || []).filter(fn);
    if (!list.length) return;
    const g = el('div', 'group');
    g.appendChild(el('div', 'group-title', title));
    const grid = el('div', 'slots');
    list.forEach(s => {
      const b = el('button', 'slot', '<b class="num">' + s.start + '</b><small>剩 ' + num(s.remain) + ' 位</small>');
      b.type = 'button';
      b.onclick = () => selectSlot(s, b);
      grid.appendChild(b);
    });
    g.appendChild(grid);
    box.appendChild(g);
  });
  if (slotNotice) {
    box.prepend(el('div', 'msg err', esc(slotNotice)));
    slotNotice = '';
    $('slotCard').scrollIntoView({ behavior: 'smooth', block: 'start' });
  }
  $('slotCard').classList.remove('hidden');
}

function selectSlot(s, btn) {
  selSlot = s;
  document.querySelectorAll('.slot').forEach(b => b.classList.remove('sel'));
  btn.classList.add('sel');
  $('chosen').innerHTML = num(selDate.replace(/-/g, '.')) + '（週' + WEEK[dow(selDate)] + '）' + num(s.start + ' – ' + s.end);
  $('formCard').classList.remove('hidden');
  $('formMsg').innerHTML = '';
  $('formCard').scrollIntoView({ behavior: 'smooth', block: 'start' });
}

$('form').addEventListener('submit', e => {
  e.preventDefault();
  if (!selSlot) return;
  const btn = $('submitBtn'), msg = $('formMsg'), v = formValues();
  const problem = checkForm(v);
  if (problem) { msg.innerHTML = '<div class="msg err">' + esc(problem) + '</div>'; return; }
  btn.disabled = true; btn.textContent = '送出中'; msg.innerHTML = '';
  run('createBooking', Object.assign({ slotId: selSlot.id }, v)).then(r => {
    saveMine({ code: r.code, key: r.key });
    $('bookingSteps').classList.add('hidden');
    $('doneView').classList.remove('hidden');
    $('doneCode').textContent = r.code;
    $('doneLabel').textContent = r.label;
    $('lineBox').classList.toggle('hidden', !r.lineAddUrl);
    if (r.lineAddUrl) { $('lineAdd').href = r.lineAddUrl; $('lineSend').href = r.lineSendUrl; }
    btn.disabled = false; btn.textContent = '送出預約';
    $('form').reset();
    window.scrollTo(0, 0);
  }).catch(err => {
    btn.disabled = false; btn.textContent = '送出預約';
    const text = errText(err);
    if (/時段/.test(text)) { slotNotice = text; load(true); }
    else msg.innerHTML = '<div class="msg err">' + esc(text) + '</div>';
  });
});

function restart() {
  $('doneView').classList.add('hidden');
  $('bookingSteps').classList.remove('hidden');
  selDate = null; load(true);
}

// ---------- 我的預約（記在這支手機上） ----------
function readMine() { try { return JSON.parse(localStorage.getItem(STORE_KEY)) || []; } catch (e) { return []; } }
function writeMine(list) { try { localStorage.setItem(STORE_KEY, JSON.stringify(list.slice(0, 10))); } catch (e) {} updateBadge(list); }
function saveMine(item) { writeMine([item].concat(readMine().filter(x => x.code !== item.code))); }
function updateBadge(list) {
  const n = (list || readMine()).length;
  $('mineCount').textContent = n; $('mineCount').classList.toggle('hidden', !n);
}

function loadMine() {
  const items = readMine();
  const box = $('mineList');
  if (!items.length) { box.innerHTML = '<div class="empty">這支手機還沒有預約紀錄。在其他裝置預約過，可用下方查詢。</div>'; return; }
  box.innerHTML = '<div class="spinner"></div>';
  run('getMyBookings', items).then(list => {
    list.sort((a, b) => (b.date + b.start).localeCompare(a.date + a.start));
    box.innerHTML = list.length ? '' : '<div class="empty">查無預約紀錄。</div>';
    list.forEach(b => box.appendChild(bookingCard(b)));
  }).catch(err => { box.innerHTML = '<div class="msg err">' + esc(errText(err)) + '</div>'; });
}

function bookingCard(b) {
  const c = el('div', 'bk');
  let body = '';
  if (b.status === '待確認') body = '<div style="margin-bottom:6px">等待店家確認' + (STORE.lineAddUrl ? '，綁定 LINE 會收到通知。' : '。') + '</div>';
  if (b.address) body += '<div class="addr">' + ICON.pin + '<div>' + esc(b.address) +
      (b.mapUrl ? '<br><a href="' + esc(b.mapUrl) + '" target="_blank" rel="noopener">在 Google 地圖開啟</a>' : '') + '</div></div>' +
      (b.phone ? '<div class="addr">' + ICON.phone + '<a class="num" href="tel:' + esc(b.phone.replace(/[^\d+]/g, '')) + '">' + esc(b.phone) + '</a></div>' : '');
  else if (b.status === '已婉拒') body = '很抱歉，這個時段無法安排，歡迎改約其他時段。';
  c.innerHTML = '<div class="bk-top"><div><div class="bk-when">' + num(b.date.replace(/-/g, '.')) + '（' + b.weekday + '）' + num(b.start) + '</div>' +
    '<div class="bk-code">預約編號 ' + num(b.code) + '</div></div><span class="tag ' + esc(b.status) + '">' + esc(b.status) + '</span></div>' +
    (body ? '<div class="bk-body">' + body + '</div>' : '');
  if (b.canCancel) {
    const act = el('div', 'bk-actions');
    const btn = el('button', 'btn ghost small', '取消預約');
    btn.type = 'button';
    btn.onclick = async () => {
      if (!(await ask('確定取消 ' + b.date.replace(/-/g, '.') + ' ' + b.start + ' 的參觀預約？', '取消預約', true))) return;
      const item = readMine().find(x => x.code === b.code) || {};
      btn.disabled = true;
      run('cancelMyBooking', b.code, item.key).then(() => { loadMine(); load(true); })
        .catch(err => { btn.disabled = false; act.appendChild(el('div', 'msg err', esc(errText(err)))); });
    };
    act.appendChild(btn);
    c.appendChild(act);
  }
  return c;
}

$('lookupForm').addEventListener('submit', e => {
  e.preventDefault();
  const f = e.target, code = f.code.value.trim().toUpperCase(), key = f.key.value.trim(), msg = $('lookupMsg');
  msg.innerHTML = '';
  if (!code || !key) { msg.innerHTML = '<div class="msg err">請輸入預約編號與手機（或姓名）</div>'; return; }
  run('lookupBooking', code, key).then(() => { saveMine({ code, key }); f.reset(); loadMine(); })
    .catch(err => { msg.innerHTML = '<div class="msg err">' + esc(errText(err)) + '</div>'; });
});

updateBadge();
load();
</script>
</body>
</html>

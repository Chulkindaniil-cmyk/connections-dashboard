<!DOCTYPE html>
<html lang="ru">
<head>
<base target="_top">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Соединения</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/chartjs-plugin-datalabels/2.2.0/chartjs-plugin-datalabels.min.js"></script>

<!-- 🔥 SUPABASE CLIENT -->
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script>
  // 🔥 ЗАМЕНИ НА СВОИ ДАННЫЕ!
  const SUPABASE_URL = 'https://qujovlodgpyxgjmudict.supabase.co';
  const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InF1am92bG9kZ3B5eGdqbXVkaWN0Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODIzNjM4NTAsImV4cCI6MjA5NzkzOTg1MH0.M1wAUxR3E4Oe3mQ6IXPmOSj9t6IXXKyyi0bKZrSzG6A';  // ← Settings → API → anon (public)
  const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_KEY);
</script>

<style>
:root{
--page:#ED131C; --accent:#C00020; --accent-soft:rgba(192,0,32,.06);
--ink:#1A2332; --sec:rgba(26,35,50,.55); --mute:rgba(26,35,50,.42);
--card:#fff; --line:rgba(0,0,0,.07); --head:#FAFAFB;
--shadow:0 6px 22px rgba(0,0,0,.18), 0 1px 3px rgba(0,0,0,.06);
--r:14px;
--ok:#1c8c4a; --warn:#E0A800; --bad:#C00020;
}
*{box-sizing:border-box}
body{margin:0;background:var(--page);color:var(--ink);
font-family:"Manrope",-apple-system,"Segoe UI",Roboto,Arial,sans-serif;-webkit-font-smoothing:antialiased}
.wrap{max-width:1200px;margin:0 auto;padding:0 18px 56px}
.hero{color:#fff;text-align:center;padding:30px 20px 22px}
.hero .eyebrow{font-size:11px;letter-spacing:.34em;text-transform:uppercase;opacity:.9;font-weight:700}
.hero h1{margin:8px 0 5px;font-size:34px;font-weight:800;letter-spacing:.01em}
.hero .sub{font-size:13px;opacity:.92}
.panel{background:var(--card);border-radius:var(--r);box-shadow:var(--shadow);padding:18px}
.stack{margin-top:16px}
.panel-title{font-size:11px;letter-spacing:.18em;text-transform:uppercase;color:var(--mute);font-weight:700;margin-bottom:6px}
.ctitle{font-size:13px;letter-spacing:.14em;text-transform:uppercase;color:var(--ink);font-weight:700}
.fgrid{display:grid;grid-template-columns:repeat(3,1fr) auto;gap:14px;margin-top:12px;align-items:start}
.field{display:flex;flex-direction:column;gap:6px;position:relative}
.field label{font-size:10.5px;letter-spacing:.1em;text-transform:uppercase;color:var(--mute);font-weight:700}
.field-actions{display:flex;gap:10px;padding-top:22px}
.trigger{appearance:none;border:1px solid var(--line);background:#fff;border-radius:10px;
padding:10px 12px;font:inherit;color:var(--ink);width:100%;text-align:left;
display:flex;justify-content:space-between;align-items:center;cursor:pointer;min-height:42px}
.trigger:hover{border-color:var(--accent)}
.trigger .arr{font-size:10px;color:var(--mute);margin-left:8px}
.dropdown{display:none;position:absolute;top:calc(100% + 4px);left:0;right:0;background:#fff;
border:1px solid var(--line);border-radius:10px;box-shadow:var(--shadow);
max-height:380px;overflow:hidden;z-index:30;flex-direction:column}
.dropdown.open{display:flex}
.dropdown .opt{padding:10px 14px;font-size:13px;cursor:pointer;color:var(--ink)}
.dropdown .opt:hover{background:var(--accent-soft)}
.dropdown .opt.active{background:var(--accent-soft);color:var(--accent);font-weight:700}
.dropdown .sep{border-top:1px solid var(--line);margin-top:4px;padding-top:10px}
.custom-dates{padding:12px;border-top:1px solid var(--line);display:none}
.custom-dates.show{display:block}
.date-inputs{display:flex;gap:8px;align-items:center}
.date-inputs input{flex:1;padding:8px 10px;border:1px solid var(--line);border-radius:8px;
font:inherit;font-size:13px;color:var(--ink)}
.date-inputs input:focus{outline:2px solid rgba(192,0,32,.25);border-color:var(--accent)}
.dd-search{padding:10px;border-bottom:1px solid var(--line)}
.dd-search input{width:100%;padding:8px 10px;border:1px solid var(--line);border-radius:8px;
font:inherit;font-size:13px;color:var(--ink)}
.dd-actions{display:flex;gap:8px;padding:8px 10px;border-bottom:1px solid var(--line)}
.dd-options{overflow-y:auto;flex:1;padding:4px 0}
.opt-item{display:flex;align-items:center;gap:8px;padding:7px 14px;cursor:pointer;font-size:13px}
.opt-item:hover{background:var(--accent-soft)}
.opt-item input[type="checkbox"]{pointer-events:none;accent-color:var(--accent)}
.opt-item label{flex:1;cursor:pointer;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.selected-count{font-size:10.5px;color:var(--mute);margin-top:4px;font-weight:600}
.btn{border-radius:10px;padding:10px 18px;font:inherit;font-weight:700;cursor:pointer;
border:1px solid var(--line);min-height:42px;white-space:nowrap}
.btn.ghost{background:#fff;color:var(--ink)}
.btn.ghost:hover{border-color:var(--ink)}
.btn.primary{background:var(--accent);color:#fff;border-color:var(--accent)}
.btn.primary:hover{filter:brightness(.94)}
.btn.tiny{padding:8px 12px;font-size:12px;min-height:34px}
.btn.pdf{background:var(--ink);color:#fff;border-color:var(--ink)}
.btn.pdf:hover{filter:brightness(1.15)}
.kpis{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-top:16px}
.kpi{background:var(--card);border-radius:var(--r);box-shadow:var(--shadow);padding:16px 18px 15px}
.kpi .kl{font-size:10.5px;letter-spacing:.08em;text-transform:uppercase;color:var(--mute);font-weight:700}
.kpi .kv{font-size:30px;font-weight:800;letter-spacing:-.01em;margin-top:9px;line-height:1.05}
.kpi .kh{font-size:11px;color:var(--mute);margin-top:6px}
.kpi .kv.ok{color:var(--ok)} .kpi .kv.warn{color:var(--warn)} .kpi .kv.bad{color:var(--bad)}
.kpi .kh.ok{color:var(--ok)} .kpi .kh.warn{color:var(--warn)} .kpi .kh.bad{color:var(--bad)}
.banner-date{text-align:center;font-size:11.5px;color:rgba(255,255,255,.92);
margin-top:10px;letter-spacing:.04em;font-weight:600}
.tables-row{display:grid;grid-template-columns:repeat(2,1fr);gap:14px;margin-top:16px}
.tables-row .panel{padding:14px}
.tbl-title{font-size:11px;letter-spacing:.14em;text-transform:uppercase;color:var(--mute);
font-weight:700;margin:0 0 8px}
table{width:100%;border-collapse:collapse;font-size:12.5px}
thead th{background:var(--head);color:var(--mute);text-transform:uppercase;letter-spacing:.05em;
font-size:10.5px;font-weight:700;padding:8px 10px;text-align:left}
thead th.c{text-align:right}
tbody td{padding:8px 10px;border-bottom:1px solid var(--line);color:var(--ink);font-variant-numeric:tabular-nums}
tbody td.c{text-align:right}
tbody tr:hover{background:var(--accent-soft)}
tbody tr.total td{background:#FAFAFB;font-weight:800;border-top:2px solid var(--line);border-bottom:none}
.empty{padding:24px;text-align:center;color:var(--sec);font-size:12.5px}
.charts-row{display:grid;grid-template-columns:1fr;gap:14px;margin-top:16px}
.chart-card{position:relative}
.chart-head{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:8px;gap:10px}
.chart-change{font-size:11px;font-weight:700;padding:4px 9px;border-radius:999px;
background:var(--head);color:var(--mute);white-space:nowrap}
.chart-change.up{background:rgba(28,140,74,.12);color:var(--ok)}
.chart-change.down{background:rgba(192,0,32,.1);color:var(--bad)}
.chart-box{position:relative;height:280px;margin-top:6px}
.bottom-actions{display:flex;gap:10px;justify-content:flex-end;flex-wrap:wrap;margin-top:16px}
.cache-info{font-size:11px;color:rgba(255,255,255,.85);text-align:right;margin:8px 2px 0;font-weight:600}
.loading{display:none;background:var(--card);border-radius:var(--r);box-shadow:var(--shadow);
padding:30px;text-align:center;color:var(--mute);font-weight:600;margin-top:16px}
.loading.show{display:block}
.spinner{border:3px solid #f3f3f3;border-top:3px solid var(--accent);border-radius:50%;
width:30px;height:30px;animation:spin 1s linear infinite;margin:0 auto 10px}
@keyframes spin{to{transform:rotate(360deg)}}
@media(max-width:1100px){
.kpis{grid-template-columns:repeat(2,1fr)}
.fgrid{grid-template-columns:1fr 1fr}
.fgrid .field-actions{grid-column:1/-1;justify-content:flex-end;padding-top:0}
}
@media(max-width:640px){
.tables-row,.kpis,.fgrid{grid-template-columns:1fr}
}
.pdf-export-mode{background:#fff !important}
.pdf-export-mode .filters,.pdf-export-mode .bottom-actions,.pdf-export-mode .cache-info{display:none !important}
.pdf-export-mode .panel{box-shadow:none !important;border:1px solid var(--line)}
.pdf-export-mode .kpi .kv{font-size:22px}
.pdf-export-mode .chart-box{height:200px}
.pdf-export-mode table{font-size:10.5px}
.pdf-export-mode thead th,.pdf-export-mode tbody td{padding:5px 7px}
</style>
</head>
<body>
<div class="hero">
<div class="eyebrow">Аналитика</div>
<h1>СОЕДИНЕНИЯ</h1>
<div class="sub">Отчёт с фильтрами по периоду и срезам</div>
<div class="banner-date" id="ystDateLabel">Данные за: —</div>
</div>
<div class="wrap">
<div class="panel filters">
<div class="panel-title">Фильтры</div>
<div class="fgrid">
<div class="field" id="periodSelector">
<label>Период</label>
<div class="trigger" id="periodTrigger" onclick="togglePeriodDropdown()">
<span id="periodText">Этот год</span><span class="arr">▾</span>
</div>
<div class="dropdown" id="periodDropdown">
<div class="opt" onclick="selectPeriod('yesterday')">Вчера</div>
<div class="opt" onclick="selectPeriod('thisWeek')">Эта неделя</div>
<div class="opt" onclick="selectPeriod('lastWeek')">Прошлая неделя</div>
<div class="opt" onclick="selectPeriod('thisMonth')">Этот месяц</div>
<div class="opt" onclick="selectPeriod('lastMonth')">Прошлый месяц</div>
<div class="opt active" onclick="selectPeriod('thisYear')">Этот год</div>
<div class="opt" onclick="selectPeriod('last7')">Последние 7 дней</div>
<div class="opt" onclick="selectPeriod('last30')">Последние 30 дней</div>
<div class="opt" onclick="selectPeriod('last90')">Последние 90 дней</div>
<div class="opt" onclick="selectPeriod('last365')">Последние 365 дней</div>
<div class="opt sep" onclick="showCustomDates()">Указать период…</div>
<div class="custom-dates" id="customDatesBlock">
<div class="date-inputs">
<input type="date" id="customDateFrom">
<span>—</span>
<input type="date" id="customDateTo">
</div>
<button class="btn primary tiny" style="width:100%;margin-top:8px" onclick="applyCustomDates()">Применить</button>
</div>
</div>
<div class="selected-count" style="visibility:hidden">0 выбрано</div>
</div>
<div class="field" id="landFilterWrapper">
<label>Ленд</label>
<div class="trigger" onclick="toggleDropdown('land')">
<span id="landTriggerText">Выберите ленд…</span><span class="arr">▾</span>
</div>
<div class="dropdown" id="landDropdown">
<div class="dd-search"><input type="text" placeholder="Поиск ленда…" onkeyup="filterOptions('land', this.value)"></div>
<div class="dd-actions">
<button class="btn ghost tiny" onclick="selectAll('land')">Выбрать все</button>
<button class="btn ghost tiny" onclick="deselectAll('land')">Снять все</button>
</div>
<div class="dd-options" id="landOptions"></div>
</div>
<div class="selected-count" id="landCount">0 выбрано</div>
</div>
<div class="field" id="respFilterWrapper">
<label>Ответственный</label>
<div class="trigger" onclick="toggleDropdown('resp')">
<span id="respTriggerText">Выберите ответственного…</span><span class="arr">▾</span>
</div>
<div class="dropdown" id="respDropdown">
<div class="dd-search"><input type="text" placeholder="Поиск…" onkeyup="filterOptions('resp', this.value)"></div>
<div class="dd-actions">
<button class="btn ghost tiny" onclick="selectAll('resp')">Выбрать все</button>
<button class="btn ghost tiny" onclick="deselectAll('resp')">Снять все</button>
</div>
<div class="dd-options" id="respOptions"></div>
</div>
<div class="selected-count" id="respCount">0 выбрано</div>
</div>
<div class="field field-actions">
<button class="btn ghost" onclick="resetFilters()">Сбросить</button>
<button class="btn primary" onclick="applyFilters()">Применить</button>
</div>
</div>
</div>
<div class="cache-info" id="cacheInfo">Загрузка…</div>
<div id="loading" class="loading"><div class="spinner"></div>Загрузка данных…</div>
<div id="exportContent">
<div class="kpis">
<div class="kpi">
<div class="kl">Соединения</div>
<div class="kv" id="ystConn">—</div>
<div class="kh" id="ystConnDelta">за день</div>
</div>
<div class="kpi">
<div class="kl">Сделка создана</div>
<div class="kv" id="ystDeal">—</div>
<div class="kh" id="ystDealPct">0%</div>
</div>
<div class="kpi">
<div class="kl">Топ колл-центр</div>
<div class="kv" id="ystTopCC" style="font-size:20px">—</div>
<div class="kh" id="ystTopCCCount">— соединений</div>
</div>
<div class="kpi">
<div class="kl">Отказы</div>
<div class="kv" id="ystRefusal">—</div>
<div class="kh" id="ystRefusalDelta">за день</div>
</div>
</div>
<div class="tables-row">
<div class="panel"><h3 class="tbl-title">Структура</h3><div id="tableContainerStructures"></div></div>
<div class="panel"><h3 class="tbl-title">Этап</h3>      <div id="tableContainerStages"></div></div>
<div class="panel"><h3 class="tbl-title">Город</h3>     <div id="tableContainerCities"></div></div>
<div class="panel"><h3 class="tbl-title">Ленд</h3>      <div id="tableContainerLands"></div></div>
</div>
<div class="charts-row">
<div class="panel chart-card">
<div class="chart-head">
<div class="ctitle" id="chartTitle1">Динамика (кол-во)</div>
<div class="chart-change" id="changeIndicator1">—</div>
</div>
<div class="chart-box"><canvas id="dailyChart1"></canvas></div>
</div>
<div class="panel chart-card">
<div class="chart-head">
<div class="ctitle" id="chartTitle2">% Сделка создана</div>
<div class="chart-change" id="changeIndicator2">—</div>
</div>
<div class="chart-box"><canvas id="dailyChart2"></canvas></div>
</div>
</div>
</div>
<div class="bottom-actions">
<button class="btn ghost" id="btnRefresh" onclick="loadData()">Обновить</button>
<button class="btn ghost" onclick="exportToCsv()">Экспорт CSV</button>
<button class="btn pdf" onclick="exportToPdf()">Экспорт PDF</button>
</div>
</div>

<script>
let currentData = null;
let currentFilters = { from: '', to: '', lands: [], responsibles: [] };
let currentPeriod = 'thisYear';
let dailyChart1 = null, dailyChart2 = null;
let loadStartTime = 0;
let allLands = [];
let allResps = [];
let loadCompleteCount = 0;
let isFirstLoad = true;

if (typeof Chart !== 'undefined' && typeof ChartDataLabels !== 'undefined') {
  Chart.register(ChartDataLabels);
}

const ACCENT = '#C00020';
const INK    = '#1A2332';
const ACCENT_FILL = 'rgba(192,0,32,0.10)';
const INK_FILL    = 'rgba(26,35,50,0.07)';

// 🔥 ИНИЦИАЛИЗАЦИЯ
document.addEventListener('DOMContentLoaded', () => {
  loadStartTime = Date.now();
  loadAllFilters();
  initDropdowns();
  loadYesterdaysKPI();
  const today = new Date();
  const from = new Date();
  from.setMonth(0, 1);
  currentFilters.from = formatDateForFilter(from);
  currentFilters.to = formatDateForFilter(today);
  loadData();
});

function initDropdowns() {
  document.addEventListener('click', function(event) {
    if (!event.target.closest('#periodSelector')) document.getElementById('periodDropdown').classList.remove('open');
    if (!event.target.closest('#landFilterWrapper')) document.getElementById('landDropdown').classList.remove('open');
    if (!event.target.closest('#respFilterWrapper')) document.getElementById('respDropdown').classList.remove('open');
  });
}

// 🔥 ЗАМЕНА getYesterdaysKPI()
async function loadYesterdaysKPI() {
  try {
    const { data: lastDateData, error: dateError } = await supabase
      .from('connections')
      .select('date_connection')
      .not('date_connection', 'is', null)
      .gte('date_connection', '2026-01-01')
      .order('date_connection', { ascending: false })
      .limit(1);

    if (dateError) throw dateError;
    if (!lastDateData || lastDateData.length === 0) return;

    const maxDate = lastDateData[0].date_connection;
    
    const { data: prevDateData } = await supabase
      .from('connections')
      .select('date_connection')
      .lt('date_connection', maxDate)
      .gte('date_connection', '2026-01-01')
      .order('date_connection', { ascending: false })
      .limit(1);

    const prevDate = prevDateData && prevDateData.length > 0 ? prevDateData[0].date_connection : null;

    const { data: currData, error: currError } = await supabase
      .from('connections')
      .select('structure, connections, stage')
      .eq('date_connection', maxDate);

    if (currError) throw currError;

    let prevData = [];
    if (prevDate) {
      const { data } = await supabase
        .from('connections')
        .select('connections, stage')
        .eq('date_connection', prevDate);
      prevData = data || [];
    }

    const connLast = currData.reduce((sum, r) => sum + (r.connections || 0), 0);
    const dealLast = currData.filter(r => String(r.stage).toLowerCase() === 'сделка создана')
                            .reduce((sum, r) => sum + (r.connections || 0), 0);
    const refusalLast = currData.filter(r => String(r.stage).toLowerCase() === 'отказ')
                               .reduce((sum, r) => sum + (r.connections || 0), 0);

    const connPrev = prevData.reduce((sum, r) => sum + (r.connections || 0), 0);
    const dealPrev = prevData.filter(r => String(r.stage).toLowerCase() === 'сделка создана')
                            .reduce((sum, r) => sum + (r.connections || 0), 0);
    const refusalPrev = prevData.filter(r => String(r.stage).toLowerCase() === 'отказ')
                               .reduce((sum, r) => sum + (r.connections || 0), 0);

    const structCount = {};
    currData.forEach(r => {
      structCount[r.structure] = (structCount[r.structure] || 0) + (r.connections || 0);
    });
    let topCCName = '—', topCCCount = 0;
    for (const [name, count] of Object.entries(structCount)) {
      if (count > topCCCount) { topCCCount = count; topCCName = name; }
    }

    const dealPct = connLast > 0 ? ((dealLast / connLast) * 100) : 0;
    const prevDealPct = connPrev > 0 ? ((dealPrev / connPrev) * 100) : 0;

    const kpi = {
      date: maxDate.split('-').reverse().join('.'),
      connections: connLast,
      dealCreated: dealLast,
      dealPct: dealPct.toFixed(2).replace('.', ',') + '%',
      topCallCenter: topCCName,
      topCallCenterCount: topCCCount,
      refusals: refusalLast,
      prevConnections: connPrev,
      prevDealCreated: dealPrev,
      prevDealPct: prevDealPct.toFixed(2).replace('.', ',') + '%',
      prevRefusals: refusalPrev
    };

    if (kpi) renderYesterdayBanner(kpi);
  } catch (er) {
    console.error('Ошибка загрузки KPI:', er);
  }
}

function togglePeriodDropdown() {
  document.getElementById('periodDropdown').classList.toggle('open');
  document.getElementById('landDropdown').classList.remove('open');
  document.getElementById('respDropdown').classList.remove('open');
}

function selectPeriod(period) {
  currentPeriod = period;
  const options = document.querySelectorAll('#periodDropdown .opt');
  options.forEach(opt => opt.classList.remove('active'));
  const periodMap = { 'yesterday':0,'thisWeek':1,'lastWeek':2,'thisMonth':3,'lastMonth':4,'thisYear':5,'last7':6,'last30':7,'last90':8,'last365':9 };
  if (periodMap[period] !== undefined) options[periodMap[period]].classList.add('active');
  document.getElementById('customDatesBlock').classList.remove('show');
  const dates = getPeriodDates(period);
  currentFilters.from = dates.from;
  currentFilters.to = dates.to;
  const periodNames = { 'yesterday':'Вчера','thisWeek':'Эта неделя','lastWeek':'Прошлая неделя','thisMonth':'Этот месяц','lastMonth':'Прошлый месяц','thisYear':'Этот год','last7':'Последние 7 дней','last30':'Последние 30 дней','last90':'Последние 90 дней','last365':'Последние 365 дней' };
  document.getElementById('periodText').textContent = periodNames[period] || 'Период';
  document.getElementById('periodDropdown').classList.remove('open');
  isFirstLoad = false;
  loadData();
}

function showCustomDates() {
  document.getElementById('customDatesBlock').classList.toggle('show');
  document.querySelectorAll('#periodDropdown .opt').forEach(opt => opt.classList.remove('active'));
}

function applyCustomDates() {
  const from = document.getElementById('customDateFrom').value;
  const to = document.getElementById('customDateTo').value;
  if (!from || !to) { alert('Пожалуйста, выберите обе даты'); return; }
  currentFilters.from = formatDateForFilter(from);
  currentFilters.to = formatDateForFilter(to);
  currentPeriod = 'custom';
  document.getElementById('periodText').textContent = `${formatDateForFilter(from)} — ${formatDateForFilter(to)}`;
  document.getElementById('customDatesBlock').classList.remove('show');
  document.getElementById('periodDropdown').classList.remove('open');
  isFirstLoad = false;
  loadData();
}

function getPeriodDates(period) {
  const today = new Date();
  const from = new Date();
  const to = new Date();
  switch(period) {
    case 'yesterday': from.setDate(today.getDate() - 1); to.setDate(today.getDate() - 1); break;
    case 'thisWeek': from.setDate(today.getDate() - (today.getDay() || 7) + 1); break;
    case 'lastWeek': { const lw = today.getDay() || 7; from.setDate(today.getDate() - lw - 6); to.setDate(today.getDate() - lw); break; }
    case 'thisMonth': from.setDate(1); break;
    case 'lastMonth': from.setMonth(today.getMonth() - 1); from.setDate(1); to.setMonth(today.getMonth()); to.setDate(0); break;
    case 'thisYear': from.setMonth(0, 1); break;
    case 'last7': from.setDate(today.getDate() - 6); break;
    case 'last30': from.setDate(today.getDate() - 29); break;
    case 'last90': from.setDate(today.getDate() - 89); break;
    case 'last365': from.setDate(today.getDate() - 364); break;
  }
  return { from: formatDateForFilter(from), to: formatDateForFilter(to) };
}

function formatDateForFilter(date) {
  const d = new Date(date);
  return `${String(d.getDate()).padStart(2,'0')}.${String(d.getMonth()+1).padStart(2,'0')}.${d.getFullYear()}`;
}

function toggleDropdown(type) {
  const dropdown = document.getElementById(type + 'Dropdown');
  const otherDropdown = document.getElementById(type === 'land' ? 'respDropdown' : 'landDropdown');
  dropdown.classList.toggle('open');
  otherDropdown.classList.remove('open');
  document.getElementById('periodDropdown').classList.remove('open');
}

function renderOptions(type, options, selectedValues) {
  const container = document.getElementById(type + 'Options');
  container.innerHTML = '';
  options.forEach(opt => {
    const div = document.createElement('div');
    div.className = 'opt-item';
    const id = `${type}_${opt.replace(/\s/g, '_')}`;
    const isChecked = selectedValues.includes(opt);
    div.innerHTML = `<input type="checkbox" id="${id}" value="${escapeAttr(opt)}" ${isChecked ? 'checked' : ''}><label>${escapeHtml(opt)}</label>`;
    div.addEventListener('click', () => {
      const cb = div.querySelector('input[type="checkbox"]');
      cb.checked = !cb.checked;
      updateSelection(type);
    });
    container.appendChild(div);
  });
  updateCount(type);
}

function filterOptions(type, query) {
  const allOpts = type === 'land' ? allLands : allResps;
  const filtered = allOpts.filter(o => o.toLowerCase().includes(query.toLowerCase()));
  const selected = currentFilters[type === 'land' ? 'lands' : 'responsibles'];
  renderOptions(type, filtered, selected);
}

function updateSelection(type) {
  const checkboxes = document.querySelectorAll(`#${type}Options input[type="checkbox"]`);
  const selected = Array.from(checkboxes).filter(cb => cb.checked).map(cb => cb.value);
  if (type === 'land') currentFilters.lands = selected;
  else currentFilters.responsibles = selected;
  updateCount(type);
}

function selectAll(type)   { document.querySelectorAll(`#${type}Options input[type="checkbox"]`).forEach(cb => cb.checked = true); updateSelection(type); }
function deselectAll(type) { document.querySelectorAll(`#${type}Options input[type="checkbox"]`).forEach(cb => cb.checked = false); updateSelection(type); }

function updateCount(type) {
  const count = currentFilters[type === 'land' ? 'lands' : 'responsibles'].length;
  const label = type === 'land' ? 'ленд' : 'ответственных';
  document.getElementById(type + 'Count').textContent = `${count} выбрано`;
  const triggerText = document.getElementById(type + 'TriggerText');
  triggerText.textContent = count === 0 ? (type === 'land' ? 'Выберите ленд…' : 'Выберите ответственного…') : `${count} ${label}`;
}

// 🔥 ЗАМЕНА getAllFilterOptions()
async function loadAllFilters() {
  try {
    const { data: landData, error: landError } = await supabase
      .from('connections')
      .select('land')
      .not('land', 'is', null)
      .neq('land', '');

    if (landError) throw landError;

    const { data: respData, error: respError } = await supabase
      .from('connections')
      .select('responsible')
      .not('responsible', 'is', null)
      .neq('responsible', '');

    if (respError) throw respError;

    const lands = [...new Set(landData.map(r => r.land).filter(Boolean))].sort();
    const responsibles = [...new Set(respData.map(r => r.responsible).filter(Boolean))].sort();

    allLands = lands;
    allResps = responsibles;

    renderOptions('land', allLands, []);
    renderOptions('resp', allResps, []);
    updateCacheInfo('Фильтры загружены');
  } catch (er) {
    alert('Ошибка сети: ' + er.message);
  }
}

function applyFilters() { loadData(); }

function resetFilters() {
  currentFilters.lands = [];
  currentFilters.responsibles = [];
  loadCompleteCount = 0;
  isFirstLoad = true;
  currentPeriod = 'thisYear';
  const today = new Date();
  const from = new Date();
  from.setMonth(0, 1);
  currentFilters.from = formatDateForFilter(from);
  currentFilters.to = formatDateForFilter(today);
  document.getElementById('periodText').textContent = 'Этот год';
  const options = document.querySelectorAll('#periodDropdown .opt');
  options.forEach(opt => opt.classList.remove('active'));
  options[5].classList.add('active');
  renderOptions('land', allLands, []);
  renderOptions('resp', allResps, []);
  loadData();
}

function loadData() {
  document.getElementById('btnRefresh').disabled = true;
  document.getElementById('loading').classList.add('show');
  loadStartTime = Date.now();
  loadCompleteCount = 0;
  loadTableData();
  loadChartData();
}

// 🔥 ЗАМЕНА getTableData()
async function loadTableData() {
  try {
    let query = supabase
      .from('connections')
      .select('structure, connections, stage, city, land, date_connection');

    if (isFirstLoad) {
      const { data: lastDate } = await supabase
        .from('connections')
        .select('date_connection')
        .not('date_connection', 'is', null)
        .gte('date_connection', '2026-01-01')
        .order('date_connection', { ascending: false })
        .limit(1);

      if (lastDate && lastDate.length > 0) {
        query = query.eq('date_connection', lastDate[0].date_connection);
      }
    } else {
      if (currentFilters.from) {
        const fromParts = currentFilters.from.split('.').reverse().join('-');
        query = query.gte('date_connection', fromParts);
      }
      if (currentFilters.to) {
        const toParts = currentFilters.to.split('.').reverse().join('-');
        query = query.lte('date_connection', toParts);
      }
    }

    if (currentFilters.lands.length > 0) {
      query = query.in('land', currentFilters.lands);
    }
    if (currentFilters.responsibles.length > 0) {
      query = query.in('responsible', currentFilters.responsibles);
    }

    const { data, error } = await query;
    if (error) throw error;

    const structureData = {};
    const stageData = {};
    const cityDataRaw = {};
    const landDataRaw = {};

    data.forEach(row => {
      if (!structureData[row.structure]) {
        structureData[row.structure] = { connections: 0, deals: 0 };
      }
      structureData[row.structure].connections += row.connections || 0;
      if (String(row.stage).toLowerCase() === 'сделка создана') {
        structureData[row.structure].deals += row.connections || 0;
      }

      stageData[row.stage] = (stageData[row.stage] || 0) + (row.connections || 0);
      cityDataRaw[row.city] = (cityDataRaw[row.city] || 0) + (row.connections || 0);
      if (row.land) {
        landDataRaw[row.land] = (landDataRaw[row.land] || 0) + (row.connections || 0);
      }
    });

    const tableRes = Object.entries(structureData).map(([name, d]) => ({
      structure: name,
      connections: d.connections,
      deals: d.deals,
      conversionRate: d.connections > 0 ? parseFloat(((d.deals / d.connections) * 100)) : 0
    })).sort((a, b) => b.connections - a.connections);

    const stageRes = Object.entries(stageData).map(([n, c]) => ({ stage: n, count: c }))
      .sort((a, b) => b.count - a.count);

    const sortedCities = Object.entries(cityDataRaw).map(([n, c]) => ({ city: n, count: c }))
      .sort((a, b) => b.count - a.count);
    const top10 = sortedCities.slice(0, 10);
    const others = sortedCities.slice(10);
    const cityDataResult = [...top10];
    if (others.reduce((s, i) => s + i.count, 0) > 0) {
      cityDataResult.push({ city: 'Другие', count: others.reduce((s, i) => s + i.count, 0) });
    }

    const sortedLands = Object.entries(landDataRaw).map(([n, c]) => ({ land: n, count: c }))
      .sort((a, b) => b.count - a.count);
    const top10Lands = sortedLands.slice(0, 10);
    const otherLands = sortedLands.slice(10);
    const landDataResult = [...top10Lands];
    if (otherLands.reduce((s, i) => s + i.count, 0) > 0) {
      landDataResult.push({ land: 'Другие', count: otherLands.reduce((s, i) => s + i.count, 0) });
    }

    let dateLabel = '—';
    if (isFirstLoad && data.length > 0) {
      const maxDate = data.reduce((max, r) => r.date_connection > max ? r.date_connection : max, data[0].date_connection);
      dateLabel = maxDate.split('-').reverse().join('.');
    } else if (currentFilters.from && currentFilters.to) {
      dateLabel = `${currentFilters.from} — ${currentFilters.to}`;
    }

    currentData = {
      tableData: tableRes,
      stageData: stageRes,
      cityData: cityDataResult,
      landData: landDataResult,
      date: dateLabel
    };

    renderTable('tableContainerStructures', tableRes, 'Структура');
    renderTable('tableContainerStages', stageRes, 'Этап');
    renderTable('tableContainerCities', cityDataResult, 'Город');
    renderTable('tableContainerLands', landDataResult, 'Ленд');
    document.getElementById('ystDateLabel').textContent = 
      isFirstLoad ? `Таблицы: данные за ${dateLabel}` : `Таблицы: за период ${dateLabel}`;

    checkLoadComplete();
  } catch (er) {
    document.getElementById('loading').classList.remove('show');
    document.getElementById('btnRefresh').disabled = false;
    alert('Ошибка загрузки таблиц: ' + er.message);
  }
}

// 🔥 ЗАМЕНА getDashboardData()
async function loadChartData() {
  try {
    let query = supabase
      .from('connections')
      .select('date_connection, connections, stage');

    if (currentFilters.from) {
      const fromParts = currentFilters.from.split('.').reverse().join('-');
      query = query.gte('date_connection', fromParts);
    }
    if (currentFilters.to) {
      const toParts = currentFilters.to.split('.').reverse().join('-');
      query = query.lte('date_connection', toParts);
    }

    if (currentFilters.lands.length > 0) {
      query = query.in('land', currentFilters.lands);
    }
    if (currentFilters.responsibles.length > 0) {
      query = query.in('responsible', currentFilters.responsibles);
    }

    const { data, error } = await query;
    if (error) throw error;

    const dates = data.map(r => r.date_connection).filter(Boolean);
    const minDate = dates.length > 0 ? dates.reduce((a, b) => a < b ? a : b) : null;
    const maxDate = dates.length > 0 ? dates.reduce((a, b) => a > b ? a : b) : null;
    const diffDays = minDate && maxDate ? Math.round((new Date(maxDate) - new Date(minDate)) / (1000 * 60 * 60 * 24)) + 1 : 0;
    const groupByMonth = diffDays > 30;

    const periodData = {};
    const periodDealCreated = {};
    const periodTotal = {};

    data.forEach(row => {
      const d = new Date(row.date_connection);
      const periodKey = groupByMonth 
        ? `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}`
        : `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}-${String(d.getDate()).padStart(2, '0')}`;

      periodTotal[periodKey] = (periodTotal[periodKey] || 0) + (row.connections || 0);
      if (String(row.stage).toLowerCase() === 'сделка создана') {
        periodDealCreated[periodKey] = (periodDealCreated[periodKey] || 0) + (row.connections || 0);
      }
      periodData[periodKey] = (periodData[periodKey] || 0) + (row.connections || 0);
    });

    const dealCreatedPctData = Object.entries(periodTotal).map(([key, total]) => {
      const deals = periodDealCreated[key] || 0;
      const pct = total > 0 ? ((deals / total) * 100) : 0;
      const parts = key.split('-');
      return {
        date: groupByMonth ? `${parts[1]}.${parts[0]}` : `${parts[2]}.${parts[1]}.${parts[0]}`,
        value: parseFloat(pct.toFixed(2))
      };
    }).sort((a, b) => a.date.localeCompare(b.date));

    const chartRes = Object.entries(periodData)
      .sort((a, b) => a[0].localeCompare(b[0]))
      .map(([key, count]) => {
        const parts = key.split('-');
        return {
          date: groupByMonth ? `${parts[1]}.${parts[0]}` : `${parts[2]}.${parts[1]}.${parts[0]}`,
          count
        };
      });

    let volumeDiff = 0;
    let pctDiff = 0;
    if (chartRes.length >= 2) {
      volumeDiff = chartRes[chartRes.length - 1].count - chartRes[chartRes.length - 2].count;
      pctDiff = dealCreatedPctData.length >= 2 
        ? dealCreatedPctData[dealCreatedPctData.length - 1].value - dealCreatedPctData[dealCreatedPctData.length - 2].value 
        : 0;
    }

    renderChart1(chartRes, groupByMonth);
    renderChart2(dealCreatedPctData, groupByMonth);
    updateChangeIndicator('changeIndicator1', volumeDiff, 'volume');
    updateChangeIndicator('changeIndicator2', pctDiff, 'pct');

    const loadTime = ((Date.now() - loadStartTime) / 1000).toFixed(2);
    updateCacheInfo(`Загружено за ${loadTime} с`);
    
    checkLoadComplete();
  } catch (er) {
    document.getElementById('loading').classList.remove('show');
    document.getElementById('btnRefresh').disabled = false;
    alert('Ошибка загрузки графиков: ' + er.message);
  }
}

function checkLoadComplete() {
  loadCompleteCount++;
  if (loadCompleteCount >= 2) {
    document.getElementById('loading').classList.remove('show');
    document.getElementById('btnRefresh').disabled = false;
    loadCompleteCount = 0;
  }
}

function updateCacheInfo(msg) { document.getElementById('cacheInfo').textContent = msg; }

function renderYesterdayBanner(m) {
  if (!m) return;
  const connEl = document.getElementById('ystConn');
  const connKH = document.getElementById('ystConnDelta');
  connEl.textContent = m.connections.toLocaleString('ru-RU');
  const connDiff = m.connections - (m.prevConnections || 0);
  setKvTone(connEl, connKH, connDiff, false);
  connKH.textContent = formatDelta(connDiff) + ' к пред. дню';
  const dealEl = document.getElementById('ystDeal');
  const dealPct = document.getElementById('ystDealPct');
  dealEl.textContent = m.dealCreated.toLocaleString('ru-RU');
  dealPct.textContent = m.dealPct;
  const currentPct = parseFloat(m.dealPct.replace('%','').replace(',','.'));
  const prevPct    = parseFloat((m.prevDealPct || '0%').replace('%','').replace(',','.'));
  const pctDiff = currentPct - prevPct;
  let tone = 'warn';
  if (m.prevConnections === 0 && m.prevDealCreated === 0) {
    tone = currentPct >= 5 ? 'ok' : 'warn';
  } else {
    if (pctDiff >= 5) tone = 'ok';
    else if (pctDiff <= -5) tone = 'bad';
    else tone = 'warn';
  }
  applyTone(dealEl,  tone);
  applyTone(dealPct, tone);
  document.getElementById('ystTopCC').textContent = m.topCallCenter;
  document.getElementById('ystTopCCCount').textContent = `${m.topCallCenterCount.toLocaleString('ru-RU')} соединений`;
  const refEl = document.getElementById('ystRefusal');
  const refKH = document.getElementById('ystRefusalDelta');
  refEl.textContent = m.refusals.toLocaleString('ru-RU');
  const refDiff = m.refusals - (m.prevRefusals || 0);
  setKvTone(refEl, refKH, refDiff, true);
  refKH.textContent = formatDelta(refDiff) + ' к пред. дню';
}

function setKvTone(kvEl, khEl, diff, invert) {
  let tone;
  if (diff >= 15)  tone = invert ? 'bad'  : 'ok';
  else if (diff <= -15) tone = invert ? 'ok' : 'bad';
  else tone = 'warn';
  applyTone(kvEl, tone);
  applyTone(khEl, tone);
}

function applyTone(el, tone) {
  el.classList.remove('ok','warn','bad');
  el.classList.add(tone);
}

function formatDelta(n) {
  if (n === 0) return '0';
  const sign = n > 0 ? '+' : '−';
  return sign + Math.abs(n).toLocaleString('ru-RU');
}

function updateChangeIndicator(elementId, diff, type) {
  const el = document.getElementById(elementId);
  if (diff === undefined || diff === null) { el.textContent = '—'; el.className = 'chart-change'; return; }
  const isUp = diff >= 0;
  const arrow = isUp ? '▲' : '▼';
  let text = (type === 'volume')
    ? `${arrow} ${diff >= 0 ? '+' : '−'}${Math.abs(diff).toLocaleString('ru-RU')}`
    : `${arrow} ${diff >= 0 ? '+' : '−'}${Math.abs(diff).toFixed(2).replace('.', ',')}%`;
  el.textContent = text;
  el.className = `chart-change ${isUp ? 'up' : 'down'}`;
}

function renderTable(containerId, data, colName) {
  const container = document.getElementById(containerId);
  if (!container) return;
  if (!data || data.length === 0) { container.innerHTML = '<div class="empty">Нет данных</div>'; return; }
  let totalConn = 0;
  if (colName === 'Структура') totalConn = data.reduce((s, r) => s + (r.connections || 0), 0);
  else totalConn = data.reduce((s, r) => s + r.count, 0);
  let html = '';
  if (colName === 'Структура') {
    html = `<table><thead><tr>
      <th>Структура</th><th class="c">Соед.</th><th class="c">Сделка</th><th class="c">Конв.</th><th class="c">Доля</th>
    </tr></thead><tbody>`;
    data.forEach(row => {
      const share = totalConn > 0 ? ((row.connections / totalConn) * 100) : 0;
      html += `<tr>
        <td>${escapeHtml(row.structure)}</td>
        <td class="c">${row.connections.toLocaleString('ru-RU')}</td>
        <td class="c">${row.deals.toLocaleString('ru-RU')}</td>
        <td class="c">${row.conversionRate.toFixed(2).replace('.', ',')}%</td>
        <td class="c">${share.toFixed(2).replace('.', ',')}%</td>
      </tr>`;
    });
    const totalDeals = data.reduce((s, r) => s + (r.deals || 0), 0);
    const totalConv = totalConn > 0 ? ((totalDeals / totalConn) * 100) : 0;
    html += `<tr class="total"><td>ИТОГО</td>
      <td class="c">${totalConn.toLocaleString('ru-RU')}</td>
      <td class="c">${totalDeals.toLocaleString('ru-RU')}</td>
      <td class="c">${totalConv.toFixed(2).replace('.', ',')}%</td>
      <td class="c">100%</td></tr></tbody></table>`;
  } else {
    const colKey = colName === 'Этап' ? 'stage' : (colName === 'Город' ? 'city' : 'land');
    html = `<table><thead><tr><th>${colName}</th><th class="c">Кол-во</th><th class="c">Доля</th></tr></thead><tbody>`;
    data.forEach(row => {
      const count = row.count || 0;
      const pct = totalConn > 0 ? ((count / totalConn) * 100).toFixed(2).replace('.', ',') + '%' : '0%';
      html += `<tr><td>${escapeHtml(row[colKey])}</td><td class="c">${count.toLocaleString('ru-RU')}</td><td class="c">${pct}</td></tr>`;
    });
    html += `<tr class="total"><td>ИТОГО</td><td class="c">${totalConn.toLocaleString('ru-RU')}</td><td class="c">100%</td></tr></tbody></table>`;
  }
  container.innerHTML = html;
}

function renderChart1(data, isMonthly) {
  if (!data || !data.length) return;
  const ctx = document.getElementById('dailyChart1').getContext('2d');
  if (dailyChart1) dailyChart1.destroy();
  document.getElementById('chartTitle1').textContent = isMonthly ? 'Динамика по месяцам' : 'Динамика по дням';
  dailyChart1 = new Chart(ctx, {
    type: 'line',
    data: { labels: data.map(d => d.date), datasets: [{
      data: data.map(d => d.count),
      borderColor: ACCENT, backgroundColor: ACCENT_FILL,
      fill: true, tension: 0.3, pointRadius: data.length > 20 ? 2 : 4,
      pointBackgroundColor: '#fff', pointBorderColor: ACCENT, pointBorderWidth: 2,
      borderWidth: 2.5
    }] },
    options: chartOpts(false, isMonthly)
  });
}

function renderChart2(data, isMonthly) {
  if (!data || !data.length) return;
  const ctx = document.getElementById('dailyChart2').getContext('2d');
  if (dailyChart2) dailyChart2.destroy();
  document.getElementById('chartTitle2').textContent = isMonthly ? '% Сделка создана (по месяцам)' : '% Сделка создана (по дням)';
  dailyChart2 = new Chart(ctx, {
    type: 'line',
    data: { labels: data.map(d => d.date), datasets: [{
      data: data.map(d => d.value),
      borderColor: INK, backgroundColor: INK_FILL,
      fill: true, tension: 0.3, pointRadius: data.length > 20 ? 2 : 4,
      pointBackgroundColor: '#fff', pointBorderColor: INK, pointBorderWidth: 2,
      borderWidth: 2.5
    }] },
    options: chartOpts(true, isMonthly)
  });
}

function chartOpts(isPct, isMonthly) {
  return {
    responsive: true, maintainAspectRatio: false,
    layout: { padding: { top: 24 } },
    plugins: {
      legend: { display: false },
      tooltip: isPct ? { callbacks: { label: c => `Доля: ${c.parsed.y}%` } } : {},
      datalabels: {
        anchor: 'end',
        align: 'top',
        offset: 4,
        color: isPct ? INK : ACCENT,
        font: { family: 'Manrope', size: 11, weight: 700 },
        formatter: v => {
          if (v === null || v === undefined) return '';
          return isPct
            ? v.toFixed(1).replace('.', ',') + '%'
            : Number(v).toLocaleString('ru-RU');
        }
      }
    },
    scales: {
      y: {
        beginAtZero: true,
        grid: { color: 'rgba(0,0,0,0.06)' },
        ticks: {
          font: { family: 'Manrope', size: 11 },
          color: 'rgba(26,35,50,0.55)',
          callback: isPct ? (v => v + '%') : undefined
        }
      },
      x: {
        grid: { display: false },
        ticks: {
          maxRotation: isMonthly ? 0 : 45, minRotation: 0,
          font: { family: 'Manrope', size: 11 },
          color: 'rgba(26,35,50,0.6)'
        }
      }
    }
  };
}

function exportToPdf() {
  if (!currentData) { alert('Нет данных для экспорта'); return; }
  document.getElementById('landDropdown').classList.remove('open');
  document.getElementById('respDropdown').classList.remove('open');
  document.getElementById('periodDropdown').classList.remove('open');
  const root = document.body;
  root.classList.add('pdf-export-mode');
  const element = document.getElementById('exportContent');
  setTimeout(() => {
    const opt = {
      margin: [5, 5, 5, 5],
      filename: `connections_report_${new Date().toISOString().slice(0,10)}.pdf`,
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { scale: 0.7, useCORS: true, scrollY: 0, logging: false, backgroundColor: '#ffffff' },
      jsPDF: { unit: 'mm', format: 'a4', orientation: 'landscape', compress: true }
    };
    html2pdf().set(opt).from(element).save()
      .then(() => root.classList.remove('pdf-export-mode'))
      .catch(err => { console.error(err); root.classList.remove('pdf-export-mode'); alert('Ошибка при создании PDF'); });
  }, 250);
}

function exportToCsv() {
  if (!currentData?.tableData) { alert('Нет данных для экспорта'); return; }
  const totalConn = currentData.tableData.reduce((a,b)=>a+(b.connections||0),0) || 1;
  const headers = ['Структура','Соединения','Сделки','Конверсия','Доля'];
  const rows = [headers.join(';')];
  currentData.tableData.forEach(r => {
    const share = (r.connections/totalConn*100).toFixed(2).replace('.', ',') + '%';
    const conv  = r.conversionRate.toFixed(2).replace('.', ',') + '%';
    rows.push([r.structure, r.connections, r.deals, conv, share]
      .map(v => { const s = String(v||''); return /[;"\n]/.test(s) ? '"'+s.replace(/"/g,'""')+'"' : s; })
      .join(';'));
  });
  const blob = new Blob(['\ufeff' + rows.join('\r\n')], { type: 'text/csv;charset=utf-8' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `connections_${new Date().toISOString().slice(0,10)}.csv`;
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
  URL.revokeObjectURL(a.href);
}

function escapeHtml(text) { const div = document.createElement('div'); div.textContent = String(text==null?'':text); return div.innerHTML; }
function escapeAttr(text) { return String(text==null?'':text).replace(/"/g,'&quot;'); }
</script>
</body>
</html>

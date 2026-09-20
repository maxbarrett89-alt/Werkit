[workout-chart.html](https://github.com/user-attachments/files/32444968/workout-chart.html)
# Werkit<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Weekly Hypertrophy Plan</title>
<style>
  :root{
    --bg:#faf8f4;
    --panel:#ffffff;
    --panel2:#f2efe8;
    --border:#e2ddd0;
    --brass:#b8792e;
    --brass-dim:#e8cd9f;
    --slate:#3f7186;
    --slate-dim:#cfe1e8;
    --text:#262421;
    --muted:#7d766a;
    --good:#3e8a5c;
  }
  *{box-sizing:border-box;}
  html,body{
    margin:0;padding:0;
    background:var(--bg);
    color:var(--text);
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Arial,sans-serif;
    -webkit-font-smoothing:antialiased;
  }
  .wrap{max-width:640px;margin:0 auto;padding:28px 18px 60px;}

  header.top{margin-bottom:22px;}
  .kicker{color:var(--brass);font-weight:700;letter-spacing:0.04em;font-size:13px;margin:0 0 4px;}
  h1{font-size:30px;line-height:1.05;margin:0 0 6px;font-weight:800;letter-spacing:-0.01em;}
  .sub{color:var(--muted);font-size:14px;margin:0;}

  .tabs{
    display:flex;gap:6px;margin:22px 0 18px;
    background:var(--panel);border:1px solid var(--border);
    border-radius:10px;padding:4px;
  }
  .tab{
    flex:1;text-align:center;padding:10px 8px;border-radius:7px;
    font-weight:700;font-size:14px;cursor:pointer;color:var(--muted);
    user-select:none;transition:background .15s ease, color .15s ease;
  }
  .tab.active{background:var(--brass);color:#20180a;}

  .day{
    border:1px solid var(--border);border-radius:12px;margin-bottom:12px;
    overflow:hidden;background:var(--panel);
  }
  .day-head{
    display:flex;align-items:center;justify-content:space-between;
    padding:14px 16px;cursor:pointer;user-select:none;
  }
  .day-head .left{display:flex;align-items:baseline;gap:10px;}
  .day-head .right{display:flex;align-items:center;gap:8px;}
  .day-time{
    font-size:12px;
    font-weight:700;
    color:var(--muted);
    background:var(--panel2);
    border:1px solid var(--border);
    padding:4px 9px;
    border-radius:999px;
    white-space:nowrap;
  }
  .mark-done-btn{
    font-size:11px;
    font-weight:700;
    padding:4px 9px;
    border-radius:999px;
    border:1px solid var(--border);
    background:var(--panel2);
    color:var(--muted);
    cursor:pointer;
    white-space:nowrap;
  }
  .mark-done-btn.on{
    background:var(--good);
    border-color:var(--good);
    color:#fff;
  }
  .day-num{font-size:12px;color:var(--muted);font-weight:700;}
  .day-title{font-size:16px;font-weight:800;}
  .chev{color:var(--muted);transition:transform .18s ease;font-size:13px;}
  .day.open .chev{transform:rotate(90deg);}

  .day-body{
    max-height:0;overflow:hidden;transition:max-height .25s ease;
    border-top:1px solid transparent;
  }
  .day.open .day-body{
    max-height:none;
    overflow:visible;
    border-top:1px solid var(--border);
  }

  .section-label{
    padding:10px 16px 4px;
    font-size:11px;
    font-weight:700;
    color:var(--muted);
    letter-spacing:0.03em;
  }

  .ex-card{
    display:flex;justify-content:space-between;align-items:center;gap:10px;
    padding:14px 16px;border-bottom:1px solid var(--border);
    cursor:pointer;transition:background .12s ease;
  }
  .ex-card:last-child{border-bottom:none;}
  .ex-card:hover, .ex-card:active{background:var(--panel2);}

  .ex-info .ex-name{font-size:14.5px;font-weight:700;display:flex;align-items:center;}
  .ex-info .ex-scheme{font-size:12px;color:var(--muted);margin-top:2px;}

  .ex-right{display:flex;align-items:center;gap:8px;flex-shrink:0;}
  .progress-chip{
    font-size:11px;font-weight:700;color:var(--brass);
    background:var(--panel2);border:1px solid var(--brass-dim);
    padding:3px 8px;border-radius:999px;min-width:38px;text-align:center;
  }
  .progress-chip.alt{color:var(--slate);border-color:var(--slate-dim);}
  .open-arrow{color:var(--muted);font-size:16px;}

  .amrap-tag{
    font-size:10px;color:var(--brass);border:1px solid var(--brass-dim);
    padding:1px 6px;border-radius:5px;margin-left:6px;font-weight:700;
  }
  .kind-icon{margin-right:7px;font-size:14px;}
  .weight-badge{
    font-size:11px;
    font-weight:700;
    color:var(--slate);
    background:var(--slate-dim);
    border:1px solid var(--slate);
    padding:3px 8px;
    border-radius:999px;
    white-space:nowrap;
  }

  .legend{
    display:flex;gap:16px;align-items:center;color:var(--muted);
    font-size:12px;margin:18px 2px 0;flex-wrap:wrap;
  }
  .legend .sw{display:inline-flex;align-items:center;gap:6px;}
  .legend .dot{width:12px;height:12px;border-radius:3px;display:inline-block;}

  footer{margin-top:26px;font-size:12px;color:var(--muted);line-height:1.5;}

  /* ---- calendar ---- */
  .cal-card{
    border:1px solid var(--border);
    border-radius:12px;
    background:var(--panel);
    padding:16px;
    margin-bottom:18px;
  }
  .cal-head{
    display:flex;
    align-items:center;
    justify-content:space-between;
    margin-bottom:12px;
  }
  .cal-title{font-size:15px;font-weight:800;}
  .cal-nav{display:flex;align-items:center;gap:10px;}
  .cal-nav button{
    background:var(--panel2);
    border:1px solid var(--border);
    color:var(--text);
    width:26px;height:26px;
    border-radius:50%;
    cursor:pointer;
    font-size:13px;
    line-height:1;
  }
  .cal-month-label{font-size:13px;font-weight:700;color:var(--muted);min-width:104px;text-align:center;}
  .cal-grid{
    display:grid;
    grid-template-columns:repeat(7,1fr);
    gap:5px;
  }
  .cal-dow{
    text-align:center;
    font-size:10px;
    font-weight:700;
    color:var(--muted);
    padding-bottom:4px;
  }
  .cal-day{
    position:relative;
    aspect-ratio:1;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:12px;
    border-radius:8px;
    color:var(--text);
    background:var(--panel2);
    border:1px solid transparent;
  }
  .cal-day.empty{background:transparent;}
  .cal-day.today{border-color:var(--brass);font-weight:800;}
  .cal-day.done{
    background:var(--brass);
    color:#2c2005;
    font-weight:800;
  }
  .cal-streak{
    margin-top:12px;
    font-size:12px;
    color:var(--muted);
  }

  /* ---- modal pop-out ---- */
  .backdrop{
    position:fixed;inset:0;background:rgba(8,9,11,0.72);
    display:none;align-items:flex-end;justify-content:center;z-index:50;
  }
  .backdrop.show{display:flex;}
  @media (min-width:560px){.backdrop{align-items:center;}}

  .modal{
    background:var(--panel);border:1px solid var(--border);
    width:100%;max-width:480px;border-radius:18px 18px 0 0;
    padding:20px 18px 26px;max-height:85vh;overflow-y:auto;
    animation:slideUp .18s ease;
  }
  @media (min-width:560px){.modal{border-radius:18px;}}
  @keyframes slideUp{from{transform:translateY(24px);opacity:0;}to{transform:translateY(0);opacity:1;}}

  .modal-head{display:flex;justify-content:space-between;align-items:flex-start;gap:10px;margin-bottom:4px;}
  .modal-title{font-size:19px;font-weight:800;display:flex;align-items:center;}
  .modal-scheme{font-size:13px;color:var(--muted);margin-top:3px;}
  .close-btn{
    background:var(--panel2);border:1px solid var(--border);color:var(--muted);
    width:30px;height:30px;border-radius:50%;font-size:16px;line-height:1;
    cursor:pointer;flex-shrink:0;
  }

  .rest-pill{
    margin-top:14px;display:inline-flex;align-items:center;gap:6px;
    background:var(--panel2);border:1px solid var(--border);color:var(--slate);
    font-size:13px;font-weight:700;padding:8px 14px;border-radius:999px;
    cursor:pointer;transition:background .15s ease, color .15s ease, border-color .15s ease;
  }
  .rest-pill:active{transform:scale(0.97);}
  .rest-pill.running{color:var(--bg);background:var(--slate);border-color:var(--slate);}
  .rest-pill.done{color:var(--bg);background:var(--good);border-color:var(--good);}

  .sets{display:flex;flex-direction:column;gap:12px;margin-top:18px;}
  .set-row{display:flex;align-items:center;gap:10px;}
  .set-label{width:46px;flex-shrink:0;font-size:12px;color:var(--muted);font-weight:700;}
  .boxes{display:flex;gap:6px;flex-wrap:wrap;}
  .rep-box{
    width:24px;height:24px;border-radius:5px;background:var(--panel2);
    border:1px solid var(--border);cursor:pointer;
    transition:background .12s ease, border-color .12s ease, transform .08s ease;
  }
  .rep-box.filled{background:var(--brass);border-color:var(--brass);}
  .rep-box:active{transform:scale(0.85);}

  .modal-footnote{margin-top:16px;font-size:12px;color:var(--muted);}

  .weight-row{
    display:flex;
    align-items:center;
    gap:8px;
    margin-top:14px;
  }
  .weight-row label{
    font-size:12px;
    font-weight:700;
    color:var(--muted);
  }
  .weight-row input{
    width:74px;
    font-size:14px;
    font-weight:700;
    color:var(--text);
    background:var(--panel2);
    border:1px solid var(--border);
    border-radius:8px;
    padding:6px 8px;
  }
  .weight-row .unit{font-size:12px;color:var(--muted);}
  .weight-hint{font-size:11px;color:var(--muted);}

  /* routine (warm-up / stretch) steps */
  .steps{display:flex;flex-direction:column;gap:8px;margin-top:16px;}
  .step-row{
    display:flex;align-items:center;justify-content:space-between;gap:10px;
    padding:10px 12px;border:1px solid var(--border);border-radius:10px;
    background:var(--panel2);
  }
  .step-left{display:flex;align-items:center;gap:10px;}
  .step-check{
    width:22px;height:22px;border-radius:50%;border:2px solid var(--border);
    flex-shrink:0;cursor:pointer;transition:background .12s ease, border-color .12s ease;
  }
  .step-check.filled{background:var(--slate);border-color:var(--slate);}
  .step-text .step-name{font-size:13.5px;font-weight:600;}
  .step-text .step-detail{font-size:12px;color:var(--muted);}
  .step-timer{
    font-size:12px;font-weight:700;color:var(--slate);
    background:var(--panel);border:1px solid var(--border);
    padding:5px 10px;border-radius:999px;cursor:pointer;flex-shrink:0;
    transition:background .15s ease, color .15s ease, border-color .15s ease;
  }
  .step-timer.running{color:var(--bg);background:var(--slate);border-color:var(--slate);}
  .step-timer.done{color:var(--bg);background:var(--good);border-color:var(--good);}
</style>
</head>
<body>
<div class="wrap">

  <header class="top">
    <p class="kicker">Muscle Building — Hypertrophy</p>
    <h1>Weekly Training Chart</h1>
    <p class="sub">Tap a card to open it, check off reps or steps, and start the timer.</p>
  </header>

  <div id="calendarSection"></div>

  <div class="tabs">
    <div class="tab active" data-plan="free">Free Weights</div>
    <div class="tab" data-plan="machine">Machines</div>
  </div>

  <div id="days"></div>

  <div class="legend">
    <span class="sw"><span class="dot" style="background:var(--brass)"></span> reps done</span>
    <span class="sw"><span class="dot" style="background:var(--slate)"></span> warm-up / stretch step</span>
    <span class="sw"><span class="dot" style="background:var(--good)"></span> timer done</span>
  </div>

  <footer>
    Rest times: 45–60s for isolation moves, 75–90s for most compound lifts, 120s for heavy squats/deadlifts. The time on each day card is the lifting portion only (working sets + rest) — it doesn't include warm-up or cool-down. Warm up 5–8 minutes before lifting and stretch after, while muscles are warm. Progress resets if you reload the page.
  </footer>

</div>

<div class="backdrop" id="backdrop">
  <div class="modal" id="modal"></div>
</div>

<script>
const PLANS = {
  free: [
    { title:"Chest & Triceps", exercises:[
      {name:"Barbell bench press", sets:4, reps:8, rest:90},
      {name:"Incline dumbbell press", sets:3, reps:10, rest:75},
      {name:"Dumbbell flyes", sets:3, reps:12, rest:60},
      {name:"Close-grip bench or dips", sets:3, reps:10, rest:75},
      {name:"Overhead tricep extension", sets:3, reps:12, rest:60},
    ]},
    { title:"Back & Biceps", exercises:[
      {name:"Deadlift", sets:3, reps:6, rest:120},
      {name:"Bent-over barbell rows", sets:4, reps:9, rest:90},
      {name:"Pull-ups", sets:3, reps:8, rest:90, amrap:true},
      {name:"Dumbbell curls", sets:3, reps:12, rest:60},
      {name:"Hammer curls", sets:3, reps:12, rest:60},
    ]},
    { title:"Legs", exercises:[
      {name:"Back squat", sets:4, reps:8, rest:120},
      {name:"Romanian deadlift", sets:3, reps:10, rest:90},
      {name:"Walking lunges", sets:3, reps:10, rest:75},
      {name:"Leg curls / good mornings", sets:3, reps:12, rest:60},
      {name:"Calf raises", sets:4, reps:15, rest:45},
    ]},
    { title:"Shoulders & Arms", exercises:[
      {name:"Dumbbell shoulder press", sets:4, reps:10, rest:90},
      {name:"Lateral raises", sets:4, reps:14, rest:60},
      {name:"Rear delt flyes", sets:3, reps:15, rest:60},
      {name:"Barbell curls", sets:3, reps:10, rest:60},
      {name:"Tricep dips", sets:3, reps:12, rest:60},
    ]},
    { title:"Full Body Pump", exercises:[
      {name:"Front squat", sets:3, reps:10, rest:90},
      {name:"Incline bench press", sets:3, reps:10, rest:75},
      {name:"Bent-over rows", sets:3, reps:10, rest:75},
      {name:"Curl + tricep superset", sets:3, reps:15, rest:45},
    ]},
  ],
  machine: [
    { title:"Chest & Triceps", exercises:[
      {name:"Chest press machine", sets:4, reps:8, rest:90},
      {name:"Incline chest press machine", sets:3, reps:10, rest:75},
      {name:"Pec deck / chest fly", sets:3, reps:12, rest:60},
      {name:"Assisted dip machine", sets:3, reps:10, rest:75},
      {name:"Tricep pushdown (cable)", sets:3, reps:12, rest:60},
    ]},
    { title:"Back & Biceps", exercises:[
      {name:"Seated row machine (heavy)", sets:3, reps:6, rest:120},
      {name:"Lat pulldown", sets:4, reps:9, rest:90},
      {name:"Assisted pull-up machine", sets:3, reps:8, rest:90, amrap:true},
      {name:"Cable curl", sets:3, reps:12, rest:60},
      {name:"Cable hammer curl", sets:3, reps:12, rest:60},
    ]},
    { title:"Legs", exercises:[
      {name:"Leg press", sets:4, reps:8, rest:120},
      {name:"Leg curl machine", sets:3, reps:10, rest:90},
      {name:"Hack squat (narrow stance)", sets:3, reps:10, rest:75},
      {name:"Leg extension", sets:3, reps:12, rest:60},
      {name:"Seated calf raise machine", sets:4, reps:15, rest:45},
    ]},
    { title:"Shoulders & Arms", exercises:[
      {name:"Shoulder press machine", sets:4, reps:10, rest:90},
      {name:"Cable lateral raise", sets:4, reps:14, rest:60},
      {name:"Rear delt machine", sets:3, reps:15, rest:60},
      {name:"Cable curl", sets:3, reps:10, rest:60},
      {name:"Tricep pushdown", sets:3, reps:12, rest:60},
    ]},
    { title:"Full Body Pump", exercises:[
      {name:"Hack squat machine", sets:3, reps:10, rest:90},
      {name:"Smith machine bench press", sets:3, reps:10, rest:75},
      {name:"Cable row", sets:3, reps:10, rest:75},
      {name:"Curl + pushdown superset", sets:3, reps:15, rest:45},
    ]},
  ]
};

// Shared across both plans (same day order/muscle groups either way)
const WARMUP = {
  name: "Warm-Up",
  duration: "5–8 min, before lifting",
  steps: [
    {name:"Light cardio", detail:"jump rope, row, or brisk walk", seconds:180},
    {name:"Arm circles", detail:"10 each direction"},
    {name:"Leg swings", detail:"10 each leg, front-to-back and side-to-side"},
    {name:"Bodyweight squats", detail:"15 reps"},
    {name:"World's greatest stretch", detail:"5 reps each side"},
    {name:"Band pull-aparts", detail:"15 reps"},
    {name:"Ramp-up set", detail:"2 light sets of your first lift at ~50% weight"},
  ]
};

const STRETCHES = [
  { name:"Cool-Down Stretch", detail:"chest & triceps, hold 30s each", steps:[
    {name:"Doorway chest stretch", detail:"each side", seconds:30},
    {name:"Overhead tricep stretch", detail:"each side", seconds:30},
    {name:"Cross-body shoulder stretch", detail:"each side", seconds:30},
  ]},
  { name:"Cool-Down Stretch", detail:"back & biceps, hold 30–45s each", steps:[
    {name:"Child's pose", detail:"", seconds:45},
    {name:"Cat-cow", detail:"8 slow reps"},
    {name:"Biceps wall stretch", detail:"each side", seconds:30},
    {name:"Lat side-bend stretch", detail:"each side", seconds:30},
  ]},
  { name:"Cool-Down Stretch", detail:"legs, hold 30s each", steps:[
    {name:"Standing quad stretch", detail:"each side", seconds:30},
    {name:"Seated hamstring stretch", detail:"each side", seconds:30},
    {name:"Calf wall stretch", detail:"each side", seconds:30},
    {name:"Figure-4 glute stretch", detail:"each side", seconds:30},
  ]},
  { name:"Cool-Down Stretch", detail:"shoulders & arms, hold 20–30s each", steps:[
    {name:"Cross-body shoulder stretch", detail:"each side", seconds:30},
    {name:"Overhead tricep stretch", detail:"each side", seconds:30},
    {name:"Wrist flexor/extensor stretch", detail:"each side", seconds:20},
  ]},
  { name:"Cool-Down Stretch", detail:"full body, hold 30–45s each", steps:[
    {name:"Standing forward fold", detail:"", seconds:30},
    {name:"Standing quad stretch", detail:"each side", seconds:30},
    {name:"Doorway chest stretch", detail:"", seconds:30},
    {name:"Child's pose", detail:"", seconds:45},
  ]},
];

let currentPlan = "free";
let restTimerHandle = null;
let workoutLog = {};       // { "YYYY-MM-DD": "Day title" }
let weightLog = {};        // { exId: "135" }
let calMonth = new Date(); calMonth.setDate(1);

function todayKey(){
  const d = new Date();
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
}
function keyFor(y,m,day){
  return `${y}-${String(m+1).padStart(2,'0')}-${String(day).padStart(2,'0')}`;
}

async function loadLog(){
  try{
    const res = await window.storage.get('workout-log', false);
    workoutLog = res && res.value ? JSON.parse(res.value) : {};
  }catch(err){
    workoutLog = {};
  }
}
async function saveLog(){
  try{
    await window.storage.set('workout-log', JSON.stringify(workoutLog), false);
  }catch(err){
    console.error('Storage error', err);
  }
}

async function loadWeights(){
  try{
    const res = await window.storage.get('exercise-weights', false);
    weightLog = res && res.value ? JSON.parse(res.value) : {};
  }catch(err){
    weightLog = {};
  }
}
async function saveWeights(){
  try{
    await window.storage.set('exercise-weights', JSON.stringify(weightLog), false);
  }catch(err){
    console.error('Storage error', err);
  }
}

async function toggleMarkDone(dayTitle, btnEl){
  const key = todayKey();
  if (workoutLog[key] === dayTitle){
    delete workoutLog[key];
    btnEl.textContent = 'Mark done';
    btnEl.classList.remove('on');
  } else {
    workoutLog[key] = dayTitle;
    btnEl.textContent = '✓ Done today';
    btnEl.classList.add('on');
  }
  await saveLog();
  renderCalendar();
}

function renderCalendar(){
  const container = document.getElementById('calendarSection');
  const y = calMonth.getFullYear();
  const m = calMonth.getMonth();
  const monthLabel = calMonth.toLocaleDateString(undefined,{month:'long', year:'numeric'});
  const firstDow = new Date(y, m, 1).getDay();
  const daysInMonth = new Date(y, m+1, 0).getDate();
  const todayStr = todayKey();

  let cells = '';
  const dowLabels = ['S','M','T','W','T','F','S'];
  dowLabels.forEach(l => cells += `<div class="cal-dow">${l}</div>`);
  for (let i=0; i<firstDow; i++) cells += `<div class="cal-day empty"></div>`;
  for (let d=1; d<=daysInMonth; d++){
    const key = keyFor(y,m,d);
    const done = workoutLog[key];
    const isToday = key === todayStr;
    cells += `<div class="cal-day${done ? ' done' : ''}${isToday ? ' today' : ''}" title="${done ? done : ''}">${d}</div>`;
  }

  // streak: consecutive days up to today with a logged workout
  let streak = 0;
  let cursor = new Date();
  while (true){
    const k = `${cursor.getFullYear()}-${String(cursor.getMonth()+1).padStart(2,'0')}-${String(cursor.getDate()).padStart(2,'0')}`;
    if (workoutLog[k]) { streak++; cursor.setDate(cursor.getDate()-1); }
    else break;
  }
  const totalThisMonth = Object.keys(workoutLog).filter(k => k.startsWith(`${y}-${String(m+1).padStart(2,'0')}`)).length;

  container.innerHTML = `
    <div class="cal-card">
      <div class="cal-head">
        <span class="cal-title">Progress</span>
        <div class="cal-nav">
          <button id="calPrev">‹</button>
          <span class="cal-month-label">${monthLabel}</span>
          <button id="calNext">›</button>
        </div>
      </div>
      <div class="cal-grid">${cells}</div>
      <div class="cal-streak">${totalThisMonth} workout${totalThisMonth===1?'':'s'} logged this month${streak > 0 ? ` · ${streak}-day streak` : ''}</div>
    </div>
  `;
  document.getElementById('calPrev').addEventListener('click', () => {
    calMonth.setMonth(calMonth.getMonth()-1);
    renderCalendar();
  });
  document.getElementById('calNext').addEventListener('click', () => {
    calMonth.setMonth(calMonth.getMonth()+1);
    renderCalendar();
  });
}

// lift progress[exId] = array of arrays of bool
const progress = {};
// routine progress[routineId] = array of bool (one per step)
const routineProgress = {};

function exId(planKey, dayIdx, exIdx){ return `${planKey}-${dayIdx}-${exIdx}`; }
function routineId(planKey, dayIdx, kind){ return `${planKey}-${dayIdx}-${kind}`; }

function ensureProgress(id, sets, reps){
  if (!progress[id]) progress[id] = Array.from({length:sets}, () => Array(reps).fill(false));
}
function ensureRoutineProgress(id, stepCount){
  if (!routineProgress[id]) routineProgress[id] = Array(stepCount).fill(false);
}

function countDone(id){ return progress[id].reduce((s,set)=>s+set.filter(Boolean).length,0); }
function countTotal(id){ return progress[id].reduce((s,set)=>s+set.length,0); }
function countRoutineDone(id){ return routineProgress[id].filter(Boolean).length; }

// ~35s to perform a working set, plus its rest before the next one — lifts only
function estimateMinutes(day){
  const totalSeconds = day.exercises.reduce((sum, ex) => {
    return sum + ex.sets * (35 + ex.rest);
  }, 0);
  return Math.round(totalSeconds / 60);
}

function renderDays(){
  const container = document.getElementById('days');
  container.innerHTML = '';
  const days = PLANS[currentPlan];

  days.forEach((day, di) => {
    const dayEl = document.createElement('div');
    dayEl.className = 'day' + (di === 0 ? ' open' : '');

    const head = document.createElement('div');
    head.className = 'day-head';
    const dateKey = todayKey();
    const isDoneToday = workoutLog[dateKey] === day.title;
    head.innerHTML = `
      <div class="left">
        <span class="day-num">Day ${di+1}</span>
        <span class="day-title">${day.title}</span>
      </div>
      <div class="right">
        <span class="day-time">~${estimateMinutes(day)} min</span>
        <span class="mark-done-btn${isDoneToday ? ' on' : ''}" id="mark-${currentPlan}-${di}">${isDoneToday ? '✓ Done today' : 'Mark done'}</span>
        <span class="chev">▶</span>
      </div>
    `;
    head.addEventListener('click', () => dayEl.classList.toggle('open'));
    head.querySelector(`#mark-${currentPlan}-${di}`).addEventListener('click', (e) => {
      e.stopPropagation();
      toggleMarkDone(day.title, e.target);
    });

    const body = document.createElement('div');
    body.className = 'day-body';

    // --- Warm-up card ---
    const wId = routineId(currentPlan, di, 'warmup');
    ensureRoutineProgress(wId, WARMUP.steps.length);
    const warmCard = document.createElement('div');
    warmCard.className = 'ex-card';
    warmCard.innerHTML = `
      <div class="ex-info">
        <div class="ex-name"><span class="kind-icon">🔥</span>${WARMUP.name}</div>
        <div class="ex-scheme">${WARMUP.duration}</div>
      </div>
      <div class="ex-right">
        <span class="progress-chip alt" id="chip-${wId}">${countRoutineDone(wId)}/${WARMUP.steps.length}</span>
        <span class="open-arrow">›</span>
      </div>
    `;
    warmCard.addEventListener('click', () => openRoutineModal(currentPlan, di, 'warmup', WARMUP));
    body.appendChild(warmCard);

    const liftLabel = document.createElement('div');
    liftLabel.className = 'section-label';
    liftLabel.textContent = 'Lifts';
    body.appendChild(liftLabel);

    day.exercises.forEach((ex, ei) => {
      const id = exId(currentPlan, di, ei);
      ensureProgress(id, ex.sets, ex.reps);

      const card = document.createElement('div');
      card.className = 'ex-card';
      const w = weightLog[id];
      card.innerHTML = `
        <div class="ex-info">
          <div class="ex-name">${ex.name}${ex.amrap ? '<span class="amrap-tag">AMRAP</span>' : ''}</div>
          <div class="ex-scheme">${ex.sets} sets × ${ex.reps} reps · ${ex.rest}s rest</div>
        </div>
        <div class="ex-right">
          ${w ? `<span class="weight-badge">${w} lb</span>` : ''}
          <span class="progress-chip" id="chip-${id}">${countDone(id)}/${countTotal(id)}</span>
          <span class="open-arrow">›</span>
        </div>
      `;
      card.addEventListener('click', () => openLiftModal(currentPlan, di, ei));
      body.appendChild(card);
    });

    // --- Stretch card ---
    const stretchDef = STRETCHES[di];
    const sId = routineId(currentPlan, di, 'stretch');
    ensureRoutineProgress(sId, stretchDef.steps.length);
    const stretchLabel = document.createElement('div');
    stretchLabel.className = 'section-label';
    stretchLabel.textContent = 'Cool-Down';
    body.appendChild(stretchLabel);

    const stretchCard = document.createElement('div');
    stretchCard.className = 'ex-card';
    stretchCard.innerHTML = `
      <div class="ex-info">
        <div class="ex-name"><span class="kind-icon">🧘</span>${stretchDef.name}</div>
        <div class="ex-scheme">${stretchDef.detail}</div>
      </div>
      <div class="ex-right">
        <span class="progress-chip alt" id="chip-${sId}">${countRoutineDone(sId)}/${stretchDef.steps.length}</span>
        <span class="open-arrow">›</span>
      </div>
    `;
    stretchCard.addEventListener('click', () => openRoutineModal(currentPlan, di, 'stretch', stretchDef));
    body.appendChild(stretchCard);

    dayEl.appendChild(head);
    dayEl.appendChild(body);
    container.appendChild(dayEl);
  });
}

function openLiftModal(planKey, dayIdx, exIdx){
  const ex = PLANS[planKey][dayIdx].exercises[exIdx];
  const id = exId(planKey, dayIdx, exIdx);
  ensureProgress(id, ex.sets, ex.reps);

  const backdrop = document.getElementById('backdrop');
  const modal = document.getElementById('modal');

  modal.innerHTML = `
    <div class="modal-head">
      <div>
        <div class="modal-title">${ex.name}${ex.amrap ? '<span class="amrap-tag">AMRAP</span>' : ''}</div>
        <div class="modal-scheme">${ex.sets} sets × ${ex.reps} reps</div>
      </div>
      <div class="close-btn" id="closeBtn">✕</div>
    </div>
    <div class="weight-row">
      <label for="weightInput">Weight used</label>
      <input type="number" inputmode="decimal" id="weightInput" placeholder="0" value="${weightLog[id] ?? ''}">
      <span class="unit">lb</span>
    </div>
    <div class="rest-pill" id="restPill">⏱ ${ex.rest}s rest</div>
    <div class="sets" id="setsWrap"></div>
    <div class="modal-footnote">Tap a box each time you finish a rep. Tap the rest pill after a set to count down before the next one.</div>
  `;

  const setsWrap = modal.querySelector('#setsWrap');
  progress[id].forEach((setArr, si) => {
    const row = document.createElement('div');
    row.className = 'set-row';
    const label = document.createElement('div');
    label.className = 'set-label';
    label.textContent = `Set ${si+1}`;
    const boxes = document.createElement('div');
    boxes.className = 'boxes';
    setArr.forEach((done, ri) => {
      const box = document.createElement('div');
      box.className = 'rep-box' + (done ? ' filled' : '');
      box.addEventListener('click', () => {
        progress[id][si][ri] = !progress[id][si][ri];
        box.classList.toggle('filled');
        const chip = document.getElementById(`chip-${id}`);
        if (chip) chip.textContent = `${countDone(id)}/${countTotal(id)}`;
      });
      boxes.appendChild(box);
    });
    row.appendChild(label);
    row.appendChild(boxes);
    setsWrap.appendChild(row);
  });

  if (restTimerHandle) { clearInterval(restTimerHandle); restTimerHandle = null; }
  const pill = modal.querySelector('#restPill');
  pill.addEventListener('click', () => startTimer(ex.rest, pill, `⏱ ${ex.rest}s rest`));
  modal.querySelector('#closeBtn').addEventListener('click', closeModal);

  const weightInput = modal.querySelector('#weightInput');
  weightInput.addEventListener('change', async () => {
    const val = weightInput.value.trim();
    if (val === '') { delete weightLog[id]; } else { weightLog[id] = val; }
    await saveWeights();
    const chip = document.getElementById(`chip-${id}`);
    // refresh the card's weight badge without a full re-render
    if (chip){
      const rightEl = chip.parentElement;
      let badge = rightEl.querySelector('.weight-badge');
      if (val === ''){
        if (badge) badge.remove();
      } else if (badge){
        badge.textContent = `${val} lb`;
      } else {
        badge = document.createElement('span');
        badge.className = 'weight-badge';
        badge.textContent = `${val} lb`;
        rightEl.insertBefore(badge, chip);
      }
    }
  });

  backdrop.classList.add('show');
}

function openRoutineModal(planKey, dayIdx, kind, def){
  const id = routineId(planKey, dayIdx, kind);
  ensureRoutineProgress(id, def.steps.length);

  const backdrop = document.getElementById('backdrop');
  const modal = document.getElementById('modal');
  const icon = kind === 'warmup' ? '🔥' : '🧘';

  modal.innerHTML = `
    <div class="modal-head">
      <div>
        <div class="modal-title"><span class="kind-icon">${icon}</span>${def.name}</div>
        <div class="modal-scheme">${def.duration || def.detail}</div>
      </div>
      <div class="close-btn" id="closeBtn">✕</div>
    </div>
    <div class="steps" id="stepsWrap"></div>
    <div class="modal-footnote">Tap the circle to mark a step done. Tap the timer on timed steps to count down.</div>
  `;

  const stepsWrap = modal.querySelector('#stepsWrap');
  def.steps.forEach((step, si) => {
    const done = routineProgress[id][si];
    const row = document.createElement('div');
    row.className = 'step-row';
    row.innerHTML = `
      <div class="step-left">
        <div class="step-check${done ? ' filled' : ''}" id="check-${id}-${si}"></div>
        <div class="step-text">
          <div class="step-name">${step.name}</div>
          ${step.detail ? `<div class="step-detail">${step.detail}</div>` : ''}
        </div>
      </div>
      ${step.seconds ? `<div class="step-timer" id="timer-${id}-${si}">⏱ ${step.seconds}s</div>` : ''}
    `;
    stepsWrap.appendChild(row);

    const check = row.querySelector(`#check-${id}-${si}`);
    check.addEventListener('click', () => {
      routineProgress[id][si] = !routineProgress[id][si];
      check.classList.toggle('filled');
      const chip = document.getElementById(`chip-${id}`);
      if (chip) chip.textContent = `${countRoutineDone(id)}/${def.steps.length}`;
    });

    if (step.seconds){
      const timerEl = row.querySelector(`#timer-${id}-${si}`);
      timerEl.addEventListener('click', () => startTimer(step.seconds, timerEl, `⏱ ${step.seconds}s`));
    }
  });

  modal.querySelector('#closeBtn').addEventListener('click', closeModal);
  backdrop.classList.add('show');
}

function closeModal(){
  document.getElementById('backdrop').classList.remove('show');
  if (restTimerHandle) { clearInterval(restTimerHandle); restTimerHandle = null; }
}

document.getElementById('backdrop').addEventListener('click', (e) => {
  if (e.target.id === 'backdrop') closeModal();
});

function startTimer(seconds, pill, resetLabel){
  if (restTimerHandle) { clearInterval(restTimerHandle); restTimerHandle = null; }
  let remaining = seconds;
  pill.classList.remove('done');
  pill.classList.add('running');
  pill.textContent = `⏱ ${remaining}s`;

  restTimerHandle = setInterval(() => {
    remaining -= 1;
    if (remaining <= 0){
      clearInterval(restTimerHandle);
      restTimerHandle = null;
      pill.classList.remove('running');
      pill.classList.add('done');
      pill.textContent = `✓ Done`;
      setTimeout(() => {
        pill.classList.remove('done');
        pill.textContent = resetLabel;
      }, 2000);
    } else {
      pill.textContent = `⏱ ${remaining}s`;
    }
  }, 1000);
}

document.querySelectorAll('.tab').forEach(tab => {
  tab.addEventListener('click', () => {
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    tab.classList.add('active');
    currentPlan = tab.dataset.plan;
    closeModal();
    renderDays();
  });
});

(async function init(){
  await loadLog();
  await loadWeights();
  renderCalendar();
  renderDays();
})();
</script>
</body>
</html>

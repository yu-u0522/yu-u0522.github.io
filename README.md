# yu-u0522.github.io
<!DOCTYPE html>

<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Academic Atelier — 課題カウントダウン</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400;1,600&family=IM+Fell+English:ital@0;1&family=Noto+Serif+JP:wght@400;500;700&display=swap" rel="stylesheet">
<style>
:root {
  --parchment:    #e8dcc8;
  --parchment-dk: #d4c4a8;
  --ink:          #1e130a;
  --ink-mid:      #3a2410;
  --ink-soft:     #5a3d28;
  --sepia:        #7a5230;
  --sepia-lt:     #a07448;
  --rust:         #8b3a1e;
  --rust-lt:      #b85c38;
  --sage:         #4a6040;
  --aged-red:     #7a2e1a;
  --gold:         #8a6820;
  --gold-lt:      #c09840;
}

- { margin:0; padding:0; box-sizing:border-box; }

body {
background: var(–parchment);
color: var(–ink);
font-family: ‘Noto Serif JP’, ‘IM Fell English’, serif;
min-height: 100vh;
position: relative;
overflow-x: hidden;
}

/* ── Aged paper texture overlay ── */
body::before {
content: ‘’;
position: fixed; inset: 0;
background-image:
url(“data:image/svg+xml,%3Csvg xmlns=‘http://www.w3.org/2000/svg’ width=‘400’ height=‘400’%3E%3Cfilter id=‘n’%3E%3CfeTurbulence type=‘fractalNoise’ baseFrequency=‘0.65’ numOctaves=‘3’ stitchTiles=‘stitch’/%3E%3CfeColorMatrix type=‘saturate’ values=‘0’/%3E%3C/filter%3E%3Crect width=‘400’ height=‘400’ filter=‘url(%23n)’ opacity=‘0.07’/%3E%3C/svg%3E”),
repeating-linear-gradient(
92deg,
transparent,
transparent 180px,
rgba(90,60,30,0.025) 180px,
rgba(90,60,30,0.025) 181px
),
repeating-linear-gradient(
2deg,
transparent,
transparent 120px,
rgba(90,60,30,0.02) 120px,
rgba(90,60,30,0.02) 121px
);
pointer-events: none;
z-index: 0;
}

/* Vignette */
body::after {
content: ‘’;
position: fixed; inset: 0;
background: radial-gradient(ellipse at center, transparent 60%, rgba(30,19,10,0.18) 100%);
pointer-events: none;
z-index: 0;
}

.page {
position: relative;
z-index: 1;
max-width: 780px;
margin: 0 auto;
padding: 36px 28px 60px;
}

/* ── Decorative corner marks ── */
.corner {
position: fixed;
width: 60px; height: 60px;
opacity: 0.35;
pointer-events: none;
z-index: 2;
}
.corner svg { width: 100%; height: 100%; }
.corner-tl { top: 12px; left: 12px; }
.corner-tr { top: 12px; right: 12px; transform: scaleX(-1); }
.corner-bl { bottom: 12px; left: 12px; transform: scaleY(-1); }
.corner-br { bottom: 12px; right: 12px; transform: scale(-1); }

/* ── Header ── */
.header {
text-align: center;
margin-bottom: 28px;
padding-bottom: 20px;
position: relative;
}

.header-top-rule {
display: flex;
align-items: center;
gap: 10px;
margin-bottom: 18px;
color: var(–sepia);
font-size: 11px;
letter-spacing: 5px;
}
.header-top-rule::before,
.header-top-rule::after {
content: ‘’;
flex: 1;
height: 1px;
background: linear-gradient(90deg, transparent, var(–sepia-lt), transparent);
}

.header h1 {
font-family: ‘IM Fell English’, ‘Cormorant Garamond’, serif;
font-size: clamp(26px, 4.5vw, 42px);
font-weight: 400;
color: var(–ink);
letter-spacing: 1px;
line-height: 1.15;
margin-bottom: 6px;
text-shadow: 1px 1px 0 rgba(255,240,200,0.5);
}

.header h1 em {
font-style: italic;
color: var(–sepia);
}

.header-date {
font-family: ‘Cormorant Garamond’, serif;
font-size: 12px;
letter-spacing: 4px;
color: var(–sepia-lt);
margin-top: 10px;
}

.ornament-rule {
display: flex;
align-items: center;
gap: 12px;
margin-top: 16px;
color: var(–gold);
font-size: 13px;
letter-spacing: 6px;
}
.ornament-rule::before,
.ornament-rule::after {
content: ‘’;
flex: 1;
height: 1.5px;
background: linear-gradient(90deg, transparent, var(–gold-lt), transparent);
}

/* ── Section titles ── */
.section-title {
font-family: ‘IM Fell English’, serif;
font-size: 14px;
letter-spacing: 4px;
text-transform: uppercase;
color: var(–sepia);
display: flex;
align-items: center;
gap: 10px;
margin-bottom: 16px;
}
.section-title::after {
content: ‘’;
flex: 1;
height: 1px;
background: linear-gradient(90deg, var(–sepia-lt), transparent);
opacity: 0.5;
}

/* ── Countdown cards ── */
.countdown-list {
display: flex;
flex-direction: column;
gap: 12px;
margin-bottom: 32px;
}

.task-card {
background: linear-gradient(135deg, rgba(255,248,230,0.7) 0%, rgba(232,220,200,0.5) 100%);
border: 1px solid rgba(122,82,48,0.3);
border-radius: 4px;
padding: 14px 18px;
position: relative;
box-shadow:
inset 0 1px 0 rgba(255,248,220,0.7),
0 2px 8px rgba(30,19,10,0.08),
0 1px 2px rgba(30,19,10,0.06);
transition: box-shadow 0.2s;
animation: fadeIn 0.4s ease both;
}

@keyframes fadeIn {
from { opacity:0; transform: translateY(8px); }
to   { opacity:1; transform: translateY(0); }
}

.task-card:hover {
box-shadow:
inset 0 1px 0 rgba(255,248,220,0.7),
0 4px 16px rgba(30,19,10,0.12),
0 1px 3px rgba(30,19,10,0.08);
}

/* urgency left border */
.task-card.urgent   { border-left: 4px solid var(–aged-red); }
.task-card.soon     { border-left: 4px solid var(–rust-lt); }
.task-card.normal   { border-left: 4px solid var(–sepia-lt); }
.task-card.done     { border-left: 4px solid var(–sage); opacity: 0.6; }

.task-card.done .task-name,
.task-card.done .task-subject { text-decoration: line-through; }

.task-top {
display: flex;
align-items: flex-start;
gap: 12px;
}

.task-meta {
flex: 1;
min-width: 0;
}

.task-name {
font-family: ‘IM Fell English’, serif;
font-size: 16px;
color: var(–ink);
line-height: 1.3;
margin-bottom: 3px;
}

.task-subject {
font-size: 11px;
letter-spacing: 2px;
color: var(–sepia-lt);
text-transform: uppercase;
}

.countdown-badge {
text-align: right;
flex-shrink: 0;
}

.countdown-num {
font-family: ‘Cormorant Garamond’, serif;
font-size: 32px;
font-weight: 600;
line-height: 1;
color: var(–ink);
}
.task-card.urgent .countdown-num { color: var(–aged-red); }
.task-card.soon   .countdown-num { color: var(–rust-lt); }
.task-card.done   .countdown-num { color: var(–sage); }

.countdown-unit {
font-size: 9px;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–sepia);
display: block;
margin-top: 1px;
}

.task-deadline-text {
font-size: 11px;
color: var(–sepia);
margin-top: 6px;
font-style: italic;
}

/* Task actions */
.task-actions {
position: absolute;
top: 10px; right: 12px;
display: none;
gap: 6px;
}

.task-card:hover .task-actions { display: flex; }

.btn-icon {
background: none;
border: 1px solid rgba(122,82,48,0.3);
border-radius: 3px;
width: 26px; height: 26px;
cursor: pointer;
font-size: 13px;
color: var(–sepia);
display: flex; align-items: center; justify-content: center;
transition: all 0.15s;
}
.btn-icon:hover { background: rgba(122,82,48,0.12); }

/* ── Add task form ── */
.add-form {
background: rgba(255,248,230,0.5);
border: 1px dashed rgba(122,82,48,0.35);
border-radius: 4px;
padding: 18px 20px;
margin-bottom: 32px;
}

.form-row {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 10px;
margin-bottom: 10px;
}

.form-group { display: flex; flex-direction: column; gap: 4px; }
.form-group.full { grid-column: 1 / -1; }

.form-label {
font-size: 9px;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–sepia);
}

.form-input {
background: rgba(255,248,230,0.8);
border: 1px solid rgba(122,82,48,0.3);
border-radius: 3px;
padding: 7px 10px;
font-family: ‘Noto Serif JP’, serif;
font-size: 13px;
color: var(–ink);
outline: none;
transition: border-color 0.2s;
}
.form-input:focus { border-color: var(–sepia-lt); background: rgba(255,252,240,0.95); }
.form-input::placeholder { color: var(–sepia-lt); opacity: 0.6; }

.btn-add {
background: var(–ink-mid);
color: var(–parchment);
border: none;
border-radius: 3px;
padding: 9px 22px;
font-family: ‘Cormorant Garamond’, serif;
font-size: 14px;
letter-spacing: 2px;
cursor: pointer;
transition: all 0.2s;
display: block;
margin-left: auto;
}
.btn-add:hover { background: var(–sepia); }

/* ── Empty state ── */
.empty-state {
text-align: center;
padding: 28px;
color: var(–sepia-lt);
font-style: italic;
font-size: 14px;
}

/* ── Footer ── */
.footer {
text-align: center;
margin-top: 36px;
padding-top: 20px;
border-top: 1px solid rgba(122,82,48,0.2);
font-family: ‘Cormorant Garamond’, serif;
font-size: 11px;
font-style: italic;
color: var(–sepia-lt);
letter-spacing: 2px;
}

/* ── Modal (edit) ── */
.modal-overlay {
display: none;
position: fixed; inset: 0;
background: rgba(20,12,5,0.55);
z-index: 100;
align-items: center;
justify-content: center;
}
.modal-overlay.open { display: flex; }

.modal {
background: var(–parchment);
border: 1px solid rgba(122,82,48,0.4);
border-radius: 6px;
padding: 28px;
width: 90%;
max-width: 420px;
box-shadow: 0 20px 60px rgba(20,12,5,0.35);
}

.modal-title {
font-family: ‘IM Fell English’, serif;
font-size: 20px;
color: var(–ink);
margin-bottom: 20px;
}

.modal-actions {
display: flex;
gap: 10px;
justify-content: flex-end;
margin-top: 16px;
}

.btn-cancel {
background: none;
border: 1px solid rgba(122,82,48,0.3);
color: var(–sepia);
border-radius: 3px;
padding: 8px 18px;
font-family: ‘Cormorant Garamond’, serif;
font-size: 14px;
cursor: pointer;
}

/* ── Responsive ── */
@media (max-width: 500px) {
.form-row { grid-template-columns: 1fr; }
.page { padding: 24px 16px 48px; }
}
</style>

</head>
<body>

<!-- Decorative corners -->

<div class="corner corner-tl">
  <svg viewBox="0 0 60 60" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path d="M4 4 L4 28 M4 4 L28 4" stroke="#7a5230" stroke-width="1.5"/>
    <path d="M4 4 L14 14" stroke="#7a5230" stroke-width="0.8" opacity="0.5"/>
    <circle cx="4" cy="4" r="2.5" fill="#7a5230"/>
    <path d="M16 4 Q20 8 16 12" stroke="#7a5230" stroke-width="0.8" fill="none"/>
    <path d="M4 16 Q8 20 12 16" stroke="#7a5230" stroke-width="0.8" fill="none"/>
  </svg>
</div>
<div class="corner corner-tr"></div>
<div class="corner corner-bl"></div>
<div class="corner corner-br"></div>

<div class="page">

  <!-- Header -->

  <header class="header">
    <div class="header-top-rule">ACADEMIA</div>
    <h1>The Scholar's <em>Atelier</em></h1>
    <div class="header-date" id="todayDate"></div>
    <div class="ornament-rule">✦ ✦ ✦</div>
  </header>

  <!-- Countdown section -->

  <div class="section-title">📜 &nbsp; Assignments &amp; Deadlines</div>

  <div class="countdown-list" id="taskList"></div>

  <!-- Add task -->

  <div class="add-form">
    <div class="section-title" style="font-size:11px; margin-bottom:14px;">＋ &nbsp; New Assignment</div>
    <div class="form-row">
      <div class="form-group full">
        <label class="form-label">課題名</label>
        <input class="form-input" id="inp-name" type="text" placeholder="e.g. マーケティング最終レポート">
      </div>
      <div class="form-group">
        <label class="form-label">教科</label>
        <input class="form-input" id="inp-subject" type="text" placeholder="e.g. 経営学">
      </div>
      <div class="form-group">
        <label class="form-label">締め切り日</label>
        <input class="form-input" id="inp-date" type="date">
      </div>
    </div>
    <button class="btn-add" onclick="addTask()">✦ &nbsp; 課題を追加する</button>
  </div>

  <footer class="footer">
    — &nbsp; Knowledge is the most precious jewel a scholar can wear &nbsp; —
  </footer>
</div>

<!-- Edit Modal -->

<div class="modal-overlay" id="editModal">
  <div class="modal">
    <div class="modal-title">課題を編集する</div>
    <div class="form-group" style="margin-bottom:10px;">
      <label class="form-label">課題名</label>
      <input class="form-input" id="edit-name" type="text">
    </div>
    <div class="form-row">
      <div class="form-group">
        <label class="form-label">教科</label>
        <input class="form-input" id="edit-subject" type="text">
      </div>
      <div class="form-group">
        <label class="form-label">締め切り日</label>
        <input class="form-input" id="edit-date" type="date">
      </div>
    </div>
    <div class="modal-actions">
      <button class="btn-cancel" onclick="closeModal()">キャンセル</button>
      <button class="btn-add" onclick="saveEdit()">保存する</button>
    </div>
  </div>
</div>

<script>
// ── Data ──────────────────────────────────────────────
const STORAGE_KEY = 'academic-atelier-tasks-v1';

let tasks = [];
let editingId = null;

function loadTasks() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (raw) tasks = JSON.parse(raw);
  } catch(e) { tasks = []; }

  // seed sample data if empty
  if (tasks.length === 0) {
    const today = new Date();
    const d = (offset) => {
      const dt = new Date(today);
      dt.setDate(dt.getDate() + offset);
      return dt.toISOString().split('T')[0];
    };
    tasks = [
      { id: uid(), name: '経営学 最終レポート', subject: '経営学', deadline: d(3),  done: false },
      { id: uid(), name: 'マーケティング課題', subject: 'マーケ', deadline: d(7),  done: false },
      { id: uid(), name: '統計学 小テスト',    subject: '統計学', deadline: d(14), done: false },
    ];
    saveTasks();
  }
}

function saveTasks() {
  try { localStorage.setItem(STORAGE_KEY, JSON.stringify(tasks)); } catch(e){}
}

function uid() { return Date.now().toString(36) + Math.random().toString(36).slice(2); }

// ── Countdown logic ───────────────────────────────────
function daysUntil(dateStr) {
  const today = new Date();
  today.setHours(0,0,0,0);
  const dl = new Date(dateStr);
  dl.setHours(0,0,0,0);
  return Math.round((dl - today) / 86400000);
}

function urgencyClass(days, done) {
  if (done) return 'done';
  if (days < 0)  return 'urgent';
  if (days <= 3) return 'urgent';
  if (days <= 7) return 'soon';
  return 'normal';
}

function formatDeadline(dateStr) {
  const dt = new Date(dateStr + 'T00:00:00');
  return dt.toLocaleDateString('ja-JP', { year:'numeric', month:'long', day:'numeric', weekday:'short' });
}

function countdownLabel(days, done) {
  if (done) return '✓';
  if (days < 0)  return Math.abs(days);
  if (days === 0) return '今日';
  return days;
}

function countdownUnit(days, done) {
  if (done) return 'SUBMITTED';
  if (days < 0)  return 'DAYS OVERDUE';
  if (days === 0) return 'DUE TODAY';
  return 'DAYS LEFT';
}

// ── Render ────────────────────────────────────────────
function render() {
  const list = document.getElementById('taskList');

  // Sort: overdue first, then by deadline, done at bottom
  const sorted = [...tasks].sort((a, b) => {
    if (a.done !== b.done) return a.done ? 1 : -1;
    return new Date(a.deadline) - new Date(b.deadline);
  });

  if (sorted.length === 0) {
    list.innerHTML = '<div class="empty-state">— 現在登録されている課題はありません —</div>';
    return;
  }

  list.innerHTML = sorted.map((t, i) => {
    const days  = daysUntil(t.deadline);
    const cls   = urgencyClass(days, t.done);
    const num   = countdownLabel(days, t.done);
    const unit  = countdownUnit(days, t.done);
    const delay = i * 0.07;

    return `
    <div class="task-card ${cls}" style="animation-delay:${delay}s">
      <div class="task-top">
        <div class="task-meta">
          <div class="task-name">${escHtml(t.name)}</div>
          <div class="task-subject">${escHtml(t.subject)}</div>
          <div class="task-deadline-text">⏳ &nbsp;${formatDeadline(t.deadline)}</div>
        </div>
        <div class="countdown-badge">
          <span class="countdown-num">${num}</span>
          <span class="countdown-unit">${unit}</span>
        </div>
      </div>
      <div class="task-actions">
        <button class="btn-icon" title="${t.done ? '未提出に戻す' : '提出済にする'}" onclick="toggleDone('${t.id}')">${t.done ? '↩' : '✓'}</button>
        <button class="btn-icon" title="編集" onclick="openEdit('${t.id}')">✎</button>
        <button class="btn-icon" title="削除" onclick="deleteTask('${t.id}')">✕</button>
      </div>
    </div>`;
  }).join('');
}

function escHtml(s) {
  return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

// ── Actions ───────────────────────────────────────────
function addTask() {
  const name    = document.getElementById('inp-name').value.trim();
  const subject = document.getElementById('inp-subject').value.trim();
  const deadline= document.getElementById('inp-date').value;
  if (!name || !deadline) { alert('課題名と締め切り日を入力してください。'); return; }
  tasks.push({ id: uid(), name, subject: subject || '—', deadline, done: false });
  saveTasks();
  render();
  document.getElementById('inp-name').value    = '';
  document.getElementById('inp-subject').value = '';
  document.getElementById('inp-date').value    = '';
}

function deleteTask(id) {
  tasks = tasks.filter(t => t.id !== id);
  saveTasks(); render();
}

function toggleDone(id) {
  const t = tasks.find(t => t.id === id);
  if (t) { t.done = !t.done; saveTasks(); render(); }
}

function openEdit(id) {
  const t = tasks.find(t => t.id === id);
  if (!t) return;
  editingId = id;
  document.getElementById('edit-name').value    = t.name;
  document.getElementById('edit-subject').value = t.subject;
  document.getElementById('edit-date').value    = t.deadline;
  document.getElementById('editModal').classList.add('open');
}

function closeModal() {
  document.getElementById('editModal').classList.remove('open');
  editingId = null;
}

function saveEdit() {
  const t = tasks.find(t => t.id === editingId);
  if (!t) return;
  t.name    = document.getElementById('edit-name').value.trim() || t.name;
  t.subject = document.getElementById('edit-subject').value.trim() || t.subject;
  t.deadline= document.getElementById('edit-date').value || t.deadline;
  saveTasks(); render(); closeModal();
}

document.getElementById('editModal').addEventListener('click', (e) => {
  if (e.target === e.currentTarget) closeModal();
});

// Enter key on add form
['inp-name','inp-subject','inp-date'].forEach(id => {
  document.getElementById(id).addEventListener('keydown', e => {
    if (e.key === 'Enter') addTask();
  });
});

// ── Date display ──────────────────────────────────────
function updateDate() {
  const now = new Date();
  const formatted = now.toLocaleDateString('ja-JP', {
    year: 'numeric', month: 'long', day: 'numeric', weekday: 'long'
  });
  document.getElementById('todayDate').textContent = formatted;
}

// ── Init ──────────────────────────────────────────────
loadTasks();
render();
updateDate();

// Refresh countdown every minute
setInterval(() => { render(); updateDate(); }, 60000);
</script>

</body>
</html>

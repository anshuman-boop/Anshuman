[Smart-Washroom-QR-System (7).html](https://github.com/user-attachments/files/28191278/Smart-Washroom-QR-System.7.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IRIS Smart Washroom - Complaint Management</title>
<style>
* { box-sizing:border-box; }
:root {
  --primary:#2563eb;
  --primary-dark:#1d4ed8;
  --bg:#f8fafc;
  --text:#0f172a;
  --muted:#64748b;
  --border:#e2e8f0;
  --success:#16a34a;
  --warn:#ea580c;
  --danger:#dc2626;
}
html,body { height:100%; }
body {
  margin:0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Inter, Helvetica, Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
  -webkit-font-smoothing: antialiased;
}
.app { min-height:100vh; }
.header {
  max-width:1200px; margin:0 auto; padding:14px 16px;
  display:flex; align-items:center; justify-content:space-between; gap:12px;
  position:sticky; top:0; background:rgba(248,250,252,.85); backdrop-filter:blur(8px); z-index:10;
  border-bottom:1px solid #eef2f7;
}
.brand { display:flex; align-items:center; gap:10px; }
.logo {
  width:40px; height:40px; background:var(--primary); border-radius:12px;
  display:grid; place-items:center; font-size:22px; color:white; box-shadow:0 4px 12px rgba(37,99,235,.25);
}
.brand h1 { font-size:16px; margin:0; font-weight:800; letter-spacing:.2px; }
.brand p { margin:0; font-size:12px; color:var(--muted); margin-top:-2px; }
.mode-toggle { display:flex; background:#e2e8f0; padding:3px; border-radius:12px; }
.toggle-btn {
  border:0; background:transparent; padding:8px 16px; border-radius:9px;
  font-weight:600; font-size:14px; color:#475569; cursor:pointer; transition:.18s;
}
.toggle-btn.active { background:white; color:var(--primary); box-shadow:0 1px 3px rgba(0,0,0,.08), 0 1px 2px rgba(0,0,0,.06); }

.employee-container { max-width:440px; margin:8px auto 0; padding:0 16px 40px; }
.card {
  background:white; border:1px solid #eef2f7; border-radius:18px; padding:16px;
  margin-bottom:14px; box-shadow:0 1px 2px rgba(16,24,40,.04);
}
.card h3 { margin:0; font-size:15px; font-weight:700; }
.card-header { display:flex; justify-content:space-between; align-items:center; margin-bottom:12px; }
label { display:block; font-size:13px; font-weight:600; color:#334155; margin-bottom:6px; }

select, input[type=text], textarea {
  width:100%; padding:11px 12px; border:1px solid var(--border); border-radius:10px;
  font-size:14px; background:#fbfdff; outline:none; transition:.15s; font-family:inherit;
}
select:focus, input:focus, textarea:focus {
  border-color:var(--primary); box-shadow:0 0 0 3px rgba(37,99,235,.12); background:white;
}
textarea { min-height:84px; resize:vertical; }

.location-pill {
  margin-top:10px; display:inline-flex; align-items:center; gap:6px;
  background:#eff6ff; color:#1e40af; padding:6px 11px; border-radius:999px;
  font-size:12.5px; font-weight:600; border:1px solid #dbeafe;
}

.category-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; }
.category-btn {
  border:1.5px solid #e5e7eb; background:white; border-radius:14px; padding:12px;
  text-align:left; cursor:pointer; transition:.15s; display:flex; flex-direction:column; gap:6px;
}
.category-btn:hover { border-color:#c7d2fe; background:#f8fafc; transform:translateY(-1px); }
.category-btn.selected { border-color:var(--primary); background:#eff6ff; box-shadow:inset 0 0 0 1.5px var(--primary); }
.cat-emoji { font-size:21px; line-height:1; }
.cat-name { font-size:13px; font-weight:650; color:#0f172a; }

.priority-badge {
  padding:5px 9px; border-radius:8px; font-size:11px; font-weight:800;
  text-transform:uppercase; letter-spacing:.3px; border:1px solid transparent;
}
.priority-high { background:#fee2e2; color:#b91c1c; border-color:#fecaca; }
.priority-medium { background:#ffedd5; color:#c2410c; border-color:#fed7aa; }
.priority-low { background:#dcfce7; color:#166534; border-color:#bbf7d0; }

.upload-btn {
  width:100%; border:1.5px dashed #cbd5e1; background:#f8fafc; padding:14px;
  border-radius:12px; font-weight:650; color:#334155; cursor:pointer; transition:.15s;
}
.upload-btn:hover { border-color:var(--primary); color:var(--primary); background:#eff6ff; }
.photo-grid { display:flex; gap:8px; margin-top:10px; flex-wrap:wrap; }
.photo-thumb { position:relative; width:78px; height:78px; border-radius:10px; overflow:hidden; border:1px solid #e2e8f0; }
.photo-thumb img { width:100%; height:100%; object-fit:cover; }
.photo-remove {
  position:absolute; top:4px; right:4px; width:20px; height:20px; border-radius:50%;
  background:rgba(0,0,0,.72); color:white; border:0; font-size:14px; line-height:1;
  cursor:pointer; display:grid; place-items:center;
}

.primary-btn {
  width:100%; background:var(--primary); color:white; border:0; padding:14px;
  border-radius:12px; font-weight:700; font-size:15px; cursor:pointer;
  box-shadow:0 6px 14px rgba(37,99,235,.25); transition:.15s;
}
.primary-btn:hover { background:var(--primary-dark); transform:translateY(-1px); }
.primary-btn:active { transform:translateY(0); }
.footnote { text-align:center; font-size:12px; color:#64748b; margin-top:10px; }

#adminView { max-width:1200px; margin:0 auto; padding:8px 16px 40px; display:none; }
.stats-grid { display:grid; grid-template-columns:repeat(2,1fr); gap:12px; margin-bottom:14px; }
@media(min-width:900px){ .stats-grid{ grid-template-columns:repeat(4,1fr); } }
.stat-card { background:white; border:1px solid #eef2f7; border-radius:16px; padding:14px; box-shadow:0 1px 2px rgba(16,24,40,.04); }
.stat-label { font-size:12px; color:#64748b; font-weight:600; margin-bottom:4px; text-transform:uppercase; letter-spacing:.4px; }
.stat-value { font-size:28px; font-weight:800; color:#0f172a; line-height:1; }
.stat-sub { font-size:11px; color:#94a3b8; margin-top:4px; }

.filters-card { display:flex; gap:8px; flex-wrap:wrap; align-items:center; }
.filters-card select { width:auto; flex:1 1 140px; min-width:0; padding:9px 10px; font-size:13px; background:white; }
.icon-btn { padding:9px 12px; border:1px solid #e2e8f0; background:white; border-radius:10px; cursor:pointer; font-weight:600; }

.table-card { padding:8px 12px 12px; }
.table-wrapper { overflow-x:auto; margin:0 -4px; padding:0 4px; }
table { width:100%; border-collapse:separate; border-spacing:0 8px; min-width:920px; }
thead th { font-size:11px; text-transform:uppercase; letter-spacing:.5px; color:#64748b; font-weight:700; padding:0 10px 4px; text-align:left; white-space:nowrap; }
tbody td { background:white; padding:12px 10px; font-size:13px; border-top:1px solid #eef2f7; border-bottom:1px solid #eef2f7; vertical-align:middle; }
tbody tr { transition:.12s; }
tbody tr:hover td { background:#fbfdff; }
tbody tr td:first-child { border-left:1px solid #eef2f7; border-top-left-radius:12px; border-bottom-left-radius:12px; }
tbody tr td:last-child { border-right:1px solid #eef2f7; border-top-right-radius:12px; border-bottom-right-radius:12px; }
.ticket-id { font-family:ui-monospace, SFMono-Regular, Menlo, monospace; font-weight:700; color:#1d4ed8; font-size:12px; }
.badge-sm { padding:4px 8px; border-radius:7px; font-size:11px; font-weight:700; display:inline-block; border:1px solid transparent; }
.badge-sm.priority-high { background:#fee2e2; color:#991b1b; border-color:#fecaca; }
.badge-sm.priority-medium { background:#ffedd5; color:#9a3412; border-color:#fed7aa; }
.badge-sm.priority-low { background:#dcfce7; color:#14532d; border-color:#bbf7d0; }
.age { font-weight:700; font-variant-numeric:tabular-nums; }
.age.breach { color:var(--danger); }
.age.ok { color:#059669; }
.status-select { padding:6px 8px; border-radius:8px; border:1px solid #e2e8f0; font-size:12px; font-weight:600; background:#f8fafc; }
.assign-input { width:118px; padding:6px 8px; border:1px solid #e2e8f0; border-radius:8px; font-size:12px; background:#fbfdff; }
.action-btns { display:flex; gap:6px; }
.action-btn { padding:6px 10px; border:1px solid #e2e8f0; background:white; border-radius:8px; font-size:12px; cursor:pointer; font-weight:600; transition:.12s; white-space:nowrap; }
.action-btn:hover { background:#f1f5f9; border-color:#cbd5e1; }

.analytics-grid { display:grid; grid-template-columns:1fr; gap:12px; margin-top:14px; }
@media(min-width:900px){ .analytics-grid{ grid-template-columns:1fr 1fr; } }
.analytics-grid h4 { margin:0 0 12px; font-size:14px; font-weight:700; }
.bar-row { display:grid; grid-template-columns:90px 1fr 30px; align-items:center; gap:10px; margin-bottom:10px; }
.bar-label { font-size:12px; color:#334155; font-weight:500; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
.bar-track { height:10px; background:#f1f5f9; border-radius:999px; overflow:hidden; }
.bar-fill { height:100%; background:linear-gradient(90deg,var(--primary),#60a5fa); border-radius:999px; transition:width .5s; }

.modal { position:fixed; inset:0; background:rgba(15,23,42,.55); backdrop-filter:blur(4px); display:none; align-items:center; justify-content:center; padding:20px; z-index:50; }
.modal.show { display:flex; animation:fadeIn .18s ease; }
@keyframes fadeIn { from{opacity:0} to{opacity:1} }
.modal-card { background:white; border-radius:20px; max-width:440px; width:100%; box-shadow:0 20px 50px rgba(0,0,0,.22); max-height:90vh; overflow:auto; animation:pop .18s ease; }
@keyframes pop { from{transform:scale(.96); opacity:0} to{transform:scale(1); opacity:1} }
.modal-head { padding:18px 18px 0; display:flex; justify-content:space-between; align-items:start; }
.modal-body { padding:18px; }
.success-icon { width:60px; height:60px; background:#dcfce7; color:#16a34a; border-radius:50%; display:grid; place-items:center; font-size:30px; margin:0 auto 12px; box-shadow:inset 0 0 0 3px #bbf7d0; }
.close-btn { border:0; background:#f1f5f9; width:32px; height:32px; border-radius:9px; cursor:pointer; font-size:20px; line-height:1; color:#475569; }
.close-btn:hover { background:#e2e8f0; }

.timeline { border-left:2px solid #e2e8f0; margin-left:8px; padding-left:16px; }
.timeline-item { position:relative; padding-bottom:14px; }
.timeline-item:before { content:''; position:absolute; left:-22px; top:3px; width:10px; height:10px; background:white; border:2px solid var(--primary); border-radius:50%; }
.timeline-time { font-size:11px; color:#64748b; }
.timeline-text { font-size:13px; font-weight:500; color:#0f172a; }
.hidden { display:none !important; }
</style>
</head>
<body>
<div class="app">
  <header class="header">
    <div class="brand">
      <div class="logo">🚻</div>
      <div>
        <h1>IRIS Facilities</h1>
        <p>Smart Washroom</p>
      </div>
    </div>
    <div class="mode-toggle">
      <button id="modeEmployee" class="toggle-btn active">Employee</button>
      <button id="modeAdmin" class="toggle-btn">Admin</button>
    </div>
  </header>

  <!-- EMPLOYEE VIEW -->
  <div id="employeeView">
    <div class="employee-container">
      <div class="card">
        <label>Location (Scan QR)</label>
        <select id="locationSelect"></select>
        <div id="locationPill" class="location-pill">📍 Select location</div>
      </div>

      <div class="card">
        <div class="card-header">
          <h3>What's the issue?</h3>
          <span id="priorityBadge" class="priority-badge priority-low" style="display:none">Low</span>
        </div>
        <div class="category-grid" id="categoryGrid"></div>
      </div>

      <div class="card">
        <label>Add photo (optional, max 3)</label>
        <input type="file" id="photoInput" accept="image/*" multiple hidden accept="image/*">
        <button type="button" id="photoBtn" class="upload-btn">📷 Take / Upload Photo</button>
        <div id="photoPreview" class="photo-grid"></div>
      </div>

      <div class="card">
        <label>Comments</label>
        <textarea id="comments" placeholder="Describe issue details… e.g., 2nd cubicle, near mirror"></textarea>
        <label style="margin-top:12px">Employee ID</label>
        <input type="text" id="employeeId" value="EMP1024">
      </div>

      <button id="submitTicket" class="primary-btn">Raise Ticket →</button>
      <p class="footnote">Avg response: High 30m • Medium 1h • Low 2h</p>
    </div>
  </div>

  <!-- ADMIN VIEW -->
  <div id="adminView">
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-label">Open</div>
        <div class="stat-value" id="statOpen">0</div>
        <div class="stat-sub">Needs assignment</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">In Progress</div>
        <div class="stat-value" id="statInProg">0</div>
        <div class="stat-sub">Active work</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">Avg Resolution</div>
        <div class="stat-value" id="statAvg">—</div>
        <div class="stat-sub">Last 20 tickets</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">SLA Breach</div>
        <div class="stat-value" id="statBreach" style="color:var(--danger)">0</div>
        <div class="stat-sub">Overdue now</div>
      </div>
    </div>

    <div class="card filters-card">
      <select id="filterWing">
        <option value="All">All Wings</option>
        <option value="A">Wing A</option>
        <option value="B">Wing B</option>
        <option value="C">Wing C</option>
      </select>
      <select id="filterStatus">
        <option value="All">All Status</option>
        <option>Open</option>
        <option>Assigned</option>
        <option>In Progress</option>
        <option>Resolved</option>
        <option>Closed</option>
      </select>
      <select id="filterPriority">
        <option value="All">All Priority</option>
        <option>High</option>
        <option>Medium</option>
        <option>Low</option>
      </select>
      <button id="refreshBtn" class="icon-btn" title="Refresh">↻ Refresh</button>
    </div>

    <div class="card table-card">
      <div class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>Location</th>
              <th>Category</th>
              <th>Priority</th>
              <th>Age</th>
              <th>Status</th>
              <th>Assign To</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody id="ticketTable"></tbody>
        </table>
      </div>
    </div>

    <div class="analytics-grid">
      <div class="card">
        <h4>Complaints by Wing</h4>
        <div id="chartWing"></div>
      </div>
      <div class="card">
        <h4>Complaints by Category</h4>
        <div id="chartCategory"></div>
      </div>
    </div>
  </div>
</div>

<!-- SUCCESS MODAL -->
<div id="successModal" class="modal">
  <div class="modal-card">
    <div class="modal-body" style="text-align:center;padding:28px 20px">
      <div class="success-icon">✓</div>
      <h2 style="margin:0 0 6px;font-size:22px;font-weight:800">Ticket Raised</h2>
      <p style="margin:0 0 18px;color:#64748b;font-size:14px">Housekeeping team has been notified instantly</p>
      
      <div style="background:#f8fafc;border:1px solid #e2e8f0;border-radius:14px;padding:14px;text-align:left;font-size:13.5px;margin-bottom:16px">
        <div style="display:flex;justify-content:space-between;margin-bottom:8px"><span style="color:#64748b">Ticket ID</span><strong id="successId" style="font-family:ui-monospace;color:#1d4ed8"></strong></div>
        <div style="display:flex;justify-content:space-between;margin-bottom:8px"><span style="color:#64748b">Location</span><span id="successLoc" style="font-weight:600"></span></div>
        <div style="display:flex;justify-content:space-between;margin-bottom:8px"><span style="color:#64748b">Issue</span><span id="successCat" style="font-weight:600"></span></div>
        <div style="display:flex;justify-content:space-between"><span style="color:#64748b">ETA</span><strong id="successEta" style="color:#059669"></strong></div>
      </div>
      <div style="display:flex;gap:8px;margin-bottom:10px">
        <button class="action-btn" style="flex:1;padding:10px" onclick="simulateWA()">💬 WhatsApp</button>
        <button class="action-btn" style="flex:1;padding:10px" onclick="simulateEmail()">✉️ Email</button>
      </div>
      <button onclick="closeSuccess()" class="primary-btn" style="margin-top:4px">Done</button>
      <p style="font-size:11px;color:#94a3b8;margin:10px 0 0">You will receive updates on this ticket</p>
    </div>
  </div>
</div>

<!-- DETAIL MODAL -->
<div id="detailModal" class="modal" onclick="if(event.target.id==='detailModal')closeDetail()">
  <div class="modal-card">
    <div class="modal-head">
      <h3 style="margin:0;font-size:17px;font-weight:800">Ticket Details</h3>
      <button class="close-btn" onclick="closeDetail()">×</button>
    </div>
    <div class="modal-body" id="detailContent"></div>
  </div>
</div>

<script>

  // ===== CONFIG: Change this to your WhatsApp number for testing =====
  const ADMIN_WHATSAPP = '91XXXXXXXXXX'; // Replace with your number with country code, no + or spaces
  const SEND_WHATSAPP = true; // Set to false to disable WhatsApp
  // =================================================================

(() => {
const WASHROOMS = [
  {name:'Wing A Floor 1 Main Side Gents', code:'W-A1-MS-G'},
  {name:'Wing A Floor 1 Main Side Ladies', code:'W-A1-MS-L'},
  {name:'Wing B Floor 1 Main Side Gents', code:'W-B1-MS-G'},
  {name:'Wing B Floor 1 Main Side Ladies', code:'W-B1-MS-L'},
  {name:'Wing B Floor 1 Back Side Gents', code:'W-B1-BS-G'},
  {name:'Wing B Floor 1 Back Side Ladies', code:'W-B1-BS-L'},
  {name:'Wing B Floor 2 Main Side Gents', code:'W-B2-MS-G'},
  {name:'Wing B Floor 2 Main Side Ladies', code:'W-B2-MS-L'},
  {name:'Wing B Floor 2 Back Side Gents', code:'W-B2-BS-G'},
  {name:'Wing B Floor 2 Back Side Ladies', code:'W-B2-BS-L'},
  {name:'Wing B Floor 3 Back Side Gents', code:'W-B3-BS-G'},
  {name:'Wing B Floor 3 Back Side Ladies', code:'W-B3-BS-L'},
  {name:'Wing C Floor 2 Main Side Gents', code:'W-C2-MS-G'},
  {name:'Wing C Floor 2 Main Side Ladies', code:'W-C2-MS-L'},
  {name:'Wing C Floor 5 Main Side Gents', code:'W-C5-MS-G'},
  {name:'Wing C Floor 5 Main Side Ladies', code:'W-C5-MS-L'},
];

const CATEGORIES = [
  {name:'Cleaning', emoji:'🧹', priority:'Low'},
  {name:'Bad Odor', emoji:'👃', priority:'Medium'},
  {name:'Water Leakage', emoji:'💧', priority:'High'},
  {name:'Blocked Toilet', emoji:'🚽', priority:'High'},
  {name:'Tissue Refill', emoji:'🧻', priority:'Low'},
  {name:'Soap Refill', emoji:'🧴', priority:'Low'},
  {name:'Broken Fixture', emoji:'🔧', priority:'Medium'},
  {name:'Electrical', emoji:'💡', priority:'High'},
  {name:'Pest', emoji:'🐜', priority:'Medium'},
  {name:'Other', emoji:'➕', priority:'Low'},
];

const STORAGE_KEY='iris_smart_washroom_v1';
let tickets = [];
let selectedCategory=null;
let selectedPriority='Low';
let photos=[];

function loadTickets(){
  const raw = localStorage.getItem(STORAGE_KEY);
  if(raw){ tickets = JSON.parse(raw); }
  else {
    const now = Date.now();
    tickets = [
      {
        id:'IRIS-2026-01842',
        locationCode:'W-B1-BS-G',
        locationName:'Wing B Floor 1 Back Side Gents',
        category:'Water Leakage',
        priority:'High',
        status:'Open',
        createdAt:new Date(now-25*60000).toISOString(),
        employeeId:'EMP1024',
        comments:'Tap near 2nd cubicle leaking continuously',
        photos:[],
        assignedTo:'',
        timeline:[{at:new Date(now-25*60000).toISOString(), action:'Created', by:'EMP1024'}],
        slaMinutes:30
      },
      {
        id:'IRIS-2026-01839',
        locationCode:'W-A1-MS-L',
        locationName:'Wing A Floor 1 Main Side Ladies',
        category:'Cleaning',
        priority:'Low',
        status:'In Progress',
        createdAt:new Date(now-92*60000).toISOString(),
        employeeId:'EMP0871',
        comments:'Floor needs mopping urgently',
        photos:[],
        assignedTo:'Rajesh K.',
        timeline:[
          {at:new Date(now-92*60000).toISOString(), action:'Created', by:'EMP0871'},
          {at:new Date(now-80*60000).toISOString(), action:'Assigned to Rajesh K.', by:'Admin'},
          {at:new Date(now-45*60000).toISOString(), action:'In Progress', by:'Rajesh K.'}
        ],
        slaMinutes:120
      },
      {
        id:'IRIS-2026-01831',
        locationCode:'W-C2-MS-G',
        locationName:'Wing C Floor 2 Main Side Gents',
        category:'Blocked Toilet',
        priority:'High',
        status:'Resolved',
        createdAt:new Date(now-185*60000).toISOString(),
        resolvedAt:new Date(now-150*60000).toISOString(),
        employeeId:'EMP1120',
        comments:'Second toilet blocked',
        photos:[],
        assignedTo:'Amit S.',
        timeline:[
          {at:new Date(now-185*60000).toISOString(), action:'Created', by:'EMP1120'},
          {at:new Date(now-180*60000).toISOString(), action:'Assigned to Amit S.', by:'Admin'},
          {at:new Date(now-150*60000).toISOString(), action:'Resolved', by:'Amit S.'}
        ],
        slaMinutes:30
      }
    ];
    saveTickets();
  }
}
function saveTickets(){ localStorage.setItem(STORAGE_KEY, JSON.stringify(tickets)); }

function initEmployee(){
  const locSel = document.getElementById('locationSelect');
  locSel.innerHTML = WASHROOMS.map(w=>`<option value="${w.code}">${w.name} (${w.code})</option>`).join('');
  locSel.value = 'W-B1-BS-G'; // default to match example
  updateLocationPill();
  locSel.onchange = updateLocationPill;

  const grid = document.getElementById('categoryGrid');
  grid.innerHTML = CATEGORIES.map(c=>`
    <button class="category-btn" data-cat="${c.name}">
      <span class="cat-emoji">${c.emoji}</span>
      <span class="cat-name">${c.name}</span>
    </button>
  `).join('');
  grid.querySelectorAll('.category-btn').forEach(btn=>{
    btn.onclick=()=>{
      grid.querySelectorAll('.category-btn').forEach(b=>b.classList.remove('selected'));
      btn.classList.add('selected');
      selectedCategory = btn.dataset.cat;
      const cat = CATEGORIES.find(x=>x.name===selectedCategory);
      selectedPriority = cat.priority;
      updatePriorityBadge();
    }
  });

  document.getElementById('photoBtn').onclick = ()=> document.getElementById('photoInput').click();
  document.getElementById('photoInput').onchange = handlePhotos;
  document.getElementById('submitTicket').onclick = submitTicket;
}

function updateLocationPill(){
  const code = document.getElementById('locationSelect').value;
  const w = WASHROOMS.find(x=>x.code===code);
  document.getElementById('locationPill').textContent = `📍 ${w.name}`;
}
function updatePriorityBadge(){
  const badge = document.getElementById('priorityBadge');
  if(!selectedCategory){ badge.style.display='none'; return; }
  badge.style.display='inline-flex';
  badge.textContent = selectedPriority;
  badge.className = 'priority-badge priority-'+selectedPriority.toLowerCase();
}

function handlePhotos(e){
  const files = Array.from(e.target.files).slice(0,3-photos.length);
  files.forEach(file=>{
    const reader = new FileReader();
    reader.onload = ev=>{ photos.push(ev.target.result); renderPhotos(); };
    reader.readAsDataURL(file);
  });
  e.target.value='';
}
function renderPhotos(){
  const wrap = document.getElementById('photoPreview');
  wrap.innerHTML = photos.map((src,i)=>`
    <div class="photo-thumb">
      <img src="${src}" alt="preview">
      <button class="photo-remove" onclick="removePhoto(${i})">×</button>
    </div>
  `).join('');
}
window.removePhoto = (i)=>{ photos.splice(i,1); renderPhotos(); }

function submitTicket(){
  if(!selectedCategory){ alert('Please select a category'); return; }
  const locCode = document.getElementById('locationSelect').value;
  const loc = WASHROOMS.find(w=>w.code===locCode);
  const comments = document.getElementById('comments').value.trim();
  const empId = document.getElementById('employeeId').value.trim() || 'EMP1024';
  const id = 'IRIS-2026-'+String(Math.floor(10000+Math.random()*89999));
  const sla = selectedPriority==='High'?30:selectedPriority==='Medium'?60:120;
  const now = new Date().toISOString();
  const ticket = {
    id, locationCode:loc.code, locationName:loc.name,
    category:selectedCategory, priority:selectedPriority,
    status:'Open', createdAt:now, employeeId:empId, comments,
    photos:[...photos], assignedTo:'',
    timeline:[{at:now, action:'Created', by:empId}],
    slaMinutes:sla
  };
  tickets.unshift(ticket);
  saveTickets();
  showSuccess(ticket);
  selectedCategory=null; selectedPriority='Low'; photos=[];
  document.querySelectorAll('.category-btn').forEach(b=>b.classList.remove('selected'));
  document.getElementById('priorityBadge').style.display='none';
  document.getElementById('comments').value='';
  renderPhotos();
  renderAdmin();
}

function showSuccess(ticket){
  const modal = document.getElementById('successModal');
  document.getElementById('successId').textContent = ticket.id;
  document.getElementById('successLoc').textContent = ticket.locationName;
  document.getElementById('successCat').textContent = ticket.category;
  document.getElementById('successEta').textContent = ticket.slaMinutes+' mins';
  modal.classList.add('show');
}
window.closeSuccess = ()=> document.getElementById('successModal').classList.remove('show');
window.simulateWA = ()=> alert('WhatsApp notification sent (simulated)\nTicket: '+document.getElementById('successId').textContent);
window.simulateEmail = ()=> alert('Email sent to facility@company.com (simulated)');

function initAdmin(){
  document.getElementById('filterWing').onchange = renderAdmin;
  document.getElementById('filterStatus').onchange = renderAdmin;
  document.getElementById('filterPriority').onchange = renderAdmin;
  document.getElementById('refreshBtn').onclick = renderAdmin;
  renderAdmin();
  setInterval(renderAdmin,60000);
}

function renderAdmin(){
  const now = Date.now();
  const open = tickets.filter(t=>t.status==='Open').length;
  const inprog = tickets.filter(t=>t.status==='In Progress' || t.status==='Assigned').length;
  const resolved = tickets.filter(t=>t.status==='Resolved'||t.status==='Closed').slice(0,20);
  const avgRes = resolved.length ? Math.round(resolved.reduce((a,t)=>a+((new Date(t.resolvedAt||t.createdAt)-new Date(t.createdAt))/60000),0)/resolved.length) : 0;
  const breach = tickets.filter(t=> !['Resolved','Closed'].includes(t.status) && ((now-new Date(t.createdAt))/60000) > t.slaMinutes ).length;
  
  document.getElementById('statOpen').textContent=open;
  document.getElementById('statInProg').textContent=inprog;
  document.getElementById('statAvg').textContent= avgRes ? avgRes+'m' : '—';
  document.getElementById('statBreach').textContent=breach;

  const wing = document.getElementById('filterWing').value;
  const status = document.getElementById('filterStatus').value;
  const priority = document.getElementById('filterPriority').value;

  let list = [...tickets];
  if(wing!=='All') list = list.filter(t=> t.locationCode.startsWith('W-'+wing));
  if(status!=='All') list = list.filter(t=> t.status===status);
  if(priority!=='All') list = list.filter(t=> t.priority===priority);

  const tbody = document.getElementById('ticketTable');
  tbody.innerHTML = list.map(t=>{
    const age = Math.floor((now - new Date(t.createdAt))/60000);
    const breached = age > t.slaMinutes && !['Resolved','Closed'].includes(t.status);
    return `
    <tr onclick="viewTicket('${t.id}')" style="cursor:pointer">
      <td><span class="ticket-id">${t.id}</span><div style="font-size:11px;color:#64748b;margin-top:2px">${formatTime(t.createdAt)}</div></td>
      <td><div style="font-weight:600;font-size:12.5px">${t.locationName}</div><div style="font-size:11px;color:#64748b">${t.locationCode}</div></td>
      <td>${t.category}</td>
      <td><span class="badge-sm priority-${t.priority.toLowerCase()}">${t.priority}</span></td>
      <td><span class="age ${breached?'breach':'ok'}">${age}m</span><div style="font-size:10px;color:#94a3b8">SLA ${t.slaMinutes}m</div></td>
      <td onclick="event.stopPropagation()">
        <select class="status-select" data-id="${t.id}" onchange="changeStatus('${t.id}',this.value)">
          ${['Open','Assigned','In Progress','Resolved','Closed'].map(s=>`<option ${t.status===s?'selected':''}>${s}</option>`).join('')}
        </select>
      </td>
      <td onclick="event.stopPropagation()"><input class="assign-input" placeholder="Assign to" value="${t.assignedTo||''}" onchange="assignTicket('${t.id}',this.value)"></td>
      <td onclick="event.stopPropagation()">
        <div class="action-btns">
          <button class="action-btn" onclick="viewTicket('${t.id}')">View</button>
          <button class="action-btn" onclick="quickResolve('${t.id}')">✓ Resolve</button>
        </div>
      </td>
    </tr>`;
  }).join('') || `<tr><td colspan="8" style="text-align:center;padding:32px;color:#94a3b8">No tickets match filters</td></tr>`;

  renderCharts(list);
}

window.changeStatus = (id, status)=>{
  const t = tickets.find(x=>x.id===id); if(!t) return;
  t.status = status;
  if(status==='Resolved' || status==='Closed') t.resolvedAt = new Date().toISOString();
  t.timeline.push({at:new Date().toISOString(), action:status, by:'Admin'});
  saveTickets(); renderAdmin();
};
window.assignTicket = (id, name)=>{
  const t = tickets.find(x=>x.id===id); if(!t) return;
  t.assignedTo = name;
  if(t.status==='Open' && name) t.status='Assigned';
  t.timeline.push({at:new Date().toISOString(), action:`Assigned to ${name}`, by:'Admin'});
  saveTickets(); renderAdmin();
};
window.quickResolve = (id)=> changeStatus(id,'Resolved');

window.viewTicket = (id)=>{
  const t = tickets.find(x=>x.id===id); if(!t) return;
  const modal = document.getElementById('detailModal');
  document.getElementById('detailContent').innerHTML = `
    <div style="display:flex;justify-content:space-between;align-items:start;margin-bottom:12px;gap:10px">
      <div>
        <div class="ticket-id" style="font-size:15px">${t.id}</div>
        <div style="font-size:13px;color:#475569;margin-top:4px">${t.locationName} • ${t.locationCode}</div>
      </div>
      <span class="badge-sm priority-${t.priority.toLowerCase()}">${t.priority} • ${t.status}</span>
    </div>
    <div style="background:#f8fafc;border:1px solid #eef2f7;border-radius:12px;padding:12px;margin-bottom:12px;font-size:13px;line-height:1.5">
      <div><strong>Category:</strong> ${t.category}</div>
      <div><strong>Reported by:</strong> ${t.employeeId} • ${formatTime(t.createdAt)}</div>
      <div><strong>Assigned:</strong> ${t.assignedTo||'—'}</div>
      <div><strong>SLA:</strong> ${t.slaMinutes} mins ${((Date.now()-new Date(t.createdAt))/60000 > t.slaMinutes && !['Resolved','Closed'].includes(t.status))?'<span style="color:#dc2626;font-weight:700">• BREACHED</span>':''}</div>
      ${t.comments?`<div style="margin-top:8px;padding-top:8px;border-top:1px dashed #e2e8f0"><strong>Comments:</strong> ${t.comments}</div>`:''}
    </div>
    ${t.photos.length?`<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:14px">${t.photos.map(p=>`<img src="${p}" style="width:88px;height:88px;object-fit:cover;border-radius:10px;border:1px solid #e2e8f0">`).join('')}</div>`:''}
    <h4 style="margin:0 0 8px;font-size:13px;font-weight:700;color:#334155">Timeline</h4>
    <div class="timeline">
      ${t.timeline.slice().reverse().map(ev=>`
        <div class="timeline-item">
          <div class="timeline-time">${formatTime(ev.at)}</div>
          <div class="timeline-text">${ev.action} ${ev.by?`• ${ev.by}`:''}</div>
        </div>
      `).join('')}
    </div>
    <div style="display:flex;gap:8px;margin-top:16px">
      <button class="action-btn" style="flex:1;padding:10px" onclick="escalateTicket('${t.id}')">⚠️ Escalate</button>
      <button class="action-btn" style="flex:1;background:#fee2e2;border-color:#fecaca;color:#b91c1c;padding:10px" onclick="closeTicket('${t.id}')">Close Ticket</button>
    </div>
  `;
  modal.classList.add('show');
};
window.closeDetail = ()=> document.getElementById('detailModal').classList.remove('show');
window.escalateTicket = (id)=>{
  const t = tickets.find(x=>x.id===id); if(!t) return;
  t.timeline.push({at:new Date().toISOString(), action:'Escalated to Supervisor', by:'Admin'});
  t.priority = 'High'; t.slaMinutes=30;
  saveTickets(); alert('Ticket escalated and priority set to HIGH'); viewTicket(id); renderAdmin();
};
window.closeTicket = (id)=>{ changeStatus(id,'Closed'); closeDetail(); };

function renderCharts(list){
  const wings = {'A':0,'B':0,'C':0};
  list.forEach(t=>{ const w = t.locationCode.split('-')[1]; if(wings[w]!=null) wings[w]++ });
  const maxW = Math.max(1,...Object.values(wings));
  document.getElementById('chartWing').innerHTML = Object.entries(wings).map(([k,v])=>`
    <div class="bar-row">
      <div class="bar-label">Wing ${k}</div>
      <div class="bar-track"><div class="bar-fill" style="width:${(v/maxW)*100}%"></div></div>
      <div style="font-size:12px;font-weight:700;text-align:right">${v}</div>
    </div>
  `).join('');

  const cats = {}; CATEGORIES.forEach(c=>cats[c.name]=0);
  list.forEach(t=>{ cats[t.category]=(cats[t.category]||0)+1 });
  const maxC = Math.max(1,...Object.values(cats));
  const catEntries = Object.entries(cats).filter(([,v])=>v>0).sort((a,b)=>b[1]-a[1]);
  document.getElementById('chartCategory').innerHTML = catEntries.map(([k,v])=>`
    <div class="bar-row">
      <div class="bar-label" title="${k}">${k}</div>
      <div class="bar-track"><div class="bar-fill" style="width:${(v/maxC)*100}%"></div></div>
      <div style="font-size:12px;font-weight:700;text-align:right">${v}</div>
    </div>
  `).join('') || '<div style="color:#94a3b8;font-size:12px;text-align:center;padding:20px">No data yet</div>';
}

function formatTime(iso){
  const d = new Date(iso);
  return d.toLocaleString('en-IN',{day:'2-digit',month:'short',hour:'2-digit',minute:'2-digit'});
}

document.getElementById('modeEmployee').onclick = ()=> switchMode('employee');
document.getElementById('modeAdmin').onclick = ()=> switchMode('admin');
function switchMode(m){
  document.getElementById('modeEmployee').classList.toggle('active', m==='employee');
  document.getElementById('modeAdmin').classList.toggle('active', m==='admin');
  document.getElementById('employeeView').style.display = m==='employee'?'block':'none';
  document.getElementById('adminView').style.display = m==='admin'?'block':'none';
  if(m==='admin') renderAdmin();
}

loadTickets(); initEmployee(); initAdmin(); switchMode('employee');
})();

  // Photo handling for both camera and gallery
  const photoCamera = document.getElementById('photoCamera');
  const photoGallery = document.getElementById('photoGallery');
  const photoPreview = document.getElementById('photoPreview');
  const photoImg = document.getElementById('photoImg');
  const removePhoto = document.getElementById('removePhoto');
  let currentPhotoFile = null;
  
  function handlePhotoSelect(e){
    const file = e.target.files[0];
    if(file){
      currentPhotoFile = file;
      const reader = new FileReader();
      reader.onload = function(ev){
        photoImg.src = ev.target.result;
        photoPreview.style.display = 'block';
      }
      reader.readAsDataURL(file);
    }
  }
  
  if(photoCamera) photoCamera.onchange = handlePhotoSelect;
  if(photoGallery) photoGallery.onchange = handlePhotoSelect;
  
  if(removePhoto) removePhoto.onclick = function(){
    currentPhotoFile = null;
    photoCamera.value = '';
    photoGallery.value = '';
    photoPreview.style.display = 'none';
  }

</script>
</body>
</html>

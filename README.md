<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Mohammadreza Solimani — GitHub Profile</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --surface-0: #f0efec;
    --surface-1: #f7f6f3;
    --surface-2: #ffffff;
    --text-primary: #0b0b0b;
    --text-secondary: #52514e;
    --text-muted: #898781;
    --border: rgba(11,11,11,0.10);
    --border-strong: rgba(11,11,11,0.18);
    --bg-accent: #e6f1fb;
    --text-accent: #185fa5;
    --border-accent: #b5d4f4;
    --radius: 8px;
  }

  body.dark {
    --surface-0: #0d1117;
    --surface-1: #161b22;
    --surface-2: #21262d;
    --text-primary: #e6edf3;
    --text-secondary: #c3c2b7;
    --text-muted: #898781;
    --border: rgba(255,255,255,0.10);
    --border-strong: rgba(255,255,255,0.18);
    --bg-accent: #0c2d4a;
    --text-accent: #85b7eb;
    --border-accent: #185fa5;
  }

  body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: var(--surface-0);
    color: var(--text-primary);
    min-height: 100vh;
    transition: background .3s, color .3s;
  }

  .page { max-width: 780px; margin: 0 auto; padding: 2rem 1.5rem; }

  /* Toolbar */
  .toolbar {
    display: flex; align-items: center; gap: 8px;
    margin-bottom: 1.5rem; flex-wrap: wrap;
  }
  .btn {
    font-size: 13px; padding: 6px 14px; cursor: pointer;
    border: 0.5px solid var(--border-strong); border-radius: var(--radius);
    background: transparent; color: var(--text-primary);
    display: flex; align-items: center; gap: 5px;
    transition: background .15s;
  }
  .btn:hover { background: var(--surface-1); }
  .btn-primary { background: #2a78d6; color: #fff; border-color: transparent; }
  .btn-primary:hover { opacity: .88; background: #2a78d6; }
  .copy-toast {
    font-size: 12px; color: #0ca30c; margin-left: 6px;
    opacity: 0; transition: opacity .3s;
  }
  .copy-toast.show { opacity: 1; }

  /* Avatar + Bio */
  .avatar-row { display: flex; gap: 20px; align-items: flex-start; margin-bottom: 1.5rem; }
  .avatar {
    width: 80px; height: 80px; border-radius: 50%;
    background: #2a78d6; flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    font-size: 24px; font-weight: 500; color: #fff;
    border: 2.5px solid var(--border-strong);
  }
  .bio h1 { font-size: 20px; font-weight: 500; }
  .bio .handle { font-size: 13px; color: var(--text-muted); margin: 3px 0 9px; }
  .bio p { font-size: 13px; color: var(--text-secondary); line-height: 1.6; margin-bottom: 10px; }
  .tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .tag {
    font-size: 11px; padding: 3px 10px; border-radius: 100px;
    background: var(--bg-accent); color: var(--text-accent);
    border: 0.5px solid var(--border-accent);
    display: flex; align-items: center; gap: 4px;
  }

  /* Stats */
  .stats-row { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-bottom: 1.5rem; }
  .stat {
    background: var(--surface-1); border: 0.5px solid var(--border);
    border-radius: 10px; padding: 12px; text-align: center;
  }
  .stat .n { font-size: 20px; font-weight: 500; }
  .stat .l { font-size: 11px; color: var(--text-muted); margin-top: 3px; }

  /* Section label */
  .sec {
    font-size: 10px; font-weight: 500; letter-spacing: .07em;
    text-transform: uppercase; color: var(--text-muted); margin-bottom: 10px;
  }

  /* Two col */
  .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 1.5rem; }
  .card {
    background: var(--surface-2); border: 0.5px solid var(--border);
    border-radius: 12px; padding: 16px;
  }
  .card h3 {
    font-size: 13px; font-weight: 500; margin-bottom: 14px;
    display: flex; align-items: center; gap: 6px;
    color: var(--text-primary);
  }

  /* Lang sliders */
  .slider-row { margin-bottom: 10px; }
  .sm { display: flex; justify-content: space-between; font-size: 12px; margin-bottom: 4px; align-items: center; }
  .dot { width: 8px; height: 8px; border-radius: 50%; display: inline-block; margin-right: 5px; }
  .track { height: 5px; background: var(--surface-0); border-radius: 3px; overflow: hidden; }
  .fill { height: 100%; border-radius: 3px; transition: width .4s ease; }
  input[type=range] { width: 100%; margin-bottom: 4px; accent-color: #2a78d6; cursor: pointer; }

  /* Skill grid */
  .skill-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 1.5rem; }
  .pill {
    background: var(--surface-1); border: 0.5px solid var(--border);
    border-radius: 8px; padding: 8px 12px;
    display: flex; align-items: center; gap: 7px;
    font-size: 12px; color: var(--text-secondary);
  }
  .pill i { font-size: 15px; color: var(--text-muted); }

  /* Heatmap */
  .hcard {
    background: var(--surface-2); border: 0.5px solid var(--border);
    border-radius: 12px; padding: 16px; margin-bottom: 1.5rem;
  }
  .hcard h3 { font-size: 13px; font-weight: 500; margin-bottom: 12px; color: var(--text-primary); }
  .hmap { display: grid; grid-template-columns: repeat(52, 1fr); gap: 2px; }
  .hc { width: 100%; aspect-ratio: 1; border-radius: 2px; }

  /* Repos */
  .repo-list { display: flex; flex-direction: column; gap: 8px; margin-bottom: 1.5rem; }
  .repo {
    background: var(--surface-2); border: 0.5px solid var(--border);
    border-radius: 10px; padding: 12px 15px;
    display: flex; justify-content: space-between; align-items: flex-start;
  }
  .rname { font-size: 13px; font-weight: 500; color: var(--text-accent); display: flex; align-items: center; gap: 5px; }
  .rdesc { font-size: 12px; color: var(--text-muted); margin-top: 3px; }
  .rmeta { display: flex; gap: 10px; font-size: 11px; color: var(--text-muted); align-items: center; flex-shrink: 0; margin-left: 12px; }
  .rmeta span { display: flex; align-items: center; gap: 3px; }

  /* README output */
  .readme-out {
    background: var(--surface-1); border: 0.5px solid var(--border);
    border-radius: 10px; padding: 14px;
    font-family: 'Courier New', monospace; font-size: 12px;
    color: var(--text-secondary); white-space: pre-wrap; word-break: break-all;
    line-height: 1.7; margin-bottom: 1.5rem; display: none;
  }
  .readme-out.show { display: block; }

  @media (max-width: 560px) {
    .two-col { grid-template-columns: 1fr; }
    .stats-row { grid-template-columns: repeat(2, 1fr); }
    .skill-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<div class="page">

  <div class="toolbar">
    <button class="btn btn-primary" onclick="toggleMode()">
      <i class="ti ti-sun" id="modeIco"></i>
      <span id="modeTxt">Light mode</span>
    </button>
    <button class="btn" onclick="exportReadme()">
      <i class="ti ti-download"></i> Export README.md
    </button>
    <span class="copy-toast" id="toast">Copied to clipboard!</span>
  </div>

  <!-- Profile header -->
  <div class="avatar-row">
    <div class="avatar">MS</div>
    <div class="bio">
      <h1>Mohammadreza Solimani</h1>
      <div class="handle">@mohammadrezasolimani</div>
      <p>Deep learning researcher passionate about neural architectures, computer vision, and reproducible ML. Building tools that push the frontier of AI research.</p>
      <div class="tags">
        <span class="tag"><i class="ti ti-map-pin"></i> Iran</span>
        <span class="tag">PyTorch / TensorFlow</span>
        <span class="tag">Deep Learning</span>
        <span class="tag">Open to collab</span>
      </div>
    </div>
  </div>

  <!-- Stats -->
  <div class="stats-row">
    <div class="stat"><div class="n">24</div><div class="l">Repositories</div></div>
    <div class="stat"><div class="n">138</div><div class="l">Followers</div></div>
    <div class="stat"><div class="n" id="s-contrib">947</div><div class="l">Contributions</div></div>
    <div class="stat"><div class="n">86</div><div class="l">Stars earned</div></div>
  </div>

  <!-- Languages + Radar -->
  <p class="sec">Language proficiency — drag sliders to adjust</p>
  <div class="two-col">
    <div class="card">
      <h3><i class="ti ti-code"></i> Languages</h3>
      <div id="langBars"></div>
    </div>
    <div class="card">
      <h3><i class="ti ti-chart-radar"></i> Deep learning skills</h3>
      <div style="position:relative;height:210px;">
        <canvas id="radarC" role="img" aria-label="Radar chart of deep learning skills for Mohammadreza Solimani">
          Skills: Math 85, PyTorch 88, Vision 80, NLP 75, MLOps 65, Writing 78.
        </canvas>
      </div>
    </div>
  </div>

  <!-- Skill tree -->
  <p class="sec">Deep learning skill tree</p>
  <div class="skill-grid" id="skillGrid"></div>

  <!-- Heatmap -->
  <p class="sec">Contribution activity</p>
  <div class="hcard">
    <h3 id="heatTitle">Past year — 947 contributions</h3>
    <div class="hmap" id="hmap" role="img" aria-label="GitHub contribution heatmap"></div>
  </div>

  <!-- Repos -->
  <p class="sec">Pinned repositories</p>
  <div class="repo-list" id="repoList"></div>

  <!-- README export output -->
  <div class="readme-out" id="readmeOut"></div>

</div>

<script>
let dark = false;
let radarChart = null;

const langs = [
  { name: 'Python', pct: 90, color: '#2a78d6' },
  { name: 'C++',    pct: 65, color: '#4a3aa7' },
  { name: 'CUDA',   pct: 52, color: '#1baf7a' },
  { name: 'MATLAB', pct: 58, color: '#eda100' },
  { name: 'Bash',   pct: 40, color: '#e34948' },
  { name: 'Julia',  pct: 32, color: '#73726c' },
];

const skills = [
  ['ti-math-function',  'Math and linear algebra'],
  ['ti-brain',          'Neural architectures'],
  ['ti-eye',            'Computer vision'],
  ['ti-message-chatbot','NLP and LLMs'],
  ['ti-wand',           'Diffusion models'],
  ['ti-chart-line',     'Optimization theory'],
  ['ti-server',         'MLOps and deployment'],
  ['ti-test-pipe',      'Research and ablations'],
  ['ti-transform',      'Data pipelines'],
  ['ti-cpu',            'GPU and CUDA programming'],
];

const repos = [
  { name: 'dl-vision-toolkit',      desc: 'Modular deep learning toolkit for vision tasks — segmentation, detection, classification', stars: 42, forks: 11, lang: 'Python' },
  { name: 'neural-ode-experiments', desc: 'Experiments with neural ODEs and continuous-depth networks', stars: 27, forks: 6,  lang: 'Python' },
  { name: 'cuda-attention',         desc: 'Custom CUDA kernels for efficient self-attention in transformers', stars: 17, forks: 4,  lang: 'CUDA'   },
];

/* ── Language bars ── */
function renderLangs() {
  document.getElementById('langBars').innerHTML = langs.map((l, i) => `
    <div class="slider-row">
      <div class="sm">
        <span><span class="dot" style="background:${l.color}"></span>${l.name}</span>
        <span style="color:var(--text-muted);min-width:34px;text-align:right" id="p${i}">${Math.round(l.pct)}%</span>
      </div>
      <input type="range" min="0" max="100" step="1" value="${l.pct}" oninput="upLang(${i}, this.value)" />
      <div class="track"><div class="fill" id="b${i}" style="width:${l.pct}%;background:${l.color}"></div></div>
    </div>`).join('');
}

function upLang(i, v) {
  langs[i].pct = parseInt(v);
  document.getElementById('p' + i).textContent = Math.round(v) + '%';
  document.getElementById('b' + i).style.width = v + '%';
}

/* ── Skills ── */
function renderSkills() {
  document.getElementById('skillGrid').innerHTML = skills.map(([ic, lbl]) =>
    `<div class="pill"><i class="ti ${ic}"></i><span>${lbl}</span></div>`).join('');
}

/* ── Repos ── */
function renderRepos() {
  document.getElementById('repoList').innerHTML = repos.map(r => `
    <div class="repo">
      <div>
        <div class="rname"><i class="ti ti-book-2" style="font-size:13px"></i>${r.name}</div>
        <div class="rdesc">${r.desc}</div>
      </div>
      <div class="rmeta">
        <span><i class="ti ti-star"></i>${r.stars}</span>
        <span><i class="ti ti-git-fork"></i>${r.forks}</span>
        <span>${r.lang}</span>
      </div>
    </div>`).join('');
}

/* ── Heatmap ── */
function renderHeatmap() {
  const light = ['#ebedf0','#9be9a8','#40c463','#30a14e','#216e39'];
  const dk    = ['#161b22','#0e4429','#006d32','#26a641','#39d353'];
  const cols  = dark ? dk : light;
  let html = '', total = 0;
  for (let w = 0; w < 52; w++) {
    for (let d = 0; d < 7; d++) {
      const r  = Math.abs(Math.sin(338 * (w * 7 + d + 1)) * 997) % 1;
      const ci = r < .48 ? 0 : r < .65 ? 1 : r < .80 ? 2 : r < .92 ? 3 : 4;
      total += [0, 1, 3, 6, 10][ci];
      html += `<div class="hc" style="background:${cols[ci]}"></div>`;
    }
  }
  document.getElementById('hmap').innerHTML = html;
  document.getElementById('heatTitle').textContent = `Past year — ${total.toLocaleString()} contributions`;
  document.getElementById('s-contrib').textContent = total.toLocaleString();
}

/* ── Radar ── */
function renderRadar() {
  const gc = dark ? 'rgba(255,255,255,0.08)' : 'rgba(0,0,0,0.07)';
  const lc = dark ? '#898781' : '#73726c';
  if (radarChart) radarChart.destroy();
  radarChart = new Chart(document.getElementById('radarC'), {
    type: 'radar',
    data: {
      labels: ['Math', 'PyTorch', 'Vision', 'NLP/LLMs', 'MLOps', 'Writing'],
      datasets: [{
        data: [85, 88, 80, 75, 65, 78],
        backgroundColor: 'rgba(42,120,214,0.12)',
        borderColor: '#2a78d6',
        borderWidth: 2,
        pointBackgroundColor: '#2a78d6',
        pointBorderColor: dark ? '#21262d' : '#fff',
        pointBorderWidth: 2,
        pointRadius: 4,
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: { legend: { display: false } },
      scales: { r: {
        min: 0, max: 100,
        ticks: { display: false },
        grid: { color: gc },
        pointLabels: { font: { size: 10 }, color: lc },
        angleLines: { color: gc },
      }}
    }
  });
}

/* ── Dark / Light toggle ── */
function toggleMode() {
  dark = !dark;
  document.body.classList.toggle('dark', dark);
  document.getElementById('modeIco').className = dark ? 'ti ti-moon' : 'ti ti-sun';
  document.getElementById('modeTxt').textContent = dark ? 'Dark mode' : 'Light mode';
  renderHeatmap();
  renderRadar();
}

/* ── Export README ── */
function exportReadme() {
  const badges = langs.map(l =>
    `![${l.name}](https://img.shields.io/badge/${encodeURIComponent(l.name)}-${Math.round(l.pct)}%25-${l.color.replace('#','')}?style=flat-square)`
  ).join('\n');
  const skillBadges = skills.map(([, lbl]) =>
    `![${lbl}](https://img.shields.io/badge/-${encodeURIComponent(lbl)}-2a78d6?style=flat-square)`
  ).join('\n');

  const md = `# Hi, I'm Mohammadreza Solimani 👋

> Deep learning researcher passionate about neural architectures, computer vision, and reproducible ML.

## Language proficiency
${badges}

## Deep learning skills
${skillBadges}

## GitHub stats
![GitHub stats](https://github-readme-stats.vercel.app/api?username=mohammadrezasolimani&show_icons=true&theme=default)

---
*Profile built with GitHub Profile Builder*
`;

  const out = document.getElementById('readmeOut');
  out.textContent = md;
  out.classList.add('show');

  navigator.clipboard.writeText(md).then(() => {
    const t = document.getElementById('toast');
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 2500);
  }).catch(() => {});
}

/* ── Init ── */
renderLangs();
renderSkills();
renderRepos();
renderHeatmap();
renderRadar();
</script>
</body>
</html>

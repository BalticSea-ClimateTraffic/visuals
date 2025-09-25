---
layout: page
title: Rain projections
---

Seasonal maximum daily precipitation:  
historical (1986–2005), mid-century (2041–2060), late-century (2081–2100).  
Select a season and a future period to compare against the historical baseline.

<label for="seasonDropdown">Season:</label>
<select id="seasonDropdown">
  <option value="JJA" selected>JJA (Jun–Aug)</option>
  <option value="DJF">DJF (Dec–Feb)</option>
</select>

<label for="periodDropdown">Future period:</label>
<select id="periodDropdown">
  <option value="midcentury" selected>Mid-century (2041–2060)</option>
  <option value="latecentury">Late-century (2081–2100)</option>
</select>

<div class="plots-row">
  <div class="plot-col">
    <div class="plot-title">Historical mean (1986–2005)</div>
    <div class="holder"><object id="plot-hist" type="text/html" data=""></object></div>
  </div>
  <div class="plot-col">
    <div class="plot-title">Future mean (RCP4.5)</div>
    <div class="holder"><object id="plot-future" type="text/html" data=""></object></div>
  </div>
  <div class="plot-col">
    <div class="plot-title">Future / Historical (ratio, RCP4.5)</div>
    <div class="holder"><object id="plot-diff" type="text/html" data=""></object></div>
  </div>
</div>

<style>
label { margin-right: 8px; font-weight: 600; }
select { margin: 10px 16px 20px 0; padding: 6px 10px; font-size: 16px; }

.plots-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 14px;
  align-items: stretch;
}
.plot-col { display: flex; flex-direction: column; min-height: 400px; }
.plot-title { font-weight: 600; margin: 6px 0 8px; }
.holder { flex: 1 1 auto; }
.plot-col object {
  width: 100%; height: 100%; min-height: 360px;
  border: none; background: #f7f7f7;
}
.missing {
  display: grid; place-items: center; height: 100%;
  background: #fff3f3; border: 1px solid #f2caca; color: #a33;
  font-family: system-ui, sans-serif; padding: 1rem; text-align: center;
}
@media (max-width: 1000px) { .plots-row { grid-template-columns: 1fr; } }
</style>

<script>
const seasonDropdown = document.getElementById('seasonDropdown');
const periodDropdown = document.getElementById('periodDropdown');

const histObj   = document.getElementById('plot-hist');
const futureObj = document.getElementById('plot-future');
const diffObj   = document.getElementById('plot-diff');

// If your HTML files live in a subfolder, set it here, e.g. 'figs/'.
// Leave empty string if they are alongside this page.
const PATH_PREFIX = ''; // e.g., 'figs/' if needed

// Your files (per your screenshot) are named like:
// PLOT_rx1day_<SEASON>_hist.html
// PLOT_rx1day_<SEASON>_mid.html
// PLOT_rx1day_<SEASON>_late.html
// PLOT_rx1day_<SEASON>_ratio_mid.html
// PLOT_rx1day_<SEASON>_ratio_late.html
function buildFilenames(season, period) {
  const periodShort = (period === 'midcentury') ? 'mid' : 'late';
  const base = `PLOT_rx1day_${season}`;
  return {
    hist: `${base}_hist.html`,
    fut:  `${base}_${periodShort}.html`,
    diff: `${base}_ratio_${periodShort}.html`,
  };
}

// Replace an <object> with an inline “missing” message
function showMissing(objEl, url) {
  const parent = objEl.parentElement;
  parent.innerHTML = `<div class="missing">File not found:<br><code>${url}</code></div>`;
}

// Set an object’s data if the file exists; otherwise show a message
async function loadObject(objEl, relUrl) {
  const url = PATH_PREFIX + relUrl;
  try {
    const res = await fetch(url, { method: 'HEAD', cache: 'no-store' });
    if (res.ok) {
      // add a cache-buster in case the browser cached an older version
      objEl.setAttribute('data', url + '?v=' + Date.now());
    } else {
      showMissing(objEl, url);
    }
  } catch (e) {
    showMissing(objEl, url);
  }
}

async function updatePlots() {
  const season = seasonDropdown.value;           // "JJA" or "DJF"
  const period = periodDropdown.value;           // "midcentury" or "latecentury"
  const { hist, fut, diff } = buildFilenames(season, period);

  // Reset holders (in case we previously showed a missing message)
  for (const obj of [histObj, futureObj, diffObj]) {
    const holder = obj.parentElement;
    holder.innerHTML = '';
    holder.appendChild(obj);
  }

  await Promise.all([
    loadObject(histObj,   hist),
    loadObject(futureObj, fut),
    loadObject(diffObj,   diff),
  ]);
}

seasonDropdown.addEventListener('change', updatePlots);
periodDropdown.addEventListener('change', updatePlots);
updatePlots();
</script>

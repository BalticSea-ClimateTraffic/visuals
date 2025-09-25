---
layout: page
title: Rain test
---

Seasonal maximum daily precipitation:  
historical (1986–2005), mid-century (2041–2060), late-century (2081–2100).  
Select an ID, a season, and a future period to compare against the historical baseline.

<label for="idDropdown">ID:</label>
<select id="idDropdown">
  <option value="rx1day" selected>rx1day</option>
  <!-- Add more IDs if you generate them, e.g. prcptot, r10mm, etc. -->
</select>

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
    <iframe id="plot-hist" src="" loading="lazy"></iframe>
  </div>
  <div class="plot-col">
    <div class="plot-title">Future mean (RCP4.5)</div>
    <iframe id="plot-future" src="" loading="lazy"></iframe>
  </div>
  <div class="plot-col">
    <div class="plot-title">Future / Historical (ratio, RCP4.5)</div>
    <iframe id="plot-diff" src="" loading="lazy"></iframe>
  </div>
</div>

<style>
label { margin-right: 8px; font-weight: 600; }
select { margin: 10px 16px 20px 0; padding: 6px 10px; font-size: 16px; }

.plots-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  align-items: start;
}
.plot-col { display: flex; flex-direction: column; align-items: center; }
.plot-title { font-weight: 600; margin: 6px 0 8px; }

iframe {
  width: 100%;
  height: 520px;        /* adjust to taste */
  border: 1px solid #ccc;
  background: #f7f7f7;
}

@media (max-width: 900px) {
  .plots-row { grid-template-columns: 1fr; }
  iframe { height: 520px; }
}
</style>

<script>
const idDropdown     = document.getElementById('idDropdown');
const seasonDropdown = document.getElementById('seasonDropdown');
const periodDropdown = document.getElementById('periodDropdown');

const histFrame   = document.getElementById('plot-hist');
const futureFrame = document.getElementById('plot-future');
const diffFrame   = document.getElementById('plot-diff');

/* Your plot HTMLs live in PLOTs_HCLIM/ */
const PATH_PREFIX = 'PLOTs_HCLIM/';

function buildFilenames(id, season, period) {
  // Map mid/late labels to short tokens in filenames
  const periodShort = (period === 'midcentury') ? 'mid' : 'late';
  const base = `PLOT_${id}_${season}`;
  return {
    hist: `${base}_hist.html`,
    fut:  `${base}_${periodShort}.html`,
    diff: `${base}_ratio_${periodShort}.html`,
  };
}

function updatePlots() {
  const id     = idDropdown.value;
  const season = seasonDropdown.value;
  const period = periodDropdown.value;

  const { hist, fut, diff } = buildFilenames(id, season, period);

  histFrame.src   = PATH_PREFIX + hist;
  futureFrame.src = PATH_PREFIX + fut;
  diffFrame.src   = PATH_PREFIX + diff;
}

// Update on any change
[idDropdown, seasonDropdown, periodDropdown].forEach(el =>
  el.addEventListener('change', updatePlots)
);

// Initial load
updatePlots();
</script>

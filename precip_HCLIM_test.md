---
layout: page
title: Rain
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
  gap: 10px;
  align-items: start;
}
.plot-col { display: flex; flex-direction: column; align-items: center; }
.plot-title { font-weight: 600; margin: 6px 0 8px; }

/* Nice, readable size without scrollbars */
iframe {
  width: 100%;
  height: 100px;           /* adjust if you want bigger/smaller */
  border: 1px solid #ccc;
  background: #f7f7f7;
}
@media (max-width: 100px) {
  .plots-row { grid-template-columns: 1fr; }
  iframe { height: 100px; } /* same height on mobile, full width */
}
</style>

<script>
const seasonDropdown = document.getElementById('seasonDropdown');
const periodDropdown = document.getElementById('periodDropdown');

const histFrame   = document.getElementById('plot-hist');
const futureFrame = document.getElementById('plot-future');
const diffFrame   = document.getElementById('plot-diff');

// If the plot HTMLs are in a subfolder, set it here (e.g., 'figs/'); else leave ''.
const PATH_PREFIX = '';

function buildFilenames(season, period) {
  // Using your PLOT_ prefix + names
  const periodShort = (period === 'midcentury') ? 'mid' : 'late';
  const base = `PLOT_rx1day_${season}`;
  return {
    hist: `${base}_hist.html`,
    fut:  `${base}_${periodShort}.html`,
    diff: `${base}_ratio_${periodShort}.html`,
  };
}

function updatePlots() {
  const season = seasonDropdown.value;
  const period = periodDropdown.value;
  const { hist, fut, diff } = buildFilenames(season, period);

  histFrame.src   = PATH_PREFIX + hist;
  futureFrame.src = PATH_PREFIX + fut;
  diffFrame.src   = PATH_PREFIX + diff;
}

seasonDropdown.addEventListener('change', updatePlots);
periodDropdown.addEventListener('change', updatePlots);
updatePlots();
</script>

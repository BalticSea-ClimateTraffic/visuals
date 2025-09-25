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
    <object id="plot-hist" type="text/html" data=""></object>
  </div>
  <div class="plot-col">
    <div class="plot-title">Future mean (RCP4.5)</div>
    <object id="plot-future" type="text/html" data=""></object>
  </div>
  <div class="plot-col">
    <div class="plot-title">Future / Historical (ratio, RCP4.5)</div>
    <object id="plot-diff" type="text/html" data=""></object>
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
.plot-col {
  display: flex;
  flex-direction: column;
  min-height: 400px;
}
.plot-title {
  font-weight: 600;
  margin: 6px 0 8px;
}
.plot-col object {
  flex: 1 1 auto;
  width: 100%;
  height: 100%;
  border: none;
  background: #f7f7f7;
}
@media (max-width: 1000px) {
  .plots-row { grid-template-columns: 1fr; }
}
</style>

<script>
const seasonDropdown = document.getElementById('seasonDropdown');
const periodDropdown = document.getElementById('periodDropdown');

const histObj   = document.getElementById('plot-hist');
const futureObj = document.getElementById('plot-future');
const diffObj   = document.getElementById('plot-diff');

// Filenames expected:
// rx1day_<SEASON>_hist.html
// rx1day_<SEASON>_mid.html
// rx1day_<SEASON>_late.html
// rx1day_<SEASON>_ratio_mid.html
// rx1day_<SEASON>_ratio_late.html

function buildFilenames(season, period) {
  const periodShort = (period === 'midcentury') ? 'mid' : 'late';
  const base = `rx1day_${season}`;

  const hist = `${base}_hist.html`;
  const fut  = `${base}_${periodShort}.html`;
  const diff = `${base}_ratio_${periodShort}.html`;

  return { hist, fut, diff };
}

function updatePlots() {
  const season = seasonDropdown.value;  // "JJA" or "DJF"
  const period = periodDropdown.value;  // "midcentury" or "latecentury"
  const { hist, fut, diff } = buildFilenames(season, period);

  histObj.setAttribute('data', hist);
  futureObj.setAttribute('data', fut);
  diffObj.setAttribute('data', diff);
}

// Init
seasonDropdown.addEventListener('change', updatePlots);
periodDropdown.addEventListener('change', updatePlots);
updatePlots();
</script>

---
layout: page
title: Precipitation
---

Projected precipitation changes on daily scale for two seasons: summer (JJA) and winter (DJF).
The spatial means are calculated for periods: historical (1986–2005), mid-century (2041–2060), late-century (2081–2100)
using the data from high resolution regional climate model HARMONIE-Climate. The data was produced in a Nordic collaboration project 2020.

Select a precipitation index, a season, a plot style, and a future period to compare against the historical baseline.

Indices:  
Rx1day = Seasonal maximum daily precipitation  
Rx5day = Seasonal maximum 5-day precipitation  
R20mm  = Days when precipitation intensity is 20 mm or more  
SDII   = Mean precipitation amount on wet days. A wet day is defined as a day  
         with precipitation 1 mm or more.

<label for="idDropdown">Index:</label>
<select id="idDropdown">
  <option value="rx1day" selected>rx1day</option>
  <!-- Add more IDs if you generate them, e.g. prcptot, r10mm, etc. -->
</select>

<label for="seasonDropdown">Season:</label>
<select id="seasonDropdown">
  <option value="JJA" selected>JJA (Jun–Aug)</option>
  <option value="DJF">DJF (Dec–Feb)</option>
</select>

<label for="plotStyleDropdown">Plot style:</label>
<select id="plotStyleDropdown">
  <option value="maps" selected>Maps</option>
  <option value="boxplots">Boxplots</option>
</select>


<!-- Map-specific options (shown only when Plot style = Maps) -->
<div id="mapOptions" hidden>
  <label for="periodDropdown">Future period:</label>
  <select id="periodDropdown">
    <option value="midcentury" selected>Mid-century (2041–2060)</option>
    <option value="latecentury">Late-century (2081–2100)</option>
  </select>

  <label for="diffDropdown">Difference map:</label>
  <select id="diffDropdown">
    <option value="off" selected>Off</option>
    <option value="on">On</option>
  </select>
</div>

<div class="plots-row" id="plotsRow">
  <div class="plot-col" id="col-hist">
    <div class="plot-title">Historical mean (1986–2005)</div>
    <iframe id="plot-hist" src="" loading="lazy" scrolling="no"></iframe>
  </div>
  <div class="plot-col" id="col-future">
    <div class="plot-title">Future mean (RCP4.5)</div>
    <iframe id="plot-future" src="" loading="lazy" scrolling="no"></iframe>
  </div>
  <div class="plot-col" id="col-diff">
    <div class="plot-title">Future / Historical</div>
    <iframe id="plot-diff" src="" loading="lazy" scrolling="no"></iframe>
  </div>
</div>

<style>
label { margin-right: 8px; font-weight: 600; }
select { margin: 10px 16px 20px 0; padding: 6px 10px; font-size: 16px; }

.plots-row {
  display: grid;
  grid-template-columns: repeat(2, 1fr);  /* two columns for the blue maps */
  gap: 12px;
  align-items: start;
}
#col-diff { grid-column: 1 / -1; }
.plot-col { display: flex; flex-direction: column; align-items: center; }
.plot-title { font-weight: 600; margin: 6px 0 8px; }

iframe {
  width: 100%;
  border: 1px solid #ccc;
  background: #f7f7f7;
}

.hidden { display: none !important; }

@media (max-width: 900px) {
  .plots-row { grid-template-columns: 1fr; }
  iframe { height: 520px; }
}
</style>

<script>
const idDropdown        = document.getElementById('idDropdown');
const seasonDropdown    = document.getElementById('seasonDropdown');
const plotStyleDropdown = document.getElementById('plotStyleDropdown');
const periodDropdown    = document.getElementById('periodDropdown');
const diffDropdown      = document.getElementById('diffDropdown');

const mapOptions = document.getElementById('mapOptions');
const plotsRow   = document.getElementById('plotsRow');

const colHist   = document.getElementById('col-hist');
const colFuture = document.getElementById('col-future');
const colDiff   = document.getElementById('col-diff');

const histTitle   = colHist.querySelector('.plot-title');
const futureTitle = colFuture.querySelector('.plot-title');
const diffTitle   = colDiff.querySelector('.plot-title');

const histFrame   = document.getElementById('plot-hist');
const futureFrame = document.getElementById('plot-future');
const diffFrame   = document.getElementById('plot-diff');

const PATH_PREFIX = 'PLOTs_HCLIM/';

function buildMapFilenames(id, season, period) {
  const periodShort = (period === 'midcentury') ? 'mid' : 'late';
  const base = `PLOT_${id}_${season}`;
  return {
    hist: `${base}_hist.html`,
    fut:  `${base}_${periodShort}.html`,
    diff: `${base}_ratio_${periodShort}.html`,
  };
}

function buildBoxplotFilename(id, season) {
  return `PLOT_${id}_${season}_boxplots.html`;
}

function setColumns(count, diffOn = false) {
  // count: 2 for Maps, 1 for Boxplots
  plotsRow.style.gridTemplateColumns = `repeat(${count}, 1fr)`;

  // Show/hide columns
  colHist.classList.toggle('hidden', count === 1); // hide for boxplots
  colFuture.classList.remove('hidden');            // always visible
  colDiff.classList.toggle('hidden', !diffOn);     // only when diff is ON

  // If diff is visible under the two maps, span across both columns
  colDiff.style.gridColumn = diffOn ? '1 / -1' : '';
}

function updatePlots() {
  const id        = idDropdown.value;
  const season    = seasonDropdown.value;
  const plotStyle = plotStyleDropdown.value;

  const isMaps     = (plotStyle === 'maps');
  const isBoxplots = (plotStyle === 'boxplots');
  
  mapOptions.toggleAttribute('hidden', !isMaps);

  if (isMaps) {
    plotsRow.classList.remove('hidden');

    // Titles for maps
    histTitle.textContent   = 'Historical mean (1986–2005)';
    futureTitle.textContent = 'Future mean (RCP4.5)';
    diffTitle.textContent   = 'Future / Historical';

    const period = periodDropdown.value;
    const diffOn = (diffDropdown.value === 'on');

    const { hist, fut, diff } = buildMapFilenames(id, season, period);
    histFrame.src   = PATH_PREFIX + hist;
    futureFrame.src = PATH_PREFIX + fut;
    diffFrame.src   = diffOn ? (PATH_PREFIX + diff) : '';

    setColumns(2, diffOn);
    return;
  }

  if (isBoxplots) {
    plotsRow.classList.remove('hidden');

    // Single center panel with boxplots
    setColumns(1, false);
    futureTitle.textContent = 'Boxplots';
    futureFrame.src = PATH_PREFIX + buildBoxplotFilename(id, season);

    // Clear any map frames that might linger
    histFrame.src = '';
    diffFrame.src = '';
    return;
  }

  // Fallback (no style selected)
  histFrame.src = futureFrame.src = diffFrame.src = '';
  plotsRow.classList.add('hidden');
}

/* -------- Auto-resize + make inner content responsive -------- */
function attachAutosize(iframe) {
  const resize = () => {
    try {
      const doc = iframe.contentDocument || iframe.contentWindow.document;
      if (!doc) return;
      doc.documentElement.style.overflow = 'hidden';
      doc.body.style.overflow = 'hidden';
      doc.body.style.margin = '0';
      doc.querySelectorAll('img, svg, canvas').forEach(el => {
        el.style.maxWidth = '100%';
        el.style.height = 'auto';
      });
      const h = Math.max(doc.body.scrollHeight, doc.documentElement.scrollHeight);
      iframe.style.height = h + 'px';
    } catch (e) {
      console.warn('Autosize failed:', e);
    }
  };
  iframe.addEventListener('load', () => {
    resize();
    setTimeout(resize, 50);
    setTimeout(resize, 300);
    setTimeout(resize, 1000);
  });
  window.addEventListener('resize', resize);
}

[histFrame, futureFrame, diffFrame].forEach(attachAutosize);

/* Re-load plots when user changes selections */
[idDropdown, seasonDropdown, plotStyleDropdown, periodDropdown, diffDropdown].forEach(el =>
  el.addEventListener('change', updatePlots)
);

/* Initial load */
updatePlots();
</script>





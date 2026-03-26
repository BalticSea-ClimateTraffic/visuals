---
layout: page
title: Extreme rainfall
---

Here you can explore how intense and heavy precipitation may change across seasons and future periods. The plots show different indicators of extreme rainfall, meaning situations when a large amount of rain or snow falls within a short time. Such events are important because they can affect drainage systems, increase the risk of flooding, and weaken railway foundations and other infrastructure. Some guidance on how to interpret the results is provided below the plots.

The model data are based on high-resolution regional climate simulations using the HARMONIE-Climate model, developed through Nordic collaboration. The projections follow the RCP4.5 emissions scenario, which represents a future with moderate climate mitigation where greenhouse gas emissions peak around mid-century and then gradually decline. Therefore, the results on this page describe plausible mid-range climate change impacts rather than worst-case outcomes.

# How to use
The plots are interactive. First, choose a precipitation index from the drop-down menu. Each index describes a different aspect of heavy rainfall. Then select a season and a plot style.

You can explore two seasons:
- Summer (June–August)
- Winter (December–February)

For map plots, you can also select a future period:
- Mid-century (2041–2060)
- Late-century (2081–2100)

You can optionally display a difference map that shows the ratio between future and historical conditions. This helps to identify where the largest relative changes are projected.

---
Choose:
<div style="margin-bottom: 10px;">

  <!-- Row 1 -->
  <div style="margin-bottom: 6px;">
    <label for="idDropdown">Index: </label>
    <select id="idDropdown">
      <option value="rx1day" selected>Seasonal maximum daily precipitation</option>
      <option value="rx5day">Seasonal maximum 5-day precipitation</option>
      <option value="r20mm">Days with precipitation ≥ 20 mm</option>
      <option value="sdii">Mean precipitation on wet days</option>
    </select>

    <label for="seasonDropdown" style="margin-left: 20px;">Season: </label>
    <select id="seasonDropdown">
      <option value="JJA" selected>Summer (June–August)</option>
      <option value="DJF">Winter (December–February)</option>
    </select>
  </div>

  <!-- Row 2 -->
  <div style="margin-bottom: 6px;">
    <label for="plotStyleDropdown">Plot style: </label>
    <select id="plotStyleDropdown">
      <option value="maps" selected>Maps</option>
      <option value="boxplots">Boxplots</option>
    </select>

    <span id="mapOptions" style="margin-left: 20px;">
      <label for="periodDropdown">Future period: </label>
      <select id="periodDropdown">
        <option value="midcentury" selected>Mid-century (2041–2060)</option>
        <option value="latecentury">Late-century (2081–2100)</option>
      </select>
    </span>
  </div>

  <!-- Row 3 -->
  <div id="diffRow">
    <span id="mapOptionsDiff">
      <label for="diffDropdown">Difference map: </label>
      <select id="diffDropdown">
        <option value="off" selected>Off</option>
        <option value="on">On</option>
      </select>
    </span>
  </div>

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

.plots-row {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
  align-items: start;
}
#col-diff { grid-column: 1 / -1; }
.plot-col { display: flex; flex-direction: column; align-items: center; }
.plot-title { font-weight: normal; margin: 6px 0 8px; }

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

#mapOptions { white-space: nowrap; }
#idDropdown, #seasonDropdown, #plotStyleDropdown,
#periodDropdown, #diffDropdown {
  display: inline-block;
}

label {
  display: inline-block;
  margin-right: 4px;
  font-weight: normal;
}

select {
  display: inline-block;
  margin: 0 12px 0 0;
  padding: 4px 8px;
  font-size: 15px;
}

label, select {
  vertical-align: middle;
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
  plotsRow.style.gridTemplateColumns = `repeat(${count}, 1fr)`;
  colHist.classList.toggle('hidden', count === 1);
  colFuture.classList.remove('hidden');
  colDiff.classList.toggle('hidden', !diffOn);
  colDiff.style.gridColumn = diffOn ? '1 / -1' : '';
}

function updatePlots() {
  const id        = idDropdown.value;
  const season    = seasonDropdown.value;
  const plotStyle = plotStyleDropdown.value;

  const isMaps     = (plotStyle === 'maps');
  const isBoxplots = (plotStyle === 'boxplots');
  
  document.getElementById('mapOptions').style.display = isMaps ? 'inline-block' : 'none';
  document.getElementById('mapOptionsDiff').style.display = isMaps ? 'inline-block' : 'none';


  if (isMaps) {
    plotsRow.classList.remove('hidden');

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

    // allow autosize for maps  
    histFrame.style.height = '';
    futureFrame.style.height = '';
    diffFrame.style.height = '';

    return;

  }

  if (isBoxplots) {
    plotsRow.classList.remove('hidden');

    setColumns(1, false);
    futureTitle.textContent = 'Boxplots';
    futureFrame.src = PATH_PREFIX + buildBoxplotFilename(id, season);

    // set fixed height for boxplots (prevents oversized blank space)
    futureFrame.style.height = '520px';

    histFrame.src = '';
    diffFrame.src = '';
    return;
  }


  histFrame.src = futureFrame.src = diffFrame.src = '';
  plotsRow.classList.add('hidden');
}

[idDropdown, seasonDropdown, plotStyleDropdown, periodDropdown, diffDropdown].forEach(el =>
  el.addEventListener('change', updatePlots)
);
  
/* -------- Auto-resize iframe height based on content -------- */
function attachAutosize(iframe) {
  const resize = () => {
    try {
      const doc = iframe.contentDocument || iframe.contentWindow.document;
      if (!doc) return;

      // Remove default margins
      doc.body.style.margin = '0';

      // Make main containers responsive
      doc.querySelectorAll('div').forEach(el => {
        el.style.maxWidth = '100%';
      });

      // Scale plot elements
      doc.querySelectorAll('img, svg, canvas').forEach(el => {
        el.style.maxWidth = '100%';
        el.style.height = 'auto';
      });

      // Only autosize vertically for maps
      if (plotStyleDropdown.value === 'maps') {
        const h = Math.max(doc.body.scrollHeight, doc.documentElement.scrollHeight);
        iframe.style.height = h + 'px';
      }
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




/* Attach autosize to all plot frames */
[histFrame, futureFrame, diffFrame].forEach(attachAutosize);

updatePlots();
</script>

# Interpretation
The indices describe different characteristics of heavy rainfall events:

- Seasonal maximum daily precipitation: the largest amount of precipitation recorded in a single day within a season  
- Seasonal maximum five-day precipitation: the largest accumulated precipitation over any consecutive five-day period  
- Days with heavy precipitation: the number of days in a season when precipitation reaches at least 20 mm  
- Mean precipitation on wet days: the average precipitation amount on days with measurable precipitation (at least 1 mm)

In general, increasing values in these indices indicate a higher likelihood of intense rainfall events, which may increase the risk of flooding, erosion, and infrastructure damage.

When comparing historical and future maps, areas with strong increases suggest that extreme rainfall events could become more frequent or more intense. For example, an increase in the maximum daily precipitation implies that the heaviest storms may produce larger rainfall totals, even if the total seasonal precipitation does not change substantially. Similarly, more days exceeding 20 mm of precipitation indicate a greater number of heavy rainfall events that may challenge drainage capacity.

Boxplots summarise how the indices vary across regions within each country. A wider box or longer whiskers indicate larger spatial variability, meaning that some locations experience much stronger extremes than others. A shift of the entire box upward from historical to future periods suggests a consistent intensification of extreme precipitation across most regions.

It is important to note that these results describe long-term average conditions. Individual years may still include unusually dry or wet seasons, and short-lived extreme events can occur even in regions where long-term changes are small.

# Data and periods
The results are shown for three main time periods:
- Historical reference period: 1986–2005  
- Mid-century period: 2041–2060  
- Late-century period: 2081–2100  

All projections are based on regional climate model simulations driven by the RCP4.5 emissions pathway. The maps show spatial patterns of the indices, while boxplots illustrate their distribution within each country.

<br><br>
Page author: Laura Utriainen

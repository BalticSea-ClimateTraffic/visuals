---
layout: page
title: Precipitation Indices
---

<h1> CORDEX: Maximum Daily Precipitation & Heavy Precipitation Days </h1>

<p id="metricDesc" style="margin-top:0.5rem;">
  <b>Metric:</b> <br><b><i>Rx1day</i></b> — Maximum daily precipitation.  
  Average (time mean) of the seasonal maximum 1-day precipitation over Europe.
</p>
<p id="metricDesc" style="margin-top:0.5rem;">
  <br> <b><i>R20mm</i></b> — Heavy Precipitation days.  
  Average number of days in any given season when accumulated precipitation is equal or more than 20mm.
</p>


<p>
  <b>Seasons:</b> summer (JJA), winter (DJF), autumn (SON), spring (MAM).<br>
  <b>Periods:</b> Historical (1986–2005), Mid-century (2041–2060), Late-century (2081–2100).
</p>

<label for="metric">Select metric:</label>
<select id="metric" onchange="updatePlot()">
  <option value="rx1day">Maximum daily precipitation (Rx1day)</option>
  <option value="r20mm">Heavy precipitation days ≥20 mm (R20mm)</option>
</select>

<label for="period" style="margin-left:1rem;">Select period:</label>
<select id="period" onchange="updatePlot()">
  <option value="historical">Historical</option>
  <option value="mid-century">Mid-century</option>
  <option value="late-century">Late-century</option>
</select>

<label for="season" style="margin-left:1rem;">Select season:</label>
<select id="season" onchange="updatePlot()">
  <option value="DJF">DJF</option>
  <option value="MAM">MAM</option>
  <option value="JJA">JJA</option>
  <option value="SON">SON</option>
</select>

<br><br>

<div style="position: relative; width: 100%; height: 600px; text-align: center;">

  <div id="spinner" 
       style="display:none; position:absolute; top:50%; left:50%; transform:translate(-50%,-50%);
              border:8px solid #f3f3f3; border-top:8px solid #3498db; border-radius:50%;
              width:60px; height:60px; animation:spin 1s linear infinite;">
  </div>

  <!-- Store the resolved base path in data-base -->
  <img
    id="plotImage"
    data-base="{{ '/CORDEX_PR/' | relative_url }}"
    src="{{ '/CORDEX_PR/PLOT_R20mm_sum_Europe_timmean_late-century_JJA.png' | relative_url }}"
    alt="Climate plot"
    width="100%"
    height="600"
    style="border:none;"
  />
</div>

<style>
@keyframes spin { 0% {transform:rotate(0)} 100% {transform:rotate(360deg)} }
</style>

<script>
(function() {
  // Map UI values -> filename bits + human-friendly text
  const METRIC_MAP = {
    "rx1day": {
      prefix: "PLOT_Rx1day_mean_Europe_timmean",
      label: "Rx1day — Maximum daily precipitation",
      desc: "<b>Metric:</b> <i>Rx1day</i> — Maximum daily precipitation. Average (time mean) of the seasonal maximum 1-day precipitation over Europe."
    },
    "r20mm": {
      prefix: "PLOT_R20mm_sum_Europe_timmean",
      label: "R20mm — Heavy precipitation days (≥20 mm)",
      desc: "<b>Metric:</b> <i>R20mm</i> — Average number of days per season with daily precipitation ≥ 20 mm."
    }
  };

  const PERIOD_MAP = {
    "historical": "historical",
    "mid-century": "mid-century",
    "late-century": "late-century"
  };

  window.updatePlot = function updatePlot() {
    const metricKey = document.getElementById("metric").value;   // "rx1day" | "r20mm"
    const periodUI = document.getElementById("period").value;    // "historical" | "mid-century" | "late-century"
    const season = document.getElementById("season").value;      // "DJF" | "MAM" | "JJA" | "SON"

    const img = document.getElementById("plotImage");
    const spinner = document.getElementById("spinner");
    const metricDesc = document.getElementById("metricDesc");

    // Base path normalization
    let base = img.dataset.base || "";
    base = base.replace(/\/+$/, "") + "/";

    const metric = METRIC_MAP[metricKey];
    const periodToken = PERIOD_MAP[periodUI] || periodUI;

    // Build filename for the chosen metric/period/season
    const filename = `${metric.prefix}_${periodToken}_${season}.png`;
    const newSrc = base + filename;

    // Update description
    metricDesc.innerHTML = metric.desc;

    console.log("Loading plot:", newSrc);
    spinner.style.display = "block";

    const testImg = new Image();
    testImg.onload = function() {
      img.src = newSrc;
      img.alt = `${metric.label} | ${periodUI} | ${season}`;
      spinner.style.display = "none";
    };
    testImg.onerror = function() {
      spinner.style.display = "none";
      alert(`Plot not found:\n${newSrc}\n\nCheck that the file exists with EXACT casing.`);
    };
    testImg.src = newSrc;
  };
})();
</script>

<br><br><br>

Further description about the CORDEX project can be found at:<br>
<a href="https://euro-cordex.net/060378/index.php.en">EURO-CORDEX data</a>

<marquee>Finnish Meteorological Institute</marquee>

<br><br>
Page maintained and updated by <a href="https://en.ilmatieteenlaitos.fi/cv-akash-deshmukh"> Akash Deshmukh </a>

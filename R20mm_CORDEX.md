---
layout: page
title: Maximum Wind Speed (sfcWindmax)
---

<h1>sfcWindmax from CORDEX</h1>
Average seasonal maximum near-surface wind speed.
<p>
<b>Seasons:</b> summer (JJA), winter (DJF), autumn (SON), spring (MAM).
</p>
<p>
<b>Periods:</b> Historical (1986–2005), Mid-century (2041–2060), Late-century (2081–2100).
</p>

<label for="mode">Mode:</label>
<select id="mode" onchange="updateUI(); updatePlot();">
  <option value="absolute" selected>Absolute</option>
  <option value="diff-mid">Difference (mid − historical)</option>
  <option value="diff-late">Difference (late − historical)</option>
</select>

<span id="periodRow">
  <label for="period">Select period:</label>
  <select id="period" onchange="updatePlot()">
    <option value="historical">Historical</option>
    <option value="mid-century">Mid-century</option>
    <option value="late-century">Late-century</option>
  </select>
</span>

<label for="season">Select season:</label>
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

  <!-- Base path now points to CORDEX_PR -->
  <img
    id="plotImage"
    data-base="{{ '/CORDEX_PR/' | relative_url }}"
    src="{{ '/CORDEX_PR/PLOT_sfcWindmax_Europe_timmean_historical_DJF.png' | relative_url }}"
    alt="Wind plot"
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
  // Map UI period values -> exact tokens used in filenames
  const PERIOD_MAP = {
    "historical":   "historical",
    "mid-century":  "mid-century",   // change if your files use e.g. "mid_century"
    "late-century": "late-century"
  };

  // Show/hide period selector depending on "Mode"
  window.updateUI = function updateUI() {
    const mode = document.getElementById("mode").value;
    const periodRow = document.getElementById("periodRow");
    periodRow.style.display = (mode === "absolute") ? "inline-block" : "none";
  };

  // Build filename for the current selection
  function buildFilename(basePath, mode, periodUI, season) {
    const seasonTok = season; // "DJF" | "MAM" | "JJA" | "SON"

    if (mode === "absolute") {
      const periodTok = PERIOD_MAP[periodUI] || periodUI;
      // Absolute file pattern (from CORDEX_PR):
      // PLOT_sfcWindmax_Europe_timmean_<period>_<season>.png
      return basePath + `PLOT_sfcWindmax_Europe_timmean_${periodTok}_${seasonTok}.png`;
    }

    // Difference file pattern (from CORDEX_PR):
    // diff_sfcWindmax_<season>_<future>-minus-hist.png
    if (mode === "diff-mid") {
      return basePath + `diff_sfcWindmax_${seasonTok}_mid-minus-hist.png`;
    }
    if (mode === "diff-late") {
      return basePath + `diff_sfcWindmax_${seasonTok}_late-minus-hist.png`;
    }

    // Fallback
    return basePath + `PLOT_sfcWindmax_Europe_timmean_historical_${seasonTok}.png`;
  }

  window.updatePlot = function updatePlot() {
    const mode    = document.getElementById("mode").value;
    const period  = document.getElementById("period").value;
    const season  = document.getElementById("season").value;

    const img     = document.getElementById("plotImage");
    const spinner = document.getElementById("spinner");

    let base = img.dataset.base || "";
    base = base.replace(/\/+$/, "") + "/";

    const newSrc = buildFilename(base, mode, period, season);

    spinner.style.display = "block";

    const testImg = new Image();
    testImg.onload = function() {
      img.src = newSrc;
      const label =
        (mode === "absolute")
          ? `sfcWindmax — ${period} — ${season}`
          : (mode === "diff-mid")
              ? `Difference (mid − historical) — ${season} — sfcWindmax`
              : `Difference (late − historical) — ${season} — sfcWindmax`;
      img.alt = label;
      spinner.style.display = "none";
    };
    testImg.onerror = function() {
      spinner.style.display = "none";
      alert(`Plot not found:\n${newSrc}\n\nCheck that the file exists with EXACT spelling and casing.`);
    };
    testImg.src = newSrc;
  };

  // Initialize controls
  updateUI();
})();
</script>

<br><br><br>

Further description about the CORDEX project can be found on the following link:<br>
<a href="https://euro-cordex.net/060378/index.php.en">EURO-CORDEX data</a>

<marquee>Finnish Meteorological Institute</marquee>

<br><br>
Page author: Akash Deshmukh

---
layout: page
title: Maximum Wind Speed (sfcWindmax)
---

<h1> sfcWindmax from CORDEX</h1>
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

  <!-- Store the resolved base path in data-base -->
  <img
    id="plotImage"
    data-base="{{ '/CORDEX_WIND/' | relative_url }}"
    src="{{ '/CORDEX_WIND/PLOT_sfcWindmax_Europe_timmean_historical_DJF.png' | relative_url }}"
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
  // Map UI period values -> exact filename tokens you use on disk
  const PERIOD_MAP = {
    "historical":   "historical",
    "mid-century":  "mid-century",   // adjust if your files use a different spelling (e.g., mid_century)
    "late-century": "late-century"
  };

  // Helper: show/hide period selector when mode changes
  window.updateUI = function updateUI() {
    const mode = document.getElementById("mode").value;
    const periodRow = document.getElementById("periodRow");
    // Hide period for difference modes; show for absolute
    periodRow.style.display = (mode === "absolute") ? "inline-block" : "none";
  };

  // Build filename based on UI
  function buildFilename(basePath, mode, periodUI, season) {
    const seasonTok = season; // "DJF" | "MAM" | "JJA" | "SON"

    if (mode === "absolute") {
      const periodTok = PERIOD_MAP[periodUI] || periodUI;
      // Absolute filename pattern:
      // PLOT_sfcWindmax_Europe_timmean_<period>_<season>.png
      return basePath + `PLOT_sfcWindmax_Europe_timmean_${periodTok}_${seasonTok}.png`;
    }

    // Difference filename patterns (choose one future vs historical)
    // diff_sfcWindmax_<season>_<future>-minus-hist.png
    if (mode === "diff-mid") {
      return basePath + `diff_sfcWindmax_${seasonTok}_mid-minus-hist.png`;
    }
    if (mode === "diff-late") {
      return basePath + `diff_sfcWindmax_${seasonTok}_late-minus-hist.png`;
    }

    // Fallback to absolute historical if something unexpected happens
    return basePath + `PLOT_sfcWindmax_Europe_timmean_historical_${seasonTok}.png`;
  }

  window.updatePlot = function updatePlot() {
    const mode    = document.getElementById("mode").value;      // absolute | diff-mid | diff-late
    const period  = document.getElementById("period").value;    // only used for absolute
    const season  = document.getElementById("season").value;

    const img     = document.getElementById("plotImage");
    const spinner = document.getElementById("spinner");

    let base = img.dataset.base || "";
    base = base.replace(/\/+$/, "") + "/";

    const newSrc = buildFilename(base, mode, period, season);

    console.log("Loading plot:", newSrc);
    spinner.style.display = "block";

    // Preload to avoid flicker / broken images
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
      alert(`Plot not found:\n${newSrc}\n\nCheck that the file exists with EXACT casing.`);
    };
    testImg.src = newSrc;
  };

  // Initialize UI state on load
  updateUI();
})();
</script>

<br><br><br>

Further description about the CORDEX project can be found on the following link:<br>
<a href="https://euro-cordex.net/060378/index.php.en">EURO-CORDEX data</a>

<marquee>Finnish Meteorological Institute</marquee>

<br><br>
Page author: Akash Deshmukh

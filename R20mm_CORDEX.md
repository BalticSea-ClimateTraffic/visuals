---
layout: page
title: Wind Speed
---

<h1>Maximum surface wind speed from CORDEX</h1>
Average seasonal maximum near-surface wind speed (m/s).
<p>
<b>Seasons:</b> summer (JJA), winter (DJF), autumn (SON), spring (MAM).
</p>
<p>
<b>Periods:</b> Historical (1986–2005), Mid-century (2041–2060), Late-century (2081–2100).
</p>

<b><label for="mode">Mode:</label></b> 
<select id="mode" onchange="updateUI(); updatePlot();">
  <option value="absolute" selected>Absolute</option>
  <option value="diff-mid">Difference (mid − historical)</option>
  <option value="diff-late">Difference (late − historical)</option>
</select>

<span id="periodRow">
 <b> <label for="period">Select period:</label></b> 
  <select id="period" onchange="updatePlot()">
    <option value="hist">Historical</option>
    <option value="mid">Mid-century</option>
    <option value="late">Late-century</option>
  </select>
</span>

<b><label for="season">Select season:</label></b> 
<select id="season" onchange="updatePlot()">
  <option value="DJF">DJF</option>
  //<option value="MAM">MAM</option>
  <option value="JJA">JJA</option>
  //<option value="SON">SON</option>
</select>

<br><br>

<div style="position: relative; width: 100%; height: 600px; text-align: center;">
  <div id="spinner" 
       style="display:none; position:absolute; top:50%; left:50%; transform:translate(-50%,-50%);
              border:8px solid #f3f3f3; border-top:8px solid #3498db; border-radius:50%;
              width:60px; height:60px; animation:spin 1s linear infinite;">
  </div>

  <!-- Base path: CORDEX_PR -->
  <img
    id="plotImage"
    data-base="{{ '/CORDEX_PR/' | relative_url }}"
    src="{{ '/CORDEX_PR/hist_DJF_mean_1986-2005_subset_map.png' | relative_url }}"
    alt="sfcWindmax — Historical — DJF"
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
  // Years used in your absolute filenames
  const YEARS = {
    hist: "1986-2005",
    mid:  "2041-2060",
    late: "2081-2100"
  };

  // Show/hide "period" when switching mode
  window.updateUI = function updateUI() {
    const mode = document.getElementById("mode").value;
    const periodRow = document.getElementById("periodRow");
    periodRow.style.display = (mode === "absolute") ? "inline-block" : "none";
  };

  // Build filename based on your actual patterns
  function buildFilename(basePath, mode, periodKey, season) {
    const seasonTok = season; // DJF | MAM | JJA | SON

    if (mode === "absolute") {
      // <scenario>_<SEASON>_mean_<years>_subset_map.png
      const yrs = YEARS[periodKey];
      const scen = periodKey; // hist | mid | late
      return basePath + `${scen}_${seasonTok}_mean_${yrs}_subset_map.png`;
    }

    // Differences already match your names:
    // diff_sfcWindmax_<SEASON>_<future>-minus-hist.png
    if (mode === "diff-mid") {
      return basePath + `diff_sfcWindmax_${seasonTok}_mid-minus-hist.png`;
    }
    if (mode === "diff-late") {
      return basePath + `diff_sfcWindmax_${seasonTok}_late-minus-hist.png`;
    }

    // Fallback
    return basePath + `hist_${seasonTok}_mean_${YEARS.hist}_subset_map.png`;
  }

  window.updatePlot = function updatePlot() {
    const mode    = document.getElementById("mode").value;   // absolute | diff-mid | diff-late
    const period  = document.getElementById("period").value; // hist | mid | late (absolute only)
    const season  = document.getElementById("season").value; // DJF|MAM|JJA|SON

    const img     = document.getElementById("plotImage");
    const spinner = document.getElementById("spinner");

    let base = img.dataset.base || "";
    base = base.replace(/\/+$/, "") + "/";

    const newSrc = buildFilename(base, mode, period, season);

    spinner.style.display = "block";

    const testImg = new Image();
    testImg.onload = function() {
      img.src = newSrc;

      // Pretty labels
      const periodLabel = (period === "hist") ? "Historical"
                          : (period === "mid") ? "Mid-century"
                          : "Late-century";

      const label =
        (mode === "absolute")
          ? `sfcWindmax — ${periodLabel} — ${season}`
          : (mode === "diff-mid")
              ? `Difference (mid − historical) — ${season} — sfcWindmax`
              : `Difference (late − historical) — ${season} — sfcWindmax`;

      img.alt = label;
      spinner.style.display = "none";
    };
    testImg.onerror = function() {
      spinner.style.display = "none";
      alert(`Plot not found:\n${newSrc}\n\nCheck that the file exists with EXACT spelling/casing.`);
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


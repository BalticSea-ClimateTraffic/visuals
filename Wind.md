---
layout: page
title: Wind
---

Maximum surface wind speed from CORDEX
Average seasonal maximum near-surface wind speed (m/s).
<p>
<b>Seasons:</b> summer (JJA) and winter (DJF)
</p>
<p>
<b>Periods:</b> Historical (1986–2005), Mid-century (2041–2060), Late-century (2081–2100).
</p>


<div style="margin-bottom: 15px;">
  <label for="mode1">Mode: </label>
  <select id="mode1">
    <option value="absolute" selected>Absolute</option>
    <option value="diff-mid">Difference (mid − historical)</option>
    <option value="diff-late">Difference (late − historical)</option>
  </select>

  <span id="periodRow1" style="margin-left: 15px;">
    <label for="period1">Period: </label>
    <select id="period1">
      <option value="hist">Historical</option>
      <option value="mid">Mid-century</option>
      <option value="late">Late-century</option>
    </select>
  </span>

  <label for="season1" style="margin-left: 15px;">Season: </label>
  <select id="season1">
    <option value="DJF">DJF</option>
    <!-- <option value="MAM">MAM</option> -->
    <option value="JJA">JJA</option>
    <!-- <option value="SON">SON</option> -->
  </select>
</div>

<--<iframe
  id="plotFrame1"
  data-base="{{ '/CORDEX_PR/' | relative_url }}"
  src="{{ '/CORDEX_PR/hist_DJF_mean_1986-2005_subset_map.html' | relative_url }}"
  width="100%"
  height="600px"
  style="border:none; opacity:1; transition: opacity 0.5s;"
></iframe> -->

<iframe
  id="plotFrame1"
  data-base="{{ '/Winds/' | relative_url }}"
  src="{{ '/Winds/hist_DJF_mean_1986-2005_map.html' | relative_url }}"
  width="100%"
  height="600px"
  style="border:none; opacity:1; transition: opacity 0.5s;"
></iframe>

<--<script>
(function () {
  // Years used in your absolute filenames
  const YEARS = {
    hist: "1986-2005",
    mid:  "2041-2060",
    late: "2081-2100"
  };

  const modeSelect1   = document.getElementById('mode1');
  const periodSelect1 = document.getElementById('period1');
  const seasonSelect1 = document.getElementById('season1');
  const periodRow1    = document.getElementById('periodRow1');
  const iframe1       = document.getElementById('plotFrame1');

  // Show/hide period selector depending on mode
  function updateUI1() {
    const mode = modeSelect1.value;
    periodRow1.style.display = (mode === "absolute") ? "inline-block" : "none";
  }

  // Build filename based on your actual patterns
  function buildFilename(basePath, mode, periodKey, season) {
    const seasonTok = season; // DJF | JJA

    if (mode === "absolute") {
      // <scenario>_<SEASON>_mean_<years>_subset_map.html
      const yrs = YEARS[periodKey];
      const scen = periodKey; // hist | mid | late
      return basePath + `${scen}_${seasonTok}_mean_${yrs}_subset_map.html`;
    }

    // Differences:
    // diff_sfcWindmax_<SEASON>_<future>-minus-hist.html
    if (mode === "diff-mid") {
      return basePath + `diff_sfcWindmax_${seasonTok}_mid-minus-hist.html`;
    }
    if (mode === "diff-late") {
      return basePath + `diff_sfcWindmax_${seasonTok}_late-minus-hist.html`;
    }

    // Fallback
    return basePath + `hist_${seasonTok}_mean_${YEARS.hist}_subset_map.html`;
  }

  function updatePlot1() {
    const mode   = modeSelect1.value;   // absolute | diff-mid | diff-late
    const period = periodSelect1.value; // hist | mid | late
    const season = seasonSelect1.value; // DJF|JJA

    let base = iframe1.dataset.base || "";
    base = base.replace(/\/+$/, "") + "/";

    const newSrc = buildFilename(base, mode, period, season);

    // Fade-out, swap src, fade-in
    iframe1.style.opacity = 0;
    setTimeout(() => {
      iframe1.src = newSrc;
      iframe1.onload = () => {
        iframe1.style.opacity = 1;
      };
    }, 400);
  }

  modeSelect1.addEventListener('change', function () {
    updateUI1();
    updatePlot1();
  });
  periodSelect1.addEventListener('change', updatePlot1);
  seasonSelect1.addEventListener('change', updatePlot1);

  // Initialize UI and plot
  updateUI1();
})();
</script> -->


<script>
(function () {

  const YEARS = {
    hist: "1986-2005",
    mid:  "2041-2060",
    late: "2081-2100"
  };

  const modeSelect1   = document.getElementById('mode1');
  const periodSelect1 = document.getElementById('period1');
  const seasonSelect1 = document.getElementById('season1');
  const periodRow1    = document.getElementById('periodRow1');
  const iframe1       = document.getElementById('plotFrame1');

  function updateUI1() {
    const mode = modeSelect1.value;
    periodRow1.style.display = (mode === "absolute") ? "inline-block" : "none";
  }

  function buildFilename(basePath, mode, periodKey, season) {

    // ✅ ABSOLUTE FILES
    // hist_DJF_mean_1986-2005_map.html
    // mid_JJA_mean_2041-2060_map.html
    // late_JJA_mean_2081-2100_map.html
    if (mode === "absolute") {
      const yrs = YEARS[periodKey];
      return basePath + `${periodKey}_${season}_mean_${yrs}_map.html`;
    }

    // ✅ MID DIFFERENCE FILES
    // diff_mid_DJF_mean_2041-2060_minus_hist_DJF_mean_1986-2005.html
    if (mode === "diff-mid") {
      return basePath +
        `diff_mid_${season}_mean_2041-2060_minus_hist_${season}_mean_1986-2005.html`;
    }

    // ✅ LATE DIFFERENCE FILES
    // diff_late_JJA_mean_2081-2100_minus_hist_JJA_mean_1986-2005.html
    if (mode === "diff-late") {
      return basePath +
        `diff_late_${season}_mean_2081-2100_minus_hist_${season}_mean_1986-2005.html`;
    }

    // ✅ Fallback
    return basePath + `hist_${season}_mean_1986-2005_map.html`;
  }

  function updatePlot1() {
    const mode   = modeSelect1.value;
    const period = periodSelect1.value;
    const season = seasonSelect1.value;

    let base = iframe1.dataset.base || "";
    base = base.replace(/\/+$/, "") + "/";

    const newSrc = buildFilename(base, mode, period, season);

    iframe1.style.opacity = 0;
    setTimeout(() => {
      iframe1.src = newSrc;
      iframe1.onload = () => {
        iframe1.style.opacity = 1;
      };
    }, 400);
  }

  modeSelect1.addEventListener('change', function () {
    updateUI1();
    updatePlot1();
  });

  periodSelect1.addEventListener('change', updatePlot1);
  seasonSelect1.addEventListener('change', updatePlot1);

  updateUI1();
})();
</script>


<br>





<br><br><br>

Further description about the CORDEX project can be found on the following link:<br>
<a href="https://euro-cordex.net/060378/index.php.en">EURO-CORDEX data</a>

<marquee>Finnish Meteorological Institute</marquee>

<br><br>


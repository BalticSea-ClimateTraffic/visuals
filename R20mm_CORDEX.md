---
layout: page
title: Heavy Precipitation Days
---

<h1> R20mm from CORDEX</h1>
Average number of days in any given season when accumulated precipitation is equal or more than 20mm. 
<p>
<b>Seasons:</b> summer (JJA), winter (DJF), Autumn (SON) and Spring (MAM).
</p>
<p>
<b>Periods: </b> Historical (1986–2005), Mid-century (2041–2060), Late-century (2081–2100).
</p>

<label for="period">Select period:</label>
<select id="period" onchange="updatePlot()">
  <option value="historical">Historical</option>
  <option value="mid-century">Mid-century</option>
  <option value="late-century">Late-century</option>
</select>

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
    data-base="{{ '/CORDEX_PR/' | relative_url }}"
    src="{{ '/CORDEX_PR/PLOT_R20mm_sum_Europe_timmean_historical_DJF.png' | relative_url }}"
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
  // Map UI values -> exact filename tokens
  const PERIOD_MAP = {
    "historical": "historical",
    "mid-century": "mid-century",   // <-- change to match your actual files (mid-century, mid_century, midcentury)
    "late-century": "late-century"  // <-- change to match your actual files
  };

  // If your real filenames actually use hyphens, use:
  // "mid-century": "mid-century",
  // "late-century": "late-century",

  window.updatePlot = function updatePlot() {
    const periodUI = document.getElementById("period").value;  // "historical" | "mid-century" | "late-century"
    const season = document.getElementById("season").value;    // "DJF" | "MAM" | "JJA" | "SON"

    const img = document.getElementById("plotImage");
    const spinner = document.getElementById("spinner");

    
    let base = img.dataset.base || "";
    base = base.replace(/\/+$/, "") + "/";

    
    const periodToken = PERIOD_MAP[periodUI] || periodUI;

    
    const filename = `PLOT_R20mm_sum_Europe_timmean_${periodToken}_${season}.png`;
    const newSrc = base + filename;

    console.log("Loading plot:", newSrc);

    spinner.style.display = "block";

    
    const testImg = new Image();
    testImg.onload = function() {
      img.src = newSrc;
      img.alt = `Plot for ${periodUI} - ${season}`;
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

Further description about the CORDEX project can be found on following link:
<a href="https://euro-cordex.net/060378/index.php.en"> EURO-CORDEX data </a>

<marquee>  Finnish Meteorological Institute </marquee> 

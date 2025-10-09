---
layout: page
title: Heavy Precipitation Days
---

<h1>Heavy Precipitation days</h1>

<p>
Projected precipitation changes on daily scale for two seasons: summer (JJA) and winter (DJF).
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
function updatePlot() {
  const period = document.getElementById("period").value;  // "historical" | "mid-century" | "late-century"
  const season = document.getElementById("season").value;  // "DJF" | "MAM" | "JJA" | "SON"

  const img = document.getElementById("plotImage");
  const spinner = document.getElementById("spinner");
  const base = img.dataset.base.replace(/\/+$/, '') + '/';

  // Build filename EXACTLY like your stored files
  const filename = `PLOT_R20mm_sum_Europe_timmean_${period}_${season}.png`;
  const newSrc = base + filename;

  spinner.style.display = "block";

  // Set handlers BEFORE changing src
  img.onload = () => { spinner.style.display = "none"; };
  img.onerror = () => {
    spinner.style.display = "none";
    alert(`Plot not found: ${newSrc}`);
  };

  img.src = newSrc;
  img.alt = `Plot for ${period} - ${season}`;
}
</script>

<br><br><br>

Further description about the data, model used etc. <br>

Page Author: me, myself and I  

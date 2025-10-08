---
layout: page 
title: Heavy Precipitation Days
---


# Heavy Precipitation days

Projected precipitation changes on daily scale for two seasons: summer (JJA) and winter (DJF). The spatial means are calculated for periods: historical (1986–2005), mid-century (2041–2060), late-century (2081–2100) using the data from high resolution regional climate model HARMONIE-Climate. The data was produced in a Nordic collaboration project 2020.

Select a precipitation index, a season, a plot style, and a future period to compare against the historical baseline.

Indices:
Rx1day = Seasonal maximum daily precipitation
Rx5day = Seasonal maximum 5-day precipitation
R20mm = Days when precipitation intensity is 20 mm or more

<h3>Climate plot</h3>

<!-- Dropdown controls -->
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

<!-- Container for image and spinner -->
<div style="position: relative; width: 100%; height: 600px; text-align: center;">

  <!-- Spinner -->
  <div id="spinner" 
       style="
         display: none;
         position: absolute;
         top: 50%;
         left: 50%;
         transform: translate(-50%, -50%);
         border: 8px solid #f3f3f3;
         border-top: 8px solid #3498db;
         border-radius: 50%;
         width: 60px;
         height: 60px;
         animation: spin 1s linear infinite;">
  </div>

  <!-- Image -->
  <img 
    id="plotImage"
    src="{{ '/CORDEX_PR/PLOT_R20mm_sum_Europe_timmean_historical_DJF.png' | relative_url }}"
    alt="Climate plot"
    width="100%"
    height="600"
    style="border:none;"
  />

</div>

<!-- Spinner animation -->
<style>
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>

<script>
function updatePlot() {
  const period = document.getElementById("period").value;
  const season = document.getElementById("season").value;
  const plotImg = document.getElementById("plotImage");
  const spinner = document.getElementById("spinner");

  // Show the spinner
  spinner.style.display = "block";

  // Build the filename dynamically
  const filename = `{{ '/CORDEX_PR/' | relative_url }}PLOT_R20mm_sum_Europe_timmean_${period}_${season}.png`;

  // When image finishes loading, hide spinner
  plotImg.onload = () => {
    spinner.style.display = "none";
  };

  // In case the image fails to load
  plotImg.onerror = () => {
    spinner.style.display = "none";
    alert("⚠️ Plot not found for this combination.");
  };

  // Update the image source and alt text
  plotImg.src = filename;
  plotImg.alt = `Plot for ${period} - ${season}`;
}
</script>

<br><br><br>

Further description about the data, model used etc. <br>

Page Author: me, myself and I  

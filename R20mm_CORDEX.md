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

<br><br>

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

<!-- Image for plot -->
<img 
  id="plotImage"
  src="{{ '/CORDEX_PR/PLOT_R20mm_sum_Europe_timmean_historical_DJF.png' | relative_url }}"
  alt="Climate plot"
  width="100%"
  height="600"
  style="border:none;"
/>

<script>
function updatePlot() {
  const period = document.getElementById("period").value;
  const season = document.getElementById("season").value;

  // Build the filename dynamically
  const filename = `{{ '/CORDEX_PR/' | relative_url }}PLOT_R20mm_sum_Europe_timmean_${period}_${season}.png`;

  const plotImg = document.getElementById("plotImage");
  plotImg.src = filename;
  plotImg.alt = `Plot for ${period} - ${season}`;
}
</script>

<br><br><br>
Further description about the data, model used etc. <br>

Page Author: me, myself and I  

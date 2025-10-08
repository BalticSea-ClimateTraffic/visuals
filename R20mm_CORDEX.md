---
layout: page 
title: Heavy Precipitation
---


# Summer-time Precipitation

This is a description text lalala. 

<br><br>

<!-- Dropdown controls -->
<label for="period">Select period:</label>
<select id="period" onchange="updatePlot()">
  <option value="historical">Historical</option>
  <option value="mid-century">Mid-century</option>
</select>

<label for="season">Select season:</label>
<select id="season" onchange="updatePlot()">
  <option value="DJF">DJF</option>
  <option value="MAM">MAM</option>
  <option value="JJA">JJA</option>
  <option value="SON">SON</option>
</select>

<br><br>

<!-- Iframe for plot -->
<iframe id="plotFrame" 
        src="PLOT_historical_DJF.png" 
        width="100%" 
        height="600" 
        style="border:none;">
</iframe>

<script>
function updatePlot() {
  // get dropdown values
  const period = document.getElementById("period").value;
  const season = document.getElementById("season").value;

  // construct file name based on convention
  const filename = `PLOT_${period}_${season}.png`;

  // update iframe
  document.getElementById("plotFrame").src = filename;
}
</script>

<br><br><br>
Further description about the data, model used etc. <br>

Page Author: me, myself and I  

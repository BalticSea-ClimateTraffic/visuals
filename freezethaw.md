---
layout: page
title: Freeze-Thaw Cycles
---

Interactive plots about freeze-thaw cycles (zero-degree crossings) per day


## Interactive Plots

<div style="margin-bottom: 15px;">
  <label for="period1">Period: </label>
  <select id="period1">
    <option value="hist">Historical</option>
    <option value="rect">Recent</option>
    <option value="midc">Mid-Century</option>
  </select>

  <label for="season1" style="margin-left: 15px;">Season: </label>
  <select id="season1">
    <option value="DJF">DJF</option>
    <option value="MAM">MAM</option>
    <option value="JJA">JJA</option>
    <option value="SON">SON</option>
  </select>


<iframe id="plotFrame1" src="PLOTS_Nadine/PLOT_interactive_ZDCs_perDay_hist_DJF.html" 
        width="100%" 
        height="490px" 
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<script>
  const periodSelect1 = document.getElementById('period1');
  const seasonSelect1 = document.getElementById('season1');
  const iframe1       = document.getElementById('plotFrame1');

  function updatePlot1() {
    const period = periodSelect1.value;
    const season = seasonSelect1.value;

    const newSrc = `PLOTS_Nadine/PLOT_interactive_ZDCs_perDay_${period}_${season}.html`;

    iframe1.style.opacity = 0;
    setTimeout(() => {
      iframe1.src = newSrc;
      iframe1.onload = () => { iframe1.style.opacity = 1; };
    }, 400);
  }

  periodSelect1.addEventListener('change', updatePlot1);
  seasonSelect1.addEventListener('change', updatePlot1);
</script>



<br><br><br>
## Further information

Used scenario: RCP 8.5 (worst-case climate change scenario)
Used models: EC-Earth3/Era-Interim, HCLIM ALADIN cy38, FMI-RoadSurf <br><br>

Periods: <br>
- "Historical": 1986-2005, <br>
- "Recent": 1999-2018, <br>
- "Mid-Century": 2041-2060<br><br>

Seasons: <br>
- "DJF": meteorological Winter (December-February), <br>
- "MAM": meteorological Spring (March-May), <br>
- "JJA": meteorological Summer (June-August), <br>
- "SON": meteorological Autumn (September-November)<br><br>


Page Author: Nadine-Cyra Freistetter
Sources: model runs for paper https://doi.org/10.1007/s10113-022-01920-4
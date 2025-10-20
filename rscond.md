---
layout: page 
title: Road Cover
---

Seasonal average road surface cover/condition (on asphalt) ranging from dry, moist, or wet, to slush, frost, partly icy or icy, and snow.<br>
More information on the bottom of the page.

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
    <option value="DJF">Winter</option>
    <option value="MAM">Spring</option>
    <option value="JJA">Summer</option>
    <option value="SON">Autumn</option>
  </select>

  <label for="type1" style="margin-left: 15px;">Road Surface Condition: </label>
  <select id="type1">
    <option value="dry">Dry road</option>
    <option value="snowy">Snow on road</option>
    <option value="icy">Icy or partly icy road</option>
  </select>
</div>

<iframe id="plotFrame1" src="PLOTS_Nadine/PLOT_interactive_GSCond_hist_DJF_dry.html" 
        width="100%" 
        height="600px" 
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<script>
  const periodSelect1 = document.getElementById('period1');
  const seasonSelect1 = document.getElementById('season1');
  const typeSelect1   = document.getElementById('type1');
  const iframe1       = document.getElementById('plotFrame1');

  function updatePlot1() {
    const period = periodSelect1.value;
    const season = seasonSelect1.value;
    const type   = typeSelect1.value;

    const newSrc = `PLOTS_Nadine/PLOT_interactive_GSCond_${period}_${season}_${type}.html`;

    iframe1.style.opacity = 0;
    setTimeout(() => {
      iframe1.src = newSrc;
      iframe1.onload = () => { iframe1.style.opacity = 1; };
    }, 400);
  }

  periodSelect1.addEventListener('change', updatePlot1);
  seasonSelect1.addEventListener('change', updatePlot1);
  typeSelect1.addEventListener('change', updatePlot1);
</script>



<br>
## Further information

Used scenario: RCP 8.5 (worst-case climate change scenario)<br>
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

Surface condition on the road (asphalt)<br>
1=dry, 2=moist, 3=wet, 4=slush, 5=frost, 6=partly icy, 7=icy, 8=snow<br><br>


Page Author: Nadine-Cyra Freistetter <br>
Sources: model runs for paper https://doi.org/10.1007/s10113-022-01920-4
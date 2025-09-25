---
layout: page 
title: Precipitation-Type
---

Average Phase of Precipitation during Season <br><br>

Periods: <br>
- "Historical": 1986-2005, <br>
- "Recent": 1999-2018, <br>
- "Mid-Century": 2041-2060<br><br>

Seasons: <br>
- "DJF": meteorological Winter (December-February), <br>
- "MAM": meteorological Spring (March-May), <br>
- "JJA": meteorological Summer (June-August), <br>
- "SON": meteorological Autumn (September-November)<br><br>

Precipitation Phase/Type:
- "water": rain, <br>
- "sleet": rain containing some ice, <br>
- "snow": snow<br><br>



## Interactive Plots


<div style="margin-bottom: 15px;">
  <label for="period">Period: </label>
  <select id="period">
    <option value="hist">Historical</option>
    <option value="rect">Recent</option>
    <option value="midc">Mid-Century</option>
  </select>

  <label for="season" style="margin-left: 15px;">Season: </label>
  <select id="season">
    <option value="DJF">DJF</option>
    <option value="MAM">MAM</option>
    <option value="JJA">JJA</option>
    <option value="SON">SON</option>
  </select>

  <label for="type" style="margin-left: 15px;">Precipitation Phase: </label>
  <select id="type">
    <option value="water">Water</option>
    <option value="snow">Snow</option>
  </select>
</div>



<iframe id="plotFrame" src="PLOT_interactive_GPType_hist_DJF_water.html" 
        width="100%" 
        height="490px" 
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>



<script>
  const periodSelect = document.getElementById('period');
  const seasonSelect = document.getElementById('season');
  const typeSelect = document.getElementById('type');
  const iframe = document.getElementById('plotFrame');

  function updatePlot() {
    const period = periodSelect.value;
    const season = seasonSelect.value;
    const type = typeSelect.value;

    const newSrc = `PLOT_interactive_GPType_${period}_${season}_${type}.html`;

    // Fade out
    iframe.style.opacity = 0;
    setTimeout(() => {
      iframe.src = newSrc;
      // Fade in
      iframe.onload = () => { iframe.style.opacity = 1; };
    }, 400);
  }

  periodSelect.addEventListener('change', updatePlot);
  seasonSelect.addEventListener('change', updatePlot);
  typeSelect.addEventListener('change', updatePlot);
</script>

<br><br><br>






## Static Plots


<div style="margin-bottom: 15px;">
  <label for="period">Period: </label>
  <select id="period">
    <option value="hist">Historical</option>
    <option value="rect">Recent</option>
    <option value="midc">Mid-Century</option>
  </select>

  <label for="season" style="margin-left: 15px;">Season: </label>
  <select id="season">
    <option value="DJF">DJF</option>
    <option value="MAM">MAM</option>
    <option value="JJA">JJA</option>
    <option value="SON">SON</option>
  </select>

  <label for="type" style="margin-left: 15px;">Type: </label>
  <select id="type">
    <option value="water">Water</option>
    <option value="snow">Snow</option>
  </select>
</div>

<iframe id="plotFrame" src="PLOT_static_GPType_hist_DJF_water.html" 
        width="100%" 
        height="900px" 
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<script>
  const periodSelect = document.getElementById('period');
  const seasonSelect = document.getElementById('season');
  const typeSelect = document.getElementById('type');
  const iframe = document.getElementById('plotFrame');

  function updatePlot() {
    const period = periodSelect.value;
    const season = seasonSelect.value;
    const type = typeSelect.value;

    const newSrc = `PLOT_static_GPType_${period}_${season}_${type}.html`;

    // Fade out
    iframe.style.opacity = 0;
    setTimeout(() => {
      iframe.src = newSrc;
      // Fade in
      iframe.onload = () => { iframe.style.opacity = 1; };
    }, 400);
  }

  periodSelect.addEventListener('change', updatePlot);
  seasonSelect.addEventListener('change', updatePlot);
  typeSelect.addEventListener('change', updatePlot);
</script>




<br><br><br>
## Further information

Used scenario: RCP 8.5 (worst-case climate change scenario)
Used models: EC-Earth3/Era-Interim, HCLIM ALADIN cy38, FMI-RoadSurf 
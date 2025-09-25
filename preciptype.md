---
layout: page 
title: Precipitation-Type
---

Average Phase of Precipitation during Season <br><br>
Interactive & static plots.<br>
For more explanation, see bottom of the page.




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

  <label for="type1" style="margin-left: 15px;">Precipitation Phase: </label>
  <select id="type1">
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
  const periodSelect = document.getElementById('period1');
  const seasonSelect = document.getElementById('season1');
  const typeSelect = document.getElementById('type1');
  const iframe = document.getElementById('plotFrame');

  function updatePlot() {
    const period = periodSelect.value;
    const season = seasonSelect.value;
    const type = typeSelect.value;

    const newSrc = `PLOT_interactive_GPType_${period1}_${season1}_${type1}.html`;

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
  <label for="period2">Period: </label>
  <select id="period2">
    <option value="hist">Historical</option>
    <option value="rect">Recent</option>
    <option value="midc">Mid-Century</option>
  </select>

  <label for="season2" style="margin-left: 15px;">Season: </label>
  <select id="season2">
    <option value="DJF">DJF</option>
    <option value="MAM">MAM</option>
    <option value="JJA">JJA</option>
    <option value="SON">SON</option>
  </select>

  <label for="type2" style="margin-left: 15px;">Type: </label>
  <select id="type2">
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
  const periodSelect = document.getElementById('period2');
  const seasonSelect = document.getElementById('season2');
  const typeSelect = document.getElementById('typ2e');
  const iframe = document.getElementById('plotFrame');

  function updatePlot() {
    const period = periodSelect.value;
    const season = seasonSelect.value;
    const type = typeSelect.value;

    const newSrc = `PLOT_static_GPType_${period2}_${season2}_${type2}.html`;

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

Precipitation Phase/Type:
- "water": rain, <br>
- "sleet": rain containing some ice, <br>
- "snow": snow<br><br>
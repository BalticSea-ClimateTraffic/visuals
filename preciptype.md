---
layout: page 
title: Precipitation type
---



Here you can explore how different types of precipitation may change across time and seasons. The plot shows the precipitation type, meaning whether precipitation falls as water (rain), sleet (rain mixed with ice), or snow. These forms depend strongly on temperature and are important for understanding weather conditions, climate impacts, and everyday activities such as driving or walking.<br>
<br>
The model data used here come from the study “Climate change impacts on future driving and walking conditions in Finland, Norway and Sweden” (Reg Environ Change, 2022). The data are based on climate model simulations using the RCP 8.5 scenario, which represents a high greenhouse gas emissions pathway and is often referred to as a worst-case climate change scenario. Therefore, the results on this page should be used as extreme-case estimates. <br>
<br>

# How to use
The plot is fully interactive. <br>
First, use the drop-down menus to choose a period, a season, and a precipitation phase. 
You can explore three time periods Historical (1986–2005), Recent (1999–2018), and Mid-Century (2041–2060), in four meteorological seasons <br>
- Winter (DJF): December–February<br>
- Spring (MAM): March–May<br>
- Summer (JJA): June–August<br>
- Autumn (SON): September–November<br>
This allows you to compare past conditions with recent years and possible future changes under climate change.<br>
<br>
You can zoom in by dragging a box over an area or by using the zoom tools in the toolbar. To move around the map, click and drag the plot. You can select specific regions by focusing on the area of interest and adjusting the view. The toolbar also allows you to reset the view to the original extent at any time. If you would like to save the figure, you can download the plot as a PNG image directly using the camera icon. Hovering over the plot will show additional information for each location.<br>
The plot can sometimes react slowly depending on your internet connection and other factors. 
<br><br>

Choose:
<div style="margin-bottom: 15px;">
  <label for="period1">Period: </label>
  <select id="period1">
    <option value="hist">Historical (1986–2005)</option>
    <option value="rect">Recent (1999–2018)</option>
    <option value="midc">Mid-Century (2041–2060)</option>
  </select>

  <label for="season1" style="margin-left: 15px;">Season: </label>
  <select id="season1">
    <option value="DJF">Winter (December–February)</option>
    <option value="MAM">Spring (March–May)</option>
    <option value="JJA">Summer (June–August)</option>
    <option value="SON">Autumn (September–November)</option>
  </select>

  <label for="type1" style="margin-left: 15px;">Precipitation Phase: </label>
  <select id="type1">
    <option value="water">Rain</option>
    <option value="snow">Snow</option>
  </select>
</div>

<iframe id="plotFrame1" src="PLOTS_Nadine/PLOT_interactive_Heatmap_GPType_water_hist_DJF.html" 
        width="100%" 
        height="750px" 
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

    const newSrc = `PLOTS_Nadine/PLOT_interactive_Heatmap_GPType_${type}_${period}_${season}.html`;

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

# Interpretation


<br><br><br>
---
Page Author: Nadine-Cyra Freistetter<br>
Sources: [model runs for paper](https://doi.org/10.1007/s10113-022-01920-4)

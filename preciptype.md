---
layout: page 
title: Precipitation type
---



Here you can explore how different types of precipitation may change across time and seasons. The plot shows the precipitation type, meaning whether precipitation falls as water (rain), sleet (rain mixed with ice), or snow. These forms depend strongly on temperature and are important for understanding weather conditions, climate impacts, and everyday activities such as driving or walking. Some general observations are presented under "Interpretation" below the plot.<br>
<br>
The model data used here come from the study “Climate change impacts on future driving and walking conditions in Finland, Norway and Sweden” (Reg Environ Change, 2022). The data are based on climate model simulations using the RCP 8.5 scenario, which represents a high greenhouse gas emissions pathway and is often referred to as a worst-case climate change scenario. Therefore, the results on this page should be used as extreme-case estimates. <br>
<br>

# How to use
The plot is fully interactive. First, use the drop-down menus to choose a period, a season, and a precipitation phase. 
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

---
Choose:
<div style="margin-bottom: 15px;">
  <label for="period1">Period: </label>
  <select id="period1">
    <option value="hist">Historical (1986–2005)</option><br>
    <option value="rect">Recent (1999–2018)</option><br>
    <option value="midc">Mid-Century (2041–2060)</option>
  </select>

  <label for="season1" style="margin-left: 15px;">Season: </label>
  <select id="season1">
    <option value="DJF">Winter (December–February)</option>
    <option value="MAM">Spring (March–May)</option>
    <option value="JJA">Summer (June–August)</option>
    <option value="SON">Autumn (September–November)</option>
  </select>
  
  <br>

  <label for="type1" style="margin-left: 15px;">Precipitation Phase: </label>
  <select id="type1">
    <option value="snow">Snow</option>
    <option value="water">Rain</option>
  </select>

  <label for="cities1" style="margin-left: 15px;">Show Cities: </label>
  <select id="cities1">
    <option value="cities">On</option>
    <option value="plain">Off</option>
  </select>
</div>

<iframe id="plotFrame1" src="PLOTS_Nadine/PLOT_interactive_Heatmap_cities_GPType_snow_hist_DJF.html" 
        width="100%" 
        height="700px" 
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<div style="margin-top:10px;">
  <a id="downloadPlot1"
     href="#"
     download
     style="display:none; font-weight:bold;">
     ⬇ Download this plot as HTML
  </a>
</div>

<script>
  const periodSelect1 = document.getElementById('period1');
  const seasonSelect1 = document.getElementById('season1');
  const typeSelect1   = document.getElementById('type1');
  const citiesSelect1 = document.getElementById('cities1');
  const iframe1       = document.getElementById('plotFrame1');
  const downloadLink1 = document.getElementById('downloadPlot1');

  function updatePlot1() {
    const period = periodSelect1.value;
    const season = seasonSelect1.value;
    const type   = typeSelect1.value;
    const cities = citiesSelect1.value;

    const newSrc = `PLOTS_Nadine/PLOT_interactive_Heatmap_${cities}_GPType_${type}_${period}_${season}.html`;
    
    iframe1.style.opacity = 0;

    setTimeout(() => {
      iframe1.src = newSrc;
      downloadLink1.href = newSrc;

      iframe1.onload = () => {iframe1.style.opacity = 1; };
    }, 400);
  }

  periodSelect1.addEventListener('change', updatePlot1);
  seasonSelect1.addEventListener('change', updatePlot1);
  typeSelect1.addEventListener('change', updatePlot1);
  citiesSelect1.addEventListener('change', updatePlot1);
</script>

# Interpretation
Snowfall is projected to decrease across all regions, with the strongest reductions in the south and along coastal areas, and across all seasons, with strongest changes expected in autumns.<br>

<b>West and South of the Baltic Sea (including southern Sweden)</b><br>
In winter, historical conditions show that around 70% of precipitation fell as snow in Poland, while most other regions experienced 50–60% snowfall. By mid-century, snowfall could decrease noticeably, with Poland dropping to about 50–60% and most other areas to 30–40%. In spring, snowfall historically accounted for around 25% of precipitation (35% in southern Sweden). By mid-century, this could decline to around 15%, or about 25% in southern Sweden. In autumn, snowfall historically occurred 15–20% of the time (25% in southern Sweden), but by mid-century this could fall to around 10%, or about 15% in southern Sweden.<br> <br>

<b>East of the Baltic Sea</b><br>
In winter, snowfall historically dominated, with around 85% of inland precipitation and about 70% near the Baltic coast. By mid-century, snowfall could decrease to around 65–70% inland and about 55% near the coast, with archipelago regions dropping to around 40%. In spring, historical snowfall accounted for about 35% of precipitation, with slightly higher values in Estonia, decreasing to around 25% by mid-century. In autumn, snowfall historically occurred 25–30% of the time, falling to around 20% by mid-century.<br> <br>

<b>North of the Baltic Sea</b><br>
In winter, precipitation historically fell as snow almost 100% of the time, except in archipelago regions where snowfall occurred around 70% of the time. By mid-century, snowfall is expected to remain above 90% across much of central and northern Sweden, but decreases markedly in Finland, with central Finland around 85%, southern Finland around 75%, and archipelago regions partly below 50%. In spring, historical snowfall reached around 80% occurrence in Lapland, about 60% in central Sweden and Finland, and around 50% in southern Finland. By mid-century, these values could drop to 60–70% in Lapland, around 50% in central Finland, and 30–35% in southern Finland, as well as to about 60% in central Sweden. In autumn, snowfall historically accounted for around 70% in Lapland, 55–60% in central Sweden and Finland, and about 35% in southern Finland. By mid-century, this could decline to around 50% in Lapland, 30% in central Finland, about 20% in southern Finland, and to 45% in central Sweden.<br> <br>

<b>Important note:</b> These results represent average conditions over long time periods in the worst-case climate change scenario RCP 8.5, and do not capture short-lived extreme events, such as warm spells, cold spells, or extreme precipitation events, which may still occur and can strongly affect local conditions.<br>

<br><br>
---
Page Author: Nadine-Cyra Freistetter<br>
Sources: [model runs for paper](https://doi.org/10.1007/s10113-022-01920-4)

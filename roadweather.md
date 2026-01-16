---
layout: page
title: Road weather
---

<style>
/* Floating table of contents box on the right side */
#toc-box {
  position: fixed;          /* stick to viewport instead of page flow */
  top: 200px;               /* distance from top */
  right: 20px;              /* distance from right edge */
  width: 220px;             /* adjust width as needed */
  background-color: #f9f9f9;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 0 6px rgba(0,0,0,0.1);
  padding: 12px 16px;
  font-size: 0.95em;
  z-index: 1000;            /* keep it above other elements */
}

#toc-box strong {
  display: block;
  margin-bottom: 8px;
  font-size: 1em;
}

#toc-box a {
  text-decoration: underline;
  color: #0055aa;
  display: block;
  margin-bottom: 6px;
  transition: color 0.2s ease;
}

#toc-box a:hover {
  color: #003d80;
}

html {
  scroll-behavior: smooth;  /* enables nice smooth scrolling */
}

/* Make sure content doesn’t get hidden under the TOC on narrow screens */
@media (max-width: 900px) {
  #toc-box {
    position: static;
    width: auto;
    box-shadow: none;
    border: none;
    background: transparent;
    margin-bottom: 20px;
  }
}
</style>

<div id="toc-box">
  <strong>Jump to:</strong>
  <a href="#road-temperature">Road Surface Temperature</a>  
  <a href="#freeze-thaw-cycles">Freeze-Thaw Cycles on Road</a>
  <a href="#road-cover">Road Condition</a>
</div>

Here you can explore how road conditions and temperatures may change across time and regions. The figures show road surface temperature, freeze–thaw cycles, and road surface condition, all of which are closely linked to safety and mobility. Road surface temperature affects ice formation and snow melt, freeze–thaw cycles indicate how often surfaces repeatedly freeze and thaw, and road surface condition describes whether roads are dry, wet, icy, or covered in snow or slush. These indicators help us understand how climate change may impact driving and walking conditions in different areas throughout the year. Some general observations are presented under the “Interpretation” sections below the figures.

The model data used here come from the study “Climate change impacts on future driving and walking conditions in Finland, Norway and Sweden” (Reg Environ Change, 2022). The data are based on climate model simulations using the RCP 8.5 scenario, which represents a high greenhouse gas emissions pathway and is often referred to as a worst-case climate change scenario. Therefore, the results on this page should be used as extreme-case estimates. 


## How to use
The figures are fully interactive. First, use the drop-down menus to choose a period and a season. 
You can explore three time periods Historical (1986–2005), Recent (1999–2018), and Mid-Century (2041–2060), in four meteorological seasons <br>
- Winter (DJF): December–February<br>
- Spring (MAM): March–May<br>
- Summer (JJA): June–August<br>
- Autumn (SON): September–November<br>

This allows you to compare past conditions with recent years and possible future changes under climate change.<br>
For <a href="#road-cover">Road Condition</a> you can additionally choose the road surface condition (cover): dry road, snow on road or ice on road.<br>
<br>
You can zoom in by dragging a box over an area or by using the zoom tools in the toolbar. To move around the map, click and drag the figure. You can select specific regions by focusing on the area of interest and adjusting the view. The toolbar also allows you to reset the view to the original extent at any time. If you would like to save the figure, you can download the figure as a PNG image directly using the camera icon. Hovering over the figure will show additional information for each location.<br>
The figure can sometimes react slowly depending on your internet connection and other factors. 
<br><br>

---

# Road Surface Temperature (Asphalt)
{:#road-temperature}

These figures show the temperature of asphalt road surfaces, which can differ from air temperature due to solar radiation, traffic, and surface properties. Road surface temperature is a key factor for winter maintenance, traffic safety, and the formation of ice or snow on roads. By hovering your mouse across the map, you can see mean, maximum, and minimum temperature (on average) for each grid point.
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
  
  <label for="cities1" style="margin-left: 15px;">Show Cities: </label>
  <select id="cities1">
    <option value="cities">On</option>
    <option value="plain">Off</option>
  </select>
</div>

<iframe id="plotFrame1" src="PLOTS_Nadine/PLOT_interactive_Heatmap_cities_GTSurf_avgmean_hist_DJF.html"
        width="100%"
        height="720px"
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<div style="margin-top:10px;">
  <a id="downloadPlot1"
     href="#"
     download
     style="display:none; font-weight:bold;">
     ⬇ Download this figure as HTML
  </a>
</div>

<script>
const periodSelect1 = document.getElementById('period1');
const seasonSelect1 = document.getElementById('season1');
const citiesSelect1 = document.getElementById('cities1');
const iframe1       = document.getElementById('plotFrame1');
const downloadLink1 = document.getElementById('downloadPlot1');

function updatePlot1() {
  const period = periodSelect1.value;
  const season = seasonSelect1.value;
  const cities = citiesSelect1.value;

  const newSrc = `PLOTS_Nadine/PLOT_interactive_Heatmap_${cities}_GTSurf_avgmean_${period}_${season}.html`;

  iframe1.style.opacity = 0;

  setTimeout(() => {
    iframe1.src = newSrc;
    downloadLink1.href = newSrc;

    iframe1.onload = () => {iframe1.style.opacity = 1;};
  }, 400);
}
periodSelect1.addEventListener('change', updatePlot1);
seasonSelect1.addEventListener('change', updatePlot1);
citiesSelect1.addEventListener('change', updatePlot1);
</script>
# Interpretation 
Road surface temperatures are projected to rise across Europe, with winters becoming milder in the south and west, spring and autumn temperatures generally staying above freezing, and summer heat spreading farther north, while the far north will still experience freezing conditions in winter.<br>

<b>West and South of the Baltic Sea (including southern Sweden)</b><br>
In the past, winter road surface temperatures were usually close to zero, with maximum values often rising above freezing. By mid-century (2041–2060), these regions are expected to experience mostly positive road surface temperatures during winter. In spring and autumn, roads have historically been above freezing on average, and this pattern is expected to continue, with nighttime temperatures rarely dropping below zero. In summer, average maximum road surface temperatures were historically near or above 30°C only in southern Germany and Poland, but by mid-century, such road temperatures are likely to be observed in the entire region.<br>


<b>East of the Baltic Sea</b><br>
Historically, winter road surface temperatures were on average well below freezing. By mid-century, average temperatures will still be below freezing, though maximum values may come close to or exceed zero, indicating that freeze–thaw cycles might increase (see <a href="#freeze-thaw-cycles">Freeze-Thaw Cycles</a> below). In spring and autumn, roads were mostly above freezing, and by mid-century they are expected to remain above or near freezing. Summer temperatures are projected to increase, following the same general pattern as in western regions with average maximum road temperatures around 30°C.<br>

<b>North of the Baltic Sea</b><br>
Winter road surface temperatures have historically been well below freezing, and even by mid-century, average winter temperatures are expected to remain below zero. Maximum temperatures, however, are likely to rise closer to zero, suggesting more frequent freeze–thaw cycles. In spring, even far-northern and glaciated regions are projected to reach positive or near-zero road surface temperatures by mid-century. Autumn shows a similar pattern, with generally positive averages but minimum temperatures dropping a few degrees below zero. Summer temperatures remain lower than the rest of Europe, with northern Fennoscandia being the main exceptions to the overall warming trend.<br>
<br>
<b>Attention</b>: The <b>average</b> maximum road surface temperture (average over the entire 2041-2060 period) does not portray individual heat waves in which road surface temperatures can be much higher than 30°C.

<br><br><br>


---
# Freeze-Thaw Cycles
{:#freeze-thaw-cycles}

These figures illustrate how often temperatures cross the freezing point, causing water on the road to freeze and thaw. It shows the average number of freeze–thaw cycles, as well as the minimum and maximum values observed during the selected period. Frequent freeze–thaw cycles can increase road wear, damage surfaces, and raise maintenance needs.
<br><br>
Choose:
<div style="margin-bottom: 15px;">
  <label for="period2">Period: </label>
  <select id="period2">
    <option value="hist">Historical (1986–2005)</option>
    <option value="rect">Recent (1999–2018)</option>
    <option value="midc">Mid-Century (2041–2060)</option>
  </select>

  <label for="season2" style="margin-left: 15px;">Season: </label>
  <select id="season2">
    <option value="DJF">Winter (December–February)</option>
    <option value="MAM">Spring (March–May)</option>
    <option value="JJA">Summer (June–August)</option>
    <option value="SON">Autumn (September–November)</option>
  </select>
  
  <label for="cities2" style="margin-left: 15px;">Show Cities: </label>
  <select id="cities2">
    <option value="cities">On</option>
    <option value="plain">Off</option>
  </select>
</div>

<iframe id="plotFrame2" src="PLOTS_Nadine/PLOT_interactive_Heatmap_cities_ZDCs_perDay_hist_DJF.html"
        width="100%"
        height="720px"
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<div style="margin-top:10px;">
  <a id="downloadPlot2"
     href="#"
     download
     style="display:none; font-weight:bold;">
     ⬇ Download this figure as HTML
  </a>
</div>

<script>
const periodSelect2 = document.getElementById('period2');
const seasonSelect2 = document.getElementById('season2');
const citiesSelect2 = document.getElementById('cities2');
const iframe2       = document.getElementById('plotFrame2');
const downloadLink2 = document.getElementById('downloadPlot2');

function updatePlot2() {
  const period = periodSelect2.value;
  const season = seasonSelect2.value;
  const cities = citiesSelect2.value;

  const newSrc = `PLOTS_Nadine/PLOT_interactive_Heatmap_${cities}_ZDCs_perDay_${period}_${season}.html`;

  iframe2.style.opacity = 0;

  setTimeout(() => {
    iframe2.src = newSrc;
    downloadLink2.href = newSrc;
    iframe2.onload = () => { iframe2.style.opacity = 1; };
  }, 400);
}
periodSelect2.addEventListener('change', updatePlot2);
seasonSelect2.addEventListener('change', updatePlot2);
citiesSelect2.addEventListener('change', updatePlot2);
</script>

<br><br>

# Interpretation
Across Europe, zero-degree crossings are expected to become slightly less frequent in the south and west of the Baltic Sea, while in northern regions they may increase slightly, especially during winter and autumn, indicating potential changes in freeze–thaw cycles.

<b>East, West, and South of the Baltic Sea (including southern Sweden)</b><br>
In autumn, historically, the regionally averaged maximum number of zero-degree crossings (ZDCs) per day was around 13, occasionally reaching 20, but the daily mean was stable at 1, meaning such high numbers were rare. By mid-century, the mean ZDCs per day will sometimes be 0 and sometimes 1, with the average maximum dropping to around 10 per day.<br>
<br>
In winter, historically, the mean number of ZDCs was about 2, with an average maximum of 15. By mid-century, the mean remains mostly 2, and the average maximum decreases slightly to 14.<br>
<br>
In spring, historical values showed an average maximum of 12 ZDCs per day, with a mean of 1, and slightly higher means of 2 in some Baltic countries. By mid-century, the average maximum drops to 10, while the mean remains around 1.<br>

<b>North of the Baltic Sea</b><br>
In autumn, historically, the mean number of ZDCs was 2, with an average maximum of 14 across the region. By mid-century, the mean will be 1–2, with an average maximum around 16, occasionally reaching up to 24 ZDCs per day.<br>
<br>
In winter, historically, most areas had almost no ZDCs, with an average maximum of 9. By mid-century, the mean will be around 1 in southern Fennoscandia and 0 in the far north, with the average maximum rising to 13.<br>
<br>
In spring, historically, the mean ZDCs were 2, with an average maximum of 14. By mid-century, the mean remains around 2 and the average maximum decreases to 11.<br>

<br><br><br>


---
# Road Condition
{:#road-cover}

This figure presents the seasonal average road surface condition on asphalt. Conditions range from dry, moist, or wet to more hazardous states such as slush, frost, partly icy or icy, and snow. These categories help us describe typical driving conditions and how they may change across seasons and future climate periods. You can only choose between three major conditions, but by hovering your mouse across the map, you can see the exact value for all conditions for every grid point. The "snow on road" value might be intuitively on the low side for far-north regions because the road weather model which calculated these values assumes that average traffic on the road is packing the snow into icy and partly icy conditions over time. Therefore, it is recommended to add up the "snow", "icy", and "partly icy" categories for a quick estimate of how often difficult driving conditions could occur (the model assumes no road maintenance is happening at all).
<br><br>
Choose:
<div style="margin-bottom: 15px;">
  <label for="period3">Period: </label>
  <select id="period3">
    <option value="hist">Historical (1986–2005)</option>
    <option value="rect">Recent (1999–2018)</option>
    <option value="midc">Mid-Century (2041–2060)</option>
  </select>

  <label for="season3" style="margin-left: 15px;">Season: </label>
  <select id="season3">
    <option value="DJF">Winter (December–February)</option>
    <option value="MAM">Spring (March–May)</option>
    <option value="JJA">Summer (June–August)</option>
    <option value="SON">Autumn (September–November)</option>
  </select>

  <br>

  <label for="type3" style="margin-left: 15px;">Road Surface Condition: </label>
  <select id="type3">
    <option value="icysum">Icy or partly icy road</option>
    <option value="snow">Snow on road</option>
    <option value="dry">Dry road</option>
  </select>
  
  <label for="cities3" style="margin-left: 15px;">Show Cities: </label>
  <select id="cities3">
    <option value="cities">On</option>
    <option value="plain">Off</option>
  </select>
</div>

<iframe id="plotFrame3" src="PLOTS_Nadine/PLOT_interactive_Heatmap_cities_GSCond_icysum_hist_DJF.html"
        width="100%"
        height="720px"
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<div style="margin-top:10px;">
  <a id="downloadPlot3"
     href="#"
     download
     style="display:none; font-weight:bold;">
     ⬇ Download this figure as HTML
  </a>
</div>

<script>
const periodSelect3 = document.getElementById('period3');
const seasonSelect3 = document.getElementById('season3');
const typeSelect3   = document.getElementById('type3');
const citiesSelect3 = document.getElementById('cities3');
const iframe3       = document.getElementById('plotFrame3');
const downloadLink3 = document.getElementById('downloadPlot3');


function updatePlot3() {
  const period = periodSelect3.value;
  const season = seasonSelect3.value;
  const type   = typeSelect3.value;
  const cities = citiesSelect3.value;

  const newSrc = `PLOTS_Nadine/PLOT_interactive_Heatmap_${cities}_GSCond_${type}_${period}_${season}.html`;

  iframe3.style.opacity = 0;

  setTimeout(() => {
    iframe3.src = newSrc;
      downloadLink3.href = newSrc;

    iframe3.onload = () => { iframe3.style.opacity = 1; };
  }, 400);
}
periodSelect3.addEventListener('change', updatePlot3);
seasonSelect3.addEventListener('change', updatePlot3);
typeSelect3.addEventListener('change', updatePlot3);
citiesSelect3.addEventListener('change', updatePlot3);
</script>
# Interpretation 
Snowy and icy road conditions are expected to decrease for many regions around the Baltic sea as climate change progresses. Overall, winter road conditions are expected to become much milder in the south and west of the Baltic Sea, and slightly milder east the baltic sea, while northern European roads will remain largely icy and snowy, though partly icy conditions could become more common.<br>

<b>West and South of the Baltic Sea (including southern Sweden)</b><br>
In historical winters, the west and south of the Baltic Sea, including southern Sweden, experienced mostly dry roads, with dry conditions around 60% of the time, while snow or ice covered the roads for more than 30% of the time. By mid-century (2041–2060), dry roads in this region are expected to become even more common, occurring close to 70% of the time, while snow and ice will be present less than 20% of the time.<br>

<b>East of the Baltic Sea</b><br>
In the east of the Baltic Sea, winters were historically harsher. Roads were dry only 30–40% of the time, and snow and ice covered them for more than half of the season. By mid-century, conditions become slightly milder, with dry roads expected over 50% of the time, though snow and ice will still cover around 40% of the roads.<br>

<b>North of the Baltic Sea</b><br>
In the north, including northern Fennoscandia, snowy and icy conditions have long dominated, with roads covered over 70% of the time. Looking ahead to mid-century, dry roads remain relatively rare, occurring only 20–30% of the time. Partly icy conditions become more frequent, but overall snow and ice will still cover roughly 70% of the roads.<br>

<br>
---
Data, figures, and text by <a href="https://en.ilmatieteenlaitos.fi/cv-nadine-cyra-freistetter"> Nadine-Cyra Freistetter </a><br>
Sources: [model runs for paper](https://doi.org/10.1007/s10113-022-01920-4)







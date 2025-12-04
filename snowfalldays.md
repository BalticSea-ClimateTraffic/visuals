---
layout: page
title: Snowfall-days
---
---
<br>


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
  <a href="#snowfalldays">Snowfall days</a>
  <a href="#Hsnowfalldays">Heavy snowfall days</a>
  <a href="#further-info">Further Information</a>
</div>


---

# Days with snowfall
{:#snowfalldays}

<div style="margin-bottom: 15px;">
  <label for="period1">Period: </label>
  <select id="period1">
    <option value="hist">Historical</option>
    <option value="midc">Mid-Century</option>
    <option value="diff">Change between Hist and MidC</option>
  </select>

  <label for="season1" style="margin-left: 15px;">Season: </label>
  <select id="season1">
    <option value="DJF">Winter</option>
    <option value="JJA">Summer</option>
    <option value="Year">Whole year</option>
  </select>
</div>

<iframe id="plotFrame1" src="PLOTS_Anton/PLOT_Snday_hist_DJF.html"
        width="900px"
        height="700px"
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<script>
const periodSelect1 = document.getElementById('period1');
const seasonSelect1 = document.getElementById('season1');
const iframe1       = document.getElementById('plotFrame1');

function updatePlot1() {
  const period = periodSelect1.value;
  const season = seasonSelect1.value;
  const newSrc = `PLOTS_Anton/PLOT_Snday_${period}_${season}.html`;

  iframe1.style.opacity = 0;
  setTimeout(() => {
    iframe1.src = newSrc;
    iframe1.onload = () => { iframe1.style.opacity = 1; };
  }, 400);
}
periodSelect1.addEventListener('change', updatePlot1);
seasonSelect1.addEventListener('change', updatePlot1);
</script>
<br><br>

<br><br><br>




# Days with heavy snowfall
{:#Hsnowfalldays}



<div style="margin-bottom: 15px;">
  <label for="period2">Period: </label>
  <select id="period2">
    <option value="hist">Historical</option>
    <option value="midc">Mid-Century</option>
    <option value="diff">Change between Hist and MidC</option>
  </select>

  <label for="season2" style="margin-left: 15px;">Season: </label>
  <select id="season2">
    <option value="DJF">Winter</option>
    <option value="JJA">Summer</option>
    <option value="Year">Whole year</option>
  </select>
</div>

<iframe id="plotFrame2" src="PLOTS_Anton/PLOT_HSnday_hist_DJF.html"
        width="900px"
        height="700px"
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<script>
const periodSelect2 = document.getElementById('period2');
const seasonSelect2 = document.getElementById('season2');
const iframe2       = document.getElementById('plotFrame2');

function updatePlot2() {
  const period = periodSelect2.value;
  const season = seasonSelect2.value;
  const newSrc = `PLOTS_Anton/PLOT_HSndays_${period}_${season}.html`;

  iframe2.style.opacity = 0;
  setTimeout(() => {
    iframe2.src = newSrc;
    iframe2.onload = () => { iframe2.style.opacity = 1; };
  }, 400);
}
periodSelect2.addEventListener('change', updatePlot2);
seasonSelect2.addEventListener('change', updatePlot2);
</script>
<br><br>

<br><br><br>





# Further Information
{:#further-info}
Used scenario: Historical until 2015 - SSP245 ("moderate" pathway for future greenhouse gas emissions) for midcentury 
Used Data: NEX-GDDP-CMIP6, Statistically downscaled climate model dataset made by NASA. Based on 30 CMIP6 climate model simulations, https://www.nccs.nasa.gov/services/data-collections/land-based-products/nex-gddp-cmip6 

Periods:  
- Historical: 1995–2014  
- Mid-Century: 2041–2060  

Seasons:  
- Winter: December, January, February (DJF)
- Summer: June, July, August (JJA)
<br><br><br>

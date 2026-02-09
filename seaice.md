---
layout: page
title: Sea Ice
---
---
<br>


<style>
/* Floating table of contents box on the right side */
#toc-box {
  position: fixed;          /* stick to viewport instead of page flow */
  top: 200px;               /* distance from top */
  right: 300px;              /* distance from right edge */
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
  <a href="#seaice">Snowfall days</a>
  <a href="#further-info">Further Information</a>
</div>
Sea ice concentration is the fraction (or percentage) of the ocean surface that is covered by sea ice within a given area. It ranges from 0 (completely ice-free water) to 1 or 100% (entirely ice-covered) and is commonly derived from satellite observations, but can be also simulated with climate models. 
<strong>Limitations::</strong> Sea ice concentration describes the fractional ice cover but does not capture ice thickness, ice strength, or ice type. As a result, areas with the same concentration may have very different navigability or hazard levels.

The model data used in the figures shown above are based on climate Digital Twin (nextGEMS) simulations. These are high-resolution simulations that provide detailed spatial information, for example for sea ice conditions in the Baltic Sea. However, it should be noted that the results are based on a single model and a single realization, and that simulated conditions may differ slightly from observations even for historical periods. High-resolution information on sea ice conditions is generally limited. Despite these limitations, the simulations provide a useful indication of how sea ice conditions may change in the future.


<strong>How to use</strong>
The figures show average sea ice concentration for each month for a near-historical period (1990–2019) and a future period (2030–2049), based on the high-emission scenario SSP3-7.0. The displayed month can be selected using the drop-down menus.

The presented values are multi-year means. Interannual variability is not shown, and conditions in individual years may differ from the average.

---


# Sea Ice Concentration
{:#seaice}

<div style="margin-bottom: 15px;">

  <label for="month" style="margin-left: 15px;">Month: </label>
<select id="month">
  <option value="0">January</option>
  <option value="1">February</option>
  <option value="2">March</option>
  <option value="3">April</option>
  <option value="4">May</option>
  <option value="5">June</option>
  <option value="6">July</option>
  <option value="7">August</option>
  <option value="8">September</option>
  <option value="9">October</option>
  <option value="10">November</option>
  <option value="11">December</option>
</select>

</div>
<iframe
  id="plotFrame1"
  src="PLOTS_Anton/seaice_hist_fut_0.png"
  style="width:100%; border:none; opacity:1; transition: opacity 0.5s;"
></iframe>


<script>
const monthSelect1 = document.getElementById('month');
const iframe1       = document.getElementById('plotFrame1');

function updatePlot1() {
  const month = monthSelect1.value;
  const newSrc = `PLOTS_Anton/seaice_hist_fut_${month}.png`;

  iframe1.style.opacity = 0;
  setTimeout(() => {
    iframe1.src = newSrc;
    iframe1.onload = () => { iframe1.style.opacity = 1; };
  }, 400);
}
monthSelect1.addEventListener('change', updatePlot1);
</script>
<br><br>

<br><br><br>






# Further Information
{:#further-info}
Used scenario: Historical until 2015 - from 2015: SSP3-7.0 (a high greenhouse-gas emissions climate scenario)

Used Data: Climate Digital Twins, nextGEMS, model: IFS-FESOM - https://destine.ecmwf.int/climate-change-adaptation-digital-twin-climate-dt/

Periods:  1990–2019 and 2030–2049  

<br><br><br>

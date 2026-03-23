---
layout: page
title: Wind speed
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



# Maximum wind speed
---
On this page, you can find the average maximum wind speed for each month and how it is projected to change in the near future and by the end of the century, based on climate model simulations. Maximum wind speed is an important indicator for the traffic sector because strong gusts can cause accidents, vehicle instability, infrastructure damage, and service disruptions.

The figures on this page are based on high-resolution regional climate model simulations from the EURO-CORDEX initiative. These projections follow the RCP 8.5 scenario, which represents a high-emission pathway. Although this scenario is unlikely to occur, it provides a useful indication of how conditions could change in a worst-case scenario.

It should also be noted that, even though the results are based on multiple simulations, they are still affected by individual model biases. Maximum wind speed may not be a reliable indicator of changes in average wind speed or wind gusts, and it does not provide information about wind direction, which may be relevant for some applications.

# How to use
The plot is fully interactive. Use the drop-down menus to select either absolute values for the current climate (2005–2014) or the projected changes in maximum wind speed for the future (mid-century (2041–2060) or end of the century (2081–2100)) relative to the current climate.

The figures show monthly average values for the selected period. You can change the month using the drop-down menu at the top.
<br>
You can zoom in by dragging a box over an area or by using the zoom tools in the toolbar. To move around the map, click and drag the plot. You can select specific regions by focusing on the area of interest and adjusting the view. The toolbar also allows you to reset the view to the original extent at any time. If you would like to save the figure, you can download the plot as a PNG image directly using the camera icon. Hovering over the plot will show additional information for each location.<br>
<!-- Maximum wind speed -->

<div style="margin-bottom: 15px;">
  <label for="period1">Period: </label>
  <select id="period1">
    <option value="2005-2024">2005–2024</option>
    <option value="2041-2060_minus_2005-2024_">Change at mid-century</option>
    <option value="2081-2100_minus_2005-2024_">Change at end of century</option>
  </select>

  <label for="month1" style="margin-left: 15px;">Month: </label>
  <select id="month1">
    <option value="01">January</option>
    <option value="02">February</option>
    <option value="03">March</option>
    <option value="04">April</option>
    <option value="05">May</option>
    <option value="06">June</option>
    <option value="07">July</option>
    <option value="08">August</option>
    <option value="09">September</option>
    <option value="10">October</option>
    <option value="11">November</option>
    <option value="12">December</option>
  </select>
</div>

<iframe id="plotFrame1"
        src="PLOTS_Anton/PLOT_sfcWindmax_2005-2024_ll0.10_m01.html"
        width="900px"
        height="700px"
        style="border:none; opacity:1; transition: opacity 0.5s;">
</iframe>

<script>
const periodSelect1 = document.getElementById('period1');
const monthSelect1  = document.getElementById('month1');
const iframe1       = document.getElementById('plotFrame1');

function updatePlot1() {
  const period = periodSelect1.value;
  const month  = monthSelect1.value;
  const prefix = (period === "2005-2024") ? "PLOT" : "PLOT_DIFF";

  const newSrc = `PLOTS_Anton/${prefix}_sfcWindmax_${period}_ll0.10_m${month}.html`;

  iframe1.style.opacity = 0;
  setTimeout(() => {
    iframe1.src = newSrc;
    iframe1.onload = () => { iframe1.style.opacity = 1; };
  }, 400);
}

periodSelect1.addEventListener('change', updatePlot1);
monthSelect1.addEventListener('change', updatePlot1);
</script>

# Interpretation
Based on these climate model simulations, no major changes in maximum wind speeds are expected in general. However, winds in the Bothnian Bay will be stronger in spring than they are today. These changes will be visible aldready by the middle of this century. The results reveal intriguing changes in the southern parts of the Baltic Sea during midwinter. According to the results, maximum winds will weaken by the middle of the century, but will be stronger than they are today by the end of the century. However, there is a great uncertainty associated with these results.

<br><br><br>



# Further Information
{:#further-info}
Used scenario: RCP 8.5 (Representative Concentration Pathway 8.5) is a high greenhouse-gas emissions scenario used in climate research to explore a worst-case future. It assumes continued growth in emissions throughout the 21st century, driven by high population growth, heavy reliance on fossil fuels, limited climate policies, and slow technological change. Under this pathway, radiative forcing reaches 8.5 W/m² by 2100, leading to strong global warming, more frequent and intense extreme weather events, rising sea levels, and significant impacts on natural and human systems. Although RCP 8.5 is now considered unlikely, it remains useful for understanding upper-bound climate risks and the potential consequences of very high emissions.

Used Data: EURO-CORDEX (European branch of the Coordinated Regional Climate Downscaling Experiment). It is a major international climate research initiative that provides high-resolution climate projections for Europe. Here we have used 12km resolution data based on two regional climate models, with several GCM boundary conditions.

Periods:  
- Historical: 2005–2014  
- Mid-Century: 2041–2060
- End-Century: 2081–2100   

<br><br><br>
Page author: Anton Laakso

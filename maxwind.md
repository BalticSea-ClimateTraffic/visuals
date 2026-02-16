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



Maximum wind speed
---
On this page, you can find the average maximum wind speed for each month and how it is projected to change in the near future and by the end of the century, based on climate model simulations. Maximum wind speed is an important indicator for the traffic sector because strong gusts can cause accidents, vehicle instability, infrastructure damage, and service disruptions.

The figures on this page are based on high-resolution regional climate model simulations from the EURO-CORDEX initiative. These projections follow the RCP 8.5 scenario, which represents a high-emission pathway. Although this scenario is unlikely to occur, it provides a useful indication of how conditions could change in a worst-case scenario.

It should also be noted that, even though the results are based on multiple simulations, they are still affected by individual model biases. Maximum wind speed may not be a reliable indicator of changes in average wind speed or wind gusts, and it does not provide information about wind direction, which may be relevant for some applications.


# Maximum wind speed
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

<br><br><br>



# Further Information
{:#further-info}
Used scenario:
Used Data: 
Periods:  
- Historical: 1995–2014  
- Mid-Century: 2041–2060  

<br><br><br>

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
DIIBADAABAAA

---

# Sea Ice Concentration
{:#seaice}

<div style="margin-bottom: 15px;">

  <label for="month" style="margin-left: 15px;">Season: </label>
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
  const newSrc = `PLOTS_Anton/seaice_hist_fut_${month}.png`;

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






# Further Information
{:#further-info}
Used scenario: Historical until 2015 - SSP245 ("moderate" pathway for future greenhouse gas emissions) for midcentury 
Used Data: 

Periods:  
- Historical: 1990–2019  
- Mid-Century: 2030–2049  

<br><br><br>

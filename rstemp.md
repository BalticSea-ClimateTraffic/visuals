---
layout: page 
title: Road Temperature
---

Seasonal avergae road surface temperature historical (1999-2018) and mid-centruy (2041-2060)

<select id="yearDropdown">
  <option value="2000">Year 2000</option>
  <option value="2018">Year 2018</option>
</select>
<select id="monthDropdown">
  <option value="Jan">January</option>
  <option value="Jul">July</option>
</select>

<div id="plot-container">
  <div id="2000_Jan" class="active">
    <object type="text/html" data="MeanRST_2000_Jan_day.html"></object>
  </div>
  <div id="2000_Jul">
    <object type="text/html" data="MeanRST_2000_Jul_day.html"></object>
  </div>
  <div id="2018_Jan">
    <object type="text/html" data="MeanRST_2018_Jan_day.html"></object>
  </div>
  <div id="2018_Jul">
    <object type="text/html" data="MeanRST_2018_Jul_day.html"></object>
  </div>
</div>

<style>
/* Dropdown styling */
select { margin: 10px 10px 20px 0; padding: 5px 10px; font-size: 16px; }

/* Plot container styling */
#plot-container {
  position: relative;
  width: 100%;
  /*max-width: 1000px;*/
  height: 13000px; /* adjust to your preferred height */
  margin: 0 auto;
  overflow: hidden; /* prevent scrollbars */
}

/* Each plot div */
#plot-container > div {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 0.5s ease-in-out;
  pointer-events: none; /* only active div responds */
}

/* Active plot */
#plot-container > div.active {
  opacity: 1;
  pointer-events: auto;
}

/* Make the <object> fill the div */
#plot-container object {
  width: 100%;
  height: 100%;
  border: none;
}
</style>

<script>
const yearDropdown = document.getElementById('yearDropdown');
const monthDropdown = document.getElementById('monthDropdown');
const plots = document.querySelectorAll('#plot-container > div');

function updatePlot() {
  const selected = yearDropdown.value + '_' + monthDropdown.value;
  plots.forEach(div => div.classList.remove('active'));
  const activeDiv = document.getElementById(selected);
  if (activeDiv) activeDiv.classList.add('active');
}

// Update plot when either dropdown changes
yearDropdown.addEventListener('change', updatePlot);
monthDropdown.addEventListener('change', updatePlot);

// Initialize display
updatePlot();
</script>

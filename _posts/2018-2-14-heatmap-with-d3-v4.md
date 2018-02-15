---
layout: post
title:  "A Heatmap with D3 v4"
description: "Making a heatmap of tuition prices over ten years"
date:   2018-2-14 16:00:00 +0000

---

This is a heat map of in-state college tuition for 2007-2017 made with d3 v4. The states make up the x-axis, the years make up the y-axis and the colors of the squares indicate how high the tuition is. This heat map is useful for seeing which states charge the highest in-state tuition and whether there are any noticeable trends (usually upward trends) among states.

<img src="https://www.ashlynnpai.com/assets/tuition_heatmap.png" width="600" alt="Tuition Heatmap" class="img-center" />

Here is the code and the project hosted on codepen:

<https://github.com/ashlynnpai/charts/blob/master/tuition-heatmap/chart.js>

<https://codepen.io/ashlynnpai/full/WMEXXj/>

Since much of the code is standard to other types of d3 maps, I'm focusing here on the code that is specific to this heatmap. The full code in the Github file is commented and I hope is easy enough to follow, but feel free to let me know if it isn't. 


The data was pulled in this format:

[{"uni": "University of Alaska Fairbanks", "state": "AK", "tuition": 5283, "year": 2007}, {"uni": "University of Alaska Fairbanks", "state": "AK", "tuition": 5372, "year": 2008}]

### Setting and Scaling the Axes

The scale functions take in the data that needs to be displayed on each axis and scales them to available space (here it's the width and height of the chart). I used scaleBand() to scale the x-axis to the list of state names. At first I thought scaleOrdinal() was the appropriate function to use with categories, but it caused the squares for all the states to pile on top of each other. I spent a few hours trying to get it to work until realizing that scaleBand() accomplished what I wanted.  

~~~ javascript
var x = d3.scaleBand()
    .range([0, width]);
var y = d3.scaleTime()
    .range([height, 0]);
~~~

The domain input sets the state names and years as the values for the x and y axes:

~~~ javascript
const states = d3.set(data.map((d) => {return d.state})).values();
    x.domain(states);
    y.domain(d3.extent(data, d => d.year));
~~~

### Setting the Colors for the Heatmap

The scaleQuantize() function takes the tuition data and divides it into slices based on how many different colors the heat map will use. I went with four colors and therefore four quartiles of tuition data.

~~~ javascript
var color = d3.scaleQuantize()
    .domain(d3.extent(data, d => d.tuition))
    .range(["#bdb7d6", "#948DB3", "#605885", "#433B67"]);
~~~

Now we can draw a series of 20 x 20 pixel squares on the chart.

~~~ javascript
const cellSize = 20;

svg.selectAll("rect")
    .data(data)
    .enter().append("rect")
    .attr('width', cellSize)
    .attr('height', cellSize)
    .attr('x', d => x(d.state))
    //put the cells on top of the y increments to prevent x-axis labels overlapping
    .attr('y', d => y(d.year) - cellSize)
    //set colors based on tuition
    .attr('fill', d => color(d.tuition))
    .style("stroke", "#d6cdb7")
~~~

### Making the Legend

Finally, I want to make a legend that shows the tuition cut off points for the different colors. The quantile function takes a <b>sorted</b> array and computes the specified points in the data. This gives me the values that separate the four quartiles and I write them to the DOM.

~~~ javascript
    var tuition = d3.set(data.map((d) => {return d.tuition})).values();
    tuition.sort(function(a,b){return a - b})
    var q1 = d3.quantile(tuition, .25);
    var q2 = d3.quantile(tuition, .5);
    var q3 = d3.quantile(tuition, .75);
    var q4 = d3.quantile(tuition, 1);
    d3.select("#q1").node().innerHTML = "$0 - $" + q1;
    d3.select("#q2").node().innerHTML = "$" + q1 + " - $" + q2 ;
    d3.select("#q3").node().innerHTML = "$" + q2 + " - $" + q3 ;
    d3.select("#q4").node().innerHTML = "$" + q3 + " - $" + q4 ;
~~~

The code at Github covers drawing the chart and the axes and creating tooltips that display the names of the universities and the tuition prices.

### Sources

The tuition data file is at my Github: 
<https://raw.githubusercontent.com/ashlynnpai/charts/master/tuition-heatmap/data.json>

I originally downloaded the data as an Excel file from the College Board and used a Python library openpyxl to parse the data:
<https://trends.collegeboard.org/college-pricing/figures-tables/tuition-fees-flagship-universities-over-time>

These are some tutorials and examples I used in building previous charts and I borrowed some of that code for this project:

Tooltips: <https://bl.ocks.org/d3noob/257c360b3650b9f0a52dd8257d7a2d73> 

Bar Charts: <https://www.pshrmn.com/tutorials/d3/bar-charts/>

Scatterplots: <https://bl.ocks.org/d3noob/6f082f0e3b820b6bf68b78f2f7786084> 

I really enjoyed making this project, finding a data set that was interesting to me and presenting the data visually. I also learned that my own alma mater, the University of Hawaii, has been trending upward in tuition over the past ten years, moving from Quartile 1 to Quartile 3, whereas many other states have held their tuition prices comparably steady.
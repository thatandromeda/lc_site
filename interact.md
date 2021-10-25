---
layout: page
title: Interact
---

<div id="scatter_area"></div>

<!-- Load d3.js -->
<script src="https://d3js.org/d3.v4.js"></script>

<script>

// set the dimensions and margins of the graph
var margin = {top: 10, right: 40, bottom: 30, left: 30},
    width = 450 - margin.left - margin.right,
    height = 400 - margin.top - margin.bottom;

// append the svg object to the body of the page
var svg = d3.select("#scatter_area")
  .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform",
          "translate(" + margin.left + "," + margin.top + ")");

// Create data
var data = [
    {x:Math.random()*100, y:Math.random()*100},
    {x:Math.random()*100, y:Math.random()*100},
    {x:Math.random()*100, y:Math.random()*100}
]

// X scale and Axis
var x = d3.scaleLinear()
    .domain([0, 100])         // This is the min and the max of the data
    .range([0, width]);       // This is the corresponding value I want in Pixel

// X scale and Axis
var y = d3.scaleLinear()
    .domain([0, 100])         // This is the min and the max of the data
    .range([height, 0]);       // This is the corresponding value I want in Pixel

svg
  .selectAll()
  .data(data)
  .enter()
  .append("circle")
    .attr("cx", function(d){ return x(d.x) })
    .attr("cy", function(d){ return y(d.y) })
    .attr("r", 7)

svg.selectAll("circle")
    .on('mouseover', function (d) {
        d3.select(this).style("fill", "orange");
        return tooltip.style("visibility", "visible")
          .style("top", (d3.event.pageY-10)+"px")
          .style("left",(d3.event.pageX+10)+"px");
    })
    .on('mouseout', function (d) {
        d3.select(this).style("fill", "black");
        return tooltip.style("visibility", "hidden");
    });

var tooltip = d3.select("body")
    .append("div")
    .style("outline", "thin solid orange")
    .style("padding", "5px")
    .style("position", "absolute")
    .style("z-index", "10")
    .style("visibility", "hidden")
    .text("this is the point you have hovered over");
</script>

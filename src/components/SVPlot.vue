<script setup>
import {onMounted, ref} from 'vue'
import * as d3 from "d3"
import plot_data from '../assets/plot_data.json'

/* Placeholder Variables for data that will be provided or calculated */
const genome_position_limits = [50186300, 50186900]
const max_insert_size = 300

/* SVG Variables */
let svg          = null
let drawing_clip = null
let drawing      = null
let splits       = null
let pairss       = null
let x_scale = d3.scaleLinear()
let y_scale = d3.scaleLinear()

/* Formatting dimension calculations */
const axis_label_width = 40
const right_margin = 10
let container_width = null
let x_range_limit = null
/* Functions */

// Initialize SVG structure and named elements
function initSvg() {
  // Use template ref, holder, to access the width of the holding div.
  container_width = holder.scrollWidth || 1000
  x_range_limit = container_width - axis_label_width -right_margin;

  svg = d3.select("#structVarReads")
    .attr("viewBox", `0 0 ${container_width} 100`)
    .style("display", "block")

   splits = svg.select("split-reads");
   pairss = svg.select("paired-reads");

}

// Run when data arrives to populate svg
function initPlotData(){
  // Map data limits to viewbox scales
  x_scale.domain(genome_position_limits)
    .range([0, x_range_limit])

  y_scale.domain([0, max_insert_size])
    .range([100, 0])

  svg.append("rect")
    .attr("height", "50%")
    .attr("width", "50%")
    .style("fill", "#00B4D8")

    /*
  rects_genes = drawing.selectAll("rec")
        .data(this.genes)
        .enter()
        .append("rect")
        .attr("height", 3)
        .attr("shape-rendering", "crispEdges")
        .style("pointer-events", "none")
        .style("fill", "#00B4D8");
     */


}

function oldSvg() {
  // Use template ref, holder, to access the width of the holding div.
  const container_width = holder.scrollWidth || 1000

  const depth_upper_limit = this.roundUpToTens(this.max_mean_seq_depth)
  const axis_label_width = 40
  const right_margin = 10
  const x_range_limit = container_width - axis_label_width -right_margin;

  // Map data to viewbox scale
  this.x_scale.domain(this.segmentRegions)
              .range([0,x_range_limit]);
  this.y_scale.domain([0, depth_upper_limit])
              .range([100, 0]);

  // Match viewbox to containing element width setting the aspect ratio at draw time.
  this.svg = d3.select("#depthSvg")
      .attr("viewBox", `0 0 ${container_width} 100`)

}

onMounted(() => {
  initSvg()
  initPlotData()
})

</script>

<template>
  <pre>
    Demo
  </pre>
  <div id="holder" ref="holder" class="child-component">
    <svg id="structVarReads" style="display: block;" height="100px" width="100%" preserveAspectRatio="none">
      <clipPath id="depth-clip">
        <rect x="0%" y="0%" width="100%" height="100%"></rect>
      </clipPath>
      <g id="depths-container">
        <g id="depths"></g>
        <g id="y-axis" style="font-size: 9px"></g>
        <text id="axis-title" transform="translate(-30,50) rotate(-90)"
          style="font-size: 10px; text-anchor: middle;">Avg. Depth</text>
        <line id="highlight" class="highlight_line" x1="0" y1="0" x2="0" y2="100%"
          stroke-width="2" stroke-linecap="round" stroke="#e77f00" visibility="hidden"/>
      </g>
      <g id="alignments">
        <g id="split-reads"  class="sv__splits"></g>
        <g id="paired-reads" class="sv__pairs"></g>
        <g id="long-reads"   class="sv__longs"></g>
      </g>
    </svg>
  </div>
  <pre>
    Demo Done
  </pre>
</template>

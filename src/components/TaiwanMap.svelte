<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  import * as topojson from 'topojson';
  import InteractiveTool from "./InteractiveTool.svelte";
  import { selectedVar, itemsList } from '../stores/MapInfo.js'
  import gs2json from "../helper/gs2json.js";

  let googleSheetData, mapSelectedSheetData, varColorScale, enterTownPaths

  const varColorScaleGenerator = (gd) => {
    
    const minVarValue = d3.min([...gd].map(d => d[1]))
    const maxVarValue = d3.max([...gd].map(d => d[1]))

    return d3.scaleLinear()
      .domain([minVarValue, maxVarValue])
      .range(["#FDF4FA", "#023C5E"])
  }

  const changeVar = (reactiveVar) => {

    mapSelectedSheetData = Object.assign(new Map(googleSheetData.map(d => [d['townid'], +d[reactiveVar]])))

    varColorScale = varColorScaleGenerator(mapSelectedSheetData, reactiveVar)

    if(enterTownPaths){
      enterTownPaths
        .attr("fill", d => $selectedVar[0] !== 'nothing' ? varColorScale(mapSelectedSheetData.get(d.properties['TOWNID'])) : "#25877F")
    }

  }

  $: {

    $selectedVar[0] !== 'nothing' ? changeVar($selectedVar) : null
    
  }

  onMount(async () => {
  // canvas dimension
  const width = window.innerWidth;
  const height = window.innerHeight;

  // attribute data input
  const url = "https://spreadsheets.google.com/feeds/list/1TY3eMLbH-WvXku5BLK9Nco6-u1PHj0q8Clkk06zG9eo/1/public/values?alt=json"
  const res = await fetch(url);
  googleSheetData = await res.json().then(d => gs2json(d));
  
  itemsList.update(() => {
    const colList = Object.keys(googleSheetData[0]).map(d => ({"value": d, "label": d}))
            return colList;
        })

  // geometry data input
  const twTownResponse = await fetch("./data/tw_town.json")
  const twTownData = await twTownResponse.json()
  const twTownFeatures = topojson.feature(twTownData, twTownData.objects.tw_town).features

  const twCountyResponse = await fetch("./data/tw_county.json")
  const twCountyData = await twCountyResponse.json()
  const twCountyFeatures = topojson.feature(twCountyData, twCountyData.objects.tw_county).features

  // projection setting
  const twProjection = d3.geoMercator()
      .translate([width / 2, height / 2])
      .scale(10000)
      .center([121, 23.84394])

  const twGeoPath = d3.geoPath()
      .projection( twProjection )
  
  // draw tw county map
  const svg = d3.select(".interactive-map svg")
    .attr("width", width)
    .attr("height", height)

  const counties = svg.selectAll(".county")
    .data(twCountyFeatures)
    .enter()
    .append("path")
    .attr("class", "county")
    .attr("id", d => d.properties['COUNTYID'])
    .attr("fill", "#25877F")
    .attr("opacity", 1)
    .attr("stroke", "#333")
    .attr("stroke-width", 0.5)
    .attr("d", twGeoPath)
    .on("click", function (d) { countyZoom(d.properties.COUNTYID) })



  // zoom func
  function backToCounty() {
    const t = d3.transition().duration(800)

    twProjection.scale(10000).translate([width / 2, height / 2])

    counties.transition(t)
        .attr("d", twGeoPath)
        .attr("opacity", 1)
        .style("fill", "#25877F")

    svg.selectAll(".town")
        .data([])
        .exit().transition(t)
        .attr("d", twGeoPath)
        .style("opacity", 0)
        .remove()
  }

  function countyZoom(COUNTYID) {
    const county = twCountyFeatures.find(function (d) { return d.properties.COUNTYID === COUNTYID })
    const countyTowns = twTownFeatures.filter(function (d) { return d.properties.COUNTYID === COUNTYID })

    const t = d3.transition().duration(800)

    const towns = svg.selectAll('.town')
        .data(countyTowns, function (d) { return d.properties.COUNTYID })

    enterTownPaths = towns.enter().append('path')
        .attr("id", d => d.properties['TOWNID'])
        .attr("class", "town")
        .attr("d", twGeoPath)
        .attr("fill", d => $selectedVar[0] !== 'nothing' ? varColorScale(mapSelectedSheetData.get(d.properties['TOWNID'])) : "#25877F")
        .style("opacity", 0)
        .on("click", function () { backToCounty() })


    twProjection.fitExtent(
        [[30, 30], [width - 30, height - 30]],
        county
    )

    counties.transition(t)
        .attr('d', twGeoPath)
        .attr("opacity", 0.5)
        .style('fill', '#25877F')

    enterTownPaths.transition(t)
        .attr('d', twGeoPath)
        .attr("stroke", "#333")
        .attr("stroke-width", 0.5)
        .style('opacity', 1)

    towns.exit().transition(t)
        .attr('d', twGeoPath)
        .style('opacity', 0)
        .remove()
    }
  })

</script>

<div class="interactive-map">
  <svg id ="tw-map"></svg>
</div>
<InteractiveTool/>


<style>
  .interactive-map{
    margin: 0 auto;
  }
</style>

<!-- markup (zero or more items) goes here -->
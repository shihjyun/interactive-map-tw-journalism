<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  import * as topojson from 'topojson';
  import InteractiveTool from "./InteractiveTool.svelte";
  import { selectedVar, itemsList } from '../stores/MapInfo.js'
  import gs2json from "../helper/gs2json.js";

  let googleSheetData, mapSelectedSheetData, varColorScale, enterTownPaths
  let hoverCounty = ""
  let hoverTown = ""
  let varValue = ""
  let inCountyLevel = true

  const varColorScaleGenerator = (gd) => {
    
    const minVarValue = d3.min([...gd].map(d => d[1]))
    const maxVarValue = d3.max([...gd].map(d => d[1]))

    return d3.scaleLinear()
      .domain([minVarValue, maxVarValue])
      .range(["#F9F1F8", "#015342"])
  }

  const changeVar = (reactiveVar) => {

    mapSelectedSheetData = Object.assign(new Map(googleSheetData.map(d => [d['townid'], +d[reactiveVar]])))

    varColorScale = varColorScaleGenerator(mapSelectedSheetData, reactiveVar)

    if(enterTownPaths){
      enterTownPaths
        .attr("fill", d => $selectedVar[0] !== '請選擇變數' ? varColorScale(mapSelectedSheetData.get(d.properties['TOWNID'])) : "#25877F")
    }

  }

  $: {

    $selectedVar[0] !== '請選擇變數' ? changeVar($selectedVar) : null
    
  }

  onMount(async () => {
  // canvas dimension
  const width = window.innerWidth * 0.95;
  const height = window.innerHeight * 0.95;

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
    .style("cursor", "pointer")
    .on("click", function (d) { countyZoom(d.properties.COUNTYID) })
    .on("mouseover", handleCountyMouseOver)
    .on("mouseout", handleCountyMouseOut)



  // zoom func
  function backToCounty() {
    // tooltip setting
    inCountyLevel = true
    document.querySelector(".town-tooltip").style.display = "none"

    const t = d3.transition().duration(800)

    twProjection.scale(10000).translate([width / 2, height / 2])

    counties.transition(t)
        .attr("d", twGeoPath)
        .attr("opacity", 1)
        .attr("fill", "#25877F")

    svg.selectAll(".town")
        .data([])
        .exit().transition(t)
        .attr("d", twGeoPath)
        .attr("opacity", 0)
        .remove()
  }

  function countyZoom(COUNTYID) {
    // tootip hover setting
    inCountyLevel = false
    document.querySelector(".county-tooltip").style.display = "none"

    const county = twCountyFeatures.find(function (d) { return d.properties.COUNTYID === COUNTYID })
    const countyTowns = twTownFeatures.filter(function (d) { return d.properties.COUNTYID === COUNTYID })

    const t = d3.transition().duration(800)

    const towns = svg.selectAll('.town')
        .data(countyTowns, function (d) { return d.properties.COUNTYID })

    enterTownPaths = towns.enter().append('path')
        .attr("id", d => d.properties['TOWNID'])
        .attr("class", "town")
        .attr("d", twGeoPath)
        .attr("fill", d => $selectedVar[0] !== '請選擇變數' ? varColorScale(mapSelectedSheetData.get(d.properties['TOWNID'])) : "#25877F")
        .attr("opacity", 0)
        .on("click", function () { backToCounty() })
        .on("mouseover", handleTownMouseOver)
        .on("mouseout", handleTownMouseOut)


    twProjection.fitExtent(
        [[130, 130], [width - 130, height - 130]],
        county
    )

    counties.transition(t)
        .attr('d', twGeoPath)
        .attr("opacity", 0.5)
        .attr('fill', '#25877F')

    enterTownPaths.transition(t)
        .attr('d', twGeoPath)
        .attr("stroke", "#333")
        .attr("stroke-width", 0.5)
        .attr('opacity', 1)

    towns.exit().transition(t)
        .attr('d', twGeoPath)
        .attr('opacity', 0)
        .remove()
    }
  })

  // mouse 

  function handleCountyMouseOver(d) {
    if (inCountyLevel) {
     document.querySelector(".county-tooltip").style.display = "block"
     hoverCounty = d3.select(this).data()[0]["properties"]["COUNTYNAME"] 
    }
  }

  function handleCountyMouseOut(d) {
    d3.select(this)
  }

  function handleTownMouseOver(d) {
    if (!inCountyLevel) {
    document.querySelector(".town-tooltip").style.display = "block"

    const hoverTownProperty = d3.select(this).data()[0]["properties"]
    hoverTown = hoverTownProperty["COUNTYNAME"] + hoverTownProperty["TOWNNAME"]
    varValue = $selectedVar[0] !== '請選擇變數' ? mapSelectedSheetData.get(hoverTownProperty['TOWNID']) : ""
    }
  }

  function handleTownMouseOut(d) {
    d3.select(this)
  }

</script>

<div class="interactive-map">
  <svg id ="tw-map"></svg>
</div>
<div class="tooltip">
  <div class="county-tooltip">
     <h2>{hoverCounty}</h2>
  </div>
  <div class="town-tooltip">
     <p>{hoverTown}</p>
     <InteractiveTool/>
     <div id="var-value">
       <p>{varValue}</p>
     </div>
  </div>
</div>



<style>
  .interactive-map{
    z-index: 1;
    margin: 0 auto;
  }
  .town-tooltip{
    text-align: center;
    display: none;
    width: 200px;
    top: 15%;
    right: 10%;
    position: fixed;
    z-index: 2;
    border: #25877F 1.2px solid;
    background-color: rgba(255, 255, 255, 0.5);    
  }
  .town-tooltip p{
    margin: 5% auto;
    color: #25877F;
    letter-spacing: 1.2px;
    
  }
  .town-tooltip #var-value{
    margin: 5% 10% 10% 10%;
    border-top: #25877F 1.2px solid;
    font-weight: bold;
  }

  .town-tooltip #var-value p{
    margin-top: 10%;
  }
  
  .county-tooltip{
    display: none;
    width: 140px;
    top: 15%;
    right: 10%;
    position: fixed;
    z-index: 2;
    border: #25877F 1.2px solid;
    background-color: rgba(255, 255, 255, 0.85);
  }
  .county-tooltip h2{
    text-align: center;
    margin: 10% auto;
    color: #25877F;
    letter-spacing: 2px;
  }
</style>

<!-- markup (zero or more items) goes here -->
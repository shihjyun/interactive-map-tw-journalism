<script>
  import { onMount, afterUpdate } from 'svelte';
  import * as d3 from 'd3';
  import * as topojson from 'topojson';
  import InteractiveTool from "./InteractiveTool.svelte";
  import { selectedVar } from '../stores/MapInfo.js'


  let twTownData
  let twTownFeatures
  // let varColorScale

  const twProjection = d3.geoMercator()
      .scale(6000)
      .center([122, 23.84394])

  const twgeoPath = d3.geoPath()
      .projection( twProjection );

  const varColorScaleGenerator = (gd, varName) => {
    
    const minVarValue = d3.min(gd.map(d => d.properties[varName]))
    const maxVarValue = d3.max(gd.map(d => d.properties[varName]))

    return d3.scaleLinear()
      .domain([minVarValue, maxVarValue])
      .range(["#FDF4FA", "#023C5E"])
  }

  const changeVar = (reactiveVar) => {
    let varColorScale = varColorScaleGenerator(twTownFeatures, reactiveVar)

    d3.selectAll("path")
      .data(twTownFeatures)
      .attr("fill", d => varColorScale(d.properties[reactiveVar]))
  }

  $: {

    $selectedVar[0] !== 'nothing' ? changeVar($selectedVar) : null
    
  }

  onMount(async () => {
    const response = await fetch("./data/tw_town_adjusted_bind_data.json");
    twTownData = await response.json();
    twTownFeatures = topojson.feature(twTownData, twTownData.objects.tw_town_adjusted_bind_data).features

    const svg = d3.select("svg")

    svg.selectAll( "path" )
      .data(twTownFeatures)
      .enter()
      .append("path" )
      .attr("id", d => d.properties['TOWNNAME'])
      .attr("fill", "#E3DBD9")
      .attr("stroke", "#333")
      .attr("stroke-width", 0.5)
      .attr("d", twgeoPath );
  })

</script>

<div class="map">
  <svg width={700}
     height={600}
     viewBox={`0 0 ${700} ${600}`}
     id ="tw-map"></svg>
</div>
<InteractiveTool/>


<style>
  .map{
    margin: 0 auto;
  }
</style>

<!-- markup (zero or more items) goes here -->
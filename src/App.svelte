<script>
	import TaiwanMap from "./components/TaiwanMap.svelte";


	let mapScope;

  const changeVar = (town) => {
    const slopeChart = d3.select(mapScope)

    slopeChart
      .selectAll('path')
      .attr("fill", "rgba(16, 14, 14, 0.2)")
  }
</script>

<main>
	<h1>互動式台灣地圖</h1>
	<TaiwanMap/>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: black;
		font-family: "Noto Sans TC";
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
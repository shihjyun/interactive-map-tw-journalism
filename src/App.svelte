<script>
	import TaiwanMap from "./components/TaiwanMap.svelte";
</script>

<main>
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
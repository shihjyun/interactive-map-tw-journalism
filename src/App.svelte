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
		max-width: 60%;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
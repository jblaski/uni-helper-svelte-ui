<script>
	import Search from './Search.svelte'
	import AutoComplete from "simple-svelte-autocomplete"

	let selectedCity;
	let searchComponent;

	async function handleSubmit() {
		let url = 'http://localhost:8080/api/proximity?cityName=' + selectedCity.cityName + '&count=1';
		let res = await fetch(url);
		let unis = await res.json();
		console.log(unis);
		alert(`Selected ${selectedCity.cityName}. Closest: ` + unis[0].providerName);
	}
</script>

<main>
	<h1>Welcome to Uni-Helper</h1>
	<p>Use the search box below to find a University near you</p>
	<Search bind:this={searchComponent} bind:selectedCity on:submit={handleSubmit}/>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
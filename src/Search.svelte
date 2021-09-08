<script>
    import AutoComplete from "simple-svelte-autocomplete";
    import { fade } from 'svelte/transition';
    import { createEventDispatcher } from "svelte";
    import { onMount } from 'svelte';


    let cities = [];
    export let selectedCity;
    
    // TODO: Instead of this, should probably use a "store"?
    const dispatch = createEventDispatcher();
    const submit = () => dispatch('submit');

	onMount(async () => {
		const res = await fetch('http://localhost:8080/api/cities');
		cities = await res.json();
	});

</script>

<p>This is my search component</p>

<AutoComplete items={cities} bind:selectedItem={selectedCity} labelFieldName="cityName" />

{#if selectedCity != null} 
    <p transition:fade>Selected town: {selectedCity.cityName}</p>
    <button disabled={!selectedCity} on:click={submit} transition:fade>Search</button>
{/if}





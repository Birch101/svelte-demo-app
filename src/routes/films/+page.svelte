<script>
	import { onMount } from 'svelte';

	/**
	 * @type {any[]}
	 */
	let films = [];

	onMount(() => {
		fetch('https://rest-api-demo-cb.azurewebsites.net/films')
			.then((response) => response.json())
			.then((result) => (films = result));
	});
</script>

<svelte:head>
	<title>Films</title>
	<meta name="description" content="These are my projects" />
</svelte:head>

<div class="text-column">
	<h1>Films</h1>
</div>

<div class="container d-flex flex-wrap align-items-center">
	{#each films as { id, title, plot }, i}
		<div class="card film-card">
			<div class="card-body">
				<h5 class="card-title">{title}</h5>
				<p class="card-text">{plot}</p>
				<a href="films/{id}" class="btn btn-primary">View Details</a>
			</div>
		</div>
	{/each}
</div>

<style>
	.film-card {
		margin: 0.5em;
		width: 18rem;
		min-height: 9em;
		min-width: 9em;
	}
</style>

<script>
	import { onMount } from 'svelte';

	/**
	 * @type {any[]}
	 */
	let films = [];

	onMount(() => {
		// TODO: ideally this url would be in config
		fetch('https://rest-api-demo-cb.azurewebsites.net/films')
			.then((response) => response.json())
			.then((result) => (films = result));
	});
</script>

<svelte:head>
	<title>TV & Films</title>
	<meta name="description" content="This is a list of all the tv series and films" />
</svelte:head>

<div class="text-column">
	<h1>TV & Films</h1>
</div>

<div class="container d-flex flex-wrap align-items-center">
	{#each films as { id, title, plot }, i}
		<div class="card film-card">
			<div class="card-header film-card-header">
				<h5>{title}</h5>
			</div>
			<div class="card-body">
				<p class="card-text">{plot}</p>
			</div>
			<div class="card-footer text-end">
				<a href="films/{id}" class="btn btn-primary">View Details</a>
            </div>
		</div>
	{/each}
</div>

<style>
	.film-card {
		margin: 0.5em;
		width: 18rem;
		min-height: 18em;
		min-width: 9em;
	}
</style>

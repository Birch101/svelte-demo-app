<script>
	import { onMount } from 'svelte';

	/**
	 * @type {any[]}
	 */
	let films = [];

	/** @type {import('./$types').PageData} */
	export let data;

	onMount(async () => {
		const res = await fetch('https://rest-api-demo-cb.azurewebsites.net/films/search', {
			method: 'POST',
			body: JSON.stringify({ filmId: data.filmId }),
			headers: {
				'Content-Type': 'application/json'
			}
		})
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
	{#each films as { id, title, year, rated, released, runtimeMinutes, genre, director, writer, actors, plot, language, country, awards, poster, metascore, imdbRating, imdbVotes, type }, i}
		<div class="card film-card">
			<div class="card-body">
				<h5 class="card-title">{title}</h5>


                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Title</span>
					</div>
					<input type="text" class="form-control" value={title} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Plot</span>
					</div>
					<textarea rows="3" class="form-control" value={plot} />
				</div>
				<div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Rated</span>
					</div>
					<input type="text" class="form-control" value={rated} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Year</span>
					</div>
					<input type="text" class="form-control" value={year} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Released</span>
					</div>
					<input type="text" class="form-control" value={released} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Runtime</span>
					</div>
					<input type="text" class="form-control" value={runtimeMinutes} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Genre</span>
					</div>
					<input type="text" class="form-control" value={genre} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Director</span>
					</div>
					<input type="text" class="form-control" value={director} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Writers</span>
					</div>
					<textarea rows="3" class="form-control" value={writer} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Actors</span>
					</div>
					<input type="text" class="form-control" value={actors} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Language</span>
					</div>
					<input type="text" class="form-control" value={language} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Country</span>
					</div>
					<input type="text" class="form-control" value={country} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Awards</span>
					</div>
					<input type="text" class="form-control" value={awards} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">Metascore</span>
					</div>
					<input type="text" class="form-control" value={metascore} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">IMDb Rating</span>
					</div>
					<input type="text" class="form-control" value={imdbRating} />
				</div>
                <div class="input-group mb-3">
					<div class="input-group-prepend">
						<span class="input-group-text film-property-prepend">IMDb Votes</span>
					</div>
					<input type="text" class="form-control" value={imdbVotes} />
				</div>
			</div>
		</div>
	{/each}
</div>

<style>
	.film-card {
		margin: 0.5em;
		width: 100%;
		min-height: 9em;
		min-width: 9em;
	}

    .film-property-prepend {
        min-width: 7em;
    }
</style>

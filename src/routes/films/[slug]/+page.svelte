<script>
	import { onMount } from 'svelte';
	import Carousel from 'svelte-carousel';

	/**
	 * @type {{ title: any; type: any; plot: any; rated: any; year: any; released: string | number | Date; runtimeMinutes: any; genre: any; director: any; writer: any; actors: any; language: any; country: any; awards: any; metascore: any; imdbRating: any; imdbVotes: any; images: any; }}
	 */
	let film;

	/** @type {import('./$types').PageData} */
	export let data;

	let carousel;

	onMount(async () => {
		// TODO: ideally this url would be in config
		const res = await fetch('https://rest-api-demo-cb.azurewebsites.net/films/search', {
			method: 'POST',
			body: JSON.stringify({ filmId: data.filmId }),
			headers: {
				'Content-Type': 'application/json'
			}
		})
			.then((response) => response.json())
			.then((result) => (film = result[0]));
	});
</script>

<svelte:head>
	<title>{film?.title}</title>
	<meta name="description" content="This is the details for {film?.title}" />
</svelte:head>

<div class="text-column">
	<h1>{film?.title} [{film?.type}]</h1>
</div>

<div class="container d-flex flex-wrap align-items-center">
	<div class="card film-card">
		<div class="card-body">
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Plot</span>
				</div>
				<textarea rows="3" readonly class="form-control" value={film?.plot} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Rated</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.rated} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Year</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.year} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Released</span>
				</div>
				<input
					type="text"
					readonly
					class="form-control"
					value={new Date(film?.released).toDateString()}
				/>
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Runtime</span>
				</div>
				<input type="text" readonly class="form-control" value="{film?.runtimeMinutes} mins" />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Genre</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.genre} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Director</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.director} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Writers</span>
				</div>
				<textarea rows="3" readonly class="form-control" value={film?.writer} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Actors</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.actors} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Language</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.language} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Country</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.country} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Awards</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.awards} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">Metascore</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.metascore} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">IMDb Rating</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.imdbRating} />
			</div>
			<div class="input-group mb-3">
				<div class="input-group-prepend">
					<span class="input-group-text film-property-prepend">IMDb Votes</span>
				</div>
				<input type="text" readonly class="form-control" value={film?.imdbVotes} />
			</div>
			{#if film !== undefined}
				<Carousel bind:this={carousel}>
					{#each film?.images as { imageURL }, i}
						<img src={imageURL} class="d-block w-100" alt="Film image {i}" />
					{/each}
				</Carousel>
			{/if}
		</div>
	</div>
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

	input[readonly] {
		background-color: white;
	}

	textarea[readonly] {
		background-color: white;
	}
</style>

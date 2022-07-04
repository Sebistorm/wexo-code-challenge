<script>
    import { onMount } from "svelte";
    import { Link } from "svelte-navigator";
    import Showcase from "../home/showcase.svelte";

    // action movies
    export let genre;
    export let movies = [];
    let count;


    onMount(async () => {
        // movies start
        fetch(`https://feed.entertainment.tv.theplatform.eu/f/jGxigC/bb-all-pas?form=json&fields=id,title,plprogram$thumbnails&byTags=genre:${genre}&byProgramType=movie`)
        .then(response => response.json())
        .then(result => {
            count = result.entries.length;
            movies = result.entries.slice(12,16);
            console.log(movies)
        })
        .catch(error => console.log('error', error));
        // movies End
	});
</script>

<div class="row">
    <div class="d-flex align-items-center">
        <h2>{genre} Movies ({count})</h2> <p class="categoryLink"><Link to="">Explore more</Link></p>
    </div>
    <div class="showcaseWrapper">
        {#each movies as movie}
            <Showcase url={movie.id.split("ProgramAvailability/")[1]} title={movie.title} imgSrc={movie.plprogram$thumbnails["orig-365x251"].plprogram$url} />
        {/each}
    </div>
</div>

<style>
.showcaseWrapper {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-row-gap: 1rem;
    grid-column-gap: 1rem;
}

h2 {
    margin-bottom: 1rem;
}

.categoryLink {
    font-size: 1.5rem;
    margin-left: 1rem;
    color: blue;
}

.row {
    margin-bottom: 2rem;
}
</style>
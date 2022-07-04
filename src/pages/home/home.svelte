<script>
    import { onMount } from "svelte";
    import { Link } from "svelte-navigator";
    import Showcase from "../../components/home/showcase.svelte";

    // action movies
    export let actionMovies = [];
    let actionMoviesCount;

    onMount(async () => {
        // action movies start
        fetch("https://feed.entertainment.tv.theplatform.eu/f/jGxigC/bb-all-pas?form=json&fields=id,title,plprogram$thumbnails&byTags=genre:action&byProgramType=movie")
        .then(response => response.json())
        .then(result => {
            //console.log(result.entries);
            actionMoviesCount = result.entries.length;
            actionMovies = result.entries.slice(0,4);
        })
        .catch(error => console.log('error', error));
        // action movies End
	});


</script>

<main>
    <div class="container">
        <h1>Wexo</h1>
        <div class="row">
            <div class="d-flex align-items-center">
                <h2>Action Movies ({actionMoviesCount})</h2> <p class="categoryLink"><Link to="">Explore more</Link></p>
            </div>
            <div class="showcaseWrapper">
                {#each actionMovies as actionMovie}
                    <Showcase url={actionMovie.id.split("ProgramAvailability/")[1]} title={actionMovie.title} imgSrc={actionMovie.plprogram$thumbnails["orig-396x272"].plprogram$url} />
                {/each}
            </div>
        </div>
    </div>
</main>

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
</style>
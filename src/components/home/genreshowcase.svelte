<script>
    import { onMount } from "svelte";
    import { Link } from "svelte-navigator";
    import Showcase from "../shared/showcase.svelte";

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
            movies = result.entries.slice(0,4);
            movies.forEach(movie => {
                if(typeof movie.plprogram$thumbnails["orig-365x251"] === "undefined") {
                    movie.plprogram$thumbnails["orig-365x251"] = "https://prod.cdn.bbaws.net/TDC_Blockbuster_-_Production/505/1012/4280009392-po-reg-appletv_orig-1641373999314.jpg";
                }
            });
        })
        .catch(error => console.log('error', error));
        // movies End
	});
</script>

<div class="row">
    <div class="headerWrapper d-flex align-items-center">
        <h2>{genre} Movies ({count})</h2> <p class="categoryLink"><Link to="/movies/{genre}">Explore more</Link></p>
    </div>
    <div class="showcaseWrapper">
        {#each movies as movie}
            <Showcase url={movie.id.split("ProgramAvailability/")[1]} title={movie.title} imgSrc={movie.plprogram$thumbnails["orig-365x251"].plprogram$url || movie.plprogram$thumbnails["orig-365x251"]} />
        {/each}
    </div>
</div>

<style>
.showcaseWrapper {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-row-gap: 2rem;
    grid-column-gap: 1rem;
}

h2 {
    margin-bottom: 1.5rem;
}

.categoryLink {
    font-size: 1.5rem;
    margin-left: 1rem;
    color: blue;
}

.row {
    margin-bottom: 2rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid #bbbbbb;
}

@media screen and (max-width: 600px) {
    .showcaseWrapper {
        grid-template-columns: 1fr 1fr;
    }
}

@media screen and (max-width: 400px) {
    .headerWrapper {
        flex-direction: column;
    }

    h2 {
        margin-bottom: .5rem;
    }
}

</style>
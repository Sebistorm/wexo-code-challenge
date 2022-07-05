<script>
    let url_string = window.location.pathname;
    let genre = url_string.split("movies/")[1]

    import { onMount } from "svelte";
    import Showcase from "../../components/shared/showcase.svelte";

    // action movies
    export let movies = [];
    let count;


    onMount(async () => {
        // movies start
        fetch(`https://feed.entertainment.tv.theplatform.eu/f/jGxigC/bb-all-pas?form=json&fields=id,title,plprogram$thumbnails&byTags=genre:${genre}&byProgramType=movie`)
        .then(response => response.json())
        .then(result => {
            count = result.entries.length;
            movies = result.entries;
            //console.log(movies)
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

<div class="container">
    <h1>{genre} ({count})</h1>
    <div class="row">
        <div class="showcaseWrapper">
            {#each movies as movie}
                <Showcase url={movie.id.split("ProgramAvailability/")[1]} title={movie.title} imgSrc={movie.plprogram$thumbnails["orig-365x251"].plprogram$url || movie.plprogram$thumbnails["orig-365x251"]} />
            {/each}
        </div>
    </div>
</div>



<style>
.showcaseWrapper {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-row-gap: 1rem;
    grid-column-gap: 1rem;
}
</style>
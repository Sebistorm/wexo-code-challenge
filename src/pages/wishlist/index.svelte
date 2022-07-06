<script>
    import {wishlist} from "../../store/store"

    import Showcase from "../../components/wishlist/showcase.svelte";

</script>

<div class="container">
    <h1>Wishlist</h1>
    <div class="row">
        <div class="showcaseWrapper">
            {#each $wishlist as movie}
                <Showcase url={movie.id} title={movie.title} imgSrc={movie.img} />
            {/each}
        </div>
    </div>
</div>


<style>
.showcaseWrapper {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-row-gap: 2rem;
    grid-column-gap: 1rem;
}

.container {
    min-height: calc(100vh - 16.2rem);
}

h1 {
    margin-bottom: 1.5rem;
}

@media screen and (max-width: 991px) {
    .showcaseWrapper {
        grid-template-columns: 1fr 1fr 1fr;
    }
}

@media screen and (max-width: 600px) {
    .showcaseWrapper {
        grid-template-columns: 1fr 1fr;
    }
}
</style>
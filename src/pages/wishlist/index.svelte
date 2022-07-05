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
    grid-row-gap: 1rem;
    grid-column-gap: 1rem;
}
</style>
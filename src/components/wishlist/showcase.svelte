<script>
    import {Link} from "svelte-navigator";

    import {wishlist} from "../../store/store";

    export let url
    export let title;
    export let imgSrc;

    const removeFromWishlist = (movieid) => {
        $wishlist = $wishlist.filter(w => w.id != movieid.url);
    }

</script>

<div class="showcase">
    <Link to="/movie/{url}"> 
        <img src="{imgSrc}" alt="{title}">
        <p>{title}</p>
    </Link>
    <button on:click="{() => removeFromWishlist({url})}" class="btn btn-primary">Delete from wishlist</button>
    
</div>

<style>



p{
    font-size: 1.5rem;
    text-align: center;
}

img {
    width: 100%;
    height: auto;
}

button {
    width: 100%;
}
</style>


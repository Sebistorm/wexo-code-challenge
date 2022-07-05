<script>
    import {Link} from "svelte-navigator";

    export let url
    export let title;
    export let imgSrc;
</script>

<div class="showcase">
    <Link to="/{url}"> 
        <img src="{imgSrc}" alt="{title}">
        <p>{title}</p>
    </Link>
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
</style>


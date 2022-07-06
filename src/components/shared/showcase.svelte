<script>
    import {Link} from "svelte-navigator";

    export let url
    export let title;
    export let imgSrc;
</script>

<div class="showcase">
    <Link to="/movie/{url}"> 
        <img src="{imgSrc}" alt="{title}">
        <p>{title}</p>
    </Link>
</div>

<style>



p{
    font-size: 1.5rem;
    text-align: center;
    margin-top: .5rem;
}

img {
    width: 100%;
    height: auto;
}

@media screen and (max-width: 991px) {
    p {
        font-size: 1rem;
    }
}
</style>


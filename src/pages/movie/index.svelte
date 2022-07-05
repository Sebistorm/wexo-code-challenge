<script>
    let url_string = window.location.pathname;
    let id = url_string.split("movie/")[1]

    import { onMount } from "svelte";
    import {wishlist} from "../../store/store";
    import Crew from "../../components/shared/crew.svelte"

    let movie = {
        title: null,
        description: null,
        year: null,
        thumbnail: null,
        genre: null
    }

    export let crew = [];

    onMount(async () => {
        // movie start
        fetch(`https://feed.entertainment.tv.theplatform.eu/f/jGxigC/bb-all-pas/${id}?form=json&`)
        .then(response => response.json())
        .then(result => {
            movie = {
                title: result.title,
                description: result.description,
                year: result.plprogram$year,
                thumbnail: result.plprogram$thumbnails["orig-594x408"].plprogram$url,
                genre: result.plprogram$tags[0].plprogram$title
            }
            crew = result.plprogram$credits;
            
        })
        .catch(error => console.log('error', error));
        // movie End
	});

    
    let movieAddedtoWishlist = false;
    $wishlist.forEach(movie => {
        if(movie.id == id) {
            movieAddedtoWishlist = true;
        }
    });
    

    const addToWishlist = () => {
        $wishlist = [...$wishlist, {
            id: id,
            title: movie.title,
            img: movie.thumbnail
        }];
        movieAddedtoWishlist = true;
    };

    const removeFromWishlist = (movieid) => {
        $wishlist = $wishlist.filter(w => w.id != movieid.id);
        movieAddedtoWishlist = false;
    }


</script>

<div class="container">
    <div class="row">
        <div class="movie">
            
            <div class="left">
                <img src="{movie.thumbnail}" alt="{movie.title}">
            </div>
            <div class="right">
                <h1>{movie.title}</h1>
                <h3>{movie.genre}</h3>
                <p>{movie.description}</p>
                <p>Releasedate: {movie.year}</p>
                {#if movieAddedtoWishlist == true}
                    <button on:click="{() => removeFromWishlist({id})}" class="btn btn-primary">Remove from Wishlist</button>
                {/if}
                {#if movieAddedtoWishlist == false}
                    <button on:click="{addToWishlist}" class="btn btn-primary">Add to Wishlist</button>
                {/if}
                
            </div>
        </div>
    </div>

    <div class="row">
        <h2 class="mb-4 mt-4">Crew</h2>
        <div class="crewWrapper">
            {#each crew as c}
                <Crew name={c.plprogram$personName} role={c.plprogram$creditType}   />
            {/each}
        </div>
    </div>

</div>


<style>
    .movie {
        display:grid;
        grid-template-columns: 1fr 2fr;
    }

    .right {
        padding: 1rem 2rem;
        background-color: #cacaca;
    }

    .left {
        display: flex;
        justify-content: end;
    }

    img {
        width: 100%;
        height: auto;
        object-fit: cover;
    }

    .crewWrapper {
        display:grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
        grid-column-gap: 1rem;
    }


    h2 {
        max-width: 200px;
        border-bottom: 1px solid #c1c1c1;
        padding-bottom: 0.5rem;
    }

</style>
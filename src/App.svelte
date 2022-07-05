<script>
  import { Router, Link, Route } from "svelte-navigator";

  import HomePage from "./pages/home/home.svelte";
  import OverviewByGenrePage from "./pages/overviewByGenre/index.svelte"
  import MoviePage from "./pages/movie/index.svelte"
  import WishlistPage from "./pages/wishlist/index.svelte";

</script>

<Router>
	<nav>
		<Link to="/">Home</Link>
		<Link to="/wishlist">Wishlist</Link>
		<Link to="blog">Blog</Link>
	</nav>
	<div>
		<Route path="/">
			<HomePage />
		</Route>
    <Route path="/wishlist">
			<WishlistPage />
		</Route>

    <Route path="movies/:genre" component={OverviewByGenrePage} />
    <Route path="movie/:id" component={MoviePage} />
	</div>
</Router>


<style>

  :global(.categoryLink a) {
    text-decoration: none !important;
    color: #282895 !important;
  }

  :global(a) {
    text-decoration: none !important;
    color: unset;
  }

  :global(a):hover {
    text-decoration: none !important;
    color: unset;
  }

  :global(.crew):nth-child(2n) {
    background-color: #cacaca;
  }
 
</style>

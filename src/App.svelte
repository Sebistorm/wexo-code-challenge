<script>
  import { Router, Link, Route } from "svelte-navigator";

  import HomePage from "./pages/home/home.svelte";
  import OverviewByGenrePage from "./pages/overviewByGenre/index.svelte"
  import MoviePage from "./pages/movie/index.svelte"
  import WishlistPage from "./pages/wishlist/index.svelte";

</script>

<Router>
	<nav>
    <div class="container">
      <Link to="/">Home</Link>
      <Link to="/wishlist">Wishlist</Link>
    </div>
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

<footer>
  <div class="container">
    <h2>Footer</h2>
  </div>
</footer>


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

  nav {
    background-color: #202429;
    color: white;
    padding: 1.3rem 0px;
    margin-bottom: 2rem;
  }

  :global(nav a) {
    padding: 0px 1rem;
    font-size: 1.1rem;
  }

  :global(nav a):hover {
    color: #ffb836;
  }

  :global(nav a):first-of-type {
    padding: 0px 1rem 0px 0px;
  }

  footer {
    background-color: #202429;
    color: white;
    padding: 1.5rem 0px;
    margin-top: 4rem;
  }
 
</style>

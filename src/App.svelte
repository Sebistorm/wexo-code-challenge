<script>
  import { Router, Link, Route } from "svelte-navigator";

  import HomePage from "./pages/home/home.svelte";
  import OverviewByGenre from "./pages/overviewByGenre/index.svelte"

</script>

<Router>
	<nav>
		<Link to="/">Home</Link>
		<Link to="about">About</Link>
		<Link to="blog">Blog</Link>
	</nav>
	<div>
		<Route path="/">
			<HomePage />
		</Route>
    <Route path="movies/:genre" component={OverviewByGenre} />
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
 
</style>

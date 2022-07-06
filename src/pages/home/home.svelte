<script>
    import GenreShowcase from "../../components/home/genreshowcase.svelte";



</script>

<main>
    <div class="container">
        <h1>Wexo</h1>
        
        <GenreShowcase genre="Action" />
        <GenreShowcase genre="War" />
        <GenreShowcase genre="Thriller" />
        <GenreShowcase genre="Romance" />
        <GenreShowcase genre="Crime" />
        <GenreShowcase genre="Documentary" />
        <GenreShowcase genre="Horror" />
        <GenreShowcase genre="Comedy" />
        <GenreShowcase genre="Drama" />
        
    </div>
</main>

<style>
    h1 {
        margin-bottom: 1rem;
    }

</style>
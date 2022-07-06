<script>
    export let name;
    export let role;
</script>


<div class="crew">
    <img src="https://www.kino.dk/sites/all/themes/kino/img/user-default.jpg" alt="">
    <h3>{name}</h3>
    <h4>{role}</h4>
</div>

<style>

.crew {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
}

.crew img {
    max-width: 100px;
    border-radius: 100%;
}

h3 {
    font-size: 1.2rem;
    margin-top: 0.2rem;
    margin-bottom: 0px;
    text-align: center;
}

h4 {
    font-size: 1rem;
    margin-top: 0.2rem;
    font-weight: 600;
}

</style>
<script>
    import { blur } from "svelte/transition";
    import { onMount } from "svelte";
    export let bookData = [];
    export let position;
    let ready = false;

    onMount(() => {
        ready = true;
    });

</script>

<style>
    @import "$lib/theme.css";
    .card {
        border-radius: 20px;
        background-color: var(--card);
        display: inline-block;
        padding: 10px 0px 0px 0px;
        box-shadow: 7px 7px 7px black;
        font-family: "Abel", sans-serif;
    }
    .card:hover {
        box-shadow: 10px 10px 10px black;
        border: 2px solid var(--ring);
    }
    img {
        border-radius: 20px;
        margin: 10px 15px 10px 15px;
        width: 350px;
        height: 425px;
    }
    @media screen and (max-width: 640px) {
        img {
            width: 245px;
            height: 300px;
        }
    }
    p {
        text-align: center;
        color: rgb(242, 242, 247);
    }
    .name, .author {
        margin: 0px;
        padding: 10px;
    }
    .name {
        background-color: var(--name);
    }
    .author {
        color: white;
        background-color: var(--author);
    }
    a {
        text-decoration: none;
    }
    .link {
        text-align: center;
        background-color: var(--button);
        color: rgb(28, 28, 30);
        margin: 0px;
        border-radius: 0px 0px 20px 20px;
        height: 30px;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .link:hover {
        background-color: lightgreen;
    }
</style>

{#if ready}
    <div class = "card" transition:blur={{ delay: (position + 1) * 100, duration: 500 }}>
        <center><img src={bookData[2]} alt={bookData[0]}></center>
        <p class = "name"><strong>{bookData[0]}</strong></p>
        <p class = "author"><i>{bookData[1]}</i></p>
        <a href="/"><p class = "link"><strong>Download</strong></p></a>
    </div>
{/if}
<script>
    import Bar from "./Bar.svelte";
    import Books from "./Books.svelte";
    import Database from "$lib/database.json";

    let query = "";
    let results = null;

    async function search(string) {
        string = string.toLowerCase();
        return Database.filter((book) =>
            book[0].toLowerCase().includes(string) ||
            book[1].toLowerCase().includes(string)
        );
    }

    $: if(query) {
        results = search(query);
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Abel&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Playwrite+CU:wght@100..400&display=swap');

    @import "$lib/theme.css";
    .search {
        display: flex;
        align-items: center;
        position: sticky;
        flex-direction: column;
        background-color: var(--search);
        margin: 0px auto;
        padding-bottom: 20px;
        top: 0px;
        width: 30%;
        border-radius: 0px 0px 30px 30px;
    }
    .search p {
        color: white;
        font-size: 25px;
        font-family: "Playwrite CU", cursive;
    }
    @media screen and (max-width: 640px) {
        .search {
            position: sticky;
            width: 100%;
        }
        .search p {
            font-size: 17px;
        }
    }
    .search input {
        width: 80%;
        height: 30px;
        border-radius: 20px;
        border: none;
        padding: 10px;
        font-size: 17px;
        font-weight: bold;
        font-family: "Abel", sans-serif;
    }
</style>

<Bar />


<div class = "search">
    <p>What would you like to learn today?</p>
    <input bind:value={query} placeholder="Search for books & authors...">
</div>

{#if query == ""}
    <Books {Database} />
{:else}
    {#await results}
        <h1>Waiting...</h1>
    {:then response}
        <Books Database={response} />
    {/await}
{/if}
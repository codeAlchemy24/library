<script>
    import Bar from "./Bar.svelte";
    import Books from "./Books.svelte";
    import Database from "./database.json";

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
    @import "./theme.css";
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
    .search h3 {
        color: white;
    }
    .search input {
        width: 80%;
        height: 30px;
        border-radius: 20px;
        padding: 5px;
    }
</style>

<Bar />

<br />

<div class = "search">
    <h3>What would you like to learn today?</h3>
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
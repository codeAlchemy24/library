<script>
    import Books from "./Books.svelte";
    import Database from "./database.json";

    let query = "";
    let results = [];

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
    .search {
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .search input {
        width: 50%;
        height: 30px;
        border-radius: 10px;
    }
</style>

<div class = "search">
    <input bind:value={query} placeholder="Search for book & authors...">
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
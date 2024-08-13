<script>
    import Card from "./Card.svelte";
    export let Database;
</script>

<style>
    .grid {
        display: grid;
        grid-template-columns: repeat(4, auto);
        gap: 20px;
        margin: 15px 15px;
    }
</style>

<div class = "grid">
    {#each Database as book, position}
        <Card bookData={book} {position}/>
    {/each}
</div>
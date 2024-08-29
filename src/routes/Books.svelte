<script>
    import Card from "./Card.svelte";
    import PageIndicator from "./PageIndicator.svelte";

    export let Database;

    let current = 0;
    let step = 16;
    let size = Database.length;

    function next() {
        current += step;
        if(current > size) {
            current = 0;
        }
        window.scrollTo(0, 0);
    }
    function prev() {
        current -= step;
        if(current < 0) {
            current = 0;
        }
        window.scrollTo(0, 0);
    }
</script>

<style>
    .grid {
        display: grid;
        grid-template-columns: repeat(4, auto);
        gap: 20px;
        margin: 15px 15px;
    }
    .buttons {
        display: flex;
        justify-content: center;
        gap: 20px;
        padding: 20px;
    }
    .left, .right {
        height: 50px;
        width: 75px;
        background-color: var(--author);
        color: white;
        border: 2px solid var(--author);
        font-size: 16px;
        border: 3px solid var(--gold);
    }
    .left {
        border-radius: 15px 0px 0px 15px;

    }
    .right {
        border-radius: 0px 15px 15px 0px;
    }
</style>

<div class = "grid">
    {#each Database.slice(current, current + step) as book, position}
        <Card bookData={book} {position}/>
    {/each}
</div>

<PageIndicator currentPage={(current / step) + 1} totalPages={(size / step) + 1} />

<div class = "buttons">
    <button class="left" on:click={prev}>Prev</button>
    <button class="right" on:click={next}>Next</button>
</div>
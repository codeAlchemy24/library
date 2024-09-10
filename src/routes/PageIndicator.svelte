<script>
    export let currentPage;
    export let totalPages;

    currentPage = parseInt(currentPage);
    totalPages = parseInt(totalPages);
</script>

<style>
    .block {
        display: flex;
        flex-direction: column;
        align-items: center;
        color: white;
        font-family: "Abel", sans-serif;
        font-family: "Playwrite CU", sans-serif;
    }

    .title {
        font-size: 20px;
        margin: 10px;
    }
    .pages {
        font-size: 25px;
        margin: 0px;
    }
</style>

<div class = "block">
    <p class = "title">Page</p>
    <p class = "pages"><strong>{currentPage} of {totalPages}</strong></p>
</div>
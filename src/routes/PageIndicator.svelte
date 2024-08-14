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
    }

    .title {
        font-size: 20px;
        margin: 10px;
    }
    .pages {
        font-size: 30px;
        margin: 0px;
    }
</style>

<div class = "block">
    <p class = "title">Page</p>
    <p class = "pages">{currentPage} of {totalPages}</p>
</div>
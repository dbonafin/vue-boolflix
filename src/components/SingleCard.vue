<template>

    <div class="single-card">
        <h4>{{ film.title }}</h4>
        <h4>{{ film.original_title }}</h4>
        <h4>{{ film.original_language }}</h4>
        <h4>{{ film.vote_average }}</h4>
    </div>

</template>

<script>

    export default {
        name: "SingleCard",
        props: {film: Object}
    }

</script>

<style lang="scss">

    .single-card {
        // test
        width: 200px;
        height: 300px;
        background-color: lightblue;
        h4 {
            color: black;
        }
    }

</style>
<template>

    <div class="single-card">
        <h4>Title: {{ film.title }}</h4>
        <h4>OG title: {{ film.original_title }}</h4>
        <h4>OG language: {{ film.original_language }}</h4>
        <h4>Vote: {{ film.vote_average }}</h4>
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
            margin: 5px 0;
        }
    }

</style>
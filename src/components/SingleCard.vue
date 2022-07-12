<template>

    <div class="single-card">
        <h4>Title: {{ film.title }}</h4>
        <h4>OG title: {{ film.original_title }}</h4>
        <h4>Language: <lang-flag :iso="film.original_language" :squared="false" /> </h4>
        <h4>Vote: {{ film.vote_average }}</h4>
    </div>

</template>

<script>

    import LangFlag from 'vue-lang-code-flags';

    export default {
        name: "SingleCard",
        props: { film: Object },
        components: { LangFlag },
    }

</script>

<style lang="scss">

    .single-card {
        padding: 4px;
        width: 200px;
        height: 300px;
        background-color: lightblue;
        h4 {
            color: black;
            margin: 10px 0;
        }
    }

</style>
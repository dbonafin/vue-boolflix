<template>

    <div class="single-serie">

        <h3>Tv Serie</h3>
        <h4>Name: {{ serie.name }}</h4>
        <h4>OG name: {{ serie.original_title }}</h4>
        <h4>
            Language: <lang-flag :iso="serie.original_language" :squared="false"/> 
        </h4>
        <h4>Vote: {{ serie.vote_average }}</h4>

    </div>

</template>

<script>

    import LangFlag from 'vue-lang-code-flags';

    export default {
        name: "SingleCard",
        props: { serie: Object },
        components: { LangFlag },
    }

</script>

<style lang="scss">

    @import "../style/colors.scss";

    .cards {
        display: flex;
        flex-wrap: wrap;
    }
    .single-serie {
        margin: 10px;
        padding: 4px;
        width: 200px;
        height: 300px;
        background-color: $secondary-color;
        h3 {
            text-align: center;
            margin-bottom: 30px;
            color: $primary-color;
        }
        h4 {
            margin: 10px 0;
            font-size: 14px;
        }
    }

</style>
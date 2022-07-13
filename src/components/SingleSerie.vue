<template>

    <div class="single-card">

        <h3>Tv Serie</h3>
        <img v-if="serie.poster_path" :src="imgUrl" alt="image">
        <!-- alternative image if the item does not have an image -->
        <img v-else class="alternative-img" src="https://placehold.jp/40/211f1f/ff0027/220x270.png?text=Image+Not+Found" alt="image">

        <!-- Single tv serie infos on hover -->
        <div class="overlay">
            <h4>Name: {{ serie.name }}</h4>
            <h4>OG name: {{ serie.original_title }}</h4>
            <h4>
                Language: <lang-flag :iso="serie.original_language" :squared="false"/> 
            </h4>
            <h4>Vote: {{ serie.vote_average }}</h4>
        </div>
        
    </div>

</template>

<script>

    import LangFlag from 'vue-lang-code-flags';

    export default {
        name: "SingleCard",
        data() {
            return {
                imgUrl: `https://image.tmdb.org/t/p/w185${this.serie.poster_path}`
            }
        },
        props: { serie: Object },
        components: { LangFlag },
    }

</script>

<style lang="scss">

    @import "../style/colors.scss";

</style>
<template>

    <div class="single-card">

        <h3>Tv Serie</h3>
        <img v-if="serie.poster_path" :src="imgUrl" alt="image">
        <!-- alternative image if the item does not have an image -->
        <img v-else class="alternative-img" src="https://placehold.jp/40/211f1f/ff0027/220x270.png?text=Image+Not+Found" alt="image">

        <!-- Single tv serie infos on hover -->
           <div class="overlay">
            <p><b>Title:</b> {{ serie.title }}</p>
            <p><b>OG title:</b> {{ serie.original_title }}</p>
            <p><b>Vote:</b> {{ decimalToBinary }}</p>
            <p v-if="serie.overview">
                <b>Overview: </b> 
                {{serie.overview.substring(0,80)+".."}}
            </p>
            <p v-else>
                <b>Language: </b> 
                <lang-flag :iso="serie.original_language" :squared="false"/> 
            </p>

        </div>
        
    </div>

</template>

<script>

    import LangFlag from 'vue-lang-code-flags';

    export default {
        name: "SingleCard",
        data() {
            return {
                imgUrl: `https://image.tmdb.org/t/p/w185${this.serie.poster_path}`,
            }
        },
        components: { LangFlag },
        props: { serie: Object },
        computed: {
            decimalToBinary () {
                let decimalVote = this.serie.vote_average;
                let binaryVote = decimalVote.toFixed(0);
                return binaryVote;
            }
        }
    }

</script>

<style lang="scss">

    @import "../style/colors.scss";

</style>
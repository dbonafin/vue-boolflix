<template>

    <div class="single-card">

        <h3>Film</h3>
        <img v-if="film.poster_path" :src="imgUrl" alt="image">
        <!-- alternative image if the item does not have an image -->
        <img v-else class="alternative-img" src="https://placehold.jp/40/211f1f/ff0027/220x270.png?text=Image+Not+Found" alt="image">

        <!-- Single film infos on hover -->
        <div class="overlay">
            <p><b>Title:</b> {{ film.title }}</p>
            <p><b>OG title:</b> {{ film.original_title }}</p>
            <p><b>Vote:</b> {{ decimalToBinary }}</p>
            <p v-if="film.overview">
                <b>Overview: </b> 
                {{film.overview.substring(0,80)+".."}}
            </p>
            <p v-else>
                <b>Language: </b> 
                <lang-flag :iso="film.original_language" :squared="false"/> 
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
                imgUrl: `https://image.tmdb.org/t/p/w185${this.film.poster_path}`
            }
        },
        components: { LangFlag },
        props: { film: Object },
        computed: {
            decimalToBinary () {
                let decimalVote = this.film.vote_average;
                let binaryVote = decimalVote.toFixed(0);
                return binaryVote;
            }
        }
    }

</script>

<style lang="scss">

    @import "../style/colors.scss";

    // Single card styles - same to films and tv series
    .single-card {
        margin: 20px 10px;
        padding: 4px;
        width: 200px;
        height: 300px;
        position: relative;
        background-color: $secondary-color;
        h3 {
        text-align: center;
        color: $primary-color;
        } 
        h4 {
            margin: 10px 0;
            font-size: 14px;
        }
        .overlay {
            display: none;
            position: absolute;
            left: 10px;
            top: 80px;
        }
        &:hover .overlay {
            display: block;
        }
        &:hover img {
            display: none;
        }
    }

</style>
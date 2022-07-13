<template>

    <div class="single-card">

        <h3>Film</h3>
        <!-- alternative image if the item does not have an image --> 
        <img class="alternative-img" src="https://placehold.jp/40/211f1f/ff0027/220x270.png?text=Image+Not+Found" alt="image">

        <!-- Single film infos on hover -->
        <div class="overlay">
            <h4>Title: {{ film.title }}</h4>
            <h4>OG title: {{ film.original_title }}</h4>
            <h4>
                Language: <lang-flag :iso="film.original_language" :squared="false"/> 
            </h4>
            <h4>Vote: {{ film.vote_average }}</h4>
        </div>
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

    @import "../style/colors.scss";

    // Single card styles - same to films and tv series
    .single-card {
        margin: 10px;
        padding: 4px;
        width: 200px;
        height: 300px;
        position: relative;
        background-color: $secondary-color;
        h3 {
        text-align: center;
        margin-bottom: 10px;
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
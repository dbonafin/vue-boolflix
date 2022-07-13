<template>

    <div class="single-card">

        <!-- Single film card infos - image, title, overview etc. -->

        <h3>Film</h3>
        <img v-if="film.poster_path" :src="imgUrl" alt="image">
        <!-- alternative image if the item does not have an image -->
        <img v-else class="alternative-img" src="https://placehold.jp/40/211f1f/ff0027/220x270.png?text=Image+Not+Found" alt="image">

        <!-- Single film infos on hover -->
        <div class="overlay">

            <!-- Film title options -->
            <p v-if="film.title">
                <b>Title: </b> {{ film.title }}
            </p>
            <p v-else>Title: Not available</p>

            <!-- Film original title options -->
             <p v-if="film.original_title">
                <b>Title: </b> {{ film.original_title }}
            </p>
            <p v-else>OG title: Not available</p>

            <!-- Film vote options -->
            <p v-if="film.vote_average">
                <b>Vote: </b> 
                <ul>
                    <li v-for="index in decimalToBinFilm" :key="index">
                        <font-awesome-icon icon="fa-solid fa-star" />
                    </li>
                </ul>
            </p>
            <p v-else>
                <b>Vote: </b>
                <span>Not available</span> 
            </p>

            <!-- Film overview options -->
            <p v-if="film.overview">
                <b>Overview:</b> 
                {{film.overview.substring(0,80)+".."}}
            </p>
            <p v-else>
                <b>Overview: </b>
                <span>Not available</span> 
            </p>

        </div>
    </div>

</template>

<script>

    export default {
        name: "SingleCard",
        data() {
            return {
                imgUrl: `https://image.tmdb.org/t/p/w185${this.film.poster_path}`
            }
        },
        components: {},
        props: { film: Object },
        computed: {
              decimalToBinFilm () {
                if (this.film.vote_average !== '') {
                    return Math.round(this.film.vote_average/2)
                } else {
                    return 0;
                }
               
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
            .fa-star {
                color: gold;
            }
        }
        &:hover .overlay {
            display: block;
        }
        &:hover img {
            display: none;
        }
    }

</style>
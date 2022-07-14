<template>

    <div class="single-card">
        
        <!-- Single tv serie card infos - image, title, overview etc. -->

        <img v-if="serie.poster_path" :src="imgUrl" alt="image">
        <!-- alternative image if the item does not have an image -->
        <img v-else class="alternative-img" src="https://placehold.jp/40/211f1f/ff0027/220x270.png?text=Image+Not+Found" alt="image">

        <!-- Single tv serie infos on hover -->
        <div class="overlay">
           
             <!-- Film title options -->
            <p v-if="serie.title">
                <b>Title: </b> {{ serie.title }}
            </p>
            <p v-else>Title: Not available</p>

            <!-- Film original title options -->
             <p v-if="serie.original_title">
                <b>Title: </b> {{ serie.original_title }}
            </p>
            <p v-else>OG title: Not available</p>

            <!-- Film vote options -->
            <p v-if="serie.vote_average">
                <b>Vote: </b> 
                <ul>
                      <li v-for="index in decimalToBinSerie" :key="index" class="gold-star">
                        <font-awesome-icon icon="fa-solid fa-star" />
                    </li>
                    <li v-for="n in (5 - decimalToBinSerie)" :key="n" class="white-star">
                        <font-awesome-icon  icon="fa-solid fa-star" />
                    </li>
                </ul>
            </p>
            <p v-else>
                <b>Vote: </b>
                <span>Not available</span> 
            </p>

            <!-- Film overview options -->
            <p v-if="serie.overview">
                <b>Overview:</b> 
                {{serie.overview.substring(0,80)+".."}}
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
                imgUrl: `https://image.tmdb.org/t/p/w185${this.serie.poster_path}`,
            }
        },
        components: {},
        props: { serie: Object },
        computed: {
            decimalToBinSerie () {
                if (this.serie.vote_average !== '') {
                    return Math.round(this.serie.vote_average/2)
                } else {
                    return '';
                }
               
            }
        }
    }

</script>

<style lang="scss">

    @import "../style/colors.scss";

</style>
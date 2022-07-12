<template>

    <section>
        <!-- Here the films content area  -->
        <div class="films-container">

            <!-- Films navigation area -->
           <nav>
                <h3>Film</h3>

                <div class="input-area">
                    <input 
                        v-model="searchFilm" 
                        @keyup="filterElementsByText"
                        type="search" 
                        id="input-search" 
                        placeholder="Movie name here..">

                    <button class="search-btn" @click.prevent="getFilm">Cerca</button>
                </div>
           </nav>

           <!-- Film cards area -->
           <div class="cards-container">

                <div v-for="singleFilm in filmsArray" :key="singleFilm.id">
                    <SingleCard :film="singleFilm"/>
                </div>

           </div>


        </div>

        <!-- Here the tv series content area -->
        <!-- <div class="series-container">
        </div> -->

    </section>

</template>

<script>

    import axios from "axios";
    import SingleCard from "./SingleCard.vue";

    export default {
    name: "MainSection",
    components: { SingleCard },
    data() {
        return {
            url: `https://api.themoviedb.org/3/search/movie?api_key=ba71ee58a03780066e635cc4822c198b&query=${this.searchFilm}&language=it-IT`,
            filmsArray: [],
            searchFilm: ''
        };
    },
    methods: {
        getFilm() {
            axios.get(this.url)
                .then((res) => {
                  if(this.searchFilm !== '') {        
                  this.filmsArray = res.data.results;
                  console.log(this.filmsArray);
                  } else {
                     this.filmsArray = '';
                  }
                });
        },
        filterElementsByText() {
            if (this.searchFilm === '') {
                return "";
            } else {
                return this.filmsArray.includes(this.searchFilm);   
            }
        }
    },
}

</script>

<style lang="scss">

    @import "../style/colors.scss";

    section {
        padding: 20px;
        nav {
            display: flex;
            align-items: center;
            h3 {
            font-size: 22px;
            margin: 0 10px;
            color: $text-color;
            }
            #input-search {
                padding: 4px;
                border: 1px solid black;
                border-radius: 5px;
                text-align: center;
            }
            .search-btn {
                cursor: pointer;
                margin-left: 10px;
                padding: 4px;
                border: 1px solid black;
                border-radius: 5px;
            }
        }
        .cards-container {
            display: flex;
            flex-wrap: wrap;
            margin: 10px 20px;
        }
    }

    
</style>
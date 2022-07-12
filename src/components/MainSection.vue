<template>

    <section>
        <!-- Here the films content area  -->
        <div class="films-container">

            <!-- Films navigation area -->
           <nav>
                <h3>Film</h3>

                <!-- Input that runs the search engine -->
                <div class="input-area">
                    <input 
                        v-model="searchFilm" 
                        @keyup="filterElementsByText"
                        type="search" 
                        id="input-search" 
                        placeholder="Movie name here..">
                    <!-- Button that searches the films that have the user search in their name -->
                    <button class="search-btn" @click.prevent="getFilm">Cerca</button>
                </div>
           </nav>

           <!-- Film cards area -->
           <div class="cards-container">

                <div v-for="singleFilm in filmsArray" :key="singleFilm.id" class="single-element">
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
            url: `https://api.themoviedb.org/3/search/movie?api_key=ba71ee58a03780066e635cc4822c198b`,
            filmsArray: [],
            searchFilm: ''
        };
    },
    methods: {
        getFilm() {
            // Call api for the film informations - Dynamic query for responsive results
            axios.get(`${this.url}&query=${this.searchFilm}&language=it-IT`)
                .then((res) => {
                  if(this.searchFilm !== '') {     
                  // If the input is not empty add the results to the filmsArray
                  this.filmsArray = res.data.results;
                  } else {
                  // If the input is empty don't show any info
                     this.filmsArray = '';
                  }

                  // Reset the search input 
                  this.searchFilm = '';
                });
        },
        filterElementsByText() {
            if (this.searchFilm === '') {
                return "";
            } else {
                // If the input is not empty show only the elements that include the user search
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
            margin-bottom: 20px;
            h3 {
            font-size: 22px;
            margin: 0 10px;
            color: $text-color;
            }
            // Navigation area input and button styles
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
        // Cards container and single card styles
        .cards-container {
            display: flex;
            flex-wrap: wrap;
            .single-element {
                margin: 10px 5px;
                width: calc((100% / 6) - 10px);
            }
        }
    }

    
</style>
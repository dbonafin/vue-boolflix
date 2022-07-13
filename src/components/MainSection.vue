<template>

    <section>
        <!-- Here the films content area  -->
        <div class="films-container">

            <!-- Films navigation area -->
           <nav>
                <h3>Film and TV series</h3>

                <!-- Input that runs the search engine -->
                <div class="input-area">
                    <input 
                        v-model="searchFilm" 
                        @keyup="filterFilmsByText"
                        type="search" 
                        id="input-search" 
                        placeholder="Type the name here..">
                    <!-- Button that searches the films that have the user search in their name -->
                    <button class="search-btn" @click.prevent="getFilm">Cerca</button>
                </div>
           </nav>

           <!-- Film cards area -->
           <div class="cards-container">

                <div v-for="singleFilm in filmsArray" :key="singleFilm.id" class="single-element">
                    <SingleCard :film="singleFilm"/>
                </div>

                <div v-for="singleSerie in seriesArray" :key="singleSerie.id" class="single-element">
                    <SingleSerie :serie="singleSerie"/>
                </div>

           </div>

        </div>

    </section>

</template>

<script>

    import axios from "axios";
    import SingleCard from "./SingleCard.vue";
    import SingleSerie from "./SingleSerie.vue";

    export default {
    name: "MainSection",
    data() {
        return {
            filmUrl: `https://api.themoviedb.org/3/search/movie?api_key=ba71ee58a03780066e635cc4822c198b`,
            serieUrl: `https://api.themoviedb.org/3/search/tv?api_key=ba71ee58a03780066e635cc4822c198b`,
            filmsArray: [],
            seriesArray: [],
            searchFilm: 'xzx'
        };
    },
    components: { SingleCard, SingleSerie },
    mounted() {
        this.getFilm();
        this.getSeries();
    },
    methods: {
        // Function that prints all the films with the user search in their name
        getFilm() {
            this.getSeries();
            // Call api for the film informations - Dynamic query for responsive results
            axios.get(`${this.filmUrl}&query=${this.searchFilm}&language=it-IT`)
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
         // Function that prints all the tv series with the user search in their name
        getSeries() {
                // Call api for the tv serie informations - Dynamic query for responsive results
            axios.get(`${this.serieUrl}&query=${this.searchFilm}&language=it-IT`)
                .then((res) => {
                  if(this.searchFilm !== '') {     
                  // If the input is not empty add the results to the seriesArray
                  this.seriesArray = res.data.results;
                  } else {
                  // If the input is empty don't show any info
                     this.seriesArray = '';
                  }
                }); 
        },
        // Films filter search
        filterFilmsByText() {
            if (this.searchFilm === '') {
                return "";
            } else {
                // If the input is not empty show only the elements that include the user search
                this.filterSeriesByText();
                return this.filmsArray.includes(this.searchFilm);   
            }

        },
        // Tv series filter search (able to use the same search input)
        filterSeriesByText() {
            if (this.searchFilm === '') {
                return "";
            } else {
                // If the input is not empty show only the elements that include the user search
                return this.seriesArray.includes(this.searchFilm); 
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
        }
    }

    
</style>
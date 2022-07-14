<template>

    <div class="header-div">
        <div class="logo-div">
            <h1>boolflix</h1>
        </div>

        <!-- Navigation area -->
        <nav>
            <!-- Input that runs the search engine -->
            <div class="input-area">
                <input 
                    class="nav-item"
                    v-model="searchFilm" 
                    @keyup="filterFilmsByText"
                    type="search" 
                    id="input-search">
                <!-- Button that searches the films that have the user search in their name -->
                <button class="search-btn nav-item" @click.prevent="getFilm">Cerca</button>
            </div>
        </nav>
    </div>

</template>

<script>

    import axios from "axios";

    export default {
        name: "PageHeader",
        data() {
            return {
                filmUrl: `https://api.themoviedb.org/3/search/movie?api_key=ba71ee58a03780066e635cc4822c198b`,
                serieUrl: `https://api.themoviedb.org/3/search/tv?api_key=ba71ee58a03780066e635cc4822c198b`,
                filmsArray: [],
                seriesArray: [],
                searchFilm: '',
                loadingComplete: false
            }
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
                this.loadingComplete = true;
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

    .header-div {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: $secondary-color;
        padding: 20px;
    }
    h1 {
        color: $primary-color;
        text-align: center;
        text-transform: uppercase;
    }
    nav {
        display: flex;
        align-items: center;
        h3 {
        font-size: 22px;
        margin-right: 10px;
        color: $text-color;
        }
        // Navigation area input and button styles
        .nav-item {
            color: $text-color;
            padding: 6px 10px;
            border: 1px solid $primary-color;
            background-color: $primary-color;
        }
        #input-search {
            border-radius: 5px;
            text-align: center;
        }
        .search-btn {
            cursor: pointer;
            margin-left: 10px;
            border-radius: 5px;
        }
    }   

</style>
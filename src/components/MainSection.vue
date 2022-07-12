<template>

    <section>
        <!-- Here the films content area  -->
        <div class="films-container">

            <!-- Films navigation area -->
           <nav>
                <h3>Film</h3>

                <div class="input-area">
                    <input type="search" id="input-search" placeholder="Movie name here..">
                    <button class="search-btn">Cerca</button>
                </div>
           </nav>


        </div>

        <!-- Here the tv series content area -->
        <!-- <div class="series-container">

        </div> -->

    </section>

</template>

<script>

    import axios from "axios";

    export default {
        name: "MainSection",
        data() {
            return {
                url: "https://api.themoviedb.org/3/movie/550?api_key=ba71ee58a03780066e635cc4822c198b"
            }
        },
        methods: {
            axios
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
    }

    
</style>
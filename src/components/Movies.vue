<template>
    <main>
        <h2 v-if="movieInfo.length > 0">Movies</h2>
        <div class="row row-cols-xxl-5 container mx-auto">
            <div v-for="elm in movieInfo" :key="elm.id" class="col-12 col-sm-6 col-md-4 col-lg-3 col-xxl p-2">

                <MovieCard :info="elm"/>
            
            </div>
        </div>
    </main>
</template>

<script>
import axios from 'axios';
import MovieCard from './MovieCard.vue';

export default {
    name: 'Movies',
    props: ['infoSearch', 'api_key'],
    components: {
        MovieCard
    },
    data() {
        return {
            movieInfo: [], 
        }
    },
    created(){
        //cal for trending movies
        axios
            .get("https://api.themoviedb.org/3/trending/movie/week",{
                params:{
                    api_key: this.api_key,
                }
            }
            )
            .then(
                (resp)=>{
                        this.movieInfo = resp.data.results;
                    }
            )

    },
    watch:{
        infoSearch: function() {
            
            //call for movie search
            axios
                .get("https://api.themoviedb.org/3/search/movie", {
                    params: {
                        api_key: this.api_key,
                        query: this.infoSearch,
                        language: 'it-IT'
                    }
                }
                )
                .then(
                    (resp)=>{
                        this.movieInfo = resp.data.results;
                    }
                );
        }
    }
}
</script>

<style lang="scss" scoped>

    main{
        padding-top: 16px;
        
        h2{
            text-align: center;
            color:#fff;
        }

    }
</style>
<template>
  <div id="app">
    <Header @searchMovie="searching"/>
    <div class="container-app">
      <Movies :infoSearch="searchMovie" :api_key="api_key"/>
      <Series :infoSearch="searchMovie" :api_key="api_key"/>
    </div>

  </div>
</template>

<script>
import Header from './components/Header.vue';
import Movies from './components/Movies.vue';
import Series from './components/Series.vue';



export default {
  name: 'App',
  components: {
    Header,
    Movies,
    Series
  },
  data(){
    return{
      searchMovie:"", 
      api_key: '5f982b7a134b61a8191ea027b951c118'
    }
  },
  methods:{
    searching(text){
      this.searchMovie = text;
    }
  }
}
</script>

<style lang="scss">
@import './assets/style/common.scss';

  #app{
    background-color: $secondaryColor;
    .container-app{
      margin-top: 4.375rem;
      min-height: calc(100vh - 4.375rem);
      overflow-y: auto;
    }
  }

</style>
<script>
  import axios from 'axios';
  import {store} from './store.js';

  import Search from './components/Search.vue';
  import MovieList from './components/MovieList.vue';

  export default {
    components: {
      Search,
      MovieList
    },
    data() {
      return {
        store,

      }
    },
    methods: {
      doSearch() {
        this.store.searched = true;

        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=ed158e502ecb83467e70d8afc24af02b&language=it_IT&query=${this.store.search}`).then(res => {
          this.store.movieList = res.data.results;
        });

        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=ed158e502ecb83467e70d8afc24af02b&language=it_IT&query=${this.store.search}`).then(res => {
          this.store.tvList = res.data.results;
        });

        this.store.search = ''
      },
      getTrending() {
        axios.get(`https://api.themoviedb.org/3/movie/popular?api_key=ed158e502ecb83467e70d8afc24af02b&language=en-US&page=1`).then(res => {
          this.store.movieList = res.data.results;
        });
        this.store.searched = false;
        this.store.tvList = [];
      },
     /* getReccomandations() {
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=ed158e502ecb83467e70d8afc24af02b&language=it_IT&query=${this.store.search}`).then(res => {
          console.log(res.data.results.title);
          console.log(this.store.search);
        });
      }*/
    },
    
    mounted() {
      this.getTrending();
    }
  }
</script>

<template>
  <div class="header">
    <h1 @click="getTrending()" class="home">BOOLFLIX</h1>
    <Search @search="doSearch()"></Search>
  </div>
  <h1 v-if="!store.searched">Trending Movies</h1>
  <MovieList></MovieList>
</template>

<style lang="scss">
@use './general.scss';

  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px;
    background-color: #1b1b1b;
    & h1 {
      color: red;
    }
    & .home:hover {
      cursor: pointer;
    }
  }
  h1 {
    text-align: center;
  }
</style>

<template>
    <div class="card-list" >
        <div class="card" v-for="movie in store.movieList">
            <MovieCard 
            :title="movie.title"
            :original_title="movie.original_title"
            :lang="movie.original_language"
            :score="getScore(movie.vote_average)"
            :img="getImg(movie.poster_path)"
            ></MovieCard>
        </div>
    </div>
    <h2>TV Series</h2>
    <div class="card-list">
        <div class="card" v-for="tv in store.tvList">
            <MovieCard 
            :title="tv.title"
            :original_title="tv.original_name"
            :lang="tv.original_language"
            :score="getScore(tv.vote_average)"
            :img="getImg(tv.poster_path)"
            ></MovieCard>
        </div>
    </div>
</template>

<script>
    import MovieCard from './MovieCard.vue';
    import { store } from '../store.js';

    export default {
        name: 'MovieList',
        components: {
            MovieCard
        },
        data() {
            return {
                store
            }
        },
        methods: {
            getImg(path) {
                return "https://image.tmdb.org/t/p/w342" + path;
            },
            getScore(score) {
                score = Math.ceil(score);
                let percentage = score * 10;
                return Math.ceil((5/100)*percentage);
            }
        }
    }
</script>

<style lang="scss">

    .card-list {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
        .card {
            text-align: center;
            width: calc((100%/3) - 40px);
            border: 1px solid black;
        }
    }

</style>
<template>
    <div class="modal">
        <Modal v-if="showModal" @closeModal="showModal = false" 
        :title="modalInfo.original_title"
        
        ></Modal>
    </div>

    <div class="card-list" >
        
        <div class="card" v-for="(movie, index) in store.movieList" :key="index" @click="getModal(index)">
        
            <MovieCard 
            :title="movie.title"
            :original_title="movie.original_title"
            :lang="movie.original_language"
            :score="getScore(movie.vote_average)"
            :img="getImg(movie.poster_path)"
            ></MovieCard>
        </div>
    </div>
    <h2 v-if="store.tvList.length > 0">TV Series</h2>
    <div class="card-list">
        <div class="card" v-for="(tv, index) in store.tvList" :key="index" @click="showModal = true">
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
    import Modal from './Modal.vue';
    import { store } from '../store.js';

    export default {
        name: 'MovieList',
        components: {
            MovieCard,
            Modal
        },
        data() {
            return {
                store,
                showModal: false,
                modalInfo: {}
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
            },
            getModal(index) {
                this.showModal = true;
                this.modalInfo = this.store.movieList[index];
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
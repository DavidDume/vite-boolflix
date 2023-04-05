<template>
    <div>
        <Modal v-if="showModal" @closeModal="showModal = false" 
        :title="name"
        :original_title="modalInfo.original_title"
        :lang="modalInfo.original_language"
        :score="getScore(modalInfo.vote_average)"
        :overview="modalInfo.overview"
        :id="modalInfo.id"
        :video="videoSrc"
        :isVideo="showVideo"
        :image="getImg(modalInfo.poster_path, 'w154')"
        ></Modal>
    </div>

    <div class="card-list" >
        
        <div class="card" v-for="(movie, index) in store.movieList" :key="index" @click="getModal(index, 'movie')">  
            <MovieCard :img="getImg(movie.poster_path, 'w342')"></MovieCard>
        </div>

    </div>

    <h2 v-if="store.tvList.length > 0" class="text-center">TV Series</h2>

    <div class="card-list">
        <div class="card" v-for="(tv, index) in store.tvList" :key="index" @click="getModal(index, 'tv')">
            <MovieCard :img="getImg(tv.poster_path, 'w342')"></MovieCard>
            <h5>{{ }}</h5>
        </div>
    </div>
</template>

<script>
    import MovieCard from './MovieCard.vue';
    import Modal from './Modal.vue';
    import { store } from '../store.js';
    import axios  from 'axios';

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
                modalInfo: {},
                name: '',
                videos: [],
                videoSrc: '',
                showVideo: false
            }
        },
        methods: {
            getImg(path, size) {
                if(!path) {
                    return '../../not-found-image.jpg';
                }
                return "https://image.tmdb.org/t/p/"+ size + path;
            },
            getScore(score) {
                score = Math.ceil(score);
                let percentage = score * 10;
                return Math.ceil((5/100)*percentage);
            },
            getModal(index, type) {
                this.showModal = true;
                if(type=='movie') {
                    this.modalInfo = this.store.movieList[index];
                    this.name = this.modalInfo.title;
                    this.getTrailer(type)
                } else {
                    this.modalInfo = this.store.tvList[index];
                    this.name = this.modalInfo.name;
                    this.getTrailer(type)
                }
            },
            getTrailer(type) {

                axios.get(`https://api.themoviedb.org/3/${type}/${this.modalInfo.id}/videos?api_key=ed158e502ecb83467e70d8afc24af02b`).then(res => {
                  
                    this.videos = res.data.results.filter(d => d.type == 'Trailer');

                    if(this.videos.length > 0) {
                        this.videoSrc = `https://www.youtube.com/embed/${this.videos[0].key}`;
                        this.showVideo = true;
                    } else {
                        this.videos = [];
                        this.videoSrc = '';
                        this.showVideo = false;

                    }
                    
                });
            },
        }
    }
</script>

<style lang="scss">

    .text-center {
        text-align: center;
    }

    .card-list {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        gap: 20px;
        .card {
            text-align: center;
            width: calc((100%/5) - 40px);
            & img {
                width: 100%;
            }
        }
    }

</style>
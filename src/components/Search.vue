<template>
    <div class="search-group">
        <input type="text" v-model="store.search" @keyup.enter="$emit('search')">
        <div class="reccomended" v-if="store.reccomendedList">
            <h5 class="rec-movie" v-for="m in store.reccomendedList" @click="$emit('search')">{{ m.title }}</h5>
        </div>
        <button @click="$emit('search')">Search</button>
    </div>
</template>

<script>
    import axios from 'axios';
    import {store} from '../store.js'
    export default {
        name: 'Search',
        data() {
            return {
                store
            }
        },
        computed: {
            val() {
                return this.store.search;
            }
        },
        watch: {
            val(s) {
                axios.get(`https://api.themoviedb.org/3/search/movie?api_key=ed158e502ecb83467e70d8afc24af02b&language=it_IT&query=${this.store.search}`).then(res => {
                    this.store.reccomendedList = res.data.results;
                });
            }
        }
    }
</script>

<style lang="scss">
    .reccomended {
        position: absolute;
        background-color: white;
        height: 150px;
        overflow: auto;
        & .rec-movie {
            padding: 5px;
            &:hover {
                background-color: rgb(194, 194, 194);
                cursor: pointer;
            } 
        }
    }
</style>
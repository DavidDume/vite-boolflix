<template>
    <div class="search-group">
        <input type="text" v-model="store.search" @keyup.enter="$emit('search')">
        <button @click="$emit('search')">Search</button>
    </div>
</template>

<script>

    import {store} from '../store.js'
    export default {
        name: 'Search',
        data() {
            return {
                store
            }
        }
    }
</script>

<style lang="scss">

</style>
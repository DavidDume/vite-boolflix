<template>

    <h4>{{ title }}</h4>
    <h5>{{ original_title }}</h5>
    <h5>{{ lang }}</h5>
    <h5>{{ score }}</h5>
</template>

<script>
    export default {
        name: 'MovieCard',
        props: {
            title: String,
            original_title: String,
            lang: String,
            score: String
        }
    }
</script>

<style lang="scss">



</style>
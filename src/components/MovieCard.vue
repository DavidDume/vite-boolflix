<template>

    <h4>{{ title }}</h4>
    <h5>{{ original_title }}</h5>

    <img v-if="validFlag" :src="getFlag(lang)">
    <h5 v-else="!validFlag">{{ lang }}</h5>
 
    <h5>{{ score }}</h5>
</template>

<script>
    export default {
        name: 'MovieCard',
        props: {
            title: String,
            original_title: String,
            lang: String,
            score: Number
        },
        data() {
            return {
                validFlag: true
            }
        },
        methods: {
            getFlag(flag) {
                flag = flag == 'en' ? 'gb' : flag;
                const flags = ['gb', 'it', 'de', 'fr', 'ca', 'es'];
                if(!flags.includes(flag)) {
                    this.validFlag = false;
                    return;
                }
                return `https://www.countryflagicons.com/FLAT/32/${flag.toUpperCase()}.png`;
                
            }
        }
    }
</script>

<style lang="scss">



</style>
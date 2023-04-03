<template>

    <img :src="img" alt="">

    <h4>{{ title }}</h4>
    <h5>{{ original_title }}</h5>

    <img v-if="validFlag" :src="getFlag(lang)">
    <h5 v-else="!validFlag">{{ lang }}</h5>

    <div class="stars">
        <div class="star" v-for="r in 5">
            <i class="fa-solid fa-star" v-if="r <= score" style="color: #fff700;"></i>
            <i class="fa-regular fa-star" v-else="r > score"></i>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'MovieCard',
        props: {
            title: String,
            original_title: String,
            lang: String,
            score: Number,
            img: String
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

    .stars {
        display: flex;
        align-items: center;
        justify-content: center;
    }


</style>
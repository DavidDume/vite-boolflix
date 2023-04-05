<template>

    <div class="modal-container">

       <div class="modal">
            <div class="btn">
                <button @click="$emit('closeModal')">X</button>
            </div>
            <div class="media">
                <iframe width="600" height="315"
                    :src="video" v-if="isVideo">
                </iframe>
                <img :src="image" alt="" v-else="!isVideo">
            </div>
            <h4>{{ title }}</h4>
            <h5>{{ original_title }}</h5>
            <h4>{{ overview }}</h4>
            <img v-if="validFlag" :src="getFlag(lang)">
            <h5 v-else="!validFlag">{{ lang }}</h5>
            <div class="stars">
                <div class="star" v-for="r in 5">
                    <i class="fa-solid fa-star" v-if="r <= score" style="color: #fff700;"></i>
                    <i class="fa-regular fa-star" v-else="r > score"></i>
                </div>
            </div>
        </div>

    </div>


</template>

<script>
    export default {
        name: 'Modal',
        props: {
            title: String,
            original_title: String,
            lang: String,
            score: Number,
            overview: String,
            id: Number,
            isVideo: Boolean,
            video: String,
            image: String
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


<style lang="scss" scoped>
    @use '../styles/modal.scss';

    .modal {
        width: 600px;
        height: 700px;
        background-color: white;
        border: 1px solid black;
        & .btn {
            text-align: right;
            padding: 10px;
        }

        & .media {
            display: flex;
            justify-content: center;
            align-items: center;
            img {
                width: 50%;
            }
            
        }
    }
    
    
    .stars {
        display: flex;
        align-items: center;
        justify-content: center;
    }

</style>
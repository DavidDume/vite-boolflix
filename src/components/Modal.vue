<template>

    <div class="modal-container">

       <div class="modal">
        <div class="btn">
            <button @click="$emit('closeModal')">X</button>
        </div>
        {{ title }}
       </div>

    </div>


</template>

<script>
    export default {
        name: 'Modal',
        props: {
            title: String
        }
    }
</script>


<style lang="scss" scoped>
    .modal-container {
        position: fixed;
        top: 0;
        left: 0;
        z-index: 9998;
        width: 100%;
        height: 100%;
        background: rgba(64, 64, 64, 0.36);
        border-radius: 16px;
        box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(3.3px);
        display: flex;
        justify-content: center;
        align-items: center;
        .modal {
            width: 600px;
            height: 700px;
            background-color: white;
            border: 1px solid black;
            .btn {
                text-align: right;
                padding: 10px;
            }
        }
    }

</style>
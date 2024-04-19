<template>
    <div class="backdrop-modal" v-if="showModal">
<div class="modal">
    <span @click="close()" class="close-x">x</span>
    <h2>{{ modalTitle }}</h2>
    <slot></slot>
</div>
    </div>
</template>

<script>
export default {
props: {
    modalTitle: {
        type: String,
        default: ''
    },
    showModal: {
        type: Boolean,
        required: true,
    }
},
methods: {
    close() {
        this.$emit('closeModal')
        this.$emit('update:showModal', false)
    }
},
}

</script>

<style scoped>
.backdrop-modal{
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    background-color: #0002;
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal{
width: 400px;
height: 250px;
padding: 30px;
position: relative;
background-color: white;
border-radius: 15px;
color: black;
}

.close-x{
position: absolute;
top: 15px;
right: 15px;
color: black;
cursor: pointer;
}
</style>
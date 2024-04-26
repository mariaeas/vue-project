<template>
    <div class="backdrop-modal" v-if="showModal">
        <div class="modal">
            <span @click="closeModal()" class="close-x">x</span>
            <h2>{{ modalTitle }}</h2>
            <label>Nome do Produto</label>
            <input type="text" v-model="productName">
            <label>Valor do produto</label>
            <input type="number" v-model="productValue">
            <button @click="createProduct">Criar produto!</button>
            <slot></slot>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            productName: '',
            productValue: 0,
        }
    },

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
        createProduct() {
            let data = {
                name: this.productName,
                amount: this.productValue
            }
            axios.post('product', data)
                .then((response) => {
                    console.log(response)
                })
                .catch((error) => {
                    console.log(error)
                })
        },

        closeModal() {
   
            this.$emit('update:showModal', false)
        }
    },
}

</script>

<style scoped>
.backdrop-modal {
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

.modal {
    display: grid;
    gap: 15px;
    width: 400px;
    height: fit-content;
    min-height: 200px;
    padding: 25px;
    position: relative;
    background-color: white;
    border-radius: 15px;
    color: black;
}

.modal>input {
    border: 1px solid #cdcdcd;
    border-radius: 10px;
    padding: 12px;
    font-size: 16px;
}

.modal>label {
    font-size: 16px;
}

.modal>button {
    height: 50px;
    background-color: #cdcdcd;
    border: none;
    border-radius: 10px;
}

.modal>button:hover {
    background-color: #bdbdbd;

}

.close-x {
    position: absolute;
    top: 15px;
    right: 15px;
    color: black;
    cursor: pointer;
}
</style>
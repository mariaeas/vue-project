<script>
import Modal from '../components/MyFirstComponent.vue'
import axios from 'axios'


export default {
    data() {
        return {
            selectedProduct: {},
            modalTitle: 'Meu Texto',
            showModal: false,
            route: this.$route,
            products: [],
        }
    },

    components: { Modal },

    mounted() {
        axios.defaults.baseURL = 'http://192.168.0.134:8000/api/'
        this.getProducts()
    },

    methods: {
        deleteProduct() {
            axios.delete(`product/${this.selectedProduct.id}`)
                .then((response) => {
                    console.log(response)
                    let itemIndex = this.products.findIndex(product => product.id === this.selectedProduct.id)
                    if (itemIndex) {
                        this.products.splice(itemIndex, 1)
                    }
                })
                .catch((error) => {
                    console.log(error)
                })

        },

        closeModal() {
            console.log('O modal está fechado');
        },

        redirectHome() {
            this.$router.push('/')

        },

        getProducts() {
            axios.get('product')
                .then((response) => {
                    this.products = response.data.data
                    console.log(this.products)
                })
                .catch((error) => {
                    console.log(error)
                })


        }
    },
}

</script>

<template>
    <div v-for="product in products" :key="product.id" class="product-box" @click="selectedProduct = product"
        :class="selectedProduct.id === product.id ? 'selected-box' : ''">Item!
        <h3>{{ product.name }}</h3>
        <p>{{ product.amount }}</p>
    </div>

    <Modal v-model:showModal='showModal' :modalTitle="'Meu texto!'" @closeModal="closeModal" :product="selectedProduct">
    </Modal>
    <div class="about">
        <h1>Teste!</h1>
        <button @click="selectedProduct = {}, showModal = true">Mostrar Modal</button>
        <button @click="selectedProduct = {}, showModal = true">Criar produto</button>
        <button @click="showModal = true" :disabled="!selectedProduct.id">Editar produto</button>
        <button @click="deleteProduct()">Deletar produto {{ selectedProduct.name }}</button>
    </div>


</template>

<style>
@media (min-width: 1024px) {
    .about {
        min-height: 100vh;
        display: flex;
        align-items: center;
    }
}

.selected-box {
    background-color: pink;
}

.product-box {
    transition: .3s;
    border: 1px solid pink;
    padding: 20px;
    margin: 15px;
    border-radius: 10px;
}

.product-box h3 {
    font-size: 21px;
}
</style>
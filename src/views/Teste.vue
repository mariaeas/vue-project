<script>
import Modal from '../components/MyFirstComponent.vue'

export default {
    data() {
        return {
            modalTitle: 'Meu Texto',
            showModal: true,
        }
    },

    components: { Modal },

    methods: {
        closeModal() {
            console.log('O modal está fechado');
        }
    },
}

</script>

<template>
    <Modal v-model:showModal='showModal' :modalTitle="'Meu texto!'" @closeModal="closeModal">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas neque reprehenderit beatae deserunt sequi
            facilis vel natus ea autem voluptate. Ducimus laborum labore nemo odio? Commodi iusto ipsam illo odio?</p>
    </Modal>
    <div class="about">
        <h1>Teste!</h1>
        <button @click="showModal = true">Mostrar Modal</button>
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
</style>
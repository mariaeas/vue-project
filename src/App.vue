<script>
import { onMounted } from 'vue';

export default {
  data() {
    return {
      text2: '',
      count: 0,
      count2: 0,
      firstArray: ['Maria', 'Maynara', 'João']
    }
  },

  methods: {
    addStudent() {
      if (this.firstArray.length >= 10)  {
        return
      }
      this.firstArray.push(this.text2)
      this.text2 = ''
    },
    removeLastStudent() {
      this.firstArray.pop()
    },
    removeStudent(index) {
      this.firstArray.splice(index, 1)
    },

  },

  created () {
    this.firstArray.push('Eduardo');
  },

computed: {
  sumCount() {
    return this.count + this.count2
  }
},
}
</script>

<!-- <p v-if="count > 10">Parágrafo secreto</p>
<p v-else-if="count > 5">Parágrafo do meio</p>
<p v-else-if="count < 0">É um número negativo</p>
<p v-else>Parágrafo de teste</p>-->

<!--
<header>
  <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
  
  <div class="wrapper">
    <button @click="count--">-</button>
    <h1 :class="count > 10 ? 'greenn' : ''">{{ count }}</h1>
    <button @click="count++">+</button>
  </div>
    <div class="wrapper">
      <button @click="count2--">-</button>
    <h1 :class="count2 > 10 ? 'greenn' : ''">{{ count2 }}</h1>
    <button @click="count2++">+</button>
  </div>
  <p>A soma desses dois valores é {{sumCount}}</p>
    <section>
    <input type="text" v-model="text2" @keyup.enter="addStudent()">
    <button :disabled="firstArray.length >= 10" @click="addStudent()">Adicionar nome</button>
    <p style="color:red" v-show="firstArray.length >= 10">Limite de itens atingidos!</p>
    <div v-for="(student, index) in firstArray" :key="student"><span>{{ student }}</span>
    <button @click="removeStudent(index)">Remover {{ student }}</button>
  </div>
  </section>
</header>
-->

<template>

  <RouterView />
</template>

<style scoped>
.greenn {
  color: #009488;
}
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>

<script setup>
</script>

<template>
  <main>
    <div class="title-principal">Personagem da Disney!</div>
    <div class="logo-principal">
      <img class="logo-disney" src="./Disney-logo.jpg">
    </div>
    <div class="container_input">
      <input type="search" v-model="input_busca" placeholder="Insira o nome">
      <input type="button" value="Buscar" @click="buscar()">
    </div>
    <div v-if="itens_response && itens_response.length < 1 && buscou">
      <p v-if="erro_api">Não foi possível acessar a API!</p>
      <p v-else>Nenhum registro encontrado!</p>
    </div>
    <div v-else>
      <div v-if="Array.isArray(itens_response)" class="principal">
        <div class="container_info"  v-for="(item, index) in itens_response" :key="index">
            <img :src='item.imageUrl'>
            <p>{{ item.name }}</p>
        </div>
      </div>
      <div v-else>
        <img :src='itens_response.imageUrl'>
        <p>{{ itens_response.name }}</p>
      </div>
    </div>
  </main>
</template>

<script>
import api from '../services/api'
export default {
    name: 'Menu',
    components: { api },
    data () {
      return {
        input_busca: '',
        itens_response: [],
        buscou: false,
        erro_api: false
      }
    },
    methods: {
      buscar () { 
        api.get(`?name=${this.input_busca}`).then(res => {
          this.buscou = true   
          this.itens_response = res.data.data
        }).catch(() => {
          this.erro_api = true
          this.buscou = true            
        }).finally(() => {
          setTimeout(() => {
            this.buscou = false
          }, 3000);
        })     
      }
    }
}
</script>

<style scoped>
  .container_input {
    margin-top: 20px;
    justify-content: center;
    display: flex;
  }

  .container_info {
      margin-top: 20px;
      padding: 5px;
  }

  .principal{
      display: flex;
      margin: 5px;
      flex-wrap: wrap;
  }

  .title-principal{
    margin-top: 20px;
    justify-content: center;
    display: flex;
    font-size: larger;
    font-weight: 600;
  }

  .logo-disney{
      height: 100px;
  }

  .logo-principal{
    justify-items: center;
    align-items: center;
    display: flex;
    margin-left: 43rem;
  }
</style>
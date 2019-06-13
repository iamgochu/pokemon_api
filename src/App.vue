<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="PokeDex"/>
    <card :url="item.pokemon.url" v-for="item in pokemonRockType" :key="item.pokemon.name">
     
    </card>
    <div v-for="item in pokemonRockType" :key="item.pokemon.name">
      {{item.pokemon.name}} <br>
      {{item.pokemon.url}}
    </div>
  </div>
 
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import card from './components/card.vue'

export default {
  name: 'type',
  components: {
    HelloWorld,
    card
  },
  

  data: function(){
    return{
      pokemonRockType: ""
    }
  },

  props: {
    url: String
  },

  // anything inside mounted runs as soon as the page loads
  mounted: function(){
      console.log("mounted function ran")

      const axios = require('axios');
      const vm = this;

      axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type/rock',
        responseType: 'stream'
      })

    .then(function (response) {
      console.log(response.data),
      vm.pokemonRockType = response.data.pokemon
    });
  }
  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

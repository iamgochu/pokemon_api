<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center display-1 my-5">{{activeType}} Type Pokemon</h1>
      <span :key="type.name" v-for="type in types" class="btn btn-primary m-1" v-on:click="newFunction(type.name)">
        {{type.name}}
      </span>
      <div class="row">
        <card :url="item.pokemon.url" v-for="item in currentPokemonType" :key="item.pokemon.name"></card>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import card from './components/card.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    card
  },
  

  data: function(){
    return{
      types: "",
      currentPokemonType:"",
      activeType: "rock"
    }
  },

  methods:{
    newFunction: function(name){
      console.log("newFunction works")
      this.getSpecificType(this.activeType);
      this.activeType = name;
    },

    getSpecificType: function(type){

      const axios = require('axios');
      const vm = this;

      axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type/' + type
        })

      .then(function (response) {
        // console.log(response.data),
        vm.currentPokemonType = response.data.pokemon
      });
    }
  },

  // anything inside mounted runs as soon as the page loads
  mounted: function(){
      console.log("mounted function ran")

      const axios = require('axios');
      const vm = this;

      this.getSpecificType(this.activeType);

       axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type',
      })

      .then(function (response) {
        // console.log(response.data),
        vm.types = response.data.results
      });
  }
}
</script>

<style scoped>
.card{
  text-align: center,


}
</style>
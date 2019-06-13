<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center display-1 m-5 text-capitalize">{{ activeType }} Type Pokemon</h1>
      <span v-for="type in types" :key="type" class="m-2 btn btn-primary" v-on:click=somethingHappen(type.name)>{{ type.name }}</span>
      <div class="row">
        <card :url="item.pokemon.url" v-for="item in pokemonCurrentType" :key="item.pokemon.name"></card>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import card from "./components/card.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
    card, 
  },
  data: function() {
    return {
      pokemonOfRockType: "",
      pokemonCurrentType: "",
      types: "",
      activeType: "rock"
    }
  },
  methods: {
    somethingHappen: function(name) {
      console.log("something happen")
      this.activeType = name;
      this.retrievePokemon(this.type);
    },
    retrievePokemon: function(type){
      const axios = require('axios');
      const vm = this;
      axios({
      method: "get",
      url: "https://pokeapi.co/api/v2/type/" + this.activeType
    }).then(function(response) {
      // console.log(response.data.pokemon);
      vm.pokemonCurrentType = response.data.pokemon
    });

    }
  },
  mounted: function() {
    console.log("mounted function ran");

    const axios = require("axios");
    const vm = this;

    this.retrievePokemon(this.type);

      axios({
      method: "get",
      url: "https://pokeapi.co/api/v2/type",
      responseType: "stream"
    }).then(function(response) {
      // console.log(response.data.results);
      vm.types = response.data.results
    });
  }
};
</script>

<style>

</style>

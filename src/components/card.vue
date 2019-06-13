<template>
  <div class="col-3">
    <div class="card" style="width: 18rem;">
      <!-- <img class="card-img-top" v-bind:src="pokemon.sprites.font_default" alt="None"> -->
      <div class="card-body">
        <img :src="pokemon.sprites.front_default" alt="None">
        <h5 class="card-title text-capitalize">{{ pokemon.name }}</h5>
        <p class="card-text">
          Height: {{ pokemon.height }} inches
          <br>
          Weight: {{ pokemon.weight }} pounds
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "card",
  data: function() {
    return {
      pokemon: ""
    };
  },
  props: {
    url: String
  },
  mounted: function() {
    console.log("mounted function ran");

    const axios = require("axios");
    const vm = this;

    axios({
      method: "get",
      url: vm.url,
      responseType: "stream"
    }).then(function(response) {
      // console.log(response);
      vm.pokemon = response.data;
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
    text-align: center;
    margin-bottom: 30px;
}
</style>

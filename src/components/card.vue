<template>
  <div class="hello">
    <div class="card" style="width: 18rem;">
        <img class="card-img-top" v-bind:src="pokemon.sprites['front_default']" alt="None">
        <!-- <img class="card-img-top" v-bind:src="pokemon.sprites.font_default" alt="None"> -->
        <div class="card-body">
            <h1>{{url}}</h1>
            <h5 class="card-title">{{ pokemon.name }}</h5>
            <p class="card-text"> Height: {{ pokemon.height }} inches 
            <br> Weight: {{ pokemon.weight }} pounds</p>
            
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'card',
  data: function ()
      {
          return {
              pokemon: ""
          }
      },
  props: {
    url: String
  },
  mounted: function() {
      console.log("mounted function ran")

      const axios = require('axios');
      const vm = this;

      axios({
            method: 'get',
            url: vm.url,
            responseType: 'stream'
        })
            .then(function (response) {
                // console.log(response);
                vm.pokemon = response.data
                });
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

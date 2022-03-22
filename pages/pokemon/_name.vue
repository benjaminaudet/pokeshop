<template>
  <div></div>
</template>

<script lang="ts">
import Vue from "vue";
import { component } from "vue/types/umd";

const Pokedex = require("pokeapi-js-wrapper");
const P = new Pokedex.Pokedex();

export default Vue.extend({
  name: "PokemonDetails",
  components: {},
  data: {
    pokemon: {},
  },
  async fetch() {
    this.pokemon = await P.getPokemonByName(this.$route.params.name);
  },
  fetchOnServer: false,
  methods: {},
});
</script>
<style scoped>
* {
  font-family: "Roboto";
}
.divider {
  height: 100px;
  width: 100px;
}
</style>
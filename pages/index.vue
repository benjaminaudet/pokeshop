<template>
  <div>
    <Navbar :fn="loadMorePokemons" />
    <div class="divider" />
    <Shopping :pokemons="pokemons" :loadMorePokemons="loadMorePokemons" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { component } from "vue/types/umd";
import Navbar from "../components/Navbar.vue";
import Shopping from "../components/Shopping.vue";

const Pokedex = require("pokeapi-js-wrapper");
const P = new Pokedex.Pokedex();

const LIMIT_STEP = 10;

export default Vue.extend({
  name: "IndexPage",
  components: {
    Navbar,
    Shopping,
  },
  data: () => {
    return {
      pokemons: [],
      offset: -LIMIT_STEP,
      maxOffset: 0,
      isFetching: true,
      page: 1,
    };
  },
  async fetch() {
    await this.loadMorePokemons(LIMIT_STEP * 2);
  },
  fetchOnServer: false,
  methods: {
    loadMorePokemons: async function (limit_step = LIMIT_STEP) {
      this.isFetching = true;
      const pokemons = await P.getPokemonsList({
        offset: (this.offset += limit_step),
        limit: limit_step,
      });
      pokemons.results.forEach((pokemon) => {
        this.pokemons.push(pokemon);
      });
      this.maxOffset = pokemons.count;
      this.isFetching = false;
    },
    handleScroll: async function (event) {
      await this.loadMorePokemons();
    },
    async infiniteScroll($state) {
      setTimeout(async () => {
        this.page++; // next page
        await this.loadMorePokemons();
        $state.loaded();
        $state.complete();
      }, 500);
    },
  },
});
</script>
<style scoped>
.divider {
  height: 100px;
  width: 100px;
}
</style>
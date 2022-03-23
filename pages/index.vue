<template>
  <div>
    <Navbar />
    <div class="divider" />
    <Shopping
      v-on:limit-step-selected="onChangeLimitStepSelected"
      :pokemons="pokemons"
      :loadMorePokemons="loadMorePokemons"
      :isFetching="isFetching"
      :baseLimitStep="baseLimitStep"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { component } from "vue/types/umd";
import Navbar from "../components/Navbar.vue";
import Shopping from "../components/Shopping.vue";

const Pokedex = require("pokeapi-js-wrapper");
const P = new Pokedex.Pokedex();

const BASE_LIMIT_STEP = 20;

export default Vue.extend({
  name: "IndexPage",
  components: {
    Navbar,
    Shopping,
  },
  data: () => {
    return {
      pokemons: [],
      offset: -BASE_LIMIT_STEP,
      maxOffset: 0,
      isFetching: true,
      page: 1,
      baseLimitStep: BASE_LIMIT_STEP,
      limitStep: BASE_LIMIT_STEP,
    };
  },
  async fetch() {
    await this.loadMorePokemons(BASE_LIMIT_STEP);
  },
  fetchOnServer: false,
  methods: {
    onChangeLimitStepSelected: function (limitStep) {
      this.limitStep = limitStep;
    },
    loadMorePokemons: async function (_limitStep) {
      if (!_limitStep) {
        _limitStep = this.limitStep;
      }
      this.isFetching = true;
      const pokemons = await P.getPokemonsList({
        offset: (this.offset += _limitStep),
        limit: _limitStep,
      });
      pokemons.results.forEach((pokemon) => {
        this.pokemons.push(pokemon);
      });
      this.maxOffset = pokemons.count;
      setTimeout(() => {
        this.isFetching = false;
      }, 1000);
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
* {
  font-family: "Roboto";
}
.divider {
  height: 100px;
  width: 100px;
}
</style>
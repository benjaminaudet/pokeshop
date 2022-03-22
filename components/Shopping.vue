<template>
  <div>
    <div class="limit-step-container">
      <strong>Load pokemons by chunks of :</strong>
      <select
        class="limit-step-select"
        v-model="limitStepSelected"
        @change="onChange($event)"
      >
        <option value="">{{ baseLimitStep }}</option>
        <option v-for="i in Array(4).length" :key="i">
          {{ baseLimitStep + i * baseLimitStep }}
        </option>
      </select>
    </div>
    <div class="container">
      <div
        v-for="pokemon in pokemons"
        v-bind:key="pokemon.name"
        class="pokemons-container"
      >
        <Card :pokemon="pokemon" />
      </div>
    </div>
    <h3 class="">Click on the Pokeball to load and discover more Pokemons!</h3>
    <div v-show="isFetching" class="overlay-loading scrollbar-hidden">
      <PokemonButton class="loader"></PokemonButton>
    </div>
    <PokemonButton :click="loadMorePokemons"></PokemonButton>
  </div>
</template>

<script>
export default {
  name: "Shopping",
  props: ["pokemons", "loadMorePokemons", "isFetching", "baseLimitStep"],
  data: () => {
    return {
      menuDisplay: false,
      totalPrice: 0,
      limitStepSelected: "",
    };
  },
  computed: {
    pokemonsCount: function () {
      return this.pokemons.length;
    },
    computedLimitStepSelected: function () {
      return this.limitStepSelected == ""
        ? baseLimitStep
        : parseInt(this.limitStepSelected);
    },
  },
  methods: {
    onChange: function (event) {
      this.$emit("limit-step-selected", parseInt(this.limitStepSelected));
    },
  },
};
</script>

<style scoped>
h3 {
  text-align: center;
}
.limit-step-container {
  margin-left: 10px;
}
.limit-step-container .limit-step-select {
  color: #f33;
  padding: 5px;
  font-weight: 800;
  border-radius: 9px;
  border: 2px red solid;
  margin-left: 5px;
}
.overlay-loading {
  position: fixed;
  top: 0px;
  height: 200vh;
  width: 100%;
  overflow: hidden;
  left: 0;
  background: rgba(0, 0, 0, 0.644);
  z-index: 99999;
}
.overlay-loading .loader {
  position: absolute;
  animation: rotating 1s infinite;
  -moz-animation: rotating 1s infinite;
  top: 34vh;
  left: 43.5%;
}
.scrollbar-hidden::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for IE, Edge add Firefox */
.scrollbar-hidden {
  -ms-overflow-style: none;
  scrollbar-width: none; /* Firefox */
}
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  list-style: none;
  padding: 0;
}
</style>

<template>
  <div class="container">
    <div
      v-for="pokemon in pokemons"
      v-bind:key="pokemon.name"
      class="pokemons-container"
    >
      <Card :pokemon="pokemon" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Shopping",
  props: ["pokemons"],
  data: () => {
    return {
      menuDisplay: false,
      totalPrice: 0,
    };
  },
  computed: {
    pokemonsCount: function () {
      return this.pokemons.length;
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 0;
}
</style>

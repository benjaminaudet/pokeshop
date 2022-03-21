<template>
  <li class="cards__item">
    <div v-if="pokemonData.id" class="card">
      <img
        class="card__image card__image--fence"
        :src="pokemonData.sprites.other['official-artwork'].front_default"
      />
      <div class="card__content">
        <div class="card__title">{{ pokemonData.name }}</div>
        <p class="card__text">
          This is the shorthand for flex-grow, flex-shrink and flex-basis
          combined. The second and third parameters (flex-shrink and flex-basis)
          are optional. Default is 0 1 auto.
        </p>
        <button class="btn btn--block card__btn">Button</button>
      </div>
    </div>
  </li>
</template>

<script>
const Pokedex = require("pokeapi-js-wrapper");
const P = new Pokedex.Pokedex();

export default {
  name: "Card",
  props: ["pokemon"],
  data: () => {
    return {
      menuDisplay: false,
      totalPrice: 0,
      pokemonData: {},
    };
  },
  async fetch() {
    const pokemon = await P.getPokemonByName(this.pokemon.name);
    console.log(pokemon);
    this.pokemonData = pokemon;
  },
  fetchOnServer: false,
};
</script>

<style scoped>
* {
}
.container {
  margin-top: 100px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  font-family: Roboto, sans-serif;
  color: white;
}

img {
  height: auto;
  max-width: 100%;
  vertical-align: middle;
}

.btn {
  background-color: white;
  border: 1px solid #cccccc;
  border-radius: 1rem;
  color: #696969;
  padding: 0.5rem;
  text-transform: lowercase;
}

.btn--block {
  display: block;
  width: 100%;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
}
.cards__item {
  display: flex;
  padding: 1rem;
}

.card {
  background-color: white;
  border-radius: 0.25rem;
  box-shadow: 0 0px 12px 3px rgb(143 143 143 / 50%);
  display: flex;
  flex-direction: column;
  width: 190px;
  height: 330px;
  overflow: hidden;
}

.card__content {
  display: flex;
  flex: 1 1 auto;
  flex-direction: column;
  padding: 1rem;
}
.card__image {
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  border-top-left-radius: 0.25rem;
  border-top-right-radius: 0.25rem;
  filter: contrast(70%);
  width: 300px;
  position: relative;
  transition: filter 0.5s cubic-bezier(0.43, 0.41, 0.22, 0.91);
}

.card__title {
  color: #696969;
  font-size: 1.25rem;
  font-weight: 300;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.card__text {
  flex: 1 1 auto;
  font-size: 0.875rem;
  line-height: 1.5;
  margin-bottom: 1.25rem;
}
</style>

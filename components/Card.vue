<template>
  <li class="cards__item">
    <div v-if="pokemonData.id" class="card">
      <div class="card__content">
        <div class="card__title">{{ pokemonData.name }}</div>
        <div class="card__image">
          <img
            class="card__image--fence"
            :src="pokemonData.sprites.other['dream_world'].front_default"
          />
        </div>
        <p class="card__text">
          <ul>
            <li>
              <strong>id:</strong> #<span v-for="i in 4 - String(pokemonData.id).length" :key="i">0</span
            >{{ pokemonData.id }}
            </li>
            <li>
              <strong>Types:</strong>
              <span v-for="(type, i) in pokemonData.types" :key="type.type.name">
                {{type.type.name}}<span v-show="i < pokemonData.types.length - 1">,</span>
              </span>
            </li>
            <li>

            </li>
          </ul>
        </p>
        <div class="card__button">
          <NuxtLink :to="`/pokemon/${this.pokemon.name}`" class="btn btn--block card__btn">See in details</NuxtLink>
        </div>
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
    this.pokemonData = pokemon;
    console.log(pokemon);
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
}

img {
  height: auto;
  max-width: 100%;
  vertical-align: middle;
}

.btn {
  font-style: none;
  text-decoration: none;
  text-align: center;
  background-color: white;
  border: 1px solid #cccccc;
  border-radius: 1rem;
  color: #696969;
  padding: 0.5rem;
}
.btn:hover {
  font-weight: 600;
  background-color: #f33;
  border: 1px solid #cccccc;
  border-radius: 1rem;
  color: #ffffff;
  padding: 0.5rem;
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
.card__button {
  position: relative;
}
.card__button button {
  position: absolute;
  bottom: -8vh;
}

.card {
  background-color: white;
  border-radius: 0.25rem;
  box-shadow: 0 0px 12px 3px rgb(143 143 143 / 50%);
  display: flex;
  flex-direction: column;
  width: 220px;
  height: 372px;
  overflow: hidden;
}

.card__content {
  display: flex;
  flex: 1 1 auto;
  flex-direction: column;
  padding: 1rem;
}
.card__image {
  height: 170px;
  display: flex;
  justify-content: center;
}
.card__image img {
  max-height: 150px;
  max-width: 150px;
  margin-top: 20px;
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  border-top-left-radius: 0.25rem;
  border-top-right-radius: 0.25rem;
  filter: contrast(70%);
  position: relative;
  transition: filter 0.5s cubic-bezier(0.43, 0.41, 0.22, 0.91);
}

.card__title {
  color: #252525;
  font-size: 1.25rem;
  font-weight: 600;
  letter-spacing: 2px;
  text-transform: capitalize;
  text-align: center;
}

.card__text {
  font-size: 0.875rem;
  text-align: left;
  text-transform: capitalize;
}
.card__text strong {
  text-transform: none;
}

ul,
li {
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
}
ul {
  margin-bottom: 10px;
}
</style>

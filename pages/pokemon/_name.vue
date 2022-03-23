<template>
  <div>
    <Navbar />
    <div class="container" v-if="pokemon">
      <div class="row">
        <div class="col">
          <h1>{{ pokemon.name }}</h1>
        </div>
        <div class="col id">
          <h1>
            #<span v-for="i in 4 - String(pokemon.id).length" :key="i">0</span
            >{{ pokemon.id }}
          </h1>
        </div>
        <div class="col">
          <img :src="pokemon.sprites.other['dream_world'].front_default" />
        </div>
      </div>
      <div class="row">
        <div class="card">
          <div class="title">Informations</div>
          <div class="height">
            <strong>Height: </strong>{{ (pokemon.height * 0.1).toFixed(1) }}m
          </div>
          <div class="weight">
            <strong>Weight: </strong>{{ pokemon.weight }}kg
          </div>
          <div class="base-experience">
            <strong>Base experience: </strong>{{ pokemon.base_experience }} xp
          </div>
          <div class="abilities">
            <strong>Abilities: </strong>
            <li
              v-for="ability in pokemon.abilities"
              :key="ability.ability.name"
            >
              {{ ability.ability.name }}
            </li>
          </div>
        </div>
        <div class="card">
          <div class="title">Characterics</div>
          <div
            class="stats"
            v-for="stat in pokemon.stats"
            :key="stat.stat.name"
          >
            <strong>{{ stat.stat.name }}: </strong>
            <span>
              {{ stat.base_stat }}
            </span>
          </div>
        </div>
      </div>
      <div class="add-to-cart">
        <input type="number" v-model="quantityToAdd" id="quantity" />
        <button
          class="btn btn-block"
          v-on:click="
            addArticleToCart(
              pokemon.name,
              quantityToAdd,
              pokemon.base_experience
            )
          "
        >
          Add to cart
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import VueToast from "vue-toast-notification";
import Vue from "vue";
import Navbar from "../../components/Navbar.vue";

Vue.use(VueToast);

const Pokedex = require("pokeapi-js-wrapper");
const P = new Pokedex.Pokedex();

export default Vue.extend({
  name: "PokemonDetails",
  components: {
    Navbar,
  },
  data: () => ({
    pokemon: false,
    quantityToAdd: 1,
  }),
  async fetch() {
    this.pokemon = await P.getPokemonByName(this.$route.params.name);
    console.log(this.pokemon);
  },
  fetchOnServer: false,
  methods: {
    addArticleToCart: function (name, quantity, price) {
      try {
        var articlesInCart = JSON.parse(localStorage.getItem("articles")) || [];
        const i = articlesInCart.findIndex((article) => article.name === name);
        if (articlesInCart.length > 0 && i > -1) {
          articlesInCart[i].quantity =
            parseInt(articlesInCart[i].quantity) + parseInt(quantity);
        } else {
          articlesInCart.push({ name, quantity, price });
        }
        localStorage.setItem("articles", JSON.stringify(articlesInCart));
        let instance = this.$toast.open({
          message: "Pokemon added to your shopping cart!",
          type: "success",
        });
        setTimeout(() => location.reload(), 1000);
      } catch (e) {
        console.log(e);
      }
    },
  },
});
</script>
<style scoped>
* {
  font-family: "Roboto";
  color: #3e3e3eba;
}
h1 {
  text-transform: capitalize;
  font-size: 50pt;
}
.container {
  margin-top: 100px;
  display: flex;
  flex-direction: column;
}
.add-to-cart {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  font-size: 20px;
}
.add-to-cart input {
  text-align: center;
  font-size: 20px;
}
.add-to-cart button {
  font-size: 20px;
}
.card {
  line-height: 1;
  background-color: white;
  border-radius: 9px;
  box-shadow: 0 0px 12px 3px rgb(143 143 143 / 50%);
  display: flex;
  flex-direction: column;
  width: 500px;
  height: 372px;
  overflow: hidden;
}
.card div {
  padding: 10px;
}
.card > .title {
  text-align: center;
  line-height: 3;
  padding: 0px;
  margin-bottom: 30px;
  border-bottom: 1px gray solid;
}
.abilities li {
  text-transform: capitalize;
}
.row:not(:nth-child(1)) {
  margin-top: 50px;
}
.stats strong {
  text-transform: uppercase;
}
.id {
  font-style: italic;
}
.row {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.btn {
  margin-left: 5px;
  font-style: none;
  text-decoration: none;
  text-align: center;
  background-color: #f33;
  border: 1px solid #cccccc;
  border-radius: 1rem;
  color: #ffffff;
  padding: 0.5rem;
}
.btn:hover {
  font-weight: 600;
  background-color: white;
  border: 1px solid #cccccc;
  border-radius: 1rem;
  color: #2e2e2e;
  padding: 0.5rem;
}

.btn--block {
  display: block;
  width: 100%;
}
</style>
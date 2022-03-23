<!-- Please remove this file from your project -->
<template>
  <div class="container">
    <div class="shopping-cart">
      <div class="shopping-cart-header">
        <div class="shopping-cart-total">
          <span class="lighter-text">Total:</span>
          <span class="main-color-text">{{ totalPrice }}€</span>
        </div>
      </div>
      <ul class="shopping-cart-items">
        <li
          class="clearfix"
          v-for="article in articlesInCart"
          v-bind:key="article.id"
        >
          <span class="item-name">{{ article.name }}</span>
          <span class="item-quantity"
            >Quantity: {{ article.quantity }} x {{ article.price }}€</span
          >
        </li>
      </ul>
      <div class="buttons">
        <a class="button" v-on:click="emptyCart()">Empty cart</a>
        <a class="button">Checkout</a>
      </div>
    </div>
  </div>
</template>

<script>
const Pokedex = require("pokeapi-js-wrapper");
const P = new Pokedex.Pokedex();

export default {
  name: "Cart",
  data: () => {
    return {
      articlesInCart: [],
      menuDisplay: false,
    };
  },
  mounted() {
    try {
      this.articlesInCart = JSON.parse(localStorage.getItem("articles") || "");
    } catch (e) {
      console.log(e);
    }
  },
  computed: {
    totalPrice: function () {
      let price = 0;
      if (!this.articlesInCart) {
        return 0;
      }
      this.articlesInCart.forEach((article) => {
        price += article.quantity * article.price;
      });
      return price;
    },
  },
  methods: {
    emptyCart: function () {
      this.articlesInCart = [];
      localStorage.setItem("articles", null);
    },
  },
};
</script>

<style scoped>
a {
  cursor: pointer;
}
*,
*:before,
*:after {
  box-sizing: border-box;
}
ul {
  overflow-y: scroll;
}

.container {
  position: fixed;
  z-index: 999;
  top: 100px;
  right: 20px;
}

.lighter-text {
  color: #7a7a7a;
}

.main-color-text {
  color: #f33;
  font-weight: 600;
}
.buttons {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-content: stretch;
  justify-content: space-evenly;
}
.badge {
  background-color: #f33;
  border-radius: 10px;
  color: white;
  display: inline-block;
  font-size: 12px;
  line-height: 1;
  padding: 3px 7px;
  text-align: center;
  vertical-align: middle;
  white-space: nowrap;
}

.shopping-cart {
  margin: 20px 0;
  float: right;
  background: white;
  width: 421px;
  position: relative;
  border-radius: 3px;
  padding: 20px;
  box-shadow: #505050 0px 0px 55px -6px;
}
.shopping-cart-header {
  padding-bottom: 15px;
}
.shopping-cart-total {
  float: right;
}
.shopping-cart-items {
  height: 500px;
  padding-top: 20px;
}
.shopping-cart-items li {
  margin-bottom: 18px;
  text-decoration: none;
  width: 315px;
  list-style: none;
  padding: 10px;
  border-radius: 9px;
  border: #8a8a8a 1px solid;
}

.shopping-cart-items img {
  float: left;
  margin-right: 12px;
}
.shopping-cart-items .item-name {
  display: block;
  padding-top: 10px;
  text-transform: capitalize;
  font-size: 16px;
}
.shopping-cart-items .item-price {
  color: #f33;
  margin-right: 8px;
}
.shopping-cart-items .item-quantity {
  color: #abb0be;
}

.shopping-cart:after {
  bottom: 100%;
  left: 89%;
  border: solid transparent;
  content: " ";
  height: 0;
  width: 0;
  position: absolute;
  pointer-events: none;
  border-bottom-color: white;
  border-width: 8px;
  margin-left: -8px;
}

.cart-icon {
  color: #515783;
  font-size: 24px;
  margin-right: 7px;
  float: left;
}

.button {
  background: #f33;
  color: white;
  text-align: center;
  padding: 12px;
  text-decoration: none;
  display: block;
  border-radius: 3px;
  font-size: 16px;
  margin: 25px 0 15px 0;
}
.button:hover {
  background: lighten(#f33, 3%);
}

.clearfix:after {
  content: "";
  display: table;
  clear: both;
}
</style>

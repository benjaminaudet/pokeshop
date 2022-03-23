<template>
  <div>
    <nav class="nav">
      <NuxtLink :to="`/`" class="logo">
        <img src="../static/logo.png" />
      </NuxtLink>
      <div class="menu">
        <a v-on:click="toggleMenu">
          <img src="../static/cart.png" />
        </a>
      </div>
    </nav>
    <Cart v-show="menuDisplay" />
  </div>
</template>

<script>
import Cart from "./Cart";

export default {
  name: "Navbar",
  components: {
    Cart: Cart,
  },
  data: () => {
    return {
      menuDisplay: false,
    };
  },
  methods: {
    toggleMenu: function () {
      this.menuDisplay = !this.menuDisplay;
    },
  },
};
</script>

<style scoped>
a {
  cursor: pointer;
}
.logo img {
  width: 200px;
  padding: 5px 5px;
}
.menu img {
  width: 50px;
  padding: 15px 20px;
}
.menu {
  box-shadow: #adadad 11px -16px 14px 16px;
}
nav {
  position: fixed;
  z-index: 99;
  display: flex;
  width: 100%;
  height: 80px;
  top: 0;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  left: 0;
  box-shadow: #878787 0px -34px 16px 34px;
  background: white;
}
</style>

<!-- Please remove this file from your project -->
<template>
  <nav class="nav">
    <div class="logo">
      <img src="../static/logo.png">
    </div>
    <div class="menu">
      <img src="../static/cart.png">
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style scoped>
.logo img {
  width: 200px;
  padding: 5px 5px;
}
.menu img {
  width: 50px;
  padding: 15px 20px;
}
nav {
    position: absolute;
    display: flex;
    width: 100%;
    top: 0;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    left: 0;
    box-shadow: #878787 0px -34px 16px 34px
}
</style>

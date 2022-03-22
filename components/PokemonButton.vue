<template>
  <div class="container">
    <div class="box" v-on:click="click()"></div>
  </div>
</template>
<script>
export default {
  name: "PokemonButton",
  props: ["click"],
  data: () => {
    return {};
  },
};
</script>
<style>
.container {
  display: flex;
}
.box {
  cursor: pointer;
  display: flex;
  width: 200px;
  height: 200px;
  display: inline-block;
  margin: 20px;
  position: relative;
  border: 6px solid #ccc;
  border-radius: 50%;
  background-image: -moz-radial-gradient(
      40% 40%,
      circle,
      rgba(0, 0, 0, 0.1) 40%,
      rgba(0, 0, 0, 1) 100%
    ),
    -moz-linear-gradient(-90deg, #f33 45%, #333 45%, #3f3f3f 50%, #333 55%, #fff
          55%);
  background-image: -webkit-radial-gradient(
      40% 40%,
      circle,
      rgba(0, 0, 0, 0.1) 40%,
      rgba(0, 0, 0, 1) 100%
    ),
    -webkit-linear-gradient(-90deg, #f33 45%, #333 45%, #3f3f3f 50%, #333 55%, #fff
          55%);
}
.box:before {
  content: "";
  display: block;
  position: absolute;
  z-index: 6;
  width: 20%;
  height: 20%;
  background-color: #fff;
  border-radius: 50%;
  box-shadow: 0 0 0 1px #aaa, 0 0 0 10px #fff, 0 0 0 16px #3f3f3f;
  margin: 40%;
}
.box:after {
  content: "";
  display: block;
  position: absolute;
  z-index: 1;
  width: 94%;
  height: 10%;
  background-color: rgba(0, 0, 0, 0);
  margin: 45% 3%;
  box-shadow: 12px 0 0 #fff, -12px 0 0 #fff;
}
.box:hover {
  animation: rotating 1s infinite;
  -moz-animation: rotating 1s infinite;
}
@-webkit-keyframes rotating /* Safari and Chrome */ {
  from {
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(360deg);
    -o-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
@keyframes rotating {
  from {
    -ms-transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -ms-transform: rotate(360deg);
    -moz-transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
    -o-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
</style>

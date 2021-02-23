<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: {
    Game
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

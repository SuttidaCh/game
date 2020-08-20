<template>
  <div id="app">
    <img src="img/logo.png" width="10%" />
    <p>
      <br />
    </p>
    <HelloWorld msg="WAR OF 2020" />
    <Game />
   
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Game,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

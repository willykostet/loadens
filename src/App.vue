<template>
  <div id="app">
    <a  href="https://twitter.com">
      <img style="position: fixed; right: 10px; top:10px"  width="70px" src="./assets/твитер.svg" alt=""></a>
    <GameCard msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import GameCard from './components/GameCard.vue'

export default {
  name: 'App',
  components: {
    GameCard
  }
}
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
body{
  background-image: url('./assets/фон.jpeg');
  background-position: center center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
}
</style>

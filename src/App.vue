<template>
  <div class="app">
  <img class="logo" src="./assets/main__logo.svg" alt="logo">
<h1>Remember Me</h1>
  <p>Запомни и открой все зеленые клетки</p>
    <Board/>
  </div>
</template>

<script>
import Board from './components/Board.vue'
export default {
  components: {Board}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;700&display=swap');
.app {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: 'Roboto', sans-serif;
  margin-top: 2rem;
  text-align: center;
  transition: .5s;

}
.logo {
 width: 100px;
}

</style>

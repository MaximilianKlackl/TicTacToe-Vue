<template>
  <div id="app">
    <div class="container">
      <TicTacToe/>
    </div>
  </div>
</template>

<script>
import TicTacToe from './components/TicTacToe.vue'

export default {
  name: 'App',
  components: {
    TicTacToe
  }
}
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.container{
  width: 300px;
  height: 400px;

  position: absolute;
  top:0;
  bottom: 0;
  left: 0;
  right: 0;
  
  margin: auto;
}
</style>

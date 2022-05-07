<template>
  <div class="app">
    
    
    <h1 class="h1">Запомни меня!</h1>
    <p>Запомни и открой все зеленые клетки</p>

    <BoardTest />
  </div>
</template>

<script>
import BoardTest from './components/BoardTest.vue'

export default {
  name: 'App',
  components: {
    BoardTest,
    
  }
}
</script>

<style scoped>
  .app {
    margin-top: 40px;
    text-align: center;
    font-family: Helvetica, sans-serif;
  }

  .logo {
    width: 100px;
  }

</style>

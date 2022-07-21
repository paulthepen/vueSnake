<template>
  <gameBoard />
</template>

<script>
import gameBoard from './components/GameBoard.vue'

export default {
  name: 'App',
  components: {
    gameBoard
  },
  data() {
    return {
    }
  }
}
</script>

<style>
body{
  background-color: black;
}
</style>

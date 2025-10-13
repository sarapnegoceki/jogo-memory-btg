<script setup>
  import MemoryGame from './components/MemoryGame.vue';
  import PlayerName from './components/PlayerName.vue';

  // const startGame = localStorage.getItem('player') ? true : false;
</script>

<template>
  <section class="container">
    <h1>Memory game</h1>
    <PlayerName></PlayerName>
    <MemoryGame></MemoryGame>
  </section>
</template>

<style scoped>
.container{
  padding: 30px;
}
h1{
  text-align: center;
}
</style>

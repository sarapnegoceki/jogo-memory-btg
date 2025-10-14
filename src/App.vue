<script setup>
  import { ref } from 'vue';
  import MemoryGame from './components/MemoryGame.vue';
  import PlayerName from './components/PlayerName.vue';
  import FinishGame from './components/FinishGame.vue';

  const startGame = ref(false);
  const finishGame = ref(false);

  function updatePlayerName() {
    startGame.value = localStorage.getItem('player') ? true : false;
  }

  function restartGame() {
    startGame.value = false;
    finishGame.value = true;
  }

  function startNewGame() {
    finishGame.value = false;
    startGame.value = true;
  }
</script>

<template>
  <section class="container">
    <h1>Memory game</h1>
    <PlayerName @update:setPlayerName="updatePlayerName()"></PlayerName>
    <MemoryGame v-show="startGame" @update:restartGame="restartGame()"></MemoryGame>
    <FinishGame v-show="finishGame" @update:startNewGame="startNewGame()"></FinishGame>
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
